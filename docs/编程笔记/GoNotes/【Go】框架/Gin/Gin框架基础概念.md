# Gin 框架基础概念

## 安装
```go
go get -u github.com/gin-gonic/gin
```

## 介绍
`Gin`<font style="color:rgb(68, 68, 68);">是一个用 Go 语言编写的 web 框架。</font>

## <font style="color:rgb(68, 68, 68);">基本使用</font>
```go
package main

import (
	"github.com/gin-gonic/gin"
)

func main() {
	// 创建一个默认的路由引擎
	r := gin.Default()
	// GET：请求方式；/hello：请求的路径
	// 当客户端以GET方法请求/hello路径时，会执行后面的匿名函数
	r.GET("/hello", func(c *gin.Context) {
		// c.JSON：返回JSON格式的数据
		c.JSON(200, gin.H{
			"message": "Hello world!",
		})
	})
	// 启动HTTP服务，默认在0.0.0.0:8080启动服务
	r.Run()
}
```

HTTP 编程 相对来说繁琐很多：

```go
package main

import (
	"encoding/json"
	"log"
	"net/http"
)

type IndexData struct {
	Title string `json:"title"`
	Desc string `json:"desc"`
}

func index(w http.ResponseWriter,r *http.Request)  {
	w.Header().Set("Content-Type","application/json")
	var indexData IndexData
	indexData.Title = "go_HTTP"
	indexData.Desc = "Go 的 HTTP 案例"
	jsonStr,_ := json.Marshal(indexData)
	w.Write(jsonStr)
}

func main()  {
	//程序入口，一个项目 只能有一个入口
	//web程序，http协议 ip port
	server := http.Server{
		Addr: "127.0.0.1:8080",
	}
	http.HandleFunc("/",index)
	if err := server.ListenAndServe();err != nil{
		log.Println(err)
	}
}
```

Gin 框架中使用`LoadHTMLGlob()`或者`LoadHTMLFiles()`方法进行HTML模板渲染。

```go
func main() {
	r := gin.Default()
	r.LoadHTMLGlob("templates/**/*")
	//r.LoadHTMLFiles("templates/posts/index.html", "templates/users/index.html")
	r.GET("/posts/index", func(c *gin.Context) {
		c.HTML(http.StatusOK, "posts/index.html", gin.H{
			"title": "posts/index",
		})
	})
	r.GET("users/index", func(c *gin.Context) {
		c.HTML(http.StatusOK, "users/index.html", gin.H{
			"title": "users/index",
		})
	})

	r.Run(":8080")
}
```



> 更新: 2022-04-14 11:08:27  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/dt6n63>