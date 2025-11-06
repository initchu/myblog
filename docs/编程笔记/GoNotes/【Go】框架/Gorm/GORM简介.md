# GORM 简介

## ORM 
ORM （Object Relational Mapping）对象关系映射。对象关系映射模式是一种为了解决面向对象与关系数据库存在的互不匹配的现象的技术。ORM 框架是连接数据库的桥梁，只要提供了持久化类与表的映射关系，ORM 框架在运行时就能参照映射文件的信息，把对象持久化到数据库中。当我们实现一个应用程序时（不使用 O/R Mapping），我们可能会写特别多数据访问层的代码，从数据库保存、删除、读取对象信息，而这些代码都是重复的。而使用 ORM 则会大大减少重复性代码。对象关系映射（Object Relational Mapping，简称 ORM），主要实现程序对象到关系数据库数据的映射。

## GORM
Golang 写的，GitHub 上活跃度很高的 orm 库

GORM 具有以下特点：

+ 全功能 ORM;
+ 关联(包含一个，包含多个，属于，多对多，多种包含);
+ Callbacks(创建/保存/更新/删除/查找之前/之后);
+ 预加载;
+ 事务
+ 复合主键
+ SQL Builder
+ 自动迁移
+ 日志
+ 可扩展，编写基于 GORM 回调的插件
+ 每个功能都有测试
+ 开发人员友好

注意，<font style="color:rgb(77, 77, 77);">GORM 官方支持的数据库类型有： </font>

+ <font style="color:rgb(77, 77, 77);">MySQL</font>
+ <font style="color:rgb(77, 77, 77);">PostgreSQL</font>
+ <font style="color:rgb(77, 77, 77);">SQlite</font>
+ <font style="color:rgb(77, 77, 77);">SQL Server</font>





> 更新: 2022-05-04 17:23:14  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/amual1>