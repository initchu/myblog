# Set

### HashSet 底层原理？
HashSet **基于 HashMap 实现**。放入 HashSet 中的元素实际上由 HashMap 的 key 来保存，而 HashMap 的 value 则存储了一个静态的 Object 对象：PRESENT。

```java
public class HashSet<E> extends AbstractSet<E> 
    	implements Set<E>, Cloneable, java.io.Serializable {
            
    static final long serialVersionUID = -5024744406713321676L;

    private transient HashMap<E,Object> map; //基于HashMap实现
    // ...
}
```

### HashSet、LinkedHashSet 和 TreeSet 的区别？ 
HashSet 直接实现了 Set 接口，LinkedHashSet 继承了 HashSet，TreeSet实现了 SortedSet 接口

+ HashSet 是 Set 接口的主要实现类 ， HashSet 的底层是 HashMap ，线程不安全的，可以存储 null 值； 
+ <u>LinkedHashSet 是</u>**<u> HashSet 的子类</u>**，能够按照**添加的顺序**遍历； 
+ <u>TreeSet 底层使用</u>**<u>红黑树</u>**，能够按照**添加元素的顺序**进行遍历，排序的方式**可以自定义**。 

### HashSet 是如何保证不重复的
向 HashSet 中 add 元素时，判断元素是否存在的依据，不仅要**比较hash值**，同时还要**结合 equles 方法比较**。 

HashSet 中的 add 方法会使用 HashMap 的 put 方法。以下是 HashSet 部分源码：

```java
private static final Object PRESENT = new Object(); 
private transient HashMap<E,Object> map; 

public HashSet() { 
	map = new HashMap<>(); 
}

public boolean add(E e) { 
	return map.put(e, PRESENT)==null; 
}

```

HashMap 的 key 是唯一的，由上面的代码可以看出 HashSet 添加进去的值就是作为 HashMap 的 key。所以不会重复。

<u>所以，HashMap 比较key是否相等是</u>**<u>先比较 hashcode 再使用 equals 方法比较</u>**。

### Java中的HashSet内部是如何工作的？
HashSet 的内部采用 HashMap来实现。由于 Map 需要 key 和 value，所以HashSet中所有 key 的都有一个默认 value。

类似于HashMap，HashSet 不允许重复的 key，只允许有一个null key，意思就是 HashSet 中只允许存储一个 null 对象。

> [java中的HashSet内部是如何工作的_杭州小哥哥的博客-CSDN博客](https://blog.csdn.net/W_317/article/details/122223742)
>

### HashSet 是如何保证不重复的 
+ 向 HashSet 中 add() 元素时，判断元素是否存在的依据，不仅要**比较hash值**，同时还要**结合 equles() 方法**比较。 
+ HashSet 中的 add() 方法会使用 HashMap 的 add() 方法。以下是 HashSet 部分源码： 

```java
private static final Object PRESENT = new Object();
private transient HashMap<E,Object> map;
public HashSet() {
    map = new HashMap<>();
}
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}
```

HashMap 的 key 是唯一的，由上面的代码可以看出 HashSet 添加进去的值就是作为 HashMap 的key。所以不会重复。HashMap 比较 key 是否相等是先比较 hashcode 再调用 equals() 方法。 	



> 更新: 2023-07-14 01:26:59  
> 原文: <https://www.yuque.com/joyo/interview/obfm0zo09s7ybfy5>