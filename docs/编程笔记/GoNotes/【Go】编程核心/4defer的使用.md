# 4 defer 的使用

<font style="color:rgb(36, 41, 46);background-color:rgb(251, 251, 251);">defer的作用是： 你只需要在调用普通函数或方法前加上关键字defer，就完成了defer所需要的语法。当defer语句被执行时，跟在defer后面的函数会被延迟执行。直到包含该defer语句的函数执行完毕时，defer后的函数才会被执行，不论包含defer语句的函数是通过return正常结束，还是由于panic导致的异常结束。你可以在一个函数中执行多条defer语句，它们的执行顺序与声明顺序相反。</font>

## 资源管理与出错处理
比如我们打开一个文件要关闭，“打开”和“关闭”是对应出现的。

**引入defer的概念，是为了保证程序结束的时候发生。**

### 简单实例
```go
package main

import "fmt"

func tryDefer(){
	defer fmt.Println(1)
	fmt.Println(2)
}

func main() {
	tryDefer()
}

```

结果：

```go
2
1
```

实例练习2：

```go
package main

import "fmt"

func tryDefer(){
	defer fmt.Println(1)
	defer fmt.Println(2)
	fmt.Println(3)
}

func main() {
	tryDefer()
}

```

结果

```go
3
2
1
```

**defer相当于有个栈，defer不怕中间有return，panic。**

### 应用实例
在 defer 中回滚数据库的事务

```go
func createPost(db *gorm.DB) error {
    tx := db.Begin()
    defer tx.Rollback()
    
    if err := tx.Create(&Post{Author: "Draveness"}).Error; err != nil {
        return err
    }
    
    return tx.Commit().Error
}
    
```

<font style="color:rgb(0, 0, 0);">在使用数据库事务时，我们可以使用上面的代码在创建事务后就立刻调用 Rollback 保证事务一定会回滚。哪怕事务真的执行成功了，那么调用 tx.Commit() 之后再执行 tx.Rollback() 也不会影响已经提交的事务。</font>

<font style="color:rgb(0, 0, 0);"></font>



> 更新: 2022-04-01 22:18:54  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/ohuofy>