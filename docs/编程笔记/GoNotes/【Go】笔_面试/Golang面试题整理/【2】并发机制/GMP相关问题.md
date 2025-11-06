# GMP 相关问题

# 简单讲一讲（说一说） GMP 模型
## <font style="color:rgb(0, 0, 0);">题目解析</font>
### 三个字母的含义
+ `**<font style="color:rgb(0,0,0);">G（Goroutine）</font>**`**<font style="color:rgb(0,0,0);">：</font>**<font style="color:rgb(0,0,0);">G 就是我们所说的 Go 语言中的协程 Goroutine 的缩写，</font><font style="color:rgb(51, 51, 51);">相当于操作系统中的进程控制块。</font><font style="color:rgb(0,0,0);">其中</font><font style="color:rgb(0, 0, 0);">存着 goroutine 的运行时栈信息，CPU 的一些寄存器的值以及执行的函数指令等。</font>
+ `**<font style="color:rgb(0,0,0);">M（Machine）</font>**`**<font style="color:rgb(0,0,0);">：</font>**<font style="color:rgb(0,0,0);">代表一个操作系统的主线程，对内核级线程的封装，数量对应真实的 CPU 数。</font><font style="color:rgb(0, 0, 0);">一个 M 直接关联一个 os 内核线程，用于执行 G。</font>M 会优先从关联的 P 的本地队列中直接获取待执行的 G。M 保存了 M 自身使用的栈信息、当前正在 M上执行的 G 信息、与之绑定的 P 信息。
+ `**<font style="color:rgb(0,0,0);">P（Processor）</font>**`<font style="color:rgb(0,0,0);">：</font><font style="color:rgb(0, 0, 0);">Processor 代表了 </font>M 所需<font style="color:rgb(0, 0, 0);">的上下文环境，</font>代表 M 运行 G 所需要的资源<font style="color:rgb(102, 102, 102);">。</font><font style="color:rgb(0, 0, 0);">是处理用户级代码逻辑的处理器，可以将其看作一个局部调度器使 go 代码在一个线程上跑。</font>当 P 有任务时，就需要创建或者唤醒一个系统线程来执行它队列里的任务，所以 P 和 M 是相互绑定的。总的来说，P 可以根据实际情况开启协程去工作，<font style="color:rgb(34, 34, 34);">它包含了运行 goroutine 的资源，如果线程想运行 goroutine，必须先获取 P，P 中还包含了可运行的 G 队列。</font>

### 调度过程
GO 调度器的调度过程，首先创建一个 G 对象，然后 G 被保存在 P 的本地队列或者全局队列（global queue）。这时 P 会唤醒一个 M。P 按照它的执行顺序继续执行任务。M 寻找一个空闲的 P，如果找得到，将 G 与自己绑定。然后 M 执行一个调度循环：调用 G 对象->执行->清理线程->继续寻找 Goroutine。 在 M 的执行过程中，上下文切换随时发生。当切换发生，任务的执行现场需要被保护，这样在下一次调度执行可以进行现场恢复。M 的栈保存在 G 对象中，只有现场恢复需要的寄存器( SP , PC 等)，需要被保存到 G 对象。  
如果 G 对象还没有被执行，M 可以将 G 重新放到 P 的调度队列，等待下一次的调度执行。当调度执行时，M可以通过 G 的 vdsoSP, vdsoPC 寄存器进行现场恢复。  
线程清理 G 的调度是为了实现 P/M 的绑定，所以线程清理就是释放 P 上的 G，让其他的 G 能够被调度。

在调度中，释放资源的时候分为两种：

1. 主动释放 (active release) ：典型的例子是，执行 G 任务时，发生了系统调用(system call)，这时M会  
处于阻塞（Block）状态。调度器会设置一个超时时间，来释放 P。 
2. 被动释放(passive release)：如果系统调用发生，监控程序需要扫描处于阻塞状态的 P/M 。 这时，  
超时之后，P 资源会回收，程序被安排给队列中的其他G任务。

### <font style="color:rgb(0,0,0);">源码</font>
#### <font style="color:rgb(0,0,0);">G</font>
```go
type g struct {
  stack       stack   // 描述真实的栈内存，包括上下界
  m              *m     // 当前的 m
  sched          gobuf   // goroutine 切换时，用于保存 g 的上下文      
  param          unsafe.Pointer // 用于传递参数，睡眠时其他 goroutine 可以设置 param，唤醒时该goroutine可以获取
  atomicstatus   uint32
  stackLock      uint32 
  goid           int64  // goroutine 的 ID
  waitsince      int64 // g 被阻塞的大体时间
  lockedm        *m     // G 被锁定只在这个 m 上运行
}
```

<font style="color:rgb(0, 0, 0);">其中 sched 比较重要，该字段保存了 goroutine 的上下文。goroutine 切换的时候不同于线程有 OS 来负责这部分数据，而是由一个 gobuf 结构体来保存，gobuf 的结构如下：</font>

```go
type gobuf struct {
    sp   uintptr
    pc   uintptr
    g    guintptr
    ctxt unsafe.Pointer
    ret  sys.Uintreg
    lr   uintptr
    bp   uintptr // for GOEXPERIMENT=framepointer
}
```

<font style="color:rgb(0, 0, 0);">这里可以看出该结构体保存了当前的栈指针，计数器，还有 g 自身，这里记录自身 g 的指针的目的是为了</font>**<font style="color:rgb(0, 0, 0);">能快速的访问到 goroutine 中的信息</font>**<font style="color:rgb(0, 0, 0);">。</font>

#### <font style="color:rgb(0, 0, 0);">M</font>
```go
type m struct {
    g0      *g     // 带有调度栈的goroutine

    gsignal       *g         // 处理信号的goroutine
    tls           [6]uintptr // thread-local storage
    mstartfn      func()
    curg          *g       // 当前运行的goroutine
    caughtsig     guintptr 
    p             puintptr // 关联p和执行的go代码
    nextp         puintptr
    id            int32
    mallocing     int32 // 状态

    spinning      bool // m是否out of work
    blocked       bool // m是否被阻塞
    inwb          bool // m是否在执行写屏蔽

    printlock     int8
    incgo         bool
    fastrand      uint32
    ncgocall      uint64      // cgo调用的总数
    ncgo          int32       // 当前cgo调用的数目
    park          note
    alllink       *m // 用于链接allm
    schedlink     muintptr
    mcache        *mcache // 当前m的内存缓存
    lockedg       *g // 锁定g在当前m上执行，而不会切换到其他m
    createstack   [32]uintptr // thread创建的栈
}
```

<font style="color:rgb(0, 0, 0);">结构体 M 中，有两个重要的字段：</font>

+ <font style="color:rgb(0, 0, 0);"> curg：代表结构体M当前绑定的结构体 G 。</font>
+ <font style="color:rgb(0, 0, 0);"> g0 ：是带有调度栈的 goroutine，普通的 goroutine 的栈是在</font>**<font style="color:rgb(0, 0, 0);">堆上</font>**<font style="color:rgb(0, 0, 0);">分配的可增长的栈，但是 g0 的栈是 </font>**<font style="color:rgb(0, 0, 0);">M 对应的线程</font>**<font style="color:rgb(0, 0, 0);">的栈。与调度相关的代码，会先切换到该 goroutine 的栈中再执行。</font>

#### <font style="color:rgb(0, 0, 0);">P</font>
```go
type p struct {
    lock mutex

    id          int32
    status      uint32 // 状态，可以为pidle/prunning/...
    link        puintptr
    schedtick   uint32     // 每调度一次加1
    syscalltick uint32     // 每一次系统调用加1
    sysmontick  sysmontick 
    m           muintptr   // 回链到关联的m
    mcache      *mcache
    racectx     uintptr

    goidcache    uint64 // goroutine的ID的缓存
    goidcacheend uint64

    // 可运行的goroutine的队列
    runqhead uint32
    runqtail uint32
    runq     [256]guintptr

    runnext guintptr // 下一个运行的g

    sudogcache []*sudog
    sudogbuf   [128]*sudog

    palloc persistentAlloc // per-P to avoid mutex

    pad [sys.CacheLineSize]byte
}
```

+ <font style="color:rgb(0, 0, 0);">P 的个数就是 GOMAXPROCS（最大256），启动时固定的，一般不修改；</font><font style="color:rgb(51,51,51);">GOMAXPOCS 默认值是当前电脑的核心数，单核CPU就只能设置为1，如果设置>1，在 GOMAXPOCS 函数中也会被修改为1。</font>
+ <font style="color:rgb(0, 0, 0);">M 的个数和P 的个数不一定一样多（会有休眠的M或者不需要太多的 M）（M 最大10000）；</font>
+ <font style="color:rgb(0, 0, 0);">每一个 P 保存着本地 G 任务队列，也有一个全局 G 任务队列。</font>

### <font style="color:rgb(0, 0, 0);">模型介绍</font>
![画板](./img/76ZO1iY98RZ-rd1i/1648716696731-0d4e04b1-da32-4ff8-ac44-f2f74cfb7629-332120.jpeg)

**<font style="color:rgb(0, 0, 0);">本地队列</font>**<font style="color:rgb(0, 0, 0);">：存放等待运行的 G，一个本地队列存放的G数量一般不超过 256 个，优先将新创建的 G 放在 P 的本地队列中，如果满了会放在全局队列中。</font>本地的队列是无锁的，没有数据竞争问题，处理速度比较高。

**<font style="color:rgb(0, 0, 0);">全局队列</font>**<font style="color:rgb(0, 0, 0);">：存放等待运行的 G，读写要</font>**<font style="color:rgb(0, 0, 0);">加锁</font>**<font style="color:rgb(0, 0, 0);">，所以拿取效率在多线程竞争的情况下相比于本地队列来说要低。</font>用来平衡不同的 P 的任务数量，所有的 M 共享 P 的全局队列。

## <font style="color:rgb(0, 0, 0);">面试回答模板</font>
首先呢，GMP 这三个字母的含义分别是 Goroutine，Machine，Processor。这个 <font style="color:rgb(0,0,0);">Goroutine，</font><font style="color:rgb(51, 51, 51);">相当于操作系统中的进程控制块。G 结构体中</font><font style="color:rgb(0,0,0);">其中</font><font style="color:rgb(0, 0, 0);">存着 goroutine 的运行时栈信息，CPU 的一些寄存器的值以及执行的函数指令等。</font><font style="color:rgb(0,0,0);">Machine就是代表了一个操作系统的主线。</font>M 结构体中，保存了 M 自身使用的栈信息、当前正在 M上执行的 G 信息、与之绑定的 P 信息。<font style="color:rgb(0, 0, 0);">M 直接关联一个 os 内核线程，用于执行 G。（这里思考一个这个模型的图片回答），这个 </font>M 做的事情就是从关联的 P 的本地队列中直接获取待执行的 G。剩下的 <font style="color:rgb(0, 0, 0);">Processor 是代表了 </font>M 所需<font style="color:rgb(0, 0, 0);">的上下文环境，</font>代表 M 运行 G 所需要的资源<font style="color:rgb(102, 102, 102);">。</font>当 P 有任务时，就需要创建或者唤醒一个系统线程来执行它队列里的任务。在GMP调度模型中，<font style="color:rgb(0, 0, 0);">P 的个数就是 GOMAXPROCS，是可以手动设置的，但一般不修改，</font><font style="color:rgb(51,51,51);">GOMAXPOCS 默认值是当前电脑的核心数，单核CPU就只能设置为1，如果设置>1，在 GOMAXPOCS 函数中也会被修改为1。</font>总的来说，这个 P 结构体的主要的任务就是可以根据实际情况开启协程去工作。

# 






> 更新: 2022-11-14 00:49:54  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/ie4sgv>