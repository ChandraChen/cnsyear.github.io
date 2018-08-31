---
title: Windows10家庭版 远程报错:由于CredSSP加密Oracle修正
description: 
categories:
 - Windows10
tags:
 - Windows10
---

> Windows10家庭版 远程报错:由于CredSSP加密Oracle修正

远程连接出现问题：

![image](http://cnsyear.com/images/blog/20180710091930528.png)

<!-- more -->


这个错误网上很多改变策略组方式来修正的方法。但是**家庭版没有“策略组”**，网上看到一个不错的微博，自己测试可以用，转过来记录一下。

网上找到方法 但是奈何是 "Win10家庭版" 不能使用这个办法,具体操作可以看最后的引用链接 !!!!

策略路径：“计算机配置”->“管理模板”->“系统”->“凭据分配”

设置名称： 加密 Oracle 修正

只能换另外一种改注册表 改了半天 终于改好 把详细步骤贴出来。

1、打开注册表，快捷输入 “regedit”（类似找命令提示符 输入 cmd 一样）

2、找文件夹 路径：HKLM(缩写)\Software\Microsoft\Windows\CurrentVersion\Policies\System\CredSSP\Parameters

 注意到System 后就没有了自己创建文件夹就好。

3、然后再最底部文件夹里面 新建 DWORD（32）位的。

文件名 “AllowEncryptionOracle” ，值 : 2.

保存 就可以了 。

4、不生效的话重启下试试，我没有重启就可以用了。

![image](http://cnsyear.com/images/blog/20180710092205121.png)

[原文链接>>http://www.cnblogs.com/xxaxx/p/9223231.html](http://www.cnblogs.com/xxaxx/p/9223231.html )
