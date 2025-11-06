# 关键字

## 参考
[volatile](https://www.yuque.com/joyo/interview/aimqk9zz52iregro)

## final、finally、finalize 的区别?
+ final：修饰符（关键字）有三种用法：如果一个类被声明为final，意味着它不能再派生出新的子类，即不能被继承，因此它和abstract是反义词。将变量声明为final，可以保证它们在使用中不被改变，被声明为final 的变量必须在声明时给定初值，而在以后的引用中只能读取不可修改。被声明为final 的方法也同样只能使用，不能在子类中被重写。
+ finally：通常放在try…catch的后面构造总是执行代码块，这就意味着程序无论正常执行还是发生异常，这里的代码只要JVM不关闭都能执行，可以将释放外部资源的代码写在finally块中。
+ finalize：Object类中定义的方法，Java中允许使用finalize() 方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在销毁对象时调用的，通过重写finalize() 方法可以整理系统资源或者执行其他清理工作。

## Java 中的final关键字有哪些用法？
(1)修饰类：表示该类不能被继承；

(2)修饰方法：表示方法不能被重写；

(3)修饰变量：表示变量只能一次赋值以后值不能被修改（常量）。

## <font style="color:#CF1322;">final，finally，finalize 的区别 </font>
<font style="color:rgb(51,51,51);">final：变量、类、方法的修饰符，被 final 修饰的类不能被继承，变量或方法被 final 修饰则不能被修改和重写。 </font>

<font style="color:rgb(51,51,51);">finally：异常处理时提供 finally 块来执行清除操作，不管有没有异常抛出，此处代码都会被执行。如果 try 语句块中包含 return 语句，finally 语句块是在 return 之后运行； </font>

<font style="color:rgb(51,51,51);">finalize：Object 类中定义的方法，若子类覆盖了 finalize()方法，在在垃圾收集器将对象从内存中清除前，会执行该方法，确定对象是否会被回收。 </font>

## transient关键字的作用？
<font style="color:rgb(51,51,51);">Java</font><font style="color:rgb(51,51,51);">语言的关键字，变量修饰符，如果用</font><font style="color:rgb(51,51,51);">transient</font><font style="color:rgb(51,51,51);">声明一个实例变量，当对象存储时，它的值不需要维</font><font style="color:rgb(51,51,51);">持。</font>

<font style="color:rgb(51,51,51);">也就是说被transient修饰的成员变量，在序列化的时候其值会被忽略，在被反序列化后， transient 变量的值被设为初始值， 如 int 型的是 0，对象型的是 null。</font>

## final, finally, finalize 的区别
<font style="color:rgb(51,51,51);">final </font><font style="color:rgb(51,51,51);">用于修饰属性、方法和类</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(51,51,51);">分别表示属性不能被重新赋值，方法不可被覆盖，类不可被继承。</font>

<font style="color:rgb(51,51,51);">finally 是异常处理语句结构的一部分，一般以</font><font style="color:rgb(245,0,88);">try-catch-finally </font><font style="color:rgb(51,51,51);">出现，</font><font style="color:rgb(245,0,88);">finally </font><font style="color:rgb(51,51,51);">代码块表示总是被执行。</font>

<font style="color:rgb(51,51,51);">finalize  是Object类的一个方法，该方法一般由垃圾回收器来调用，当我们调用</font><font style="color:rgb(245,0,88);">System.gc() </font><font style="color:rgb(51,51,51);">方法的时候，由垃圾回收器调用</font><font style="color:rgb(245,0,88);">finalize() </font><font style="color:rgb(51,51,51);">方法，回收垃圾，JVM并不保证此方法总被调用。</font>

## final关键字的作用？
<font style="color:rgb(51,51,51);">final</font><font style="color:rgb(51,51,51);"> </font><font style="color:rgb(51,51,51);">修饰的类不能被继承</font><font style="color:rgb(51,51,51);">。</font>

<font style="color:rgb(51,51,51);">final</font><font style="color:rgb(51,51,51);"> </font><font style="color:rgb(51,51,51);">修饰的方法不能被重写</font><font style="color:rgb(51,51,51);">。</font>

<font style="color:rgb(51,51,51);">final  修饰的变量叫常量，常量必须初始化，初始化之后值就不能被修改。</font>

## 常见的关键字有哪些？	
+ **<font style="color:rgb(51,51,51);">static</font>**

<font style="color:rgb(51,51,51);">static</font><font style="color:rgb(51,51,51);">可以用来修饰类的成员方法、类的成员变量</font><font style="color:rgb(51,51,51);">。</font>

<font style="color:rgb(51,51,51);">static</font><font style="color:rgb(51,51,51);">变量也称作</font>**<font style="color:rgb(51,51,51);">静态变量</font>**<font style="color:rgb(51,51,51);">，静态变量和非静态变量的区别是：静态变量被所有的对象所共享，在内存中</font><font style="color:rgb(51,51,51);">只有一个副本，它当且仅当在类初次加载时会被初始化。而非静态变量是对象所拥有的，在创建对象的时候被初始化，存在多个副本，各个对象拥有的副本互不影响。</font>

<font style="color:rgb(51,51,51);">以下例子，age为非静态变量，则p1打印结果是：</font><font style="color:rgb(245,0,88);">Name:zhangsan, Age:10 </font><font style="color:rgb(51,51,51);">；若age使用static修饰，则p1打印结果是：</font><font style="color:rgb(245,0,88);">Name:zhangsan, Age:12 </font><font style="color:rgb(51,51,51);">，因为static变量在内存只有一个副本。</font>

```java
public class Person { 
    String name;
    int age;

    public String toString() {
        return "Name:" + name + ", Age:" + age;
    }

    public static void main(String[] args) {
        Person p1 = new Person();
        p1.name = "zhangsan"; p1.age = 10;
        Person p2 = new Person(); p2.name = "lisi";
        p2.age = 12; 
        System.out.println(p1);
        System.out.println(p2);
    }
    
    /**Output
	 *Name:zhangsan, Age:10
	 *Name:lisi, Age:12
	 *///~
}
```

  
<font style="color:rgb(51,51,51);">static方法一般称作</font>**<font style="color:rgb(51,51,51);">静态方法</font>**<font style="color:rgb(51,51,51);">。静态方法不依赖于任何对象就可以进行访问，通过类名即可调用静态方法。</font>

```java
public class Utils {
    public static void print(String s) { 
        System.out.println("hello world: " + s);
    }

    public static void main(String[] args) {
        Utils.print("程序员大彬");
    }
}
```

**<font style="color:rgb(51,51,51);">静态代码块</font>**<font style="color:rgb(51,51,51);">只会在类加载的时候执行一次。以下例子，startDate和endDate在类加载的时候进行赋值。</font>

```java
class Person {
    private Date birthDate;
    private static Date startDate, endDate; 
    static{
        startDate = Date.valueOf("2008"); 
        endDate = Date.valueOf("2021");
    }

    public Person(Date birthDate) { 
        this.birthDate = birthDate;
    }
}
```

**<font style="color:rgb(51,51,51);">静态内部类</font>**

**<font style="color:rgb(51,51,51);">在静态方法里</font>**<font style="color:rgb(51,51,51);">，使用⾮静态内部类依赖于外部类的实例，也就是说需要先创建外部类实例，才能用这个实例去创建非静态内部类。⽽静态内部类不需要。</font>

```java
public class OuterClass { 
    class InnerClass {
    }
    static class StaticInnerClass {
    }
    public static void main(String[] args) {
        //  在静态方法里，不能直接使用OuterClass.this去创建InnerClass的实例
        //  需要先创建OuterClass的实例o，然后通过o创建InnerClass的实例
        // InnerClass innerClass = new InnerClass(); 
        OuterClass outerClass = new OuterClass(); 
        InnerClass innerClass = outerClass.new InnerClass();
        StaticInnerClass staticInnerClass = new StaticInnerClass();


        outerClass.test();
    }


    public void nonStaticMethod() {
        InnerClass innerClass = new InnerClass(); 
        System.out.println("nonStaticMethod...");
    }
}
```

+ **<font style="color:rgb(51,51,51);">final</font>**

<font style="color:rgb(51,51,51);">1.</font><font style="color:rgb(51,51,51);"> </font>**<font style="color:rgb(51,51,51);">基本数据</font>**<font style="color:rgb(51,51,51);">类型用</font><font style="color:rgb(51,51,51);">final</font><font style="color:rgb(51,51,51);">修饰，则不能修改，是常量；</font>**<font style="color:rgb(51,51,51);">对象引用</font>**<font style="color:rgb(51,51,51);">用</font><font style="color:rgb(51,51,51);">final</font><font style="color:rgb(51,51,51);">修饰，则引用只能指向该对象，</font><font style="color:rgb(51,51,51);">不能指向别的对象，但是对象本身可以修改。</font>

<font style="color:rgb(51,51,51);">2.</font><font style="color:rgb(51,51,51);"> </font><font style="color:rgb(51,51,51);">final</font><font style="color:rgb(51,51,51);">修饰的方法不能被子类重</font><font style="color:rgb(51,51,51);">写</font>

<font style="color:rgb(51,51,51);">3.</font><font style="color:rgb(51,51,51);"> </font><font style="color:rgb(51,51,51);">final</font><font style="color:rgb(51,51,51);">修饰的类不能被继承</font><font style="color:rgb(51,51,51);">。</font>

+ **<font style="color:rgb(51,51,51);">this</font>**

<font style="color:rgb(245,0,88);">this.</font><font style="color:rgb(245,0,88);">属性名称</font><font style="color:rgb(245,0,88);"> </font><font style="color:rgb(51,51,51);">指访问类中的成员变量，可以用来区分成员变量和局部变量。如下代码所示</font><font style="color:rgb(51,51,51);">，</font>

<font style="color:rgb(245,0,88);">this.name </font><font style="color:rgb(51,51,51);">访问类Person当前实例的变量。</font>

```java
/**
 * @description:
 *@author: 程序员大彬
 *@time: 2021-08-17 00:29
 */
public class Person { 
    String name;
    int age;

    public Person(String name, int age) { 
        this.name = name;
        this.age = age;
    }
}
```

<font style="color:rgb(245,0,88);">this.方法名称 </font><font style="color:rgb(51,51,51);">用来访问本类的方法。以下代码中，</font><font style="color:rgb(245,0,88);">this.born() </font><font style="color:rgb(51,51,51);">调用类 Person 的当前实例的方法。</font>

```java
/**
*@description:
*@author: 程序员大彬
*@time: 2021-08-17 00:29
*/
public class Person {
    String name;
    int age;


    public Person(String name, int age) { 
        this.born();
        this.name = name; 
        this.age = age;
    }


    void born() {
    }
}
```

+ **<font style="color:rgb(51,51,51);">super</font>**

<font style="color:rgb(51,51,51);">super  关键字用于在子类中访问父类的变量和方法。</font>

```java
class A {
    protected String name = "大彬";


    public void getName() {
        System.out.println("父类:" + name);
    }
}


public class B extends A {
    @Override
    public void getName() { 
        System.out.println(super.name); super.getName();
    }


    public static void main(String[] args) {
        B b = new B();
        b.getName();
    }
    /**
     *大彬
     *父类:大彬
     */
}
```

<font style="color:rgb(51,51,51);">在子类B中，我们重写了父类的</font><font style="color:rgb(245,0,88);">getName() </font><font style="color:rgb(51,51,51);">方法，如果在重写的</font><font style="color:rgb(245,0,88);">getName() </font><font style="color:rgb(51,51,51);">方法中我们要调用父类的相同方法，必须要通过super关键字显式指出。</font>

## Java 关键字
Java的关键字有哪些？

1、48个关键字：abstract、assert、boolean、break、byte、case、catch、char、class、continue、default、do、double、else、enum、extends、final、finally、float、for、if、implements、import、int、interface、instanceof、long、native、new、package、private、protected、public、return、short、static、strictfp、super、switch、synchronized、this、throw、throws、transient、try、void、volatile、while。

2、2个保留字（现在没用以后可能用到作为关键字）：goto、const。

3、3个特殊直接量：true、false、null。

> [Java关键字（48个关键字、2个保留字、3个特殊直接量）_爱打羽球的码猿的博客-CSDN博客_java关键字](https://blog.csdn.net/weixin_46822367/article/details/120953556)
>

## static 关键字的使用
1）类成员，直接使用类名.成员 调用。

2）静态方法只能访问静态成员。

3）静态方法不能使用this、super 关键字。

4）静态方法不能被非静态方法重写或重载。

## final 关键字
1） 被final 修饰的变量为常量不能改变。

2） 被final 修饰的方法不可以重写。

3） 被final 修饰的类不能被继承。 

## abstract 关键字
1） 被abstract 修饰的类不能实例化。

2） 被abstract 修饰的方法只能在子类中实现。

## native 关键字
非 Java 语言的编写，例如 JNI 技术。

## synchronized 关键字
多线程的同步访问控制。

## <font style="color:rgb(49,49,49);">final的用途</font>
1. final 修饰类时，这个类不能被继承了
2. final 修饰方法，此方法就不能被重写。 eg：object类中的getClas 方法
3. final 修饰变量，这个时候的变量就是一个常量。
    1. final 可以修饰属性
    2. final 可以修饰局部变量，尤其是使用final修饰形参时，表明此形参是一个常量，当我们调用此方法时，给给常量形参赋一个实参，一旦赋值以后，就只能在方法体内使用此形参，但不能进行重新赋值
4. static final 用来修饰属性 ：全局变量

> [final的作用_阿离83的博客-CSDN博客_final的作用](https://blog.csdn.net/weixin_45933454/article/details/112985755)
>

## <font style="color:rgb(36,41,46);">static和final的区别和用途</font>
+ Static
    - 修饰变量：静态变量随着类加载时被完成初始化，内存中只有一个，且JVM也只会为它分配一次内存，所有类共享静态变量。
    - 修饰方法：在类加载的时候就存在，不依赖任何实例；static方法必须实现，不能用abstract修饰。
    - 修饰代码块：在类加载完之后就会执行代码块中的内容。
    - 父类静态代码块 -> 子类静态代码块 -> 父类非静态代码块 -> 父类构造方法 -> 子类非静态代码块 -> 子类构造方法
+ Final
    - 修饰变量：
        * 编译期常量：类加载的过程完成初始化，编译后带入到任何计算式中。只能是基本类型。
        * 运行时常量：基本数据类型或引用数据类型。引用不可变，但引用的对象内容可变。
    - 修饰方法：不能被继承，不能被子类修改。
    - 修饰类：不能被继承。
    - 修饰形参：final形参不可变

## <font style="color:rgb(36,41,46);">关于 final 关键字的一些总结</font>
<font style="color:rgb(36,41,46);">final 关键字主要用在三个地方：变量、方法、类。</font>

<font style="color:rgb(36,41,46);">1. 对于一个final 变量，如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能再让其指向另一个对象。</font>

<font style="color:rgb(36,41,46);">2.</font><font style="color:rgb(36,41,46);"> </font><font style="color:rgb(36,41,46);">当用</font><font style="color:rgb(36,41,46);">final</font><font style="color:rgb(36,41,46);"> </font><font style="color:rgb(36,41,46);">修饰一个类时，表明这个类不能被继承。</font><font style="color:rgb(36,41,46);">final</font><font style="color:rgb(36,41,46);"> </font><font style="color:rgb(36,41,46);">类中的所有成员</font><font style="color:rgb(36,41,46);">方法都会被隐式地指定为</font><font style="color:rgb(36,41,46);">final </font><font style="color:rgb(36,41,46);">方法。</font>

<font style="color:rgb(36,41,46);">3.</font><font style="color:rgb(36,41,46);"> </font><font style="color:rgb(36,41,46);">使用</font><font style="color:rgb(36,41,46);">final</font><font style="color:rgb(36,41,46);"> </font><font style="color:rgb(36,41,46);">方法的原因有两个。</font>

<font style="color:rgb(36,41,46);">第一个原因是把方法锁定，以防任何继承类修改它的含义；</font>

<font style="color:rgb(36,41,46);">第二个原因是效率。在早期的Java 实现版本中，会将final 方法转为内嵌调用。但是如果方法过于庞大，可能看不到内嵌调用带来的任何性能提升（现在的Java 版本已经不需要使用final 方法进行这些优化了）。类中所有的private 方法都隐式地指定为final。</font>

## <font style="color:rgb(36,41,46);">创建一个对象用什么运算符?对象实体与对象引用有何不同?</font>
<font style="color:rgb(36,41,46);">new 运算符，new 创建对象实例（对象实例在堆内存中），对象引用指向对象实例（对象引用存放在栈内存中）。一个对象引用可以指向0 个或1 个对象（一根绳子可以不系气球，也可以系一个气球）;一个对象可以有n 个引用指向它（可以用n 条绳子系住一个气球）。</font>

## final、finally、finalize的区别
+ final可以修饰类、变量、方法，修饰类表示该类不能被继承、修饰方法表示该方法不能被重写、修饰变量表示该变量是一个常量不能被重新赋值。
+ finally一般作用在try-catch代码块中，在处理异常的时候，通常我们将一定要执行的代码方法finally代码块中，表示不管是否出现异常，该代码块都会执行，一般用来存放一些关闭资源的代码。
+ finalize是一个方法，属于Object类的一个方法，而Object类是所有类的父类，该方法一般由垃圾回收器来调用，当我们调用System.gc() 方法的时候，由垃圾回收器调用finalize()，回收垃圾，一个对象是否可回收的最后判断。

### <font style="color:#E8323C;">final、 finally、 finalize 的区别</font>
1. final

修饰符（关键字）。

如果一个类被声明为final，意味着它不能再派生出新的子类，不能作为父类被继承。因此一个类不能既被声明为 abstract的，又被声明为final的。将变量或方法声明为final，可以保证它们在使用中不被改变。被声明为final的变量必须在声明时给定初值，而在以后的引用中只能读取，不可修改。被声明为final的方法也同样只能使用，不能重载。

2. finally

代码块。

在异常处理时提供 finally 块来执行任何清除操作。如果抛出一个异常，那么相匹配的 catch 子句就会执行，然后控制就会进入 finally 块（如果有的话）。

3. finalize

方法名。

Java 技术允许使用 finalize() 方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。

这个方法是由垃圾收集器在确定这个对象没有被引用时对这个对象调用的，换句话说，finalize() 方法是在垃圾收集器删除对象之前对这个对象调用的。。

它是在 Object 类中定义的，因此所有的类都继承了它，子类覆盖 finalize() 方法以<u>整理系统资源或者执行其他清理工作</u>。

finalize()方法是对象逃脱死亡命运的最后一次机会。当对象没有被任何引用链相连时，会被GC第一次标记，并将对象放入F-Queue中。稍后，GC会对F-Queue中的对象进行第二次小规模的标记，对象如果要在finalize()中成功拯救自己，需要重新与引用链上的任何一个对象建立关联，譬如把自己(this关键字)赋值给某个类变量或对象的成员变量，那在第二次标记时它将被移除“即将回收”的集合。

特点：

（1）对象可以在被GC时自我拯救

（2）这种自救的机会只有一次，因为一个对象的finalize()方法最多只会被系统自动调用一次

### <font style="color:#CF1322;">Java 有没有 goto ?</font>
<font style="color:rgb(79,79,79);">goto 是Java中的保留字，在目前版本的Java中没有使用。（根据James Gosling（Java之父）编写的《The Java Programming Language》一书的附录中给出了一个Java关键字列表，其中有goto和const，但是这两个是目前无法使用的关键字，因此有些地方将其称之为保留字，其实保留字这个词应该有更广泛的意义，因为熟悉C语言的程序员都知道，在系统类库中使用过的有特殊意义的单词或单词的组合都被视为保留字）</font>

### 访问修饰符public，private，protected，以及不写（默认）时的区别？
区别如下：

| 作用域   |   当前类  |  同包  |  子类  |  其他 |
| --- | --- | --- | --- | --- |
| public | √ | √ | √ | √ |
| protected | √ | √ | √ | × |
| default | √ | √ | × | × |
| private | √ | × | × | × |


### 访问修饰符限制
|  | private | protected | friendly(default) |  public |
| --- | --- | --- | --- | --- |
| 同包不同 | N | Y | Y | Y |
| 同包子类 | N | Y | Y | Y |
| 不同包不同类 | N | N | N | Y |
| 不同包子类 | N | Y | N | Y |


### 请结合OO设计理念，谈谈访问修饰符public、private、protected、default在应用设计中的作用
> [浅谈java中OO的概念和设计原则(必看)_java_脚本之家](https://www.jb51.net/article/114223.htm)
>
> [访问修饰符 public、private、protected、default 在应用设计中的作用-尚硅谷java培训](http://java.atguigu.com/news/2936.html)
>





> 更新: 2022-12-02 23:35:00  
> 原文: <https://www.yuque.com/joyo/interview/wo4qum>