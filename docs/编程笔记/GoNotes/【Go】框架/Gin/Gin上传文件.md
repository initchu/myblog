# Gin 上传文件

1. 加载html文件
2. 浏览器发送POST请求给客户端，请求读取文件 ，`f,err := c.FormFile()`
3. 错误处理，如果正确的话。读取的文件保存至本地 `c.SaveUploadedFile(f,dst)`



```go
package main

import (
	"fmt"
	"github.com/gin-gonic/gin"
	"net/http"
)

func main() {
	r := gin.Default()
	r.LoadHTMLFiles("./index.html")
	r.GET("/index", func(c *gin.Context) {
		c.HTML(http.StatusOK,"index.html",nil)
	})
	r.POST("/upload", func(c *gin.Context) {
		// 从请求中读取文件
		f,err := c.FormFile("f1" ) // 从请求中获取携带的参数一样
		if err != nil{
			c.JSON(http.StatusBadRequest,gin.H{
				"message error":err.Error(),
			})
		}else{
			// 将读取到的文件保存在本地（服务器本地）
			dst := fmt.Sprintf("./%s",f.Filename)
			c.SaveUploadedFile(f,dst)
			c.JSON(http.StatusOK,gin.H{
				"status":"OK",
			})
		}
	})
	r.Run()
}
```

index.html 文件代码

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Title</title>
    
  </head>
  <body>
    <form action= "/upload" method = "post" enctype="multipart/form-data">
      
      <input type="file" name="f1">
      <input type = "submit" value ="上传">
    </form>
    
  </body>
</html>
```

上述实例代码种`dst := fmt.Sprintf("./%s",f.Filename)` 为保存的相对路径地址。传给`c.SaveUploadedFile(f,dst)`以保存到本地。

在浏览器里面选择上传的文件，如《模拟笔试1.png》，点击上传，结果显示：

![保存到了相对路径下](./img/30IE-k6VmVQBzJ2b/1651289487660-c49c8fe5-2ce0-4432-b178-bdd8b82e9013-188143.png)





> 更新: 2022-04-30 11:34:11  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/vh6wwl>