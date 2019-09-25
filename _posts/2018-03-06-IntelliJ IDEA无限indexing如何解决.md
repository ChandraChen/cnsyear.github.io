---
layout: post
title: IntelliJ IDEA无限indexing如何解决。
subtitle: 
date: 2018-03-06
categories: IntelliJ IDEA
tags: [IntelliJ IDEA]
description: IntelliJ IDEA无限indexing如何解决。
---

#### IntelliJ IDEA无限indexing如何解决。
今天早上切换了一个项目后idea就一直闪，无限indexing。。。。不明觉厉，这是咋了抽疯了！

- 尝试方法一：未成功

关掉idea，删除这个文件夹内的所有文件，重启，即可。
![image](http://cnsyear.com/images/blog/TIM截图20180306200645.png)

- 尝试方法二：成功
把项目索引删除一下，重新打开建立索引就好了。

![image](http://cnsyear.com/images/blog/TIM截图20180306200932.png)

点击 Invalidate and Restart 即可。

原文链接：
- [https://segmentfault.com/q/1010000012246851](https://segmentfault.com/q/1010000012246851)
- [https://github.com/tengj/IntelliJ-IDEA-Tutorial/blob/newMaster/IntelliJ-IDEA-cache.md](https://github.com/tengj/IntelliJ-IDEA-Tutorial/blob/newMaster/IntelliJ-IDEA-cache.md)