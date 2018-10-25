---
layout: post
title: Centos安装问题——问题解压jdk报错gzipstdinnot in gzip format
categories: [centos,liunx]
tags: [centos,liunx]
description: 
---

#### Centos安装问题——问题:解压jdk报错gzipstdinnot in gzip format

这个问题是我在配置服务器的java环境时遇到的。

通过命令: wget http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jdk-8u144-linux-x64.tar.gz从oracle官网下载jdk。3

然后执行解压命令：tar -zxvfjdk-8u144-linux-x64.tar.gz，却报错：

```
gzip: stdin: not in gzip format 
tar: Child returned status 1 
tar: Error is not recoverable: exiting now

```

通过file 命令查看，发现jdk-8u144-linux-x64.tar.gz:HTML document text...

解决方法：本地下载好传输上服务器，在解压就没问题了。

Oracle官网下载JDK：[传送门](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

*标记：如果在平安夜或者圣诞节没有收到我的任何表示，请不要怀疑我们的友谊，我只是穷了而已*