# Web 基本概念

# 基本概念
web 开发有两种，一种是静态，另一种是动态。

在java中，动态web资源开发的技术称为Javaweb。

web应用程序：可以提供浏览器访问的程序；如果有多个html的web资源，这些web资源可以被外界访问，对外界提供服务。通过URI统一资源定位符找到这个web资源存放的文件下。

Tomcat服务器。一个web应用可以有多部分组成。html，css等。

web应用程序编写完之后，需要一个服务器来统一管理。

# web 服务器
## 介绍
ASP 国内最早流行的，嵌入了VB脚本，ASP+COM；

在ASP开发里面，一个页面嵌入Java代码等等业务代码，页面极其混乱，维护成本很高。

PHP开发，开发速度很快，功能很强大，跨平台，代码很简单，问题就是PHP无法承载大访问量。

**JSP/Servlet：Sun公司主推的B/S架构（浏览和服务器）。基于Java语言。可以承载三高问题带来的影响语法像ASP，ASP转JSP，可以加强市场强度。**

## Tomcat
Tomcat 是 Apache 软件基金会（Apache Software Foundation）的 Jakarta 项目中的一个核心项目，由于有了Sun 的参与和支持，最新的 Servlet 和JSP 规范总是能在Tomcat 中得到体现，Tomcat 5 支持最新的Servlet 2.4 和 JSP 2.0 规范。因为 Tomcat 技术先进、性能稳定，而且免费，因而深受 Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的 Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试 JSP 程序的首选。对于一个 Java 初学 Web 者来说，它是最佳的选择。

:::info
服务器是一种被动操作，用来处理用户的请求并给用户一些响应信息。

Tomcat 是一个简单的轻量级服务器。适用于初学者。

:::

# Maven
在 javaweb 中，需要使用大量的 jar 包，我们手动去导入，如何能够让一个东西自动导入和配置包，Maven 诞生了。

Maven 是项目架构管理工具。

**Maven 的高级之处在于，会自动导入 jar 包，而且会自动导入这个 jar 包所依赖的其他 jar 包。**

Maven 的核心思想：约定大于配置，有约束的话就不要去违反。

Maven 规定了如何写 Java 代码。

在 IDEA 中使用 **Maven。**

pom 文件是 Maven 的核心配置文件。

在 pom 里面配置他可以，帮着导入 jar 包所依赖的其他jar包。

maven 由于约定大于配置的思想，所以会造成一些资源的导出问题。在 build 中配置 **resources**，来防止我们资源导出失败的问题。

参考链接：[https://www.cnblogs.com/lx2001/p/15008072.html](https://www.cnblogs.com/lx2001/p/15008072.html)



> 更新: 2023-09-04 20:06:46  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/ypchw08ss12483lb>