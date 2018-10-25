---
title: Centos安装Git
description: 
categories:
 - Git
 - centos
tags:
 - Git
 - centos
---

> Centos安装Git

### 使用yum安装

- 1、查看系统是否已经安装git
```
[root@localhost ~]# git --version
```

- 2、CentOS6.5 yum 安装git
```
[root@localhost ~]# yum install git
```
- 3、安装成功
```
[root@localhost ~]# git version

git version 1.7.1

[root@localhost ~]# git --version

git version 1.7.1
```
- 4、卸载git
```
[root@localhost ~]# yum remove git
```


 [原文链接](https://www.cnblogs.com/hglibin/p/8627975.html)
 
 
 *标记：兽人为自由而战，牛头人为生存而战，亡灵为不被遗忘而战，血精灵为夺回领地而战。人类为秩序而战，暗夜精灵为守护自然而战，矮人侏儒为盟约而战，德莱尼为圣光而战——各自为战，无尽之战不得蕃。
《魔兽世界》*