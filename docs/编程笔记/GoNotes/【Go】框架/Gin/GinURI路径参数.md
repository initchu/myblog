# Gin URI 路径参数

获取 URI ，path 路径参数。

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()
	//用两个斜线分割的URI，路径参数
	r.GET("/:name/:age", func(c *gin.Context) {
		//获取路径参数
		name := c.Param("name")
		age := c.Param("age")
		c.JSON(http.StatusOK,gin.H{
			"name":name,
			"age":age,
		})
	})
	r.Run()
}
```

再加一条 path：

```go
package main

import (
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()
	//用两个斜线分割的URI，路径参数
	r.GET("/user/:name/:age", func(c *gin.Context) {
		//获取路径参数
		name := c.Param("name")
		age := c.Param("age")
		c.JSON(http.StatusOK,gin.H{
			"name":name,
			"age":age,
		})
	})
	//再写路径的时候，注意路由的冲突匹配问题
	r.GET("/blog/:year/:month", func(c *gin.Context) {
		year := c.Param("year")
		month := c.Param("month")
		c.JSON(http.StatusOK,gin.H{
			"year":year,
			"month":month,
		})
	})
	r.Run()
}
```





> 更新: 2022-04-27 20:50:53  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/wonlri>