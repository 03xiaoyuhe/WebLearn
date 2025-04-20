## ORM介绍

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101439828.png)

## MyBatis-Plus 介绍

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101441842.png)

### 添加依赖

```xml
<!--        MyBatisPlus 依赖-->  
        <dependency>  
            <groupId>com.baomidou</groupId>  
            <artifactId>mybatis-plus-boot-starter</artifactId>  
            <version>3.5.7</version>  
        </dependency>
<!--        Mysql驱动依赖-->  
        <dependency>  
            <groupId>mysql</groupId>  
            <artifactId>mysql-connector-java</artifactId>  
            <version>5.1.47</version>  
        </dependency>
<!--        数据库连接池 druid-->     
<!--        阿里巴巴提供的数据连接池技术-->
		<dependency>  
            <groupId>com.alibaba</groupId>  
            <artifactId>druid-spring-boot-starter</artifactId>  
            <version>1.1.20</version>  
        </dependency>
```

### 全局配置

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101500344.png)

### 添加 @MapperScan注解

- 在 Spring Boot 启动类中添加 @MapperScan注解，扫描 Mapper 文件夹

```java
@SpringBootApplication  
// 确定Mybatis扫描包名  
@MapperScan("com.ting.learnformybatisplus.mapper")  
public class LearnForMybatisPlusApplication {  
  
    public static void main(String[] args) {  
        SpringApplication.run(LearnForMybatisPlusApplication.class, args);  
    }  
  
}
```

### Mybatis CRUD 注解

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101540514.png)

### CRUD 操作

```java
@Mapper  
public interface UserMapper {  
//  查询所有用户  
    @Select("select * from user")  
    public List<User> find();  
  
    @Insert("insert into user values(#{id}, #{username}, #{password}, #{birthday})")  
    public int insert(User user);  
}
```

如果传入参数只有一个值，在注解中直接使用`#{参数名}`即可

如果传入参数是一个对象，则在注解中保证`#{}`中传的一定是对象的属性即可。

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101644076.png)

### 使用MybatisPlus

```java
@Mapper  
public interface UserMapper extends BaseMapper<User>  
// 其中 <User> 告诉 MybatisPlus 要操作谁  
// Mybatis 会自动根据 数据库中的表，对数据库 进行增删改查  
{  
  
}
```

其中，User类的属性应该要与数据库中表的属性一一对应

#### 若表名与类名不一致

Mybatis Plus 提供了一组注解

如：

```java
@TableName("t_user")  
public class User {  
	// 标记主键，类型为自增，则在插入后，Mybatis Plus会将主键赋回对象中的主键
    @TableId(type = IdType.AUTO)  
    private Long id;        // 数据库中的主键字段  
    private String name;    // 数据库中的名称字段  
    private String password; // 数据库中的密码字段  
    private LocalDate birthday; // 数据库中的生日字段
```

> 如果不加 @TableId(type = IdType.AUTO)  ，自然的，没有反馈回实体对象，在程序运行时，实体对象的ID属性还是0，即使数据库已经自增了

> 可以看 Mybatis Plus 官方文档

## 关于查询条件

QueryWrapper\<User\> 可以进行条件查询映射

> 条件构造器