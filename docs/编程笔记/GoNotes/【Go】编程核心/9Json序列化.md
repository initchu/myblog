# 9 Json 序列化

## 一、Json的基本介绍


Json是一种**轻量级的数据交换格式**，易于人阅读和编写，同时也易于机器的解析和生成。



`key:value`



场景：

一个服务器要给浏览器返回一些数组，那么在服务器内，要把数组进行一些Json序列化，原因是json格式利于网络的传输。浏览器接收到了json就对其进行反序列化，还原成数组，在进行显示操作。

传输的过程中，都遵守json格式。



举例：

tcp编程中的应用：用go写了聊天系统。

客户端A          数组->序列化



          后台服务器Go   中转



客户端B          反序列化->数组





## 二、Json格式和在线解析
### 格式


在JS语言中，一切都是对象。因此，任何的数据类型都可以通过Json来表示，例如字符串、数组、对象、数组、map、结构体等。



JSON键值对是用来保存数据的一种方式，键值对组合中的键名写在前面`""`，使用冒号`：`分隔，然后紧接着值。



`{"name":"tom","age":18,"address":["beijing","shanghai"]}`



<font style="color:#D46B08;">任何数据类型都可以转成JSON格式。</font>

### 在线解析网站


[https://www.json.cn](https://www.json.cn)



## 三、结构体和切片 Map 切片序列化


json序列化是指，将有key-value结构的数据类型（比如结构体，map，切片）序列化成json字符串的操作。

```go
package main

import (
	"encoding/json"
	"fmt"
)

type Monster struct {
	Name string
	Age int
	Birthday string
	Sal float64
	Skill string
}
func testStruct(){
	monster := Monster{
		Name :"Niu",
		Age : 500,
		Sal :8000.0,
		Skill:"bit",
	}
	data,err := json.Marshal(&monster)
	if err != nil{
		fmt.Printf("序列化错误 err=%v\n",err)
	}
	fmt.Printf("monster序列化后=%v\n",data)
}

func main() {
	//演示将结构体，map,切片序列化
	testStruct()
}

```

加个切片序列化的代码:

```go
package main

import (
	"encoding/json"
	"fmt"
)
func testSlice(){
	var slice []map[string]interface{}
	var m1 map[string]interface{}
	//使用map之前，需要先用make
	m1 = make(map[string]interface{})
	m1["name"] = "jack"
	m1["age"] = "7"
	m1["address"] = "Beijing"
	slice = append(slice,m1)

	var m2 map[string]interface{}
	//使用map之前，需要先用make
	m2 = make(map[string]interface{})
	m2["name"] = "tom"
	m2["age"] = "20"
	m2["address"] = "Shanghai"
	slice = append(slice,m2)
	//将切片进行序列化操作
	data,err := json.Marshal(slice)
	if err != nil{
		fmt.Printf("序列号错误 err=%v\n",err)
	}
	fmt.Printf("slice序列化后=%v\n",string(data))

}

func main() {
	//演示将结构体，map,切片序列化
	testStruct()
	testSlice()
}

```



> 更新: 2022-07-03 14:29:30  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/go2ofc>