---
layout: post
title: Centos中wget的安装和使用
subtitle: 
date: 2018-04-01
categories: centos
tags: [centos]
description: Centos中wget的安装和使用。
---

#### Centos中wget的安装和使用
> 简介

CentOS wget是一个从网络上自动下载文件的自由工具。它支持HTTP，HTTPS和FTP协议，可以使用HTTP代理. 所谓的自动下载是指，CentOS wget可以在用户退出系统的之后在后台执行。

![image](http://cnsyear.com/images/blog/TIM截图20180401190718.png)

提示未找到该命令,那么需要执行安装

```Java
yum install wget
```

> 使用技巧

```Java

# CentOS wget -r -np -nd http://example.com/packages/
这条命令可以下载 http://example.com 网站上 packages 目录中的所有文件。其中，-np 的作用是不遍历父目录，-nd 表示不在本机重新创建目录结构。
 
# CentOS wget-r -np -nd --accept=iso http://example.com/centos-5/i386/
与上一条命令相似，但多加了一个 --accept=iso 选项，这指示CentOS wget仅下载 i386 目录中所有扩展名为 iso 的文件。你也可以指定多个扩展名，只需用逗号分隔即可。
 
# CentOS wget -i filename.txt
此命令常用于批量下载的情形，把所有需要下载文件的地址放到 filename.txt 中，然后 CentOS wget 就会自动为你下载所有文件了。
 
# CentOS wget -c http://example.com/really-big-file.iso
这里所指定的 -c 选项的作用为断点续传。
 
# CentOS wget -m -k (-H) http://www.example.com/
该命令可用来镜像一个网站，CentOS wget将对链接进行转换。如果网站中的图像是放在另外的站点，那么可以使用 -H 选项
```

[原文链接](https://www.cnblogs.com/liaojie970/p/5939605.html)