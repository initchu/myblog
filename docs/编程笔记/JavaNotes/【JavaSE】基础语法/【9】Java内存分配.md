# 【9】Java 内存分配

Java 用到的内存空间有以下几个方面：

+ **堆**
+ **栈**
+ **方法区**
+ ~~本地方法栈~~
+ ~~寄存器~~

从JDK8开始，就把**方法区**取消了，新增了**元空间。**

**把原来方法区的多种功能进行了拆分，有的功能放到了堆中，有的功能放到了元空间中。**

[深入理解Java虚拟机之【方法区】_java 方法区_Anton丶的博客-CSDN博客](https://blog.csdn.net/NICK_53/article/details/126264833)

![1695026802770-cc0cad3c-1d26-497b-96fc-995f7195d160.png](./img/NL3dQukb3_uaPrhu/1695026802770-cc0cad3c-1d26-497b-96fc-995f7195d160-175880.png)



> 更新: 2023-09-18 16:46:44  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/luzotsurfs6u5pm1>