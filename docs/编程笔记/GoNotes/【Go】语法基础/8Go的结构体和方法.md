# 8 Go 的结构体和方法

## 结构体的定义
<font style="color:rgb(0, 0, 0);">如下定义一个结构体类型：</font>

```go
type Body struct {
	name string
	age  int
}
```

定义结构体变量：

```go
var body Body
body.name = "coding3min"
body.age = 12
fmt.Println(body)
```

树：树的一个结点有三个信息，左孩子指针，value，右孩子指针

```go
package main
import "fmt"
type treeNode struct{
	value int
    left,right *treeNode
}
func main(){
    var root treeNode //定义一个根结点
    root = treeNode{value:3} //根结点的值
    root.left = &treeNode{}  //根结点的左子树
    root.right = treeNode{5,nil,nil} //根结点的右子树的值是5，并且没有左右孩子
    //这里永远是.下去，对比于C的->。
    root.right.left = new(treeNode) //根结点的
    //在切片里面存了tree的结点。
    nodes := []treeNode{
        {value: 3},//存了一共没有左右孩子的树
        {},//存了一个空树
        {6,nil,&root} //值为6，没有左孩子，有孩子是上面的那个根结点。
    }
    fmt.Println(nodes)
}
```

结构体数组：

```go
bodys := []Body{
	Body{"jack", 12}, Body{"lynn", 18},
}
```

<font style="color:rgb(0, 0, 0);">声明时赋值</font>

```go
body2 := Body{
	"tom", 13,
}
```

## <font style="color:rgb(0, 0, 0);">Go中的类和方法</font>
<font style="color:rgb(0, 0, 0);">Go</font><font style="color:rgb(0, 0, 0);"> 用一种特殊的方式，把结构体本身看作一个类，这个结构体里面可以定义一些方法。</font>

```go
type people struct {
	name string
}
func (p people) toString() {
	fmt.Println(p.name)
	fmt.Printf("p的地址 %p \n", &p)
}
```

`toString()`为方法。



<font style="background-color:#FADB14;">; </font><font style="background-color:#FADB14;">👾</font><font style="background-color:#FADB14;">注意：区别一下方法和函数。</font>



调用方式不一样。



```plain
函数的调用方式：函数名（实参列表）
方法的调用方式：变量.方法名字（实参列表）
```



方法是包含了接收者的函数，方法在func关键字后是**接收者**而不是函数名，接收者可以是自己定义的一个类型，这个类型可以是struct，interface，甚至我们可以重定义基本数据类型。

但对于普通函数，接收者为值类型时候，直接传递的只能是值类型。











> 更新: 2022-04-15 23:52:28  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/pywlu9>