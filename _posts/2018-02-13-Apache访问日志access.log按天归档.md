---
layout: post
title: Apache访问日志access.log按天归档
date: 2018-02-13
categories: apache
tags: [apache]
description: Apache访问日志access.log按天归档。
---


#### 问题：
Apache访问日志access.log文件记录数会一直递增，文件大小一直变大；当达到一定大小后，会导致效率问题；

#### 解决方案：
Apache访问日志access.log按天归档，每天自动生成一个新的access.log日志，避免单个文件过大导致效率问题；


#### 具体步骤如下：
OS:Windows Server 2008
- 1.更改Apache配置文件G:\IBM\HTTPServer\conf\http.conf：
将httpd.conf文件中

```Java
CustomLog logs/access.log common 前面加上#号(注释)
#CustomLog logs/access.log common
```
- 2.增加语句如下：

```Java
CustomLog "|G:\IBM\HTTPServer\bin\rotatelogs.exe logs\access_%Y_%m_%d.log 86400 480" common
```

- 3.重启Apache

```Java
G:\IBM\HTTPServer\bin\Apache.exe -k stop
G:\IBM\HTTPServer\bin\Apache.exe -k start
```


如果Apache启动失败，查看error.log日志，可以将语句中rotatelogs.exe或access.log文件路径更改成绝对路径或相对路径。

本篇文章来源于 Linux公社网站(www.linuxidc.com)  原文链接：https://www.linuxidc.com/Linux/2017-01/139238.htm

