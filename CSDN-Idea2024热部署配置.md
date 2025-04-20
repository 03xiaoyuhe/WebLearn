> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_61033357/article/details/139290535)

#### 文章目录

*   *   *   [1. 增加 pom.xml 内容](#1pomxml_1)
        *   [2. 修改 application.poperties 的内容](#2applicationpoperties_13)
        *   [3.IDEA2024 软件的其他配置](#3IDEA2024_21)
        *   [测试是否热部署成功](#_26)

#### 1. 增加 pom.xml 内容

![](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092028767.png)  
供复制

```
  <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
  </dependency>

```

点击右上角界面出现的小按钮进行同步下载依赖

#### 2. 修改 application.poperties 的内容

![](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092028768.png)  
供复制

```
spring.devtools.restart.enabled=true
spring.devtools.restart.additional-paths=src/main/java

```

#### 3.IDEA2024 软件的其他配置

3.1 File–>settings–>Advanced Settings 勾选下图选项–>apply  
![](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092028769.png)  
3.2File–>settings–>Build–>Complier–>Build project automatically(如下图勾选)  
![](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092028770.png)

#### 测试是否[热部署](https://so.csdn.net/so/search?q=%E7%83%AD%E9%83%A8%E7%BD%B2&spm=1001.2101.3001.7020)成功

1. 创建一个[控制器](https://so.csdn.net/so/search?q=%E6%8E%A7%E5%88%B6%E5%99%A8&spm=1001.2101.3001.7020)，并写一个接口文件  
![](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501092028771.png)  
2. 修改返回值内容，[刷新浏览器](https://so.csdn.net/so/search?q=%E5%88%B7%E6%96%B0%E6%B5%8F%E8%A7%88%E5%99%A8&spm=1001.2101.3001.7020)是否接口数据更新成功，测试正常，热部署成功