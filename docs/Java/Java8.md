# Java 8

参考链接

> [Java 8 新特性 及 常见 面试题_牵梦u的博客-CSDN博客_jdk8新特性面试题](https://blog.csdn.net/qq_37891300/article/details/82817900)
>
> [Java面试题--java8_青春季风暴的博客-CSDN博客_java8面试题](https://blog.csdn.net/pzq915981048/article/details/89011881)
>
> [JAVA面试题（8） - 程序员Logger - 博客园](https://www.cnblogs.com/jobbible/archive/2019/02/14/10374405.html)
>

### Java 8 新特性简介
1. 代码更少（增加了新语法：Lambda 表达式）
2. 强大的 Stream API（集合数据的操作）
3. 最大化的减少空指针异常：Optional类的使用
4. 接口的新特性
5. 注解的新特性
6. 集合的底层 源码实现
7. 新日期时间的 api

### 什么是函数式编程？
函数式编程就是一种抽象程度很高的**编程范式**，纯粹的函数式编程语言编写的函数**没有变量**。因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用。而允许使用变量的程序设计语言，由于函数内部的变量状态不确定，同样的输入，可能得到不同的输出。因此，这种函数是有副作用的。 函数式编程的一个特点就是，<u>允许把函数本身作为参数传入另一个函数，还允许返回一个函数</u>！ 函数式编程最早是数学家阿隆佐·邱奇研究的一套**函数变换逻辑**，又称Lambda Calculus（λ-Calculus），所以也经常把函数式编程称为Lambda计算。

> [一文弄懂Java8函数式编程深入浅出_Java云海.的博客-CSDN博客_深入浅出java](https://blog.csdn.net/a1472750149/article/details/122471795)
>

### Java 8中的可选项是什么？
Java 8引入了一个新的容器类`java.util.Optional`。如果某个值可用，它将包装这个值。如果该值不可用，则应返回空的可选项。因此，它代表空值、缺失值。

这个类有各种实用方法，如`isPresent()`，它可以帮助用户避免使用空值检查。由于不直接返回值，而是返回包装器对象，所以用户可以避免空指针异常。

### 解释Java 8中间操作与终端操作？
流操作可以分为两部分：

+ **中间操作**

**返回另一个Stream**的中间操作，允许操作以**查询**的形式连接。

+ **终端操作**

产生**非流**，结果如：**原始值**，**集合**或根本**没有值**。

### 什么是Lambda表达式？
+ Lambda Expression可以定义为允许用户<u>将方法作为参数传递</u>的**匿名函数**。这<u>有助于删除大量的样板代码</u>。Lambda函数<u>没有访问修饰符（私有，公共或受保护），没有返回类型声明和没有名称</u>。
+ Lambda表达式允许用户将“函数”传递给代码。所以，与以前需要一整套的接口/抽象类相比，我们可以更容易地编写代码。例如，假设我们的代码具有一些复杂的循环/条件逻辑或工作流程。使用lambda表达式，在那些有难度的地方，可以得到很好的解决。

### Lambda函数的优点


直到Java 8列表和集合通常由客户端代码从集合中获取迭代器来处理，然后使用它迭代其元素并依次处理每个元素。如果要并行处理不同的元素，那么客户代码而不是集合的责任就是组织它。 通过Java 8，可以更轻松地在多个线程上分发集合的处理。 集合现在可以在内部组织自己的迭代，将并行化的责任从客户端代码转移到库代码中。

**更少的代码行**。如上所述，用户必须仅以声明方式声明要执行的操作。 

```java
n -> System.out.println("Hello World"+ n); 
```

所以用户必须键入减少的代码量。

使用Java 8 Lambda表达式可以实现**更高的效率**。通过使用具有多核的CPU，用户可以通过使用lambda并行处理集合来利用多核CPU。

### 什么是Java8中的MetaSpace？它与PermGen Space有何不同？


使用JDK8时，**permGen**空间已被删除。那么现在将元数据信息存储在哪里？

此元数据现在存储在**本机内存**中，称为“**MetaSpace**”。该内存不是连续的Java堆内存，它允许通过垃圾收集、自动调整、**元数据并发解除分配**来改进PermGen空间。

### Lambda表达式的参数列表与Lambda箭头运算符有何不同？
Lambda表达式可以一次携带零个，一个或甚至多个参数。另一方面，Lambda箭头运算符使用图标“->”将这些参数从列表和主体中分离出来。

### <font style="color:#CF1322;">java 8 流式使⽤</font>
```java
List<Integer> evens = nums.stream().filter(num -> num % 2 == 0).collect(Collectors.toList());
// 1、stream()操作将集合转换成一个流，
// 2、filter()执行我们自定义的筛选处理，这里是通过lambda表达式筛选出所有偶数，
// 3、最后我们通过collect()对结果进行封装处理，并通过Collectors.toList()指定其封装成为一个List集合返回。
```

### <font style="color:#CF1322;background-color:rgb(255,255,255);">Java1.7与1.8、1.9、10 新特性</font>
+ 1.7
1. **switch中可以使用字串**了
2. 运用List tempList = new ArrayList<>(); 即**泛型实例化类型自动推断**
3. 语法上支持集合，而不一定是数组
4. 新增一些取环境信息的工具方法
5. Boolean类型反转，空指针安全，参与位运算
6. 两个char间的equals
7. 安全的加减乘除
8. map集合支持并发请求，且可以写成 Map map = {name:"xxx",age:18};
+ 1.8
1. 允许在接口中有默认方法实现
2. **Lambda表达式**
3. **函数式接口**
4. 方法和构造函数引用
5. Lambda的范围
6. 内置函数式接口
7. Streams
8. Parallel Streams
9. Map
10. 时间日期API
11. Annotations
+ 1.9
1. Jigsaw 项目;模块化源码
2. 简化进程API
3. 轻量级 JSON API
4. 钱和货币的API
5. 改善锁争用机制
6. 代码分段缓存
7. 智能Java编译, 第二阶段
8. HTTP 2.0客户端
9. Kulla计划: Java的REPL实现

### Java8的新特性有哪些？
+ <font style="color:rgb(51,51,51);">Lambda  表达式：Lambda允许把函数作为一个方法的参数</font>
+ <font style="color:rgb(51,51,51);">Stream API ：新添加的Stream API（java.util.stream） 把真正的函数式编程风格引入到Java中默认方法：默认方法就是一个在接口里面有了一个实现的方法。</font>
+ <font style="color:rgb(51,51,51);">Optional 类：Optional 类已经成为 Java 8 类库的一部分，用来解决空指针异常。</font>
+ <font style="color:rgb(51,51,51);">Date Time API ：加强对日期与时间的处理。</font>



> 更新: 2023-10-25 14:21:50  
> 原文: <https://www.yuque.com/joyo/interview/au19r8>