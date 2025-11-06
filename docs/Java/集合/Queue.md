# Queue

### 讲一下 ArrayDeque？ 
ArrayDeque 实现了 Deque 接口；

ArrayDeque 实现了**双端队列**，内部使用**循环数组**实现，**默认大小为 16**。

它的特点有： 

1. 在**两端添加、删除元素**的**效率较高** 
2. **<u>根据元素内容查找和删除</u>**<u>的</u>**<u>效率比较低</u>**。 
3. 没有索引位置的概念，<u>不能根据索引位置进行操作</u>。 

### ArrayDeque 和 LinkedList 的区别
**ArrayDeque **和 **LinkedList **都实现了 **Deque 接口**；

+ <u>如果只需要从</u>**<u>两端</u>**<u>进行操作，</u>**<u>ArrayDeque </u>**<u>效率更高一些；</u>
+ <u>如果同时需要根据</u>**<u>索引位置</u>**<u>进行操作，或者经常需要在</u>**<u>中间</u>**<u>进行插入和删除，LinkedList 有相应的 api（如</u>`<u>add(int index, E e)</u>`<u>，则应该选LinkedList。 </u>
+ ArrayDeque 和 LinkedList 都是**线程不安全**的，可以使用 Collections 工具类中 **synchronizedXxx() **转换成线程同步。 

> + deque（double-ended queue，**双端队列**）是一种具有**队列**和**栈**的性质的数据结构。双端队列中的元素可以从两端弹出，**相比 list 增加 [] 运算符重载**。  
[deque_百度百科](https://baike.baidu.com/item/deque/849385?fr=aladdin)
> + java.util.Deque 继承 Queue
>

### 用 Java 实现阻塞队列
> 这是一个相对艰难的多线程面试问题，它能达到很多的目的。
>
> 第一，它可以检测侯选者是否能实际的用Java 线程写程序；
>
> 第二，可以检测侯选者对并发场景的理解，并且你可以根据这个问很多问题。如果他用wait()和notify()方法来实现阻塞队列，你可以要求他用最新的Java 5 中的并发类来再写一次。
>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">阻塞队列是一种特殊的队列，它可以在队列为空时阻塞读取操作，在队列已满时阻塞写入操作。在 Java 中，可以使用 java.util.concurrent 包中的 BlockingQueue 接口来实现阻塞队列。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">以下是一个简单的阻塞队列的实现示例：</font>

```java
import java.util.concurrent.BlockingQueue;  
import java.util.concurrent.LinkedBlockingQueue;  
  
public class BlockingQueueExample {  
    private BlockingQueue<String> queue;  
  
    public BlockingQueueExample() {  
        this.queue = new LinkedBlockingQueue<>(10);  
    }  
  
    public void put(String item) throws InterruptedException {  
        queue.put(item);  
    }  
  
    public String take() throws InterruptedException {  
        return queue.take();  
    }  
}
```

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">在上面的代码中，我们使用 LinkedBlockingQueue 类来实现阻塞队列。LinkedBlockingQueue 是一个线程安全的阻塞队列，它使用 BlockingQueue 接口的实现，同时添加了线程安全保证。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">在 put 方法中，我们使用 put 方法将元素添加到队列中。如果队列已满，put 方法将阻塞直到队列有空间。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">在 take 方法中，我们使用 take 方法从队列中获取元素。如果队列为空，take 方法将阻塞直到队列中有元素。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">当队列中有元素时，put 方法将继续执行并返回成功添加的元素；当队列中没有元素时，take 方法将返回一个默认的空字符串。</font>

### 简述 ConcurrentLinkedQueue 和 LinkedBlockingQueue 的用处和不同之处
<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">ConcurrentLinkedQueue 和 LinkedBlockingQueue 都是 Java 中实现队列的数据结构，它们的主要区别在于线程安全和阻塞模式。</font>

1. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">ConcurrentLinkedQueue 是一个线程安全的非阻塞队列，它可以在多个线程之间安全地共享。这意味着多个线程可以同时对队列进行读取或写入操作而不会相互干扰。这在多线程应用程序中非常重要，因为它可以避免线程之间的竞争条件和死锁问题。</font>
2. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">LinkedBlockingQueue 是一个线程安全的阻塞队列，它可以在队列已满时阻塞写入操作，在队列为空时阻塞读取操作。这种阻塞模式可以确保在队列满或空时，线程可以等待，直到有空间或元素可用。这在处理大量数据和高并发场景中非常重要。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">因此，选择 ConcurrentLinkedQueue 还是 LinkedBlockingQueue主要取决于应用程序的需求和并发场景。对于需要高性能和线程安全的场景，可以选择 ConcurrentLinkedQueue；对于需要阻塞模式和更好的性能的场景，可以选择 LinkedBlockingQueue。</font>

### 如果想实现一个线程安全的队列，可以怎么实现？
<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">要实现一个线程安全的队列，可以使用 Java 中的 ConcurrentLinkedQueue 或 LinkedBlockingQueue。这两个类都是线程安全的，可以在多个线程之间安全地共享。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">ConcurrentLinkedQueue 是一个基于链表的线程安全队列，它使用了双向链表来维护队列中的元素。在添加元素时，如果队列已满，则插入操作将被阻塞，直到队列有空间。在删除元素时，如果队列为空，则删除操作将被阻塞，直到队列中有元素。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">LinkedBlockingQueue 是一个基于阻塞队列的线程安全队列，它使用了链表来维护队列中的元素。当队列已满时，put 方法将被阻塞，直到队列有空间。当队列为空时，take 方法将被阻塞，直到队列中有元素。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">使用这两个类来实现线程安全的队列非常简单，只需要将它们作为参数传递给其他方法即可。例如：</font>

```java
import java.util.concurrent.ConcurrentLinkedQueue;  
import java.util.concurrent.LinkedBlockingQueue;  
  
public class ThreadSafeQueueExample {  
    private ConcurrentLinkedQueue<String> queue;  
  
    public ThreadSafeQueueExample() {  
        this.queue = new ConcurrentLinkedQueue<>();  
    }  
  
    public void put(String item) throws InterruptedException {  
        queue.add(item);  
    }  
  
    public String take() throws InterruptedException {  
        return queue.take();  
    }  
}
```

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">在上面的代码中，我们创建了一个 ConcurrentLinkedQueue 对象和一个 LinkedBlockingQueue 对象，并将它们传递给其他方法。这些方法可以在多个线程之间安全地共享，并且可以避免线程之间的竞争条件和死锁问题。</font>

### 如果你提交任务时，线程池队列已满，这时会发生什么？
这里区分一下：

1. 如果使用的是无界队列 **LinkedBlockingQueue**，可以继续添加任务到阻塞队列中等待执行，因为 LinkedBlockingQueue 可以近乎认为是一个无穷大的队列，可以无限存放任务，但是过多的任务可能导致内存溢出。Executors的线程池 **SingleThreadExecutor、FixedThreadPool **使用的是无界队列**。**
2. 如果使用的是有界队列比如 **ArrayBlockingQueue**，任务首先会被添加到 ArrayBlockingQueue 中，ArrayBlockingQueue 满了，会根据 **maximumPoolSize** 的值增加线程数量，如果增加了线程数量还是处理不过来，ArrayBlockingQueue 继续满，那么则会使用**拒绝策略** RejectedExecutionHandler 处理满了的任务，默认是 **AbortPolicy**。

### 你知道哪些常⽤的阻塞队列？
JDK7 提供了 7 个阻塞队列。分别是 

1. ArrayBlockingQueue：⼀个由数组结构组成的有界阻塞队列。
2. LinkedBlockingQueue：⼀个由链表结构组成的有界阻塞队列。
3. PriorityBlockingQueue：⼀个⽀持优先级排序的⽆界阻塞队列。
4. DelayQueue：⼀个使⽤优先级队列实现的⽆界阻塞队列。
5. SynchronousQueue：⼀个不存储元素的阻塞队列。
6. LinkedTransferQueue：⼀个由链表结构组成的⽆界阻塞队列。
7. LinkedBlockingDeque：⼀个由链表结构组成的双向阻塞队列。

### 阻塞队列
> [BlockingQueue（阻塞队列）详解 - aspirant - 博客园](https://www.cnblogs.com/aspirant/p/8657801.html)
>

### 什么是阻塞队列？如何使用阻塞队列来实现生产者-消费者模型？*
`java.util.concurrent.BlockingQueue`的特性是：**当队列是空**的时，从队列中**获取或删除**元素的操作将**会被阻塞**，或者当**队列是满时**，往队列里添加元素的操作**会被阻塞**。

阻塞队列不接受空值，当你尝试向队列中添加空值的时候，它会抛出NullPointerException。

阻塞队列的实现都是**线程安全**的，所有的查询方法都是原子的并且使用了**内部锁**或者其他形式的并发控制。

BlockingQueue 接口`java.util.Queue`是`java.util.collections`框架的一部分，它主要用于实现**生产者-消费者**问题。

> 总结：空阻满阻
>

### 简单介绍下ArrayBlockingQueue
**ArrayBlockingQueue**是规定大小的BlockingQueue，其构造函数必须带一个int参数来指明其大小。其所含的对象是以**FIFO（先入先出）**顺序排序的。

### 延迟队列的实现方式
<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">延迟队列（DelayQueue）是一种特殊的队列，它可以用来存储需要延迟执行的任务。这个队列会保存任务的执行器ID，并在任务到期时自动执行。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">延迟队列的实现方式有多种，以下是其中两种常见的方式：</font>

1. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">使用 ScheduledExecutorService</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">ScheduledExecutorService 是 Java 中提供的一个用于执行定时任务的工具类。我们可以使用它来实现延迟队列。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">首先，我们需要创建一个 ScheduledExecutorService 实例，并将其绑定到一个 DelayQueue 对象上。然后，我们可以使用 scheduleAtFixedRate() 方法来定时执行任务。</font>

```java
import java.util.concurrent.Executors;  
import java.util.concurrent.ScheduledExecutorService;  
import java.util.concurrent.TimeUnit;  
import java.util.concurrent.atomic.AtomicReference;  
  
public class DelayQueueWithScheduledExecutorService {  
    private final DelayQueue<Runnable> queue;  
    private final ScheduledExecutorService executor;  
  
    public DelayQueueWithScheduledExecutorService() {  
        this.queue = new DelayQueue<>();  
        this.executor = Executors.newSingleThreadScheduledExecutor();  
    }  
  
    public void addTask(Runnable task) {  
        queue.add(task);  
        executor.scheduleAtFixedRate(task, 0, 1, TimeUnit.SECONDS);  
    }  
}
```

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">在上面的代码中，我们创建了一个 DelayQueueWithScheduledExecutorService 类，它包含一个 DelayQueue 对象和一个 ScheduledExecutorService 实例。我们使用 addTask() 方法将任务添加到队列中，并使用 scheduleAtFixedRate() 方法定时执行任务。</font>

1. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">使用 CountDownLatch</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">CountDownLatch 是 Java 中提供的一个用于协调多个线程的工具类。我们可以使用它来实现延迟队列。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">首先，我们需要创建一个 CountDownLatch 实例，并将其绑定到一个 DelayQueue 对象上。然后，我们可以使用 countDown() 方法来等待队列中的任务执行完成。</font>

```java
import java.util.concurrent.CountDownLatch;  
import java.util.concurrent.atomic.AtomicReference;  
  
public class DelayQueueWithCountDownLatch {  
    private final DelayQueue<Runnable> queue;  
    private final CountDownLatch latch;  
  
    public DelayQueueWithCountDownLatch() {  
        this.queue = new DelayQueue<>();  
        this.latch = new CountDownLatch(1);  
    }  
  
    public void addTask(Runnable task) {  
        queue.add(task);  
        latch.countDown();  
    }  
}
```

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">在上面的代码中，我们创建了一个 DelayQueueWithCountDownLatch 类，它包含一个 DelayQueue 对象和一个 CountDownLatch 实例。我们使用 addTask() 方法将任务添加到队列中，并使用 countDown() 方法等待队列中的任务执行完成。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">这两种方式都可以实现延迟队列，具体选择哪种方式取决于具体的应用场景和需求。</font>

### delayQueue和时间轮算法的异同
<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">delayQueue和时间轮算法都是用来实现延迟任务的工具，但它们之间有一些异同点：</font>

1. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">实现原理不同：delayQueue是一个基于优先级队列（Priority Queue）实现的延迟队列，而时间轮算法则是一个基于事件驱动的延迟任务调度器。</font>
2. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">任务处理方式不同：delayQueue会在任务到期时自动执行，而时间轮算法则会根据任务的优先级和到期时间来调度执行。</font>
3. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">适用场景不同：delayQueue适用于需要延迟执行的任务较多，且任务之间相互独立的情况，而时间轮算法适用于需要同时处理多个延迟任务的情况。</font>
4. <font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">并发性能不同：时间轮算法在处理大量延迟任务时，并发性能较好，而delayQueue在处理少量延迟任务时，并发性能较好。</font>

<font style="color:rgb(5, 7, 59);background-color:rgb(253, 253, 254);">总的来说，delayQueue和时间轮算法都可以实现延迟任务，具体选择哪种方式需要根据具体的应用场景和需求来决定。</font>

### <font style="color:rgb(51,51,51);">ConcurrentLinkedQueue</font>
**<font style="color:rgb(51,51,51);">非阻塞</font>**<font style="color:rgb(51,51,51);">队列。高效的并发队列，使用</font>**<font style="color:rgb(51,51,51);">链表</font>**<font style="color:rgb(51,51,51);">实现。可以看做一个</font>**<font style="color:rgb(51,51,51);">线程安全的 </font>****<font style="color:rgb(245,0,89);">LinkedList</font>**<font style="color:rgb(245,0,89);"> </font><font style="color:rgb(51,51,51);">，通过 </font>**<font style="color:rgb(51,51,51);">CAS</font>**<font style="color:rgb(51,51,51);"> 操作实现。 </font>

<font style="color:rgb(51,51,51);">如果对队列加锁的成本较高则适合使用无锁的 </font><font style="color:rgb(245,0,89);">ConcurrentLinkedQueue </font><font style="color:rgb(51,51,51);">来替代。适合在对性能要求相对较高，同时有</font><u><font style="color:rgb(51,51,51);">多个线程对队列进行读写</font></u><font style="color:rgb(51,51,51);">的场景。 </font>

**<font style="color:rgb(51,51,51);">非阻塞队列中的几种主要方法： </font>**

+ <font style="color:rgb(245,0,89);">add(E e) </font><font style="color:rgb(51,51,51);">: 将元素e插入到队列末尾，如果插入成功，则返回true；如果插入失败（即队列已满），则会抛出异常；</font>
+ <font style="color:rgb(51,51,51);"></font><font style="color:rgb(245,0,89);">remove() </font><font style="color:rgb(51,51,51);">：移除队首元素，若移除成功，则返回true； 如果移除失败（队列为空），则会抛出异常； </font>
+ <font style="color:rgb(245,0,89);">offer(E e) </font><font style="color:rgb(51,51,51);">：将元素e插入到队列末尾，如果插入成功，则返回true；如果插入失败（即队列已满），则返回false；</font>
+ <font style="color:rgb(245,0,89);">poll() </font><font style="color:rgb(51,51,51);">：移除并获取队首元素，若成功，则返回队首元素；否则返回null；</font>
+ <font style="color:rgb(51,51,51);"></font><font style="color:rgb(245,0,89);">peek() </font><font style="color:rgb(51,51,51);">：获取队首元素，若成功，则返回队首元素；否则返回 null </font>

<font style="color:rgb(51,51,51);">对于非阻塞队列，一般情况下建议使用</font>**<font style="color:rgb(51,51,51);">offer</font>**<font style="color:rgb(51,51,51);">、</font>**<font style="color:rgb(51,51,51);">poll</font>**<font style="color:rgb(51,51,51);">和</font>**<font style="color:rgb(51,51,51);">peek</font>**<font style="color:rgb(51,51,51);">三个方法，不建议使用add和remove方法。因为</font><u><font style="color:rgb(51,51,51);">使用offer、poll和peek三个方法可以通过返回值判断操作成功与否</font></u><font style="color:rgb(51,51,51);">，而使用add和remove方法却不能达到这样的效果。</font>

### <font style="color:rgb(51,51,51);">阻塞队列</font>
<font style="color:rgb(51,51,51);">阻塞队列是</font>`<font style="color:rgb(245,0,89);">java.util.concurrent</font>`<font style="color:rgb(51,51,51);">包下重要的数据结构， </font><font style="color:rgb(245,0,89);">BlockingQueue </font><font style="color:rgb(51,51,51);">提供了</font>**<font style="color:rgb(51,51,51);">线程安全</font>**<font style="color:rgb(51,51,51);">的队列访问方式：当阻塞队列进行插入数据时，如果队列已满，线程将会阻塞等待直到队列非满；从阻塞队列取数据时，如果队列已空，线程将会阻塞等待直到队列非空。并发包下很多高级同步类的实现都是基于</font><font style="color:rgb(245,0,89);">BlockingQueue </font><font style="color:rgb(51,51,51);">实现的。 </font>

<font style="color:rgb(245,0,89);">BlockingQueue </font><font style="color:rgb(51,51,51);">适合用于作为</font>**<font style="color:rgb(51,51,51);">数据共享</font>**<font style="color:rgb(51,51,51);">的通道。 </font>

<font style="color:rgb(51,51,51);">使用阻塞算法的队列</font><u><font style="color:rgb(51,51,51);">可以用一个锁（入队和出队用同一把锁）或两个锁（入队和出队用不同的锁）等方式来实现</font></u><font style="color:rgb(51,51,51);">。 </font>

<font style="color:rgb(51,51,51);">阻塞队列和一般的队列的区别就在于： </font>

1. <font style="color:rgb(51,51,51);">多线程支持，多个线程可以安全的访问队列 </font>
2. <font style="color:rgb(51,51,51);">阻塞操作，当队列为空的时候，消费线程会阻塞等待队列不为空；当队列满了的时候，生产线程就会阻塞直到队列不满</font>

### <font style="color:rgb(51,51,51);">JDK提供的阻塞队列</font>
<font style="color:rgb(51,51,51);">JDK 7 提供了7个阻塞队列：</font>

1. ArrayBlockingQueue
2. LinkedBlockingQueue
3. PriorityBlockingQueue
4. DelayQueue
5. SynchronousQueue
6. LinkedTransferQueue



+ **<font style="color:rgb(51,51,51);">ArrayBlockingQueue</font>**
    - **<font style="color:rgb(51,51,51);">有界阻塞</font>**<font style="color:rgb(51,51,51);">队列，底层采用</font>**<font style="color:rgb(51,51,51);">数组</font>**<font style="color:rgb(51,51,51);">实现。 </font>
    - <font style="color:rgb(245,0,88);">ArrayBlockingQueue </font><font style="color:rgb(51,51,51);">一旦创建，容量不能改变。其并发控制采用</font>**<font style="color:rgb(51,51,51);">可重入锁</font>**<font style="color:rgb(51,51,51);">来控制，</font><u><font style="color:rgb(51,51,51);">不管是插入操作还是读取操作，都需要获取到锁才能进行操作</font></u><font style="color:rgb(51,51,51);">。</font>
    - <font style="color:rgb(51,51,51);">此队列按照</font>**<font style="color:rgb(51,51,51);">先进先出（FIFO）</font>**<font style="color:rgb(51,51,51);">的原则对元素进行排序。</font>
    - <font style="color:rgb(51,51,51);">默认情况下不能保证线程访问队列的公平性，</font><u><font style="color:rgb(51,51,51);">参数 </font></u><u><font style="color:rgb(245,0,88);">fair </font></u><u><font style="color:rgb(51,51,51);">可用于设置线程是否公平访问队列</font></u><font style="color:rgb(51,51,51);">。</font><u><font style="color:rgb(51,51,51);">为了保证公平性，通常会降低吞吐量</font></u><font style="color:rgb(51,51,51);">。</font>

```java
private static ArrayBlockingQueue<Integer> blockingQueue 
    = new ArrayBlockingQueue<Integer>(10, true);//fair
```

+ **<font style="color:rgb(51,51,51);">LinkedBlockingQueue</font>**
    - <font style="color:rgb(245,0,88);">LinkedBlockingQueue </font><font style="color:rgb(51,51,51);">是一个用</font>**<font style="color:rgb(51,51,51);">单向链表</font>**<font style="color:rgb(51,51,51);">实现的有界队列，</font><u><font style="color:rgb(51,51,51);">可以当做</font></u>**<u><font style="color:rgb(51,51,51);">无界</font></u>**<u><font style="color:rgb(51,51,51);">队列也可以当做</font></u>**<u><font style="color:rgb(51,51,51);">有界</font></u>**<u><font style="color:rgb(51,51,51);">队列来使用</font></u><font style="color:rgb(51,51,51);">。</font>
    - <font style="color:rgb(51,51,51);">通常在创建对象时，会指定队列最大的容量。此队列的默认和最大长度为</font>`<font style="color:rgb(245,0,88);">Integer.MAX_VALUE</font>`<font style="color:rgb(51,51,51);">。</font>
    - <font style="color:rgb(51,51,51);">此队列按照</font>**<font style="color:rgb(51,51,51);">先进先出</font>**<font style="color:rgb(51,51,51);">的原则对元素进行排序。与相比起来具有更高的吞吐量。</font>
+ **<font style="color:rgb(51,51,51);">PriorityBlockingQueue</font>**
    - <font style="color:rgb(51,51,51);">支持优先级的</font>**<font style="color:rgb(51,51,51);">无界</font>**<font style="color:rgb(51,51,51);">阻塞队列。</font>
    - <font style="color:rgb(51,51,51);">默认情况下元素采取自然顺序升序排列。也可以自定义类实现 </font><font style="color:rgb(245,0,88);">compareTo() </font><font style="color:rgb(51,51,51);">方法来指定元素排序规则，或者初始化</font><font style="color:rgb(245,0,88);">PriorityBlockingQueue </font><font style="color:rgb(51,51,51);">时，指定构造参数 </font><font style="color:rgb(245,0,88);">Comparator </font><font style="color:rgb(51,51,51);">来进行排序。</font>
    - <font style="color:rgb(245,0,89);">PriorityBlockingQueue </font><u><font style="color:rgb(51,51,51);">只能指定初始的队列大小</font></u><font style="color:rgb(51,51,51);">，后面插入元素的时候，如果空间不够的话会</font>**<font style="color:rgb(51,51,51);">自动扩容</font>**<font style="color:rgb(51,51,51);">。 </font>
    - **<font style="color:rgb(245,0,89);">PriorityQueue </font>****<font style="color:rgb(51,51,51);">的线程安全版本</font>**<font style="color:rgb(51,51,51);">。</font>
    - <u><font style="color:rgb(51,51,51);">不可以插入 null 值</font></u><font style="color:rgb(51,51,51);">，同时，插入队列的对象必须是可比较大小的（comparable），否则报 </font>**<font style="color:rgb(51,51,51);">ClassCastException</font>**<font style="color:rgb(51,51,51);"> 异常。</font>
    - <font style="color:rgb(51,51,51);">它的插入操作 </font><u><font style="color:rgb(51,51,51);">put 方法不会 block</font></u><font style="color:rgb(51,51,51);">，因为它是无界队列。take 方法在队列为空的时候会阻塞。 </font>
+ **<font style="color:rgb(51,51,51);">DelayQueue</font>**
    - <font style="color:rgb(51,51,51);">支持延时获取元素的</font>**<font style="color:rgb(51,51,51);">无界阻塞</font>**<font style="color:rgb(51,51,51);">队列。</font>
    - <font style="color:rgb(51,51,51);">队列使用 </font>**<font style="color:rgb(245,0,89);">PriorityBlockingQueue</font>**<font style="color:rgb(245,0,89);"> </font><font style="color:rgb(51,51,51);">来实现。</font>
    - <font style="color:rgb(51,51,51);">队列中的元素必须实现</font>**<font style="color:rgb(51,51,51);">Delayed接口</font>**<font style="color:rgb(51,51,51);">，在创建元素时可以指定多久才能从队列中获取当前元素。只有在延迟期满时才能从队列中提取元素。 </font>
+ **<font style="color:rgb(51,51,51);">SynchronousQueue</font>**
    - **<font style="color:rgb(51,51,51);">不存储元素</font>**<font style="color:rgb(51,51,51);">的</font>**<font style="color:rgb(51,51,51);">阻塞</font>**<font style="color:rgb(51,51,51);">队列，</font><u><font style="color:rgb(51,51,51);">每一个put必须等待一个take操作，否则不能继续添加元素</font></u><font style="color:rgb(51,51,51);">。</font>
    - <font style="color:rgb(51,51,51);">支持</font>**<font style="color:rgb(51,51,51);">公平访问</font>**<font style="color:rgb(51,51,51);">队列。 </font>
    - <font style="color:rgb(245,0,89);">SynchronousQueue </font><font style="color:rgb(51,51,51);">可以看成是一个传球手，负责把生产者线程处理的数据直接传递给消费者线程。</font>
    - <font style="color:rgb(51,51,51);">队列本身不存储任何元素，非常适合</font>**<font style="color:rgb(51,51,51);">传递性场景</font>**<font style="color:rgb(51,51,51);">。 </font>
    - <font style="color:rgb(245,0,89);">SynchronousQueue </font><font style="color:rgb(51,51,51);">的</font><u><font style="color:rgb(51,51,51);">吞吐量高于</font></u>**<u><font style="color:rgb(245,0,89);">LinkedBlockingQueue</font></u>**<u><font style="color:rgb(245,0,89);"> </font></u><u><font style="color:rgb(51,51,51);">和 </font></u>**<u><font style="color:rgb(245,0,89);">ArrayBlockingQueue</font></u>**<u><font style="color:rgb(245,0,89);"> </font></u><font style="color:rgb(51,51,51);">。 </font>
+ **<font style="color:rgb(51,51,51);">LinkedTransferQueue</font>**

```java
private static ArrayBlockingQueue<Integer> blockingQueue 
    = new ArrayBlockingQueue<Integer>(10, true); //fair
```

    - <font style="color:rgb(51,51,51);">由</font>**<font style="color:rgb(51,51,51);">链表</font>**<font style="color:rgb(51,51,51);">结构组成的</font>**<font style="color:rgb(51,51,51);">无界阻塞</font>**<font style="color:rgb(51,51,51);">TransferQueue队列。相对于其他阻塞队列，多了 </font>**<font style="color:rgb(245,0,89);">tryTransfer</font>**<font style="color:rgb(245,0,89);"> </font><font style="color:rgb(51,51,51);">和 </font>**<font style="color:rgb(245,0,89);">transfer</font>**<font style="color:rgb(245,0,89);"> </font><font style="color:rgb(51,51,51);">方法。 </font>
    - <font style="color:rgb(51,51,51);">transfer方法：如果当前有消费者正在等待接收元素（take或者待时间限制的poll方法），transfer可以把生产者传入的元素立刻传给消费者。</font><u><font style="color:rgb(51,51,51);">如果没有消费者等待接收元素，则将元素放在队列的</font></u>**<u><font style="color:rgb(51,51,51);">tail节点</font></u>**<font style="color:rgb(51,51,51);">，并等到该</font><u><font style="color:rgb(51,51,51);">元素被消费者消费了才返回</font></u><font style="color:rgb(51,51,51);">。 </font>
    - <font style="color:rgb(51,51,51);">tryTransfer方法：用来试探生产者传入的元素能否直接传给消费者。</font><u><font style="color:rgb(51,51,51);">如果没有消费者在等待，则返回false</font></u><font style="color:rgb(51,51,51);">。和上述方法的区别是该方法无论消费者是否接收，方法立即返回。而transfer方法是必须等到消费者消费了才返回。</font>
+ **<font style="color:rgb(51,51,51);">原理</font>**

<font style="color:rgb(51,51,51);">JDK使用通知模式实现阻塞队列。所谓通知模式，就是当生产者往满的队列里添加元素时会阻塞生产者，当消费者消费了一个队列中的元素后，会通知生产者当前队列可用。 </font>

<font style="color:rgb(51,51,51);">ArrayBlockingQueue使用Condition来实现：</font>

```java
private final Condition notEmpty; 
private final Condition notFull;

public ArrayBlockingQueue(int capacity, boolean fair) { 
    if (capacity <= 0)
        throw new IllegalArgumentException(); 
    this.items = new Object[capacity];
    lock = new ReentrantLock(fair); 
    notEmpty = lock.newCondition();
    notFull = lock.newCondition();
}


public E take() throws InterruptedException { 
    final ReentrantLock lock = this.lock; 
	lock.lockInterruptibly();
    try {
        while (count == 0) // 队列为空时，阻塞当前消费者
            notEmpty.await();
        return dequeue();
    } finally {
        lock.unlock();
    }
}


public void put(E e) throws InterruptedException {
    checkNotNull(e);
    final ReentrantLock lock = this.lock; lock.lockInterruptibly();
    try {
        while (count == items.length) 
            notFull.await();
        enqueue(e);
    } finally {
        lock.unlock();
    }
}


private void enqueue(E x) {
    final Object[] items = this.items; 
	items[putIndex] = x;
    if (++putIndex == items.length) 
        putIndex = 0;
    count++;
    notEmpty.signal(); // 队列不为空时，通知消费者获取元素
}
```

### ArrayBlockingQueue
+ 基于**数组**、**先进先出**、**线程安全**，<u>可实现指定时间的阻塞读写</u>，并且容量可以限制
+ 组成：**1个对象数组** +** 1把锁 ReentrantLock **+** 2个条件 Condition**
+ 三种入队对比
    - offer(E e)：如果队列没满，立即返回 true； 如果队列满了，立即返回 false --> 不阻塞
    - put(E e)：如果队列满了，一直阻塞，直到数组不满了或者线程被中断 --> 阻塞
    - offer(E e, long timeout, TimeUnit unit)：在队尾插入一个元素,，如果数组已满，则进入等待，直到出现以下三种情况：--> 阻塞
        * 被唤醒
        * 等待时间超时
        * 当前线程被中断
+ 三种出对对比
    - poll()：如果没有元素，直接返回 null；如果有元素，出队
    - take()：如果队列空了，一直阻塞，直到数组不为空或者线程被中断 --> 阻塞
    - poll(long timeout, TimeUnit unit)：如果数组不空，出队；如果数组已空且已经超时，返回 null；如果数组已空且时间未超时，则进入等待，直到出现以下三种情况：
        * 被唤醒
        * 等待时间超时
        * 当前线程被中断
+ 需要注意的是，数组是一个必须指定长度的数组，在整个过程中，数组的长度不变，队头随着出入队操作一直循环后移
+ 锁的形式有公平与非公平两种
+ 在只有入队高并发或出队高并发的情况下，因为操作数组，且不需要扩容，性能很高

### LinkedBlockingQueue
+ 基于**链表**实现，<u>读写各用一把锁</u>，在高并发**读写操作都多**的情况下，性能优于 ArrayBlockingQueue
+ 组成：**1个链表** + **2把锁** + **2个条件**
+ 默认容量为整数最大值，可以看做没有容量限制
+ 三种入队与三种出队与上边完全一样，只是由于 LinkedBlockingQueue 的的容量无限，在入队过程中，没有阻塞等待



> 更新: 2023-07-16 11:34:12  
> 原文: <https://www.yuque.com/joyo/interview/givyxii5czmbim0g>