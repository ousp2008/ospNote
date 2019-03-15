# Spring 

Spring 简介：
spring的最基本的功能就是创建对象及管理这些对象之间的依赖关系，实现低耦合、高内聚。还提供像通用日志记录、性能统计、安全控制、异常处理等面向切面的能力，还能帮我们管理最头疼的数据库事务，本身提供了一套简单的JDBC访问实现，提供与 第三方数据访问框架集成（如Hibernate、JPA），与各种Java EE技术整合（如Java Mail、任务调度等等），提供一套自己的web层框架Spring MVC、而且还能非常简单的与第三方web框架集成。从这里我们可以认为Spring是一个超级粘合平台，除了自己提供功能外，还提供粘合其他技术和框架 的能力，从而使我们可以更自由的选择到底使用什么技术进行开发。而且不管是JAVA SE（C/S架构）应用程序还是JAVA EE（B/S架构）应用程序都可以使用这个平台进行开发。

spring启动过程：

web容器（比如Tomcat）会读取配置在web.xml中的监听器，从而启动spring容器。有了spring容器之后，我们才能使用spring的IOC AOP等特性

参考1：spring启动流程 [Spring启动过程分析](https://blog.csdn.net/moshenglv/article/details/53517343)

参考2：spring启动流程[Spring源码分析2 — 容器启动流程](https://blog.csdn.net/u013510838/article/details/75066884)

# springmvc的执行流程

时序图：

![1552295472547](assets/1552295472547.png)
