---
layout: post
title: Springboot通过url访问获取外部静态资源图片
subtitle: 
date: 2018-04-12
categories: SpringBoot
tags: [SpringBoot]
description: Springboot通过url访问获取外部静态资源图片。
---

#### Springboot通过url访问获取外部静态资源图片

> 方法一: 代码上配置 亲测好用

```Java
@Configuration
public class WebMvcConfiguration extends WebMvcConfigurerAdapter {
	@Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        //addResourceHandler是指你想在url请求的路径
        //addResourceLocations是图片存放的真实路径
        registry.addResourceHandler("/image/**").addResourceLocations("file:D://User/");
        super.addResourceHandlers(registry);
    }
}
```

注意：自己的项目是否配置了shiro等权限拦截要将请求设为匿名可访问。

> 方法二：配置文件中配置


```Java
#资源映射路径为/image/**，你想在url访问的请求路径
spring.mvc.static-path-pattern=/image/**
#资源映射地址为file:D://User/，图片存放的真实路径
spring.resources.static-locations=file:D://User/ 
```

如下图，看浏览器的地址栏，框框标志第一部分是我的项目名，框框标志第二部分就是上面配置的映射路径（会映射到图片存放的真实路径），框框标志第三部分就是我的图片文件名，通过上面两种方式随便一种，就可以直接在浏览器通过url访问获取图片了。

![image](http://cnsyear.com/images/blog/TIM截图20180412183307.png?11111)

[原文链接](https://blog.csdn.net/ljj_9/article/details/79650008)

*标记：人生最痛苦的地方就在于，明明已经无法忍受，却还要忍受下去。
——当年明月 《明朝那些事儿》*