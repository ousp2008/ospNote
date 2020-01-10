mybatisPlus 常用知识点

#### 一：在sql中where 后面的条件语句在mybatisplus中的表现：

 mapper（Dao层）如 UserMapper.java中



```java

@Select("select * from user ${ew.customSqlSegment}")
List<Map<String, Object>> getPageList(@Param(Constants.WRAPPER) Wrapper wrapper, Page page);
```

- 1 其中Wrapper参数会转换成 例如：where sex="男"  and  age>20 这种条件

- 2 page 如果不为空则会在自动生成的sql 末尾自动增加例如： limit 0,10 

#####  service层：

```java
String sex="男";
int age=20;
return userMapper.getPageList(
        Wrappers.query()
                .eq(StringUtils.isNotEmpty(sex), "sex", sex)
                .ge(StringUtils.isNotEmpty(age), "age", age)
),page);
```

其中传递的参数page 可以在Controller中定义：

 ###### controller层

```java
int pageNo=1;
int pageSize=10;
Page page=new Page<Map>(pageNo,pageSize);
return userService.getPageList(page);
    
```

> 前提：进行分页的配置

```java
@Slf4j
@Configuration
public class MyBatisPlusConfig {

    /**
     * mybatis-plus分页插件
     */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        PaginationInterceptor paginationInterceptor = new PaginationInterceptor();
        return paginationInterceptor;
    }

}
```

  

#### 二.若是复杂的根据条件来进行多表查询sql的话

```java
@(select u.user_id,u.name,o.trad_no from t_order o left join t_user t)
public List<Map<String, Object>> selectByConditionPage(@Param(Constants.WRAPPER) Wrapper wrappe);
```

  我们在service层传递的条件

orderMapper.selectConditionPage(

)

```java

return baseMapper.selectByConditionPage(
        Wrappers.query()
                .eq("o.status", 1)
                .eq("t.user_id", 1001)
                .between(StringUtils.isNotEmpty(startTime) && StringUtils.isNotEmpty(endTime), "o.create_time", startTime, endTime)
                .orderByDesc("o.create_time")
      
);
```



#### 三.简单的单个表sql条件的查询 可以如下：

```java
BigDecimal userBalance = userService.lambdaQuery().eq(TUser::getUserId, 1511).eq(TUser::getAge,20).one().getBalance();
```

#### 四.单个表根据某些条件更新表：

```java
boolean updateUserCount = userService.lambdaUpdate().eq(TUser::getUserId, user.getUserId())
        .eq(TUser::getBalance, oldBalance).update(user);
```

#### 五. mybatis-plus 中 如果想获取保存后数据的自增值 则实体的主键上应该加上注解

  ```java
  @TableId(type = IdType.AUTO) 主键自增 数据库中需要设置主键自增
  private Long id;
  ```

  其中 主键的策略有以下几种

  在实体类中 ID属性加注解

  ```java
  @TableId(type = IdType.AUTO) 主键自增 数据库中需要设置主键自增
  private Long id;
  @TableId(type = IdType.NONE) 默认 跟随全局策略走
  private Long id;
  @TableId(type = IdType.UUID) UUID类型主键
  private Long id;
  @TableId(type = IdType.ID_WORKER) 数值类型  数据库中也必须是数值类型 否则会报错
  private Long id;
  
  @TableId(type = IdType.ID_WORKER_STR) 字符串类型   数据库也要保证一样字符类型
  private Long id;
  
  @TableId(type = IdType.INPUT) 用户自定义了  数据类型和数据库保持一致就行
  private Long id;
  ```


>![image](http://upload-images.jianshu.io/upload_images/593616-673d01eb59c81582?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

喜欢的朋友可以关注下哦~