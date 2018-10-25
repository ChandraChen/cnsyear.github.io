---
title: git clone 报错：Peer reports incompatible or unsupported protocol version解决办法
description: 
categories:
 - Git
tags:
 - Git
---

> git clone 报错：Peer reports incompatible or unsupported protocol version解决办法

#### 问题：git通过git clone下载github上的资源到机器上，结果出现如题所示的错误。

```
[root@server data]# git clone https://github.com/pingcap/tidb-docker-compose.git
Cloning into 'tidb-docker-compose'...
fatal: unable to access 'https://github.com/pingcap/tidb-docker-compose.git/': Peer reports incompatible or unsupported protocol version.
[root@server data]# 
[root@server data]# git --version
git version 1.8.3.1

```

#### 解决方法：原因是curl,nss版本低的原因，解决办法就是更新nss,curl。

```
[root@server data]# yum update nss curl

```
*标记：我的思念犹如大海里的鱼,在万水千山之内都是皈依。——安意如 《当时只道是寻常》*