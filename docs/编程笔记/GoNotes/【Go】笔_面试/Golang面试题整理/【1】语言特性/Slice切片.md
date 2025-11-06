# Slice 切片

# <font style="color:rgb(51,51,51);">Golang 里的数组和切片有了解过吗？ </font>
**<font style="color:rgb(119,119,119);">题目序号：</font>**<font style="color:rgb(119,119,119);">（</font><font style="color:rgb(119,119,119);">3683</font><font style="color:rgb(119,119,119);">，</font><font style="color:rgb(119,119,119);">4095</font><font style="color:rgb(119,119,119);">，</font><font style="color:rgb(119,119,119);">481</font><font style="color:rgb(119,119,119);">） </font>

**<font style="color:rgb(119,119,119);">题目来源： </font>**<font style="color:rgb(119,119,119);">深信服、知乎、跟谁学 </font>

**<font style="color:rgb(119,119,119);">频次: </font>**<font style="color:rgb(119,119,119);">3</font>

<font style="color:rgb(51,51,51);">数组长度是固定的，而切片是可变长的。可以把切片看作是对底层数组的封装，每个切片的底层数据结构中，一定会包含一个数组。数组可以被称为切片的底层数组，切片也可以被看作对数组某一连续片段的引用。因此，Go 中切片属于引用类型，而数组属于值类型，通过内建函数 len，可以取得数组和切片的长度。通过内建函数 cap，可以得到数组和切片的容量。但是数组的长度和容量是相等的，并且都不可变，而且切片容量是有变化规律的。切片一旦初始化， 切片始终与保存其元素的基础数组相关联。因此，切片会和与其拥有同一基础数组的其他切片共享存储 ; 相比之下，不同的数组总是代表不同的存储。</font>

<font style="color:rgb(51,51,51);">数组和切片的关系： </font>

<font style="color:rgb(51,51,51);">切片一旦初始化， 切片始终与保存其元素的基础数组相关联。因此，切片会和与其拥有同一基础数组的其他切片共享存储 ; 相比之下，不同的数组总是代表不同的存储。 </font>

<font style="color:rgb(51,51,51);">数组和切片的区别 </font>

<font style="color:rgb(51,51,51);">1. 切片的长度可能在执行期间发生变化 ，而数组的长度不能变化，可以把切片看成一个长度可变的数组。 </font>

<font style="color:rgb(51,51,51);">2. 数组作为函数参数是进行值传递的，函数内部改变传入的数组元素值不会影响函数外部数组的元素值； 切片作为函数的参数是进行的指针传递，函数内部改变切片的值会影响函数外部的切片元素值。 </font>

<font style="color:rgb(51,51,51);">3. 数组可以比较，切片不能比较(对底层数组的引用)。</font>

**<font style="color:rgb(51,51,51);">1. Go</font>****<font style="color:rgb(51,51,51);">切片和</font>****<font style="color:rgb(51,51,51);">Go</font>****<font style="color:rgb(51,51,51);">数组 </font>**

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">切片，又称动态数组，它实际是基于数组类型做的一层封装。 </font>

**<font style="color:rgb(51,51,51);">Go</font>****<font style="color:rgb(51,51,51);">数组 </font>**

<font style="color:rgb(51,51,51);">数组是内置</font><font style="color:rgb(51,51,51);">(build-in)</font><font style="color:rgb(51,51,51);">类型</font><font style="color:rgb(51,51,51);">,</font><font style="color:rgb(51,51,51);">是一组同类型数据的集合，它是值类型，通过从</font><font style="color:rgb(51,51,51);">0</font><font style="color:rgb(51,51,51);">开始的下标索引访问元素 </font>

<font style="color:rgb(51,51,51);">值。在初始化后长度是固定的，无法修改其长度。当作为方法的参数传入时将复制一份数组而不是引用 </font>

<font style="color:rgb(51,51,51);">同一指针。数组的长度也是其类型的一部分，通过内置函数</font><font style="color:rgb(51,51,51);">len(array)</font><font style="color:rgb(51,51,51);">获取其长度。 </font>

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">数组与像</font><font style="color:rgb(51,51,51);">C/C++</font><font style="color:rgb(51,51,51);">等语言中数组略有不同，如下 </font>

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">中的数组是值类型，换句话说，如果你将一个数组赋值给另外一个数组，那么，实际上就是将 </font>

<font style="color:rgb(51,51,51);">整个数组拷贝一份。因此，在</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">中如果将数组作为函数的参数传递的话，那效率就肯定没有传递 </font>

<font style="color:rgb(51,51,51);">指针高了。 </font>

<font style="color:rgb(51,51,51);">数组的长度也是类型的一部分，这就说明 </font><font style="color:rgb(51,51,51);">[10]int </font><font style="color:rgb(51,51,51);">和 </font><font style="color:rgb(51,51,51);">[20]int </font><font style="color:rgb(51,51,51);">不是同一种数据类型。 </font>

**<font style="color:rgb(51,51,51);">Go</font>****<font style="color:rgb(51,51,51);">切片</font>**<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">语言中数组的长度是固定的，且不同长度的数组是不同类型，这样的限制带来不少局限性。 </font>

<font style="color:rgb(51,51,51);">而切片则不同，切片（</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">）是一个拥有相同类型元素的可变长序列，可以方便地进行扩容和传递，实 </font>

<font style="color:rgb(51,51,51);">际使用时比数组更加灵活，这也正是切片存在的意义。 </font>

<font style="color:rgb(51,51,51);">切片是引用类型，因此在当传递切片时将引用同一指针，修改值将会影响其他的对象。 </font>

**<font style="color:rgb(51,51,51);">2. </font>****<font style="color:rgb(51,51,51);">切片底层 </font>**

<font style="color:rgb(51,51,51);">现在就来看一下</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">语言切片的底层是什么样子吧！ </font>

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">切片</font><font style="color:rgb(51,51,51);">(slice)</font><font style="color:rgb(51,51,51);">的实现可以在源码包 </font><font style="color:rgb(51,51,51);">src/runtime/slice.go </font><font style="color:rgb(51,51,51);">中找到。在源码中，</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的数据结构定义如 </font>

<font style="color:rgb(51,51,51);">下。 </font>

<font style="color:rgb(119,0,136);">type </font><font style="color:rgb(0,0,0);">slice </font><font style="color:rgb(119,0,136);">struct </font><font style="color:rgb(51,51,51);">{ </font>

<font style="color:rgb(0,0,0);">array unsafe</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Pointer </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">指向底层数组的指针 </font>

<font style="color:rgb(34,17,153);">len </font><font style="color:rgb(119,0,136);">int </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">切片长度 </font>

<font style="color:rgb(34,17,153);">cap </font><font style="color:rgb(119,0,136);">int </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">切片容量 </font>

<font style="color:rgb(51,51,51);">} </font>

<font style="color:rgb(51,51,51);">可以看到，组成</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">切片的三元组分别为指向底层数组的指针，切片长度和切片容量。 </font>

<font style="color:rgb(51,51,51);">1. </font><font style="color:rgb(51,51,51);">指向底层数组的指针 </font>

<font style="color:rgb(51,51,51);">前面已经提到，切片实际是对数组的一层封装。这个指针便是记录其底层数组的地址，也正是切片 </font>

<font style="color:rgb(51,51,51);">开始的位置。 </font>

<font style="color:rgb(51,51,51);">2. </font><font style="color:rgb(51,51,51);">切片长度 </font>

<font style="color:rgb(51,51,51);">len </font><font style="color:rgb(51,51,51);">表示切片的长度，即切片中现存有效元素的个数，它不能超过切片的容量。可以通过 </font><font style="color:rgb(51,51,51);">len() </font><font style="color:rgb(51,51,51);">函 </font>

<font style="color:rgb(51,51,51);">数获取切片长度。 </font>

<font style="color:rgb(51,51,51);">3. </font><font style="color:rgb(51,51,51);">切片容量 </font>

<font style="color:rgb(51,51,51);">cap </font><font style="color:rgb(51,51,51);">表示切片的容量，即切片能存储元素的多少，通常是从切片的起始元素到底层数组的最后一个 </font>

<font style="color:rgb(51,51,51);">元素间的元素个数，当切片容量不足时，便会触发</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">扩容。可以通过 </font><font style="color:rgb(51,51,51);">cap() </font><font style="color:rgb(51,51,51);">函数获取切片容量。 </font>

<font style="color:rgb(51,51,51);">下图展示了一个</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">切片的底层数据结构，这个切片的长度为</font><font style="color:rgb(51,51,51);">3</font><font style="color:rgb(51,51,51);">，容量为</font><font style="color:rgb(51,51,51);">6</font><font style="color:rgb(51,51,51);">。</font>**<font style="color:rgb(51,51,51);">3. </font>****<font style="color:rgb(51,51,51);">切片使用 </font>**

<font style="color:rgb(51,51,51);">1. </font><font style="color:rgb(51,51,51);">切片定义方式 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">a </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int </font><font style="color:rgb(170,85,0);">//nil</font><font style="color:rgb(170,85,0);">切片，和</font><font style="color:rgb(170,85,0);">nil</font><font style="color:rgb(170,85,0);">相等，一般用来表示一个不存在的切片 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">b </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{} </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">空切片，和</font><font style="color:rgb(170,85,0);">nil</font><font style="color:rgb(170,85,0);">不相等，一般用来表示一个空的集合 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">c </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">} </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">有</font><font style="color:rgb(170,85,0);">3</font><font style="color:rgb(170,85,0);">个元素的切片，</font><font style="color:rgb(170,85,0);">len</font><font style="color:rgb(170,85,0);">和</font><font style="color:rgb(170,85,0);">cap</font><font style="color:rgb(170,85,0);">都为</font><font style="color:rgb(170,85,0);">3 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">d </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">c</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">] </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">有</font><font style="color:rgb(170,85,0);">2</font><font style="color:rgb(170,85,0);">个元素的切片，</font><font style="color:rgb(170,85,0);">len</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">2</font><font style="color:rgb(170,85,0);">，</font><font style="color:rgb(170,85,0);">cap</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">3 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">e </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">c</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(34,17,153);">cap</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">c</font><font style="color:rgb(51,51,51);">)] </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">有</font><font style="color:rgb(170,85,0);">2</font><font style="color:rgb(170,85,0);">个元素的切片，</font><font style="color:rgb(170,85,0);">len</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">2</font><font style="color:rgb(170,85,0);">，</font><font style="color:rgb(170,85,0);">cap</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">3 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">f </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">c</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">] </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">有</font><font style="color:rgb(170,85,0);">0</font><font style="color:rgb(170,85,0);">个元素的切片，</font><font style="color:rgb(170,85,0);">len</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">0</font><font style="color:rgb(170,85,0);">，</font><font style="color:rgb(170,85,0);">cap</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">3 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">g </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">make</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">创建一个切片，</font><font style="color:rgb(170,85,0);">len</font><font style="color:rgb(170,85,0);">和</font><font style="color:rgb(170,85,0);">cap</font><font style="color:rgb(170,85,0);">均为</font><font style="color:rgb(170,85,0);">3 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">h </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">make</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">6</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">创建一个切片，</font><font style="color:rgb(170,85,0);">len</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">3</font><font style="color:rgb(170,85,0);">，</font><font style="color:rgb(170,85,0);">cap</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">5 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">i </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">make</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">创建一个切片，</font><font style="color:rgb(170,85,0);">len</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">0</font><font style="color:rgb(170,85,0);">，</font><font style="color:rgb(170,85,0);">cap</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">3 </font>

<font style="color:rgb(51,51,51);">2. </font><font style="color:rgb(51,51,51);">从数组中切取切片 </font>

<font style="color:rgb(51,51,51);">数组和切片是紧密相连的。切片可以用来访问数组的部分或全部元素，而这个数组称为切片的底层 </font>

<font style="color:rgb(51,51,51);">数组。切片的指针指向数组第一个可以从切片中访问的元素，这个元素并不一定是数组的第一个元 </font>

<font style="color:rgb(51,51,51);">素。 </font>

<font style="color:rgb(51,51,51);">一个底层数组可以对应多个切片，这些切片可以引用数组的任何位置，彼此之前的元素可以重叠。 </font>

<font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">操作符 </font><font style="color:rgb(51,51,51);">s[i:j] </font><font style="color:rgb(51,51,51);">创建了一个新的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">，这个新的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">引用了</font><font style="color:rgb(51,51,51);">s</font><font style="color:rgb(51,51,51);">中从</font><font style="color:rgb(51,51,51);">i</font><font style="color:rgb(51,51,51);">到</font><font style="color:rgb(51,51,51);">j-1</font><font style="color:rgb(51,51,51);">索引位置的所有元素。 </font>

<font style="color:rgb(51,51,51);">如果表达式省略了</font><font style="color:rgb(51,51,51);">i</font><font style="color:rgb(51,51,51);">，那么默认是 </font><font style="color:rgb(51,51,51);">s[0:j] </font><font style="color:rgb(51,51,51);">；如果省略了</font><font style="color:rgb(51,51,51);">j</font><font style="color:rgb(51,51,51);">，默认是 </font><font style="color:rgb(51,51,51);">s[i:len(s)] </font><font style="color:rgb(51,51,51);">；</font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">示例来源：</font><font style="color:rgb(170,85,0);">The Go Programming Language </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">创建一个数组 </font>

<font style="color:rgb(0,0,0);">months </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">]</font><font style="color:rgb(119,0,136);">string</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(170,17,17);">"January"</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(170,85,0);">/*...*/</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">12</font><font style="color:rgb(51,51,51);">: </font><font style="color:rgb(170,17,17);">"December"</font><font style="color:rgb(51,51,51);">} </font>

<font style="color:rgb(0,0,0);">Q2 </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">months</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">4</font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(17,102,68);">7</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(0,0,0);">summer </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">months</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">6</font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(17,102,68);">9</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">Q2</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//["April" "May" "June"] </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">summer</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//["June" "July" "August"] </font>

<font style="color:rgb(51,51,51);">月份名称字符串数组与其对应的两个元素重叠的</font><font style="color:rgb(51,51,51);">slice </font><font style="color:rgb(51,51,51);">图示 </font>

<font style="color:rgb(119,119,119);">注意：切片与原数组或切片共享底层空间，修改切片会影响原数组或切片 </font>

<font style="color:rgb(51,51,51);">3. </font><font style="color:rgb(51,51,51);">迭代切片 </font>

<font style="color:rgb(51,51,51);">切片可以用</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">迭代，但是要注意：如果只用一个值接收</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">，则得到的只是切片的下标，用 </font>

<font style="color:rgb(51,51,51);">两个值接收</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">，则得到的才是下标和对应的值。 </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">使用一个值接收</font><font style="color:rgb(170,85,0);">range, </font><font style="color:rgb(170,85,0);">则得到的是切片的下标 </font>

<font style="color:rgb(119,0,136);">for </font><font style="color:rgb(0,0,0);">i </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(119,0,136);">range </font><font style="color:rgb(0,0,0);">months </font><font style="color:rgb(51,51,51);">{ </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">返回下标 </font><font style="color:rgb(170,85,0);">0 1 ... 12 </font>

<font style="color:rgb(51,51,51);">}</font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">使用两个值接收</font><font style="color:rgb(170,85,0);">range</font><font style="color:rgb(170,85,0);">，则得到的是下标和对应的值 </font>

<font style="color:rgb(119,0,136);">for </font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">v </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(119,0,136);">range </font><font style="color:rgb(0,0,0);">months </font><font style="color:rgb(51,51,51);">{ </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">v</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">返回下标</font><font style="color:rgb(170,85,0);">0 1 ... 12 </font><font style="color:rgb(170,85,0);">和 值 </font><font style="color:rgb(170,85,0);">"" "January" ... "December" </font>

<font style="color:rgb(51,51,51);">} </font>

<font style="color:rgb(51,51,51);">4. </font><font style="color:rgb(51,51,51);">切片拷贝 </font>

<font style="color:rgb(51,51,51);">使用 </font><font style="color:rgb(51,51,51);">copy </font><font style="color:rgb(51,51,51);">内置函数拷贝两个切片时，会将源切片的数据逐个拷贝到目的切片指向的数组中，拷贝 </font>

<font style="color:rgb(51,51,51);">数量取两个切片的最小值。</font><font style="color:rgb(51,51,51);">例如长度为</font><font style="color:rgb(51,51,51);">10</font><font style="color:rgb(51,51,51);">的切片拷贝到长度为</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">的切片时，将拷贝</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">个元素。也就是说，拷贝过程中不会发生扩 </font>

<font style="color:rgb(51,51,51);">容。 </font>

<font style="color:rgb(51,51,51);">copy</font><font style="color:rgb(51,51,51);">函数有返回值，它返回实际上复制的元素个数，这个值就是两个</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">长度的较小值。 </font>

**<font style="color:rgb(51,51,51);">4. </font>****<font style="color:rgb(51,51,51);">切片扩容</font>****<font style="color:rgb(51,51,51);">-append</font>****<font style="color:rgb(51,51,51);">函数 </font>**

**<font style="color:rgb(51,51,51);">追加元素 </font>**

<font style="color:rgb(51,51,51);">通过 </font><font style="color:rgb(51,51,51);">append() </font><font style="color:rgb(51,51,51);">函数可以在切片的尾部追加</font><font style="color:rgb(51,51,51);">N</font><font style="color:rgb(51,51,51);">个元素 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">a </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">// </font><font style="color:rgb(170,85,0);">追加一个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">// </font><font style="color:rgb(170,85,0);">追加多个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">, []</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">}</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">// </font><font style="color:rgb(170,85,0);">追加一个切片，注意追加切片时后面要加</font><font style="color:rgb(170,85,0);">... </font>

<font style="color:rgb(51,51,51);">使用</font><font style="color:rgb(51,51,51);">append()</font><font style="color:rgb(51,51,51);">函数也可以在切片头部添加元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">}, </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">// </font><font style="color:rgb(170,85,0);">在开头添加一个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">}, </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">// </font><font style="color:rgb(170,85,0);">在开头添加一个切片 </font>

<font style="color:rgb(119,119,119);">注</font><font style="color:rgb(119,119,119);">:</font><font style="color:rgb(119,119,119);">从头部添加元素会引起内存的重分配，导致已有元素全部复制一次。因此从头部添加元素 </font>

<font style="color:rgb(119,119,119);">的开销要比从尾部添加元素大很多 </font>

<font style="color:rgb(51,51,51);">通过</font><font style="color:rgb(51,51,51);">append()</font><font style="color:rgb(51,51,51);">函数链式操作从中间插入元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">], </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(51,51,51);">}, </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">:]</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">)</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">在第</font><font style="color:rgb(170,85,0);">i</font><font style="color:rgb(170,85,0);">个位置上插入</font><font style="color:rgb(170,85,0);">x </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">], </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">}, </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">:]</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">)</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">在第</font><font style="color:rgb(170,85,0);">i</font><font style="color:rgb(170,85,0);">个位置上插入切片 </font>

<font style="color:rgb(51,51,51);">使用链式操作在插入元素，在内层</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函数中会创建一个临式切片，然后将 </font><font style="color:rgb(51,51,51);">a[i:] </font><font style="color:rgb(51,51,51);">内容复制到 </font>

<font style="color:rgb(51,51,51);">新创建的临式切片中，再将临式切片追加至 </font><font style="color:rgb(51,51,51);">a[:i] </font><font style="color:rgb(51,51,51);">中。 </font>

<font style="color:rgb(51,51,51);">通过</font><font style="color:rgb(51,51,51);">append()</font><font style="color:rgb(51,51,51);">和</font><font style="color:rgb(51,51,51);">copy()</font><font style="color:rgb(51,51,51);">函数组合从中间插入元素 </font>

<font style="color:rgb(51,51,51);">使用这种方式可以避免创建过程中间的临式切片，也可以做到从中间插入元素 </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">中间插入一个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">切片扩展一个空间 </font>

<font style="color:rgb(34,17,153);">copy</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(152,26,26);">+</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">:], </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">:]) </font><font style="color:rgb(170,85,0);">//a[i:]</font><font style="color:rgb(170,85,0);">向后移动一个位置 </font>

<font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">] </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">x </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">设置新添加的元素 </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">中间插入多个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">为</font><font style="color:rgb(170,85,0);">x</font><font style="color:rgb(170,85,0);">切片扩展足够的空间 </font>

<font style="color:rgb(34,17,153);">copy</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(152,26,26);">+</font><font style="color:rgb(34,17,153);">len</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(51,51,51);">):], </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">:]) </font><font style="color:rgb(170,85,0);">//a[i:]</font><font style="color:rgb(170,85,0);">向后移动</font><font style="color:rgb(170,85,0);">len(x)</font><font style="color:rgb(170,85,0);">个位置 </font>

<font style="color:rgb(34,17,153);">copy</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">:], </font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">复制新添加的切片 </font>

<font style="color:rgb(51,51,51);">使用此方式虽然稍显复杂，但是可以减少创建中间临时切片的开销。 </font>

**<font style="color:rgb(51,51,51);">删除元素 </font>**

<font style="color:rgb(51,51,51);">很遗憾，</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">语言中并没有提供直接删除指定位置元素的方式。不过根据切片的性质，我们可以通过巧妙 </font>

<font style="color:rgb(51,51,51);">的拼接切片来达到删除指定数据的目的。</font><font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">} </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除尾部元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(34,17,153);">len</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(152,26,26);">- </font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">] </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除尾部一个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(34,17,153);">len</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(152,26,26);">- </font><font style="color:rgb(0,0,0);">N</font><font style="color:rgb(51,51,51);">] </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除尾部</font><font style="color:rgb(170,85,0);">N</font><font style="color:rgb(170,85,0);">个元素 </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除头部元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">:] </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除开头</font><font style="color:rgb(170,85,0);">1</font><font style="color:rgb(170,85,0);">个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">N</font><font style="color:rgb(51,51,51);">:] </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除开头</font><font style="color:rgb(170,85,0);">N</font><font style="color:rgb(170,85,0);">个元素 </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除中间元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">], </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(152,26,26);">+</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">:]</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除中间一个元素 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[:</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">], </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(152,26,26);">+</font><font style="color:rgb(0,0,0);">N</font><font style="color:rgb(51,51,51);">:]</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">删除中间</font><font style="color:rgb(170,85,0);">N</font><font style="color:rgb(170,85,0);">个元素 </font>

**<font style="color:rgb(51,51,51);">slice</font>****<font style="color:rgb(51,51,51);">扩容 </font>**

<font style="color:rgb(51,51,51);">很多人以为</font><font style="color:rgb(51,51,51);"> slice </font><font style="color:rgb(51,51,51);">是可以自动扩充的</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(51,51,51);">估计都是 </font><font style="color:rgb(51,51,51);">append </font><font style="color:rgb(51,51,51);">函数误导的。其实</font><font style="color:rgb(51,51,51);"> slice </font><font style="color:rgb(51,51,51);">并不会自己自动扩充</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(51,51,51);">而 </font>

<font style="color:rgb(51,51,51);">是 </font><font style="color:rgb(51,51,51);">append </font><font style="color:rgb(51,51,51);">数据时</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(51,51,51);">该函数如果发现超出了</font><font style="color:rgb(51,51,51);"> cap </font><font style="color:rgb(51,51,51);">限制自动帮我们扩的。 </font>

<font style="color:rgb(51,51,51);">使用</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">向</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">追加元素时，如果</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">空间不足，则会触发</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">扩容，扩容实际上是分配一块更大 </font>

<font style="color:rgb(51,51,51);">的内存，将原</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的数据拷贝进新</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">，然后返回新</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">，扩容后再将数据追加进去。 </font>

<font style="color:rgb(51,51,51);">例如，当向一个容量为</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">且长度也为</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">的切片再次追加</font><font style="color:rgb(51,51,51);">1</font><font style="color:rgb(51,51,51);">个元素时，就会发生扩容，如下图所示。 </font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(51,51,51);">示例来 </font>

<font style="color:rgb(51,51,51);">源</font><font style="color:rgb(51,51,51);">:Go</font><font style="color:rgb(51,51,51);">专家编程</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(51,51,51);">扩容操作只关心容量，会把原</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的数据拷贝至新</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">中，追加数据由</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">在扩容后完成。由上图可 </font>

<font style="color:rgb(51,51,51);">见，扩容后新</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的长度仍然是</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">，但容量由</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">提到了</font><font style="color:rgb(51,51,51);">10</font><font style="color:rgb(51,51,51);">，原</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的数据也都拷贝到了新的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">指向的数 </font>

<font style="color:rgb(51,51,51);">组中。 </font>

<font style="color:rgb(51,51,51);">扩容容量的选择遵循以下基本规则 </font>

<font style="color:rgb(51,51,51);">如果原</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的容量小于</font><font style="color:rgb(51,51,51);">1024</font><font style="color:rgb(51,51,51);">，则新</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的容量将扩大为原来的</font><font style="color:rgb(51,51,51);">2</font><font style="color:rgb(51,51,51);">倍； </font>

<font style="color:rgb(51,51,51);">如果原</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的容量大于</font><font style="color:rgb(51,51,51);">1024</font><font style="color:rgb(51,51,51);">，则新的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">的容量将扩大为原来的</font><font style="color:rgb(51,51,51);">1.25</font><font style="color:rgb(51,51,51);">倍； </font>

**<font style="color:rgb(51,51,51);">5. Go</font>****<font style="color:rgb(51,51,51);">切片，</font>****<font style="color:rgb(51,51,51);">Python</font>****<font style="color:rgb(51,51,51);">切片，都是切片，有什么不同？ </font>**

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">有切片</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">类型，</font><font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">有列表和元组，这两种语言都有切片操作。但是它们的切片操作是完全不 </font>

<font style="color:rgb(51,51,51);">同的。 </font>

<font style="color:rgb(51,51,51);">1. </font><font style="color:rgb(51,51,51);">最大的不同就是 </font>

<font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">的切片产生的是新的</font>**<font style="color:rgb(51,51,51);">对象</font>**<font style="color:rgb(51,51,51);">，对新对象的成员的操作不影响旧对象； </font>

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">的切片产生的是旧对象一部分的</font>**<font style="color:rgb(51,51,51);">引用</font>**<font style="color:rgb(51,51,51);">，对其成员的操作会影响旧对象；</font><font style="color:rgb(51,51,51);">究其原因还是底层实现不同 </font>

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">的切片，底层是一个三元组。指针指向一块连续的内存，长度是已有成员数，容量是最大成员 </font>

<font style="color:rgb(51,51,51);">数。切片时，一般并不会申请新的内存，而是对原指针进行移动，然后和新的长度、容量组成一个 </font>

<font style="color:rgb(51,51,51);">切片类型值返回。也就是说，</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">的切片操作通常会和生成该切片的切片或数组共享内存。 </font>

<font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">的切片，其实就是指针数组。对它进行切片，会创建新的数组。在</font><font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">的切片中，并没 </font>

<font style="color:rgb(51,51,51);">有容量的概念。 </font>

<font style="color:rgb(51,51,51);">这其实也体现了脚本语言和编译语言的不同。虽然两个语言都有类似的切片操作；但是</font><font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">主要目标 </font>

<font style="color:rgb(51,51,51);">是方便；</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">主要目标却是快速。 </font>

<font style="color:rgb(51,51,51);">2. </font><font style="color:rgb(51,51,51);">在使用中，</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">切片和</font><font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">切片也有很多不同 </font>

<font style="color:rgb(51,51,51);">首先，</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">的切片，其成员是相同类型的，</font><font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">的列表则不限制类型。 </font>

<font style="color:rgb(51,51,51);">两种语言都有</font><font style="color:rgb(51,51,51);">[a:b]</font><font style="color:rgb(51,51,51);">这种切片操作，意义也类似，但是</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">的</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">、</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">两个参数不能是负数，</font><font style="color:rgb(51,51,51);">Python</font><font style="color:rgb(51,51,51);">可以 </font>

<font style="color:rgb(51,51,51);">是负数，此时就相当于从末尾往前数。 </font>

<font style="color:rgb(51,51,51);">两种语言都有 </font><font style="color:rgb(51,51,51);">[a:b:c] </font><font style="color:rgb(51,51,51);">这种切片操作，意义却是完全不同的。</font><font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">中的</font><font style="color:rgb(51,51,51);">c</font><font style="color:rgb(51,51,51);">表示的是</font>**<font style="color:rgb(51,51,51);">容量</font>**<font style="color:rgb(51,51,51);">；而</font><font style="color:rgb(51,51,51);">Python </font>

<font style="color:rgb(51,51,51);">的</font><font style="color:rgb(51,51,51);">c</font><font style="color:rgb(51,51,51);">表示的是</font>**<font style="color:rgb(51,51,51);">步长</font>**<font style="color:rgb(51,51,51);">。 </font>

**<font style="color:rgb(51,51,51);">6. </font>****<font style="color:rgb(51,51,51);">切片陷阱 </font>**

<font style="color:rgb(51,51,51);">1. </font><font style="color:rgb(51,51,51);">无法做比较 </font>

<font style="color:rgb(51,51,51);">和数组不同的是，</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">无法做比较，因此不能用</font><font style="color:rgb(51,51,51);">==</font><font style="color:rgb(51,51,51);">来测试两个</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">是否拥有相同的元素。标准库里 </font>

<font style="color:rgb(51,51,51);">面提供了高度优化的函数 </font><font style="color:rgb(51,51,51);">bytes.Equal </font><font style="color:rgb(51,51,51);">来比较两个字节</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">。但是对于其它类型的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">，就必须 </font>

<font style="color:rgb(51,51,51);">要自己写函数来比较。 </font>

<font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">唯一允许的比较操作是和</font><font style="color:rgb(51,51,51);">nil</font><font style="color:rgb(51,51,51);">进行比较，例如 </font>

<font style="color:rgb(119,0,136);">if </font><font style="color:rgb(0,0,0);">slice </font><font style="color:rgb(152,26,26);">== </font><font style="color:rgb(34,17,153);">nil </font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(170,85,0);">/*...*/</font><font style="color:rgb(51,51,51);">} </font>

<font style="color:rgb(51,51,51);">2. </font><font style="color:rgb(51,51,51);">空切片和</font><font style="color:rgb(51,51,51);">nil</font><font style="color:rgb(51,51,51);">切片 </font>

<font style="color:rgb(51,51,51);">空切片和</font><font style="color:rgb(51,51,51);">nil</font><font style="color:rgb(51,51,51);">切片是不同的。 </font>

<font style="color:rgb(51,51,51);">nil</font><font style="color:rgb(51,51,51);">切片中，切片的指针指向的是空地址，其长度和容量都为零。</font><font style="color:rgb(51,51,51);">nil</font><font style="color:rgb(51,51,51);">切片和</font><font style="color:rgb(51,51,51);">nil</font><font style="color:rgb(51,51,51);">相等。 </font>

<font style="color:rgb(51,51,51);">空切片，切片的指针指向了一个地址，但其长度和容量也为</font><font style="color:rgb(51,51,51);">0</font><font style="color:rgb(51,51,51);">，和</font><font style="color:rgb(51,51,51);">nil</font><font style="color:rgb(51,51,51);">不相等，通常用来表示一 </font>

<font style="color:rgb(51,51,51);">个空的集合。 </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">s </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int </font><font style="color:rgb(170,85,0);">// s == nil </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">s </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">nil </font><font style="color:rgb(170,85,0);">// s == nil </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">s </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(34,17,153);">nil</font><font style="color:rgb(51,51,51);">} </font><font style="color:rgb(170,85,0);">// s == nil </font>

<font style="color:rgb(119,0,136);">var </font><font style="color:rgb(0,0,0);">s </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{} </font><font style="color:rgb(170,85,0);">// s != nil </font>

<font style="color:rgb(0,0,0);">s </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">make</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">,</font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">// s != nil </font>

<font style="color:rgb(51,51,51);">3. </font><font style="color:rgb(51,51,51);">使用</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">进行切片迭代 </font>

<font style="color:rgb(51,51,51);">当使用</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">进行切片迭代时，</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">创建了每个元素的副本，而不是直接返回对该元素的引用。 </font>

<font style="color:rgb(51,51,51);">如果使用该值变量的地址作为每个元素的指针，就会造成错误。 </font>

<font style="color:rgb(119,0,136);">func </font><font style="color:rgb(0,0,0);">main</font><font style="color:rgb(51,51,51);">() { </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">4</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">5</font><font style="color:rgb(51,51,51);">} </font>

<font style="color:rgb(119,0,136);">for </font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">v </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(119,0,136);">range </font><font style="color:rgb(0,0,0);">a </font><font style="color:rgb(51,51,51);">{ </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Printf</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(170,17,17);">"Value: %d, v-addr: %X, Elem-addr: %X\n"</font><font style="color:rgb(51,51,51);">, </font>

<font style="color:rgb(0,0,0);">v</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(152,26,26);">&</font><font style="color:rgb(0,0,0);">v</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(152,26,26);">&</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(0,0,0);">i</font><font style="color:rgb(51,51,51);">]) </font>

<font style="color:rgb(51,51,51);">} </font>

<font style="color:rgb(51,51,51);">}</font><font style="color:rgb(170,85,0);"># output </font>

<font style="color:rgb(0,0,255);">Value: </font><font style="color:rgb(51,51,51);">1, v-addr: C0000AA058, Elem-addr: C0000CC030 </font>

<font style="color:rgb(0,0,255);">Value: </font><font style="color:rgb(51,51,51);">2, v-addr: C0000AA058, Elem-addr: C0000CC038 </font>

<font style="color:rgb(0,0,255);">Value: </font><font style="color:rgb(51,51,51);">3, v-addr: C0000AA058, Elem-addr: C0000CC040 </font>

<font style="color:rgb(0,0,255);">Value: </font><font style="color:rgb(51,51,51);">4, v-addr: C0000AA058, Elem-addr: C0000CC048 </font>

<font style="color:rgb(0,0,255);">Value: </font><font style="color:rgb(51,51,51);">5, v-addr: C0000AA058, Elem-addr: C0000CC050 </font>

<font style="color:rgb(51,51,51);">从结果中可以看出，使用</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">进行迭代时，</font><font style="color:rgb(51,51,51);">v</font><font style="color:rgb(51,51,51);">的地址是始终不变的，它并不是切片中每个变量的实 </font>

<font style="color:rgb(51,51,51);">际地址。而是在使用</font><font style="color:rgb(51,51,51);">range</font><font style="color:rgb(51,51,51);">进行遍历时，将切片中每个元素都复制到了同一个变量</font><font style="color:rgb(51,51,51);">v</font><font style="color:rgb(51,51,51);">中。如果错误的 </font>

<font style="color:rgb(51,51,51);">将</font><font style="color:rgb(51,51,51);">v</font><font style="color:rgb(51,51,51);">的地址当作切边元素的地址，将会引发错误。 </font>

<font style="color:rgb(51,51,51);">4. </font><font style="color:rgb(51,51,51);">切片扩容引发的问题 </font>

<font style="color:rgb(51,51,51);">正因为有扩容机制。所以我们无法保证原始的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">和用</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">后的结果</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">指向同一个底层数 </font>

<font style="color:rgb(51,51,51);">组，也无法证明它们就指向不同的底层数组。同样，我们也无法假设旧</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">上对元素的操作会或者 </font>

<font style="color:rgb(51,51,51);">不会影响新的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">元素。所以，通常我们将</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">的调用结果再次赋给传入</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">的</font><font style="color:rgb(51,51,51);">slice</font><font style="color:rgb(51,51,51);">。 </font>

<font style="color:rgb(51,51,51);">内置</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函数在向切片追加元素时，如果切片存储容量不足以存储新元素，则会把当前切片扩 </font>

<font style="color:rgb(51,51,51);">容并产生一个新的切片。 </font>

<font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函数每次追加元素都有可能触发切片扩容，即有可能返回一个新的切片，这正是</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函 </font>

<font style="color:rgb(51,51,51);">数声明中返回值为切片的原因，使用时应该总是接收该返回值。 </font>

**<font style="color:rgb(51,51,51);">建议 </font>**

<font style="color:rgb(51,51,51);">使用</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函数时，谨记</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">可能会产生新的切片，并谨慎的处理返回值。 </font>

<font style="color:rgb(51,51,51);">5. append</font><font style="color:rgb(51,51,51);">函数误用 </font>

<font style="color:rgb(51,51,51);">使用</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函数时，需要考虑</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">返回的切片是否跟原切片共享底层的数组。下面这段程序片 </font>

<font style="color:rgb(51,51,51);">段，来看看函数返回的结果。 </font>

<font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">示例来源</font><font style="color:rgb(170,85,0);">:Go</font><font style="color:rgb(170,85,0);">专家编程 </font>

<font style="color:rgb(119,0,136);">func </font><font style="color:rgb(0,0,0);">AppendDemo</font><font style="color:rgb(51,51,51);">() { </font>

<font style="color:rgb(0,0,0);">x </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">make</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">10</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">x </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">y </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">4</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">z </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">5</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">x</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">y</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">z</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(51,51,51);">}</font>

<font style="color:rgb(170,85,0);">//output </font>

<font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">1 2 3</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">1 2 3 5</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">1 2 3 5</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(51,51,51);">题目首先创建了一个长度为</font><font style="color:rgb(51,51,51);">0</font><font style="color:rgb(51,51,51);">，容量为</font><font style="color:rgb(51,51,51);">10</font><font style="color:rgb(51,51,51);">的切片</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">，然后向切片</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">追加了</font><font style="color:rgb(51,51,51);">1</font><font style="color:rgb(51,51,51);">，</font><font style="color:rgb(51,51,51);">2</font><font style="color:rgb(51,51,51);">，</font><font style="color:rgb(51,51,51);">3</font><font style="color:rgb(51,51,51);">三个元素。其底层 </font>

<font style="color:rgb(51,51,51);">的数组结构如下图所示</font><font style="color:rgb(51,51,51);">创建切片</font><font style="color:rgb(51,51,51);">y</font><font style="color:rgb(51,51,51);">为切片</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">追加一个元素</font><font style="color:rgb(51,51,51);">4</font><font style="color:rgb(51,51,51);">后，底层数组结构如下图所示 </font>

<font style="color:rgb(51,51,51);">需要注意的是切片</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">仍然没有变化，切片</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">中记录的长度仍为</font><font style="color:rgb(51,51,51);">3</font><font style="color:rgb(51,51,51);">。继续向</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">追加元素</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">后，底层数组结 </font>

<font style="color:rgb(51,51,51);">构如下图所示 </font>

<font style="color:rgb(51,51,51);">至此，答案已经非常明确了。当向</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">继续追加元素</font><font style="color:rgb(51,51,51);">5</font><font style="color:rgb(51,51,51);">后，切片</font><font style="color:rgb(51,51,51);">y</font><font style="color:rgb(51,51,51);">的最后一个元素被覆盖掉了。 </font>

<font style="color:rgb(51,51,51);">此时切片</font><font style="color:rgb(51,51,51);">x</font><font style="color:rgb(51,51,51);">仍然为</font><font style="color:rgb(51,51,51);">[1 2 3]</font><font style="color:rgb(51,51,51);">，而切片</font><font style="color:rgb(51,51,51);">y</font><font style="color:rgb(51,51,51);">和</font><font style="color:rgb(51,51,51);">z</font><font style="color:rgb(51,51,51);">则为</font><font style="color:rgb(51,51,51);">[1 2 3 5]</font><font style="color:rgb(51,51,51);">。 </font>

**<font style="color:rgb(51,51,51);">建议 </font>**

<font style="color:rgb(51,51,51);">一般情况下，使用</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函数追加新的元素时，都会用原切片变量接收返回值来获得更新 </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">elems</font><font style="color:rgb(17,102,68);">...</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(51,51,51);">6. </font><font style="color:rgb(51,51,51);">函数传参 </font>

<font style="color:rgb(51,51,51);">Go</font><font style="color:rgb(51,51,51);">语言中将切片作为函数参数传递会有什么神奇的现象，一起来看看下面这个示例。 </font>

<font style="color:rgb(119,0,136);">package </font><font style="color:rgb(0,0,0);">main</font><font style="color:rgb(119,0,136);">import </font><font style="color:rgb(170,17,17);">"fmt" </font>

<font style="color:rgb(119,0,136);">func </font><font style="color:rgb(0,0,0);">main</font><font style="color:rgb(51,51,51);">(){ </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">{</font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">} </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">长度为</font><font style="color:rgb(170,85,0);">3</font><font style="color:rgb(170,85,0);">，容量为</font><font style="color:rgb(170,85,0);">3 </font>

<font style="color:rgb(0,0,0);">b </font><font style="color:rgb(51,51,51);">:</font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">make</font><font style="color:rgb(51,51,51);">([]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">1</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">10</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">长度为</font><font style="color:rgb(170,85,0);">1</font><font style="color:rgb(170,85,0);">，容量为</font><font style="color:rgb(170,85,0);">10 </font>

<font style="color:rgb(0,0,0);">test</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">,</font><font style="color:rgb(0,0,0);">b</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(170,17,17);">"main a ="</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(170,17,17);">"main b ="</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">b</font><font style="color:rgb(51,51,51);">) </font>

<font style="color:rgb(51,51,51);">}</font>

<font style="color:rgb(119,0,136);">func </font><font style="color:rgb(0,0,0);">test</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">,</font><font style="color:rgb(0,0,0);">b </font><font style="color:rgb(51,51,51);">[]</font><font style="color:rgb(119,0,136);">int</font><font style="color:rgb(51,51,51);">){ </font>

<font style="color:rgb(0,0,0);">a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">4</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">引发扩容，此时返回的</font><font style="color:rgb(170,85,0);">a</font><font style="color:rgb(170,85,0);">是一个新的切片 </font>

<font style="color:rgb(0,0,0);">b </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(34,17,153);">append</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(0,0,0);">b</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(17,102,68);">2</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">没有引发扩容，仍然是原切片 </font>

<font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">] </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(17,102,68);">3 </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">改变</font><font style="color:rgb(170,85,0);">a</font><font style="color:rgb(170,85,0);">切片元素 </font>

<font style="color:rgb(0,0,0);">b</font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">0</font><font style="color:rgb(51,51,51);">] </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(17,102,68);">3 </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">改变</font><font style="color:rgb(170,85,0);">b</font><font style="color:rgb(170,85,0);">切片元素 </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(170,17,17);">"test a ="</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">a</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">打印函数内的</font><font style="color:rgb(170,85,0);">a</font><font style="color:rgb(170,85,0);">切片 </font>

<font style="color:rgb(0,0,0);">fmt</font><font style="color:rgb(17,102,68);">.</font><font style="color:rgb(0,0,0);">Println</font><font style="color:rgb(51,51,51);">(</font><font style="color:rgb(170,17,17);">"test b ="</font><font style="color:rgb(51,51,51);">, </font><font style="color:rgb(0,0,0);">b</font><font style="color:rgb(51,51,51);">) </font><font style="color:rgb(170,85,0);">//</font><font style="color:rgb(170,85,0);">打印函数内的</font><font style="color:rgb(170,85,0);">b</font><font style="color:rgb(170,85,0);">切片 </font>

<font style="color:rgb(51,51,51);">}</font>

<font style="color:rgb(170,85,0);">//output </font>

<font style="color:rgb(0,0,0);">test a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">3 2 3 4</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(0,0,0);">test b </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">3 2</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(0,0,0);">main a </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">1 2 3</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(0,0,0);">main b </font><font style="color:rgb(152,26,26);">= </font><font style="color:rgb(51,51,51);">[</font><font style="color:rgb(17,102,68);">3</font><font style="color:rgb(51,51,51);">] </font>

<font style="color:rgb(51,51,51);">首先，我们创建了两个切片，</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片长度和容量均为</font><font style="color:rgb(51,51,51);">3</font><font style="color:rgb(51,51,51);">，</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切片长度为</font><font style="color:rgb(51,51,51);">1</font><font style="color:rgb(51,51,51);">，容量为</font><font style="color:rgb(51,51,51);">10</font><font style="color:rgb(51,51,51);">。将</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片和</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切 </font>

<font style="color:rgb(51,51,51);">片作为函数参数传入</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中。 </font>

<font style="color:rgb(51,51,51);">在</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中，对</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片和</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切片做了如下两点改动 </font>

<font style="color:rgb(51,51,51);">1. </font><font style="color:rgb(51,51,51);">分别使用</font><font style="color:rgb(51,51,51);">append</font><font style="color:rgb(51,51,51);">函数在</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片和</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切片中追加一个元素 </font>

<font style="color:rgb(51,51,51);">2. </font><font style="color:rgb(51,51,51);">分别对</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片和</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切片的第一个元素做了修改 </font>

<font style="color:rgb(51,51,51);">分别在主函数中和</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中输出两个切片，会发现在主函数中和</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中两个切片好像改了， </font>

<font style="color:rgb(51,51,51);">又好像没改，下面我们就来分析一下。 </font>

**<font style="color:rgb(51,51,51);">理论分析 </font>**

<font style="color:rgb(51,51,51);">当我们将一个切片作为函数参数传递给函数的时候，采用的是值传递，因此我们传递给函数的参数 </font>

<font style="color:rgb(51,51,51);">其实是上面这个切片三元组的值拷贝。当我们对切片结构中的指针进行值拷贝的时候，得到的指针 </font>

<font style="color:rgb(51,51,51);">还是指向了同一个底层数组。因此我们通过指针对底层数组的值进行修改，从而修改了切片的值。 </font>

<font style="color:rgb(51,51,51);">但是，当我们以值传递的方式传递上面的结构体的时候，同时也是传递了 </font><font style="color:rgb(51,51,51);">len </font><font style="color:rgb(51,51,51);">和 </font><font style="color:rgb(51,51,51);">cap </font><font style="color:rgb(51,51,51);">的值拷贝，因 </font>

<font style="color:rgb(51,51,51);">为这两个成员并不是指针，因此，当我们从函数返回的时候，外层切片结构体的 </font><font style="color:rgb(51,51,51);">len </font><font style="color:rgb(51,51,51);">和 </font><font style="color:rgb(51,51,51);">cap </font><font style="color:rgb(51,51,51);">这两个 </font>

<font style="color:rgb(51,51,51);">成员并没有改变。 </font>

<font style="color:rgb(51,51,51);">所以当我们传递切片给函数的时候，并且在被调函数中通过 </font><font style="color:rgb(51,51,51);">append </font><font style="color:rgb(51,51,51);">操作向切片中增加了值，但是 </font>

<font style="color:rgb(51,51,51);">当函数返回的时候，我们看到的切片的值还是没有发生变化，其实底层数组的值是已经改变了的 </font>

<font style="color:rgb(51,51,51);">（如果没有触发扩容的话），但是由于长度 </font><font style="color:rgb(51,51,51);">len </font><font style="color:rgb(51,51,51);">没有发生改变，所以我们看到的切片的值也没有发 </font>

<font style="color:rgb(51,51,51);">生改变。 </font>

**<font style="color:rgb(51,51,51);">题目再分析 </font>**

<font style="color:rgb(51,51,51);">有了前面的理论基础，我们再来分析一下</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">，</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切片的返回结果。 </font>

<font style="color:rgb(51,51,51);">1. a</font><font style="color:rgb(51,51,51);">切片作为参数传至</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中，在</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">中向</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片追加一个元素后，此时触发扩容机制，返回 </font>

<font style="color:rgb(51,51,51);">的切片已经不再是原切片，而是一个新的切片。后续对</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片中的第一个元素进行修改也是对 </font>

<font style="color:rgb(51,51,51);">新切片进行修改，对老切片不会产生任何影响。 </font>

<font style="color:rgb(51,51,51);">所以，最终在主函数中</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片仍然为</font><font style="color:rgb(51,51,51);">[1 2 3]</font><font style="color:rgb(51,51,51);">，而在</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中</font><font style="color:rgb(51,51,51);">a</font><font style="color:rgb(51,51,51);">切片变成了</font><font style="color:rgb(51,51,51);">[3 2 3 4]</font><font style="color:rgb(51,51,51);">。</font><font style="color:rgb(51,51,51);">2. b</font><font style="color:rgb(51,51,51);">切片作为参数传至</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中，在</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">中向</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切片追加一个元素后，不会触发扩容机制，返回 </font>

<font style="color:rgb(51,51,51);">的仍然是原切片，所以在后续对</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切片的修改都是在原切片中进行的修改。故在</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">函数中</font><font style="color:rgb(51,51,51);">b</font><font style="color:rgb(51,51,51);">切 </font>

<font style="color:rgb(51,51,51);">片为</font><font style="color:rgb(51,51,51);">[3 2]</font><font style="color:rgb(51,51,51);">。但是在主函数中确为</font><font style="color:rgb(51,51,51);">[3]</font><font style="color:rgb(51,51,51);">，可以看出在</font><font style="color:rgb(51,51,51);">test</font><font style="color:rgb(51,51,51);">中对切片进行修改确实反应到主函数中 </font>

<font style="color:rgb(51,51,51);">了，但是由于其</font><font style="color:rgb(51,51,51);">len</font><font style="color:rgb(51,51,51);">和</font><font style="color:rgb(51,51,51);">cap</font><font style="color:rgb(51,51,51);">没有改变，</font><font style="color:rgb(51,51,51);">len</font><font style="color:rgb(51,51,51);">仍为</font><font style="color:rgb(51,51,51);">1</font><font style="color:rgb(51,51,51);">，所以最终就只输出切片中的第一个元素</font><font style="color:rgb(51,51,51);">[3]</font><font style="color:rgb(51,51,51);">， </font>

<font style="color:rgb(51,51,51);">但其底层数组的值其实已经改变了。</font>



> 更新: 2022-09-11 22:58:31  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/hp04qo>