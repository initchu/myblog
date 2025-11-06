# Gin 的 JSON

Gin 的 Json 渲染，有两种方法。

1. 自己拼接 Json，使用 `gin.H{}`，该类型是 map 。
2. 传一个结构体进去

```go
func main() {
	r := gin.Default()

	// gin.H is a shortcut for map[string]interface{}
	r.GET("/someJSON", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{"message": "hey", "status": http.StatusOK})
	})

	r.GET("/moreJSON", func(c *gin.Context) {
		// You also can use a struct
		var msg struct {
			Name    string `json:"user"`
			Message string
			Number  int
		}
		msg.Name = "Lena"
		msg.Message = "hey"
		msg.Number = 123
		// Note that msg.Name becomes "user" in the JSON
		// Will output  :   {"user": "Lena", "Message": "hey", "Number": 123}
		c.JSON(http.StatusOK, msg)
    })
    r.run()
}
```



:::danger
**注: 结构体字段需要大写，不大写是访问不到的。**

:::



> 更新: 2022-04-27 14:15:02  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/zwk5g0>