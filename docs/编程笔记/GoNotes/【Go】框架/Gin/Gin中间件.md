# Gin 中间件

定义一个中间件 m1:来统计处理请求处理函数的耗时：

```go
package main

import (
	"fmt"
	"github.com/gin-gonic/gin"
	"net/http"
	"time"
)

//handlerFunc
func indexHandler(c *gin.Context){
	fmt.Println("index")
	c.JSON(http.StatusOK,gin.H{
		"method":"index",
	})
}

// 定义一个中间件m1:来统计处理请求处理函数的耗时
func m1(c *gin.Context){
	fmt.Println("m1 in ..")
	start := time.Now()
	c.Next() //调用后续的处理函数，indexHandler, indexHandler 执行完了，之后继续会执行下一条语句
	//c.Abort() //阻止调用后续的处理函数
	cost := time.Since(start)
	fmt.Printf("cost:%v\n",cost)
	fmt.Println("m1 out ...")
}

func main() {
	r := gin.Default()

	r.GET("/index",m1, indexHandler) //可以传多个,先来后到

	r.Run()
}
```



```go
package main

import (
	"fmt"
	"github.com/gin-gonic/gin"
	"net/http"
	"time"
)

//handlerFunc
func indexHandler(c *gin.Context){
	fmt.Println("index")
	c.JSON(http.StatusOK,gin.H{
		"method":"index",
	})
}

// 定义一个中间件m1:来统计处理请求处理函数的耗时
func m1(c *gin.Context){
	fmt.Println("m1 in ..")
	start := time.Now()
	c.Next() //调用后续的处理函数，indexHandler, indexHandler 执行完了，之后继续会执行下一条语句
	//c.Abort() //阻止调用后续的处理函数
	cost := time.Since(start)
	fmt.Printf("cost:%v\n",cost)
	fmt.Println("m1 out ...")
}

func main() {
	r := gin.Default()
	r.Use(m1) //全局注册中间件函数 m1, 每次访问一个新的路由都会执行一次这个

	r.GET("/index",m1, indexHandler) //可以传多个,先来后到
	r.GET("/shop",m1, func(c *gin.Context) {
		c.JSON(http.StatusOK,gin.H{
			"msg":"shop",
		})
	})
	r.GET("/user", func(c *gin.Context) {
		c.JSON(http.StatusOK,gin.H{
			"msg":"user",
		})
	})
	r.Run()
}
```

比如，可以写控制非登录用户不能访问某路由页面的逻辑代码。

![1651313296639-554047e5-62b5-48a4-a291-1fdb0b8d8ebb.png](./img/WNtSr10tzE11vV_v/1651313296639-554047e5-62b5-48a4-a291-1fdb0b8d8ebb-998397.png)

其他使用要点：

:::info
`gin.Default()`默认使用了`Logger`和`Recovery`中间件，其中：

+ `Logger`中间件将日志写入`gin.DefaultWriter`，即使配置了`GIN_MODE=release`。
+ `Recovery`中间件会`recover`任何`panic`。如果有`panic`的话，会写入`500`响应码。

如果不想使用上面两个默认的中间件，可以使用`gin.New()`新建一个没有任何默认中间件的路由。

:::

:::info
`gin`中间件中使用`goroutine`，当在中间件或`handler`中启动新的`goroutine`时，不能使用原始的上下文`(c *gin.Context`），必须使用其只读副本`(c.Copy())`。

go funcXX( c.Copy)

:::



  
 



> 更新: 2022-04-30 18:22:04  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/rkdkbe>