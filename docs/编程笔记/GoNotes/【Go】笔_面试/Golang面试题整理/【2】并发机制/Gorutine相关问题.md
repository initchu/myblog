# Gorutine 相关问题

# <font style="color:rgb(0, 0, 0);">Go 的抢占式调度</font>
<font style="color:rgb(0, 0, 0);">在1.1 版本中的调度器是不支持抢占式调度的，程序只能依靠 Goroutine 主动让出 CPU 资源才能触发调度。Go 语言的调度器在 1.2 版本中引入基于协作的抢占式调度，解决了以下的问题：</font>

+ <font style="color:rgb(0, 0, 0);">某些 Goroutine 可以长时间占用线程，造成其它 Goroutine 的饥饿；</font>
+ <font style="color:rgb(0, 0, 0);">垃圾回收需要暂停整个程序（Stop-the-world，STW），最长可能需要几分钟的时间，导致整个程序无法工作；</font>

<font style="color:rgb(0, 0, 0);">1.2 版本的抢占式调度虽然能够缓解这个问题，但是它实现的抢占式调度是基于协作的，在之后很长的一段时间里 Go 语言的调度器都有一些无法被抢占的边缘情况，例如：for 循环或者垃圾回收长时间占用线程，这些问题中的一部分直到 1.14 才被基于信号的抢占式调度解决。</font>

<font style="color:rgb(0, 0, 0);">抢占式分为两种：</font>

+ <font style="color:rgb(0, 0, 0);">协作式的抢占式调度</font>
+ <font style="color:rgb(0, 0, 0);">基于信号的抢占式调度 </font>

# <font style="color:rgb(0, 0, 0);">Goroutine 泄露</font>
<font style="color:rgb(51, 51, 51);">Goroutine 作为一种逻辑上理解的轻量级线程，需要维护执行用户代码的上下文信息。在运行过程中也需要消耗一定的内存来保存这类信息，而这些内存在目前版本的 Go 中是不会被释放的。因此，如果一个程序持续不断地产生新的 goroutine、且不结束已经创建的 goroutine 并复用这部分内存，就会造成内存泄漏的现象。造成</font><font style="color:rgb(33, 37, 41);">泄露的大多数原因有以下三种：</font>

+ <font style="color:rgb(33, 37, 41);">Goroutine 内正在进行 channel/mutex 等读写操作，但由于逻辑问题，某些情况下会被一直阻塞。</font>
+ <font style="color:rgb(33, 37, 41);">Goroutine 内的业务逻辑进入死循环，资源一直无法释放。</font>
+ <font style="color:rgb(33, 37, 41);">Goroutine 内的业务逻辑进入长时间等待，有不断新增的 Goroutine 进入等待。</font>



> 更新: 2022-11-14 00:51:00  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/st3xpg>