# 运算符/控制语句/math相关类

### 用最有效率的方法计算2乘以8?
 2 << 3（左移3位相当于乘以2的3次方，右移3位相当于除以2的3次方）。

补充：我们为编写的类重写hashCode方法时，可能会看到如下所示的代码，其实我们不太理解为什么要使用这样的乘法运算来产生哈希码（散列码），而且为什么这个数是个素数，为什么通常选择31这个数？前两个问题的答案你可以自己百度一下，选择31是因为可以用移位和减法运算来代替乘法，从而得到更好的性能。说到这里你可能已经想到了：31 * num <==> (num << 5) - num，左移5位相当于乘以2的5次方（32）再减去自身就相当于乘以31。现在的VM都能自动完成这个优化。

### <font style="color:#CF1322;">swtich 是否能作用在byte 上，是否能作用在long 上，是否能作用在String上?</font>
早期的JDK中，switch（expr）中，expr可以是byte、short、char、int。

从**JDK 1.5版**开始，Java中引入了枚举类型（enum），expr也可以是枚举。

从**JDK 1.7版**开始，还可以是字符串（String）。

<font style="color:#CF1322;">长整型（long）是不可以的</font>。

### Math.round(11.5) 等于多少? Math.round(-11.5)等于多少?
Math.round(11.5)的返回值是12，Math.round(-11.5)的返回值是-11。四舍五入的原理是在参数上加0.5然后进行下取整。

### &和&&的区别？
&运算符有两种用法：

(1)按位与；

(2)逻辑与。

&&运算符是短路与运算。

逻辑与跟短路与的差别是非常巨大的，虽然二者都要求运算符左右两端的布尔值都是true整个表达式的值才是true。&&之所以称为短路运算是因为，如果&&左边的表达式的值是false，右边的表达式会被直接短路掉，不会进行运算。很多时候我们可能都需要用&&而不是&，例如在验证用户登录时判定用户名不是null而且不是空字符串，应当写为：username != null &&!username.equals(“”)，二者的顺序不能交换，更不能用&运算符，因为第一个条件如果不成立，根本不能进行字符串的equals比较，否则会产生NullPointerException异常。

注意：逻辑或运算符（|）和短路或运算符（||）的差别也是如此。

补充：如果你熟悉JavaScript，那你可能更能感受到短路运算的强大，想成为JavaScript的高手就先从玩转短路运算开始吧。

### <font style="color:#CF1322;">~8等于多少？8>>>2等于多少？</font>
**<font style="color:rgb(51,51,51);">第一个答案是-9，第二个答案是2，</font>**<font style="color:rgb(34,34,34);">无符号右移高位补0	。</font>

> `~`<font style="color:rgb(77, 77, 77);">位非运算符</font>
>
> <font style="color:rgb(77, 77, 77);">公式（~X）= -(X+1)</font>
>
> [Java中 “~” 运算符的含义_未来的资深Java架构师的博客-CSDN博客_java ~](https://blog.csdn.net/zyh201314zyh/article/details/114294827)
>
> [Java 运算符 | 菜鸟教程](https://www.runoob.com/java/java-operators.html?_t_t_t=0.4433099896434123)
>

### <font style="color:#CF1322;">foreach与正常for循环效率对比</font>
对于数组来说，for和foreach循环效率差不多，但是对于**链表**来说，for循环效率明显比foreach低。

链表随机访问效率较低，for循环是通过下标获取元素，效率偏低。

> foreach循环遍历对象的时候底层是使用迭代器进行迭代的，即该对象必须直接或者间接的实现了Iterable接口，一般以able结尾代表某种能力，实现了iterable代表给予了实现类迭代的能力。
>
> [Java中foreach的实现原理 - ielgnahz - 博客园](https://www.cnblogs.com/ielgnahz/articles/11344406.html)
>

### <font style="color:#CF1322;">switch能否用String做参数</font>
以前只能支持byte、short、char、int，可以强转。

Jdk7.0以后可以，整型、枚举类型、boolean、字符串都可以。

### 在Java 中，如何跳出当前的多重嵌套循环？
在最外层循环前加一个标记如A，然后用break A;可以跳出多重循环。（Java中支持带标签的break和continue语句，作用有点类似于C和C++中的goto语句，但是就像要避免使用goto一样，应该避免使用带标签的break和continue，因为它不会让你的程序变得更优雅，很多时候甚至有相反的作用，所以这种语法其实不知道更好）



> 更新: 2022-12-13 15:31:56  
> 原文: <https://www.yuque.com/joyo/interview/ts2wsy>