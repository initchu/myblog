# C ++ STL 介绍

<font style="color:#000000;">在实际的开发过程中，合理组织数据的存取与选择处理数据的算法同等重要，存取数据的方式往往会直接影响到对它们进行增删改查操作的复杂程度和时间消耗。</font>

<font style="color:#000000;">事实上，当程序中存在对时耗要求很高的部分时，</font><font style="color:#000000;">数据结构</font><font style="color:#000000;">的选择就显得尤为重要，有时甚至直接影响程序执行的成败。</font>

<font style="color:#000000;">值得一提的是，之前我们一直在不断地重复实现一些诸如链表、集合等等这些常见的数据结构，这些代码使用起来往往都十分类似，只是为了适应不同数据的变化，可能需要在一些细节上做不同的处理。</font>

<font style="color:#000000;">所以，可以重复利用那些已有的实现来完成当前的任务。STL 中提供了专家级的几乎我们所需要的各种容器，功能更好，复用性更高。简单的理解容器，它就是一些模板类的集合，但和普通模板类不同的是，容器中封装的是组织数据的方法（也就是数据结构）。STL 提供有 3 类标准容器，分别是序列容器、排序容器和哈希容器，其中后两类容器有时也统称为关联容器。它们各自的含义如下表所示。</font>

| **<font style="color:rgb(68, 68, 68);">容器种类</font>** | **<font style="color:rgb(68, 68, 68);">功能</font>** |
| :---: | --- |
| <font style="color:rgb(68, 68, 68);">序列容器</font> | <font style="color:rgb(68, 68, 68);">主要包括 vector 向量容器、list 列表容器以及 deque 双端队列容器。之所以被称为序列容器，是因为元素在容器中的位置同元素的值无关，即容器不是排序的。将元素插入容器时，指定在什么位置，元素就会位于什么位置。</font> |
| <font style="color:rgb(68, 68, 68);">排序容器</font> | <font style="color:rgb(68, 68, 68);">包括 set 集合容器、multiset多重集合容器、map映射容器以及 multimap 多重映射容器。排序容器中的元素默认是由小到大排序好的，即便是插入元素，元素也会插入到适当位置。所以关联容器在查找时具有非常好的性能。</font> |
| <font style="color:rgb(68, 68, 68);">哈希容器</font> | C++<font style="color:rgb(68, 68, 68);"> 11 新加入 4 种关联式容器，分别是 unordered_set 哈希集合、unordered_multiset 哈希多重集合、unordered_map 哈希映射以及 unordered_multimap 哈希多重映射。和排序容器不同，哈希容器中的元素是未排序的，元素的位置由哈希函数确定。</font> |


:::info
注意：由于哈希容器直到 C++ 11 才被正式纳入 C++ 标准程序库，而在此之前，“民间”流传着 hash_set、hash_multiset、hash_map、hash_multimap 版本，不过该版本只能在某些支持 C++ 11 的编译器下使用（如 VS），有些编译器（如 gcc/g++）是不支持的。

:::



<font style="color:rgb(102, 102, 102);background-color:rgb(249, 249, 249);"></font>



> 更新: 2023-07-25 17:36:15  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/ff4izp4glir44lv9>