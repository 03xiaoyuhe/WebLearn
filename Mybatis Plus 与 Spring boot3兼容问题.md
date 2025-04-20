> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/c335000/article/details/140698076)

今天在配置 mybatis 时，出现各种问题。

编写完 USERMapper（只是继承 BaseMapper\<User\>）, 报错第一行如下所示

org.springframework.beans.factory.BeanDefinitionStoreException: Invalid bean definition with name 'USERMapper' defined in file [D:\.......\mapper\USERMapper.class]: Invalid value [type](https://so.csdn.net/so/search?q=type&spm=1001.2101.3001.7020) for attribute 'factoryBeanObjectType': java.lang.String

到处搜索解决方法并无实际用处，询问 GPT 得到的解决方法让我想把 GPT 给解决掉

偶然间发现一个博主的文章，在将原依赖：

![img](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101604666.png)

更改为：

![](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501101604667.png)

后，得以解决问题。

原博主文章地址：[SpringBoot3 整合 MyBatisPlus 时遇到的问题及解决办法_mybatis plus invalid bean definition with name-CSDN 博客](https://blog.csdn.net/qq_56111066/article/details/140559809?ops_request_misc=&request_id=&biz_id=102&utm_term=Invalid%20bean%20definition%20with%20n&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-140559809.142%5Ev100%5Epc_search_result_base1&spm=1018.2226.3001.4187 "SpringBoot3整合MyBatisPlus时遇到的问题及解决办法_mybatis plus invalid bean definition with name-CSDN博客")