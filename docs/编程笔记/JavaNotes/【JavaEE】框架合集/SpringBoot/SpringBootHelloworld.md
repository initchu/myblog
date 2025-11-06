# SpringBoot Hello world

# Spring 概述
[spring.io](https://spring.io)

Spring 宏观来讲是一个生态圈，微观来说，就是 Spring 框架。

SpringBoot 和 SpringCloud 就是生态圈内的一个东西。

SpingBoot 的底层是 Spring 框架，它可以帮助我们解决整个复杂繁重的配置方案。

Sping 底层会使用很多适配器。

可以把开发流程变得简单。

# My Hello World demo
[Build software better, together](https://github.com/benrenshan/Java_demo)

mybatisPlus + maven

```java
package org.example;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
@MapperScan("org.example.mapper")
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

@MapperScan  
作用：指定要变成实现类的接口所在的包，然后包下面的所有接口在编译之后都会生成相应的实现类  
添加位置：是在Springboot启动类上面添加，添加 @MapperScan("org.example.mapper")注解以后，org.example.mapper包下面的接口类，在编译之后都会生成相应的实现类

<font style="color:#DF2A3F;">保留疑问：在启动类加上 @RestController 和在 controller 中加有什么区别？</font>

<font style="color:#DF2A3F;">启动类不负责请求，加在启动类上应该是没什么用？</font>

:::info
如果在整个 controller 类上方添加 @RestController，其作用就相当于把该 controller 下的所有方法都加上@ResponseBody，使每个方法直接返回 response 对象。

:::

```java
package org.example.Controller;

import com.google.gson.Gson;
import org.example.pojo.Student;
import org.example.mapper.StudentMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@CrossOrigin(origins = {"*","null"})
@SuppressWarnings("all")
public class Controller {
    @Autowired
    StudentMapper studentMapper;
    private Gson gson=new Gson();
    @GetMapping("/students")
    public String getStudents(){
        List<Student> students = studentMapper.selectList(null);
        return gson.toJson(students);
    }
    @PostMapping("/add")
    public void addStudent(@RequestBody Student student){
        studentMapper.insert(student);
    }
    @PostMapping("/delete")
    public void removeStudent(@RequestBody Student student){
       studentMapper.deleteById(student);
    }
    @GetMapping("/update")
    public void updateStudent(@RequestBody Student student){
        studentMapper.updateById(student);
    }
}

```







> 更新: 2023-01-13 09:56:24  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/up71bwblb2aa6nqv>