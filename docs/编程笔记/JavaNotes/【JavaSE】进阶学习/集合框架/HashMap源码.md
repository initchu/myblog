# HashMap 源码

```java
put("aaa",444);
```

```java
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}
```

# 扰动函数
```java
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```

在HashMap存放元素时候有上面这样一段代码来处理哈希值，这是 java 8 的散列值扰动函数，用于优化散列效果。

目的是：数据分配均匀，也就是散列的效果更好，减少了hash的碰撞，让数据存放和获取的效率更佳。

# 负载因子
**负载因子是做什么的？**

负载因子，可以理解成一辆车可承重重量超过某个阈值时，把货放到新的车上。

那么在HashMap中，**<u>负载因子决定了数据量多少了以后进行扩容</u>**。

比如，我们准备了7个元素，但是最后还有3个位置空余，2个位置存放了2个元素。 

所以可能即使你数据比数组容量大时也是不一定能正正好好的把数组占满的，而是在某些小标位置出现了大量的碰撞，只能在同一个位置用链表存放，那么这样就失去了Map数组的性能。

所以，要选择一个合理的大小下进行扩容，**<u>默认值0.75就是说当阈值容量占了3/4时赶紧扩容，减少Hash碰撞</u>**。

同时0.75是一个默认构造值，在创建HashMap也可以调整，比如你希望用更多的空间换取时间，可以把负载因子调的更小一些，减少碰撞。

# 添加元素
添加元素的时候考虑有三种情况：

1. 数组位置为null
2. 数组位置不为null，键不重复，挂在下面形成链表或者红黑树
3. 数组位置不为null，键重复，元素覆盖

```java
// 1. 哈希值
// 2. 键
// 3. 值
// 4. 如果键重复了是否保留，
// 	true：老元素的值保留，不会覆盖
// 	false：表示老元素的值不保留，会进行覆盖
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,boolean evict) {
	// 定义一个局部变量，记录哈希表的数组的地址值（之前有个堆里面的，不用那个是因为写方法里面会更快）
	Node<K,V>[] tab; 
	// 临时的第三方变量，用来记录键值对对对象的地址值
	Node<K,V> p; 
	// 数组长度和索引
	int n, i; 
	// 1. 如果当前是第一次添加数据，底层创建一个默认长度为16，加载因子为0.75的数组
	// 2. 如果不是第一次添加数据，会看数组中的元素是否达到了扩容的条件
	// 如果没有达到扩容条件，底层不会做任何操作
	// 如果达到了，底层会把数据扩容为原来的两倍，并把数据全部转移到新的哈希表中
	if ((tab = table) == null || (n = tab.length) == 0){
		tab = resize();
		// 把当前数组的长度复制给 n
		n = (tab).length;
	}
	// 拿这数组长度的跟键的哈希值进行计算，计算出当前键值对对象，在数组中应存入的位置
	i = (n-1) & hash; // index
	// 获取数组中对应元素的数据
	p = tab[i];

	if ((p == null){
		// 创建一个键值对对象，直接放到数组当中
		tab[i] = newNode(hash, key, value, null);
	} else {
		// 键不重复，挂在下面形成链表或者红黑树
		Node<K,V> e; K k;
		
		// 数组中的哈希值和要添加的元素值进行比较,键不一样返回 false
		boolean b1 = p.hash == hash;
		
		if (b1 &&((k = p.key) == key || (key != null && key.equals(k))))
			e = p; 
		else if (p instanceof TreeNode)
			// 从数组中取出来的键值对是不是是不是红黑树的节点
			// 如果是，则调用 putTreeVal 按照红黑树的规则添加
			e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
		else {
			// 如果从数组中后取出来的键值对不是红黑树中的节点
			// 表示挂在链表下
			for (int binCount = 0; ; ++binCount) { 
				if ((e = p.next) == null) {
					// 创建新节点挂在链表下面
					p.next = newNode(hash, key, value, null);
					// 判断长度是否超过8
					if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
						// treeifyBin 会判断数组的长度是否大于等于64，
						// 大于则转化成红黑树
						treeifyBin(tab, hash);
					break;
				}
				// 如果哈希值一样，就会调用equals放啊比较内部的属性值是否相同
				if (e.hash == hash &&((k = e.key) == key || (key != null && key.equals(k))))
					break;
				p = e;
			}
		}
		// 键重复，元素覆盖 
		if (e != null) { // existing mapping for key
			V oldValue = e.value;
			// onlyIfAbsent: 如果键重复了是否保留，
			// 	true：老元素的值保留，不会覆盖
			// 	false：表示老元素的值不保留，会进行覆盖
			if (!onlyIfAbsent || oldValue == null){
				// 仅修改键值对里面的值，键值对还是原来的
				e.value = value;
			}
			afterNodeAccess(e);
			return oldValue;
		}
	}
	// 用于判断并发修改异常判断的值
	++modCount;
	// size 先自增
	// threshold：记录的是 数组的长度 * 0.75，哈希表的扩容时机 16 * 0.75 = 12
	if (++size > threshold){
		resize();
	}
	// 这是个linkHashMap有关的，在hashMap中忽略这段逻辑
	afterNodeInsertion(evict);
	// 没有覆盖任何元素，返回null
	return null;
}
```





































> 更新: 2024-05-21 09:45:34  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/nrivza3r37ieur6x>