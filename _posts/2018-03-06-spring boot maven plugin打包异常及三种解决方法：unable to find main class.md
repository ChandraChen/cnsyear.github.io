---
layout: post
title: Spring Boot Maven Plugin打包异常及三种解决方法Unable to find main class
subtitle: 
date: 2018-03-06
categories: [maven,SpringBoot]
tags: [maven,SpringBoot]
description: Spring Boot Maven Plugin打包异常及三种解决方法Unable to find main class。
---
#### Spring Boot Maven Plugin打包异常及三种解决方法：Unable to find main class

【背景】

spring-boot项目，打包成可执行jar，项目内有两个带有main方法的类并且都使用了@SpringBootApplication注解（或者另一种情形：你有两个main方法并且所在类都没有使用@SpringBootApplication注解），pom.xml如下

```Java
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <version>1.5.3.RELEASE</version>
    <executions>
        <execution>
            <goals>
                <goal>repackage</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```


【问题】

- 执行mvn clean package，报错如下（说点不相关的，使用install同理。因为spring-boot:repackage目标（goal）（下文会说）被绑定在package构建阶段（phases），而package阶段在install阶段之前，指定构建阶段之前的阶段都会执行。详细参见：Introduction to the Build Lifecycle）

```Java
　　[ERROR] Failed to execute goal org.springframework.boot:spring-boot-maven-plugin:1.5.3.RELEASE:repackage (default) on project webapps-api-bid: Execution default of goal org.springframework.boot:spring-boot-maven-plugin:1.5.3.RELEASE:repackage failed: Unable to find a single main class from the following candidates [com.xx.api.main.ApiBidMain, com.xx.webapps.api.main.WebappsApiBidMain]

```

- 执行mvn clean package spring-boot:repackage，报错如下，不如上面日志详细

```Java
Java
　　[ERROR] Failed to execute goal org.springframework.boot:spring-boot-maven-plugin:1.5.3.RELEASE:repackage (default) on project webapps-api-bid: Execution default of goal org.springframework.boot:spring-boot-maven-plugin:1.5.3.RELEASE:repackage failed: Unable to find main class
```

【解决】

Note：参考官网描述，没有指定<mainClass>或者继承了spring-boot-starter-parent并且<start-class>属性未配置时，会自动寻找签名是public static void main(String[] args)的方法... 所以插件懵逼了，两个妹子和谁在一起呢...
- [推荐] 通用解决方法：<configuration>下配置mainClass，指定程序入口。


```Java
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <version>1.5.3.RELEASE</version>
    <configuration>
        <mainClass>com.xx.webapps.api.main.WebappsApiBidMain</mainClass>
    </configuration>
    <executions>
        <execution>
            <goals>
                <goal>repackage</goal>
            </goals>
        </execution>
    </executions>
</plugin>

```

Spring Boot Maven Plugin提供了几个目标（goal），我们在<executions>标签里配置的<goal>repackage</goal>对应spring-boot:repackage这个目标。

 ![image](http://cnsyear.com/images/blog/TIM截图20180306220443.png)

　　这里的Start-Class就是我们配置的<mainClass>，而Main-Class受layout属性的控制，别被名字搞乱了（是不是很诡异？看看解决方法二就明白为啥如此诡异了）.... 来张图直观的感受下，对应使用上面xml配置打包后的清单文件（MANIFEST.MF）：
　　
　　
- [有限制条件] 解决方法二：如果你的pom继承自spring-boot-starter-parent（注意此前提），也可以直接在<properties>配置<start-class>（其实这里的start-class直接对应清单文件里的Start-Class）：


```Java
<properties>
    <start-class>com.xx.webapps.api.main.WebappsApiBidMain</start-class>
</properties>
```

- 解决方法三：打包的的时候注释掉其他的@SpringBootApplication... 或者你有两处main方法并且都没有使用@SpringBootApplication注解，注释掉一个main方法..... 这就是第三种解决方法233333

----



##### 我的问题通过以下解决 --- <mainClass>com.victor.App</mainClass>

```Java
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <!-- 如果没有该项配置，devtools不会起作用，即应用不会restart -->
        <fork>true</fork>
        <mainClass>com.victor.App</mainClass>
    </configuration>
    <version>1.5.3.RELEASE</version>
</plugin>
```

            
            
原文链接：https://www.cnblogs.com/thinking-better/p/7827368.html

【参考】

- 1.https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#build-tool-plugins-maven-packaging

- 2.https://docs.spring.io/spring-boot/docs/2.0.0.BUILD-SNAPSHOT/maven-plugin//repackage-mojo.html

- 3.https://stackoverflow.com/questions/23217002/how-do-i-tell-spring-boot-which-main-class-to-use-for-the-executable-jar
 

今天很残酷，明天更残酷，后天很美好!