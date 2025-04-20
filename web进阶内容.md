## 静态资源访问

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092305035.png)

静态资源会被自动放到网站根目录，直接`/{资源名}`访问

## 文件上传原理

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092311349.png)

### SpringBoot实现文件上传功能

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092314737.png)
![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092315275.png)

## 拦截器

- 拦截器在Web系统中非常常见，对于全局同一的操作，我们可以把它提取到拦截器中实现。总结起来拦截器大致有以下几种使用场景：
	- 权限检查：如登录检查，进入处理程序检查是否登录，如果没有，则直接返回登录界面
	- 性能监控：有时系统在某段时间莫名其妙很慢，可以通过拦截器在进入处理程序之前记录开始时间，在处理完成后记录结束时间，从而得到该请求的处理时间
	- 通用行为：读取cookie得到用户信息并将用户对象放入请求，从而方便后续流程使用，还有提取Locale、Theme信息等，只要是多个处理程序都需要的，即可使用拦截器实现

Spring Boot 定义了HandlerInterceptor接口来实现自定义拦截器的功能

HandlerInterceptor接口定义了preHandle、postHandle、afterCompletion
![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100013778.png)
<center>拦截器时序图</center>

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100021918.png)
<center>拦截器定义</center>

### 拦截器注册

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100023417.png)

> [!tip]
> 一般来说，SpringBoot 的配置会放在 config 包下

## 构建RESTful服务

### RESTful介绍

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100919223.png)

### RESTful的特点

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100920475.png)

### RESTful API

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100924979.png)

### HTTP Method

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100926704.png)

### HTTP 状态码

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100928686.png)

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100929497.png)

### SpringBoot实现RESTful API

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100930706.png)
![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501100933060.png)

```java
@RestController  
public class UserController {  
    @GetMapping("/user/{id}")  
    public String getUser(@PathVariable int id) {  
        return "根据ID获取用户";  
    }  
  
    @PostMapping("/user")  
    public String postUser(@RequestBody User user) {  
        return "添加用户";  
    }  
  
    @PutMapping("/user")  
    public String putUser(@RequestBody User user) {  
        return "更新用户";  
    }  
  
    @DeleteMapping("/user/{id}")  
    public String deleteUser(@PathVariable int id) {  
        return "根据ID删除用户";  
    }  
}
```

> [!tip]
> @PathVariable 用来获取路径中的参数

## Swagger

> [用于 spring-boot 的 OpenAPI 3 库 --- OpenAPI 3 Library for spring-boot](https://springdoc.org/#getting-started)

### 什么是 Swagger

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101015916.png)

> 动态生成接口文档，并提供调试功能

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101017328.png)

> [!tip]
> 在引入依赖后，还需要进行配置，即在项目中添加配置类

> SpringBoot 中，所有的配置类都要加@Configuration注解

```java
@Configuration // 告诉 Spring 这是一个配置类  
@EnableSwagger2 // 启用 Swagger 功能  
public class SwaggerConfig {  
    /**  
     * 配置Swagger2相关bean  
     */    @Bean  
    public Docket createApi(){  
        return new Docket(DocumentationType.SWAGGER_2)  
                .apiInfo(apiInfo())  
                .select()  
                .apis(RequestHandlerSelectors.basePackage("com"))//com包下的所有API都交给Swagger2管理  
                .paths(PathSelectors.any()).build();  
    }  
  
    /**  
     * 此处主要是API文档页面显示信息  
     */  
    private ApiInfo apiInfo(){  
        return new ApiInfoBuilder()  
                .title("演示文档API")// 标题  
                .description("演示项目") // 描述  
                .version("1.0") // 版本  
                .build();  
    }  
}
```

### 使用 Swagger2 进行接口测试

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101034086.png)

> [!tip]
> 可以使用 @ApiOperation 给 Api 加注释

> [!warning]
> Swagger 3.x，更新了注解方式
> 
> 详见[用于 spring-boot 的 OpenAPI 3 库 --- OpenAPI 3 Library for spring-boot](https://springdoc.org/#getting-started)

### Mybatis CRUD 注解

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101513145.png)

