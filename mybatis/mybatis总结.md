# springboot整合mybatis可以用注解版和配置版两种 [示例](https://www.cnblogs.com/gxyandwmm/p/9713672.html)
  在使用注解版时：
  ``` java 
      @Mapper
      @Component
      public interface UserMapper {

          @Select("select * from user")
          List<User> getAllUsers();
      }
     首先需要在类前加上@Mapper的注解，这样才能够标记这个接口被mybatis所查找到，如果嫌每个类都注解很麻烦
     也可以直接在Application.java中注解mapper扫描目录如@MapperScan(“com.demo.maper”)。 
    然后再直接写相应的方法并在方法上面标注mybatis动作即可，这儿不做过多的赘述 
    最后要提一下的就是@Component，因为在IDEA中有bean检测，所以为了防止它提示
    Could not autowire. No beans of ‘UserDao’ type found. Checks autowiring problems in a bean class. 
    加一个@Component注解，实际上即使不加也不影响使用。


Spring Data JPA 的时候， 只需要声明一个接口， 增删改查的方法立马就有了，而且对于一些简单的查询，通过特定格式的方法名字，声明一个接口方法就能完成。
但是JPA是基于hibernate，效率低而且很不灵活，所以大部分企业的ORM框架选择的是MyBatis
