# Spring 

Spring 简介：
spring的最基本的功能就是创建对象及管理这些对象之间的依赖关系，实现低耦合、高内聚。还提供像通用日志记录、性能统计、安全控制、异常处理等面向切面的能力，还能帮我们管理最头疼的数据库事务，本身提供了一套简单的JDBC访问实现，提供与 第三方数据访问框架集成（如Hibernate、JPA），与各种Java EE技术整合（如Java Mail、任务调度等等），提供一套自己的web层框架Spring MVC、而且还能非常简单的与第三方web框架集成。从这里我们可以认为Spring是一个超级粘合平台，除了自己提供功能外，还提供粘合其他技术和框架 的能力，从而使我们可以更自由的选择到底使用什么技术进行开发。而且不管是JAVA SE（C/S架构）应用程序还是JAVA EE（B/S架构）应用程序都可以使用这个平台进行开发。

spring启动过程：

web容器（比如Tomcat）会读取配置在web.xml中的监听器，从而启动spring容器。有了spring容器之后，我们才能使用spring的IOC AOP等特性

参考1：spring启动流程 [Spring启动过程分析](https://blog.csdn.net/moshenglv/article/details/53517343)

参考2：spring启动流程[Spring源码分析2 — 容器启动流程](https://blog.csdn.net/u013510838/article/details/75066884)


入门：[Spring入门看这一篇就够了](https://segmentfault.com/a/1190000013700859)

你应该注意定义在基于构造函数注入和基于设值函数注入中的 Beans.xml 文件的区别。唯一的区别就是在基于构造函数注入中，我们使用的是〈bean〉标签中的〈constructor-arg〉元素，而在基于设值函数的注入中，我们使用的是〈bean〉标签中的〈property〉元素。

第二个你需要注意的点是，如果你要把一个引用传递给一个对象，那么你需要使用 标签的 ref 属性，而如果你要直接传递一个值，那么你应该使用 value 属性。
 
-ref 部分表明这不是一个直接的值，而是对另一个 bean 的引用。

# springmvc的执行流程

时序图：
![1552285320244](https://github.com/ousp2008/ospNote/blob/master/spring/asserts/1552295472547.png)

# spring 常见面试题
[spring常见面试题](http://www.importnew.com/15851.html)


### bean的生命周期： [bean的生命周期](https://www.cnblogs.com/kenshinobiy/p/4652008.html)
>找工作的时候有些人会被问道Spring中Bean的生命周期，其实也就是考察一下对Spring是否熟悉，工作中很少用到其中的内容，那我们简单看一下。

    在说明前可以思考一下Servlet的生命周期：实例化，初始init，接收请求service，销毁destroy；

    Spring上下文中的Bean也类似，如下

    1、实例化一个Bean－－也就是我们常说的new；

    2、按照Spring上下文对实例化的Bean进行配置－－也就是IOC注入；

    3、如果这个Bean已经实现了BeanNameAware接口，会调用它实现的setBeanName(String)方法，此处传递的就是Spring配置文件中Bean的id值

    4、如果这个Bean已经实现了BeanFactoryAware接口，会调用它实现的setBeanFactory(setBeanFactory(BeanFactory)传递的是Spring工厂自身（可以用这个方式来获取其它Bean，只需在Spring配置文件中配置一个普通的Bean就可以）；

    5、如果这个Bean已经实现了ApplicationContextAware接口，会调用setApplicationContext(ApplicationContext)方法，传入Spring上下文（同样这个方式也可以实现步骤4的内容，但比4更好，因为ApplicationContext是BeanFactory的子接口，有更多的实现方法）；

    6、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessBeforeInitialization(Object obj, String s)方法，BeanPostProcessor经常被用作是Bean内容的更改，并且由于这个是在Bean初始化结束时调用那个的方法，也可以被应用于内存或缓存技术；

    7、如果Bean在Spring配置文件中配置了init-method属性会自动调用其配置的初始化方法。

    8、如果这个Bean关联了BeanPostProcessor接口，将会调用postProcessAfterInitialization(Object obj, String s)方法、；

    注：以上工作完成以后就可以应用这个Bean了，那这个Bean是一个Singleton的，所以一般情况下我们调用同一个id的Bean会是在内容地址相同的实例，当然在Spring配置文件中也可以配置非Singleton，这里我们不做赘述。

    9、当Bean不再需要时，会经过清理阶段，如果Bean实现了DisposableBean这个接口，会调用那个其实现的destroy()方法；

    10、最后，如果这个Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。
    
    以上10步骤可以作为面试或者笔试的模板，另外我们这里描述的是应用Spring上下文Bean的生命周期，如果应用Spring的工厂也就是BeanFactory的话去掉第5步就Ok了。
