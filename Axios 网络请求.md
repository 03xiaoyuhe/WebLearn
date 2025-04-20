## 简介

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501102358357.png)


## 发送 Get 请求

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110001026.png)

## 发送Post请求

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110003218.png)

## 异步回调问题

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110004475.png)

## 其他请求方式

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110005362.png)

> 在前后端分离架构中会存在跨域问题

## 为什么会出现跨域问题

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110032885.png)

## 跨域问题解决

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110034138.png)

### 简单请求

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110035519.png)

### 简单请求的服务器处理

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110036175.png)

### 非简单请求

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110037182.png)
![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110038380.png)

### 在Spring Boot 中配置 CORS

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110040533.png)

```java
@Configuration  
public class CorsConfig implements WebMvcConfigurer {  
  
    @Override  
    public void addCorsMappings(CorsRegistry registry) {  
        registry.addMapping("/**") // 允许跨域访问的路径  
                .allowedOrigins("*") // 允许跨域访问的源  
                .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS") // 允许请求方法  
                .maxAge(3600) // 预检间隔时间  
                .allowedHeaders("*") // 允许头设置  
                .allowCredentials(true); // 是否发送 cookie    }  
}
```

## 与 Vue整合

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501110106006.png)

