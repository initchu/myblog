# Gin 路由/路由组

## 路由
单个路由的定义方法：

```go
package main

import (
    "github.com/gin-gonic/gin"
    "net/http"
)

func main() {
    r := gin.Default()
    
    //访问 /index 的 GET 请求会走这一条处理逻辑
    //路由
    //r.HEAD()
    r.GET("/index", func(c *gin.Context) {
        c.JSON(http.StatusOK,gin.H{
            "method":"GET",
        })
    })
    //创建
    r.POST("/index", func(c *gin.Context) {
        c.JSON(http.StatusOK,gin.H{
            "method":"POST",
        })
    })
    //更新
    r.PUT("/index", func(c *gin.Context) {
        c.JSON(http.StatusOK,gin.H{
            "method":"PUT",
        })
    })
    //删除
    r.DELETE("/index", func(c *gin.Context) {
        c.JSON(http.StatusOK,gin.H{
            "method":"Delete",
        })
    })
    //Any:请求方法大集合/大杂烩
    r.Any("/user", func(c *gin.Context) {
        switch c.Request.Method {
            case http.MethodGet:
            c.JSON(http.StatusOK,gin.H{"method":"GET"})
            case http.MethodPost:
            c.JSON(http.StatusOK,gin.H{"method":"POST"})
        }
    })
    //没有定义路由的地址
    r.NoRoute(func(c *gin.Context) {
        c.JSON(http.StatusNotFound,gin.H{"msg":"404NotFound"})
    })
    r.Run()
}
```

## 路由组
想把多个路由的公共前缀提取出来，创建一个路由组的方法：

```go
package main

import (
    "github.com/gin-gonic/gin"
    "net/http"
)

func main() {
	r := gin.Default()
	userGroup := r.Group("/user")
	{
		userGroup.GET("/index", func(c *gin.Context) {...})
		userGroup.GET("/login", func(c *gin.Context) {...})
		userGroup.POST("/login", func(c *gin.Context) {...})

	}
	shopGroup := r.Group("/shop")
	{
		shopGroup.GET("/index", func(c *gin.Context) {...})
		shopGroup.GET("/cart", func(c *gin.Context) {...})
		shopGroup.POST("/checkout", func(c *gin.Context) {...})
	}
	r.Run()
}
```

```go
shopGroup := r.Group("/shop")
	{
		shopGroup.GET("/index", func(c *gin.Context) {...})
		shopGroup.GET("/cart", func(c *gin.Context) {...})
		shopGroup.POST("/checkout", func(c *gin.Context) {...})
		// 嵌套路由组
		xx := shopGroup.Group("xx")
		xx.GET("/oo", func(c *gin.Context) {...})
	}
```



> 更新: 2022-04-30 14:40:42  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/ytzg4o>