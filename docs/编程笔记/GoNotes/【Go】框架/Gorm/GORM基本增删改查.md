# GORM 基本增删改查

![画板](./img/RQrYnZCGJ61N2xfi/1676966131176-bc8bb8d8-678a-4da1-95bd-ebd96395ef2b-161137.jpeg)

# 创建
```go
package main
func CreatedTest(){
    dbres := GLOBAL_DB.Create(&TestUser{Name:"tt",Age:18}) //返回一个 db 指针
    fmt.Println(dbres.Error,dbres.ROWsAffected) // 打印日志
}
```

# 查询
```go
package main
func UpdateTest（）{
    dbres := GLOBAL_DB.Create(&TestUser{})
    
}
```

# 更新


# 删除


> 更新: 2023-02-21 17:14:44  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/qiu8twemq8goktzn>