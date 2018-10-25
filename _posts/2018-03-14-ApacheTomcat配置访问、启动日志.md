---
layout: post
title: ApacheTomcat配置访问、启动日志
subtitle: 
date: 2018-03-14
categories: Tomcat
tags: [Tomcat]
description: ApacheTomcat配置访问、启动日志。
---


#### ApacheTomcat配置访问、启动日志


> 访问日志 --该日志默认不开启 修改/conf/server.xml

```Java
<!--这里配置的是localhost域名的访问日志-->
<Host name="localhost"  appBase="webapps"
    unpackWARs="true" autoDeploy="true"
    xmlValidation="false" xmlNamespaceAware="false">

<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"  
       prefix="localhost_access_log." suffix=".txt" pattern="common" resolveHosts="false"/>

</Host>

```

>  启动日志 ---该日志默认开启 conf/logging.properties 

问题：启动start.bat发现log文件夹中没有生成相应的日志
- 排查最后找出问题所在，问题是在tomcat下的bin目录下的catalina.bat文件内容被修改到了，影响了日志的输出，看了里面的内容发现之前修改内存大小时动到了catalina.bat，在catalina.bat文件里的

```Java
## 设置了内存大小
set JAVA_OPTS=-server -Xms1024m -Xmx1024m -XX:PermSize=256M -XX:MaxNewSize=512m -XX:MaxPermSize=256m -Djava.awt.headless=true
```
把上面设置内存大小后，导致没有日志输出。
应该如下设置：

```Java
set JAVA_OPTS=%JAVA_OPTS% -server -Xms1024m -Xmx1024m -XX:PermSize=256M -XX:MaxNewSize=512m -XX:MaxPermSize=256m -Djava.awt.headless=true
```
> 总结： %JAVA_OPTS%得把这个加上，否则找不到路径

*标记：当欲望失去了枷锁，就没有了向前的路，只能转左，或者向右。左边是地狱，右边也是地狱。
——烟雨江南 《狩魔手记》*