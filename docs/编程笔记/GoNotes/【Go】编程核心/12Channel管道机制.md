# 12 Channel 管道机制

## 需求场景
假设有这样一个场景，想要将协程和主线程计算后产生的数据存放到全局的Map中。

例如，编写一个函数来计算各个数的阶乘，并放入到map中，启动了多个协程进行计算机，统计的结果放入到map中。

```go
package main
var (
    myMap = make(map[int]int, 10)
)
//test 计算n!
func test(n int){
    res := 1
    for i := 1; i < n; i++{
        res *= i
    }
    myMap[n] = res
}
func main(){
    //开启多个协程
    for i := 1;i <= 200; i++{
        go test(i)
    }
    time.Sleep(time.Second* 10)
    for i,v := range myMap{
        fmt.Printf("map[%d]=%d\n",i,v)
    }
}
```

运行结果，存入之后是混乱的。

值得考虑的是，需要保证不同的协程之间避免出现资源的争夺问题。

有两种办法可以解决，第一种是使用全局互斥锁来解决，第二种办法是使用管道机制。

## 全局互斥锁Mutex解决资源竞争问题
```go
package main
var (
    myMap = make(map[int]int, 10)
    //声明一共全局的互斥锁lock
    //sync是包，全拼"synchornized"是同步的意思
    //Mutex是互斥的意思
    lock sync.Mutex
)
//test 计算n!
func test(n int){
    res := 1
    for i := 1; i < n; i++{
        res *= i
    }
    
    //加锁
    lock.Lock()
    myMap[n] = res
    //存入之后解锁
    lock.Unlock()
}
func main(){
    //开启多个协程
    for i := 1;i <= 200; i++{
        go test(i)
    }
    time.Sleep(time.Second* 10)
    lock.Lock()
    for i,v := range myMap{
        fmt.Printf("map[%d]=%d\n",i,v)
    }
    lock.Unlock()
}
```

为什么在第28行也要加一个互斥锁？

按理说十秒钟之后上面的协程都应该执行完毕了，后面的打印就不会出现资源竞争的问题了。在实际的运行中，还是可能在打印部分出现资源竞争问题，因为虽然我们从程序设计上可以知道10秒就可以执行完所有的协程，但是主线程并不知道，因此底层仍可能出现资源争夺，这里加入互斥锁就可以解决这个问题。😅

## Channel管道机制解决资源争夺问题


前面使用全局互斥锁来解决goroutine的通信并不完美，这是因为：

+ 主线程在等待所有goroutine全部完成的时间很难确定
+ 如果主线程休眠时间长了，会加长等待时间，如果等待时间短了，可能还有goroutine处于工作状态，这时也会随主线程的退出而销毁
+ 通过全局互斥锁来实现通讯，也没有利用多个协程同时对全局变量进行读写操作



### Channel的基本介绍
+ channel本质是一个数据结构-队列
+ 数据是先进先出的
+ 管道可以保证线程安全，多个协程访问的时候，不需要加锁，channel本身就是线程安全的
+ channel是由类型的，一个string的channel只能存放string类型的数据



### 管道的定义
```go
var intChan chan int
var mapChan chan map[int]string
var perChan chan Person
var perChan2 chan *Person
```

管道是引用类型

`channel`必须初始化才能写入数据，即`make`后才能使用。

管道是由类型的，`intChan`只能写入整数`int`

### 管道的使用
```go
package main
func main(){
    //1.创建一共可以存放3个int类型的管道
	var intChan chan int
    intChan = make(chan int, 3)
    //2.查看intChan是什么
    fmt.Printf("intChan的值 = %v,intChan本身的地址 = %p\n",intChan,&intChan) //值就是一个地址
	//3.向管道写入数据
    intChan <- 10
    num := 211
    intChan <-num
    intChan <- 50 
    //给管道写入数据的时候，不能超过其容量
    fmt.Printf("channel len = %v cap = %v \n",len(intChan),cap(intChan))//3，3
	//3.从管道中读取数据
    var num2 int
    num2 = <-intChan //管道的数据推给了num2,先进先出
    fmt.Println("num2 = ",num2)
    fmt.Printf("channel len = %v cap = %v \n",len(intChan),cap(intChan)) //2,3
    //6.在没有使用协程的情况下，如果我们的管道数据已经全部取出，再取就会报告deadkock死锁,阻塞
    num3 := <-intChan //211
    num4 := <-intChan //50
    num5 := <-intChan //deadlock
    fmt.Println("num3 =",num3 ,"num4 = ",num4, "num5 = ",num5)
}
```

总结：

+ channel中只能存放**指定**的数据类型
+ channel的数据放满了之后，就不能再放入了
+ 如果从channel取出数据后，可以继续放入
+ 在没有使用协程的情况下，如果channel数据取完了，再取，就会报告deadlock



管道的使用注意事项：

**只能存放指定的数据类型之空接口！**

```go
package main
type Cat struct{
    Name string
    Age int
}
func main(){
    //定义一个存放任意数据类型的管道，3个数据
    a11Chan := make(chan interface{},3)
    a11Chan <- 10
    a11Chan <-"tom jack"
    cat = Cat{"小花猫", 4}
    a11Chan <- cat
    //我们希望获取到管道中的第三个元素，则先将前两个推出
    <-a11Chan
    <-a11Chan
    newCat := <-allChan
    fmt.Printf("newCat type = %T",newCat) //
    //转一下类型断言 
    //a := newCat.(cat)
    fmt.Printf("newCat.Name= %v",newCat.Name)//如果没有类型断言是报错的，管道存放的是空接口，里面是没有字段和方法的
}
```

### 管道的关闭
使用内置函数close可以关闭channel，当channel关闭后，就不能再向channel写入数据了，但是仍然可以从该channel读取数据。

```go
package main
func main(){
    intChan := make(chan int, 3)
    intChan<- 100
    intChan<- 200
    close(intChan)//关闭channel
    fmt.Println("运行成功")
    //读取数据
    n1 := <-intChan
    fmt.Println("n1=",n1)
}
```

### 管道的遍历
channel不能使用普通的遍历循环。

channel支持`for - range`的方式进行遍历：

+ 在遍历的时候，如果channel没有关闭，则会出现`deadlock`的错误
+ 在遍历的时候，如果channel已经关闭，则会正常遍历数据，遍历完之后，就会退出遍历 

```go
package main
func main(){
    intChan := make(chan int, 100)
    for i:= 0; i<100; i++{
        intChan<- i*2
	} 
    //Close(intChan)
    //如果管道没有关闭，则在读取结束后，出现死锁的错误
    for v:= range intChan{
        fmt.Println("v=", v)
    }
}
```

注意❌：遍历管道的时候不能使用普通的`for`循环：`<font style="color:#E8323C;">for i := 0; i < len(intChan); i++{}</font>`



## goroutine和channel结合
在一个管道中，我们需要实现以下要求：

+ 开启一个writeData协程，向管道intChan中写入50个整数。
+ 开启一个readData协程，从管道中读取writeData写入的数据。
+ 主线程需要等待writeData和readData协程都完成工作才能退出。

设计思路是：

开启两个**协程（读和写）**同时执行，同时使用两个**管道**，其中一个管道`intChan`用来存放数据，当**读协程**执行读完，向另一个管道`exitChan`中写入一个`true`，并关闭第二个管道。设置第二个管道的原因是，当开启协程之后，主线程仍旧往下执行，设置一个持续读取的循环，直到读取到了`eixtChan`里面的`true`，就证明了这两个协程执行完毕，也就是保证了“主线程需要等待writeData和readData协程都完成工作才能退出”这一个条件。

```go
 package main
//writeData 写数据
func writeData(intChane chan int){
    for i := 1; i <= 50; i++{
    	//放入数据
        intChan <- i
        fmt.Println("writeData",i)
    }
    close(intChan)//关闭
}
// readData 读数据
func readData(intChan chan int, exitChan chan bool){
    for{
        v, ok := <-intChan
        if !ok{
        	break
        }
        fmt.Printf("readData = %v\n",v)
    }
    exitChan<- true
    close(exitChan)//读完数据关闭管道
}
func main(){
    //创建两个管道
    intChan := make(chan int, 50)
    exitChan := make(chan bool, 1)
    go writeData(intChan)
    go readData(intChan, exitChan)
    for{ //防止主线程退出，一直读exitChan管道,读到了就退出 
        _,ok := <-exitChan
        if !ok{
        	break
        }
    }
}
    
```

**❗**** 注意：如果编译器发现只向管道写入数据，而没有读取，则会出现**`**deadlock**`**，原因发生了阻塞，**`**intChan**`**容量是10，而代码writeData会写入50个数据，因此会阻塞在writeData的**`**ch <- i**`** 。**

















> 更新: 2022-02-21 13:46:51  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/ptkuec>