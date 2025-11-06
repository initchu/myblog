# 【0】 Spring 概述

参考文章：

[深入浅出Spring 框架，原来以前白学了！ - 掘金](https://juejin.cn/post/7095532056632885284)

# Spring 框架概述
1. spring 是轻量级的开源的 Java EE 框架
2. Spring 可以解决企业应用开发的复杂性
3. Spring 有两个核心部分 IOC 和 AOP
    1. IOC 控制反转：把创建对象的过程交给 spring 进行管理
    2. Aop 面向切面：在不修改源代码的情况下，进行功能的添加和增强

# Spring 特点
1. 方便耦合，简化开发
2. Aop 编程支持
3. 方便程序的测试
4. 方面集成各种优秀框架
5. 方便事务的操作
6. 降低 API 开发难度

# Spring 框架入门案例
下载spring

[https://repo.spring.io](https://repo.spring.io)/release/org/springframework/spring/

5.2.6 是稳定版本。

创建一个 java 项目，将 Spring 的四个基础包以及 commons-logging 的 JAR 包复制到 lib 目录中，并发布到类路径下。

+ lib
    - commons-logging-X.X.jar
    - spring-beans-x.x.x.RELEASE.jar
    - spring-context-x.x.x.RELEASE.jar
    - spring-core-x.x.x.RELEASE.jar
    - spring-expression-x.x.x.RELEASE.jar

在 src 目录下，创建 com.javastudy.spring5 包，在包中创建接口 UserDao，然后在接口中定义一个 say() /add()方法。

```java
package com.javastudy.spring5;
public interface UserDao {
	public void say();
}
```

在这个 com.javastudy.spring5 包下，创建这个接口的实现类，UserDaoImpl，该类实现了接口的 say 方法。

```java
package com.javastudy.spring5;
public class UserDaoImpl implements UserDao{
	public void say(){
        System.out.println("userDao say hello World！");
    }
}
```

在 src 目录下，直接创建 applicationContext.xml 或者 bean1.xml 文件。在配置文件中创建一个 id 为 user 的 bean。【这种方式就是 IOC 操作（Bean 管理）的 XML 方式】

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.springframework.org/schema/beans
  http://www.springframework.org/schema/beans/spring-beans.xsd">
  <bean id="userDao" class="com.javastudy.spring5"/>
</beans>
```

2-5 行是约束配置，不需要被开发人员手写。

在 com.javastudy.spring5 下，创建测试类 TestIOC，并在类中编写 main() 方法，在 main() 方法中，需要初始化 Spring 容器，并加载配置文件，然后通过 Spring 容器获取 userDao 实例，最后调用实例中的 say() 方法。

```java
package com.javastudy.spring5;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
public class TestIOC{
	public static void main(String[] args){
        //1. 初始化 spring 容器，加载配置文件
        ApplicationContext applicationContext = new ClassPathXmlApplication("applicationContext.xml");
        //2. 通过容器获取 userDao 实例
        UserDao userDao = (UserDao) applicationContext.getBean("userDao");
        //3. 调用实例中的 say（）方法
        userDao.say();
    }
}
```







> 更新: 2023-01-05 09:27:52  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/suuwvghl7f7zyui1>