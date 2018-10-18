---
layout: post
title: mysqldump定时备份不用输入密码自动导出sql文件
date: 2018-02-05
categories: [mysql,mysqldump]
tags: [mysql,mysqldump]
description: mysqldump定时备份不用输入密码自动导出sql文件。
---

 天津师范大学系统部署到服务器后，需要每天备份数据以防止系统异常导致数据的丢失。。。服务器是windowserver的，我们直接使用系统的计划任务执行备份脚本就可以。。。。
 
### 第一步：
首先一点，你现在一个固定的地方，新建一个bat文件，用于系统的任务计划进程去执行bat中定义的相关操作！
因为是备份mysql数据库，所以我将bat文件新建在mysql的安装目录的bin目录下：
新建back_db.bat文件

![image](https://note.youdao.com/yws/api/personal/file/3F21478E38E64CD5B91AE7F112A113B4?method=download&shareKey=cd96d77ce55dea1deadf66c935e65f33)


### 第二步：
将一下的dos命令 粘贴在back_db.bat文件中
```Java
@echo off
set "Ymd=%date:~,4%%date:~5,2%%date:~8,2%"
"C:\Program Files\MySQL\MySQL Server 5.5\bin\mysqldump" -u root --password=root performance> D:\db_backup\performance_%Ymd%.sql
@echo on
```

分析：

　　1>首先  【set "Ymd=%date:~,4%%date:~5,2%%date:~8,2%"】是定义一个日期变量，用于下面拼接备份文件的名字，区别是哪一天的备份。

　　2>【"C:\Program Files\MySQL\MySQL Server 5.5\bin\mysqldump"】这里加引号是因为 bat文件中的变量如果出现空格的话，会提示无效的参数数量

　　3>mysqldump的标准格式应该是【mysqldump -u 用户名 -p 数据库名 > 导出的文件名】，在这里应该是

　　　【"C:\Program Files\MySQL\MySQL Server 5.5\bin\mysqldump" -u root -p performance> D:\db_backup\performance_%Ymd%.sql】，而这样的话，执行了此bat文件的话，dos窗口弹出后还需要手动键入数据库的连接密码，并不能实现自动的备份功能。所以，这里进行了一定的更改，更改后代码如下：【"C:\Program Files\MySQL\MySQL Server 5.5\bin\mysqldump" -u root --password=root performance> D:\db_backup\performance_%Ymd%.sql】

　　4>【D:\db_backup\performance_%Ymd%.sql】就是备份文件存储的位置，这个文件夹可以先创建好，也可以不用创建！

![image](https://note.youdao.com/yws/api/personal/file/AB20A36244924B01B028AB1A8F6C6112?method=download&shareKey=46d6ee7d11817279d1d511c1a1b476f5)

### 第三步：
找到系统的任务计划程序，打开

![image](https://note.youdao.com/yws/api/personal/file/94B8282CB73A437FBF0505F9E6DAA6A5?method=download&shareKey=a8f65209c1a1058d4d068f4df412cf8c)

![image](https://note.youdao.com/yws/api/personal/file/5533DCF69E1B463181D3CCEE76E3352A?method=download&shareKey=fa941f0fb26393ce9cbfd4ffc0901a81)


![image](https://note.youdao.com/yws/api/personal/file/5A041D10F251459CB244FE2864609DA8?method=download&shareKey=ba5cc06a1ba2a65ffd7aa8882e915911)
这是用来演示，故此设为每天都备份

![image](https://note.youdao.com/yws/api/personal/file/34D26B06A6BB41BB957AC0CEAE946A70?method=download&shareKey=646e7e989e96802c3eced817d0417648)

因为希望执行备份任务，所以，这里选择启动程序

![image](https://note.youdao.com/yws/api/personal/file/33C1C89084E044E7A0E7743AD1AAA2C4?method=download&shareKey=ed4687236b89478c32e3f9f7432a87ae)

选择需要执行的程序的脚本文件

![image](https://note.youdao.com/yws/api/personal/file/7EFA462CEC7B48518A723649446F4E98?method=download&shareKey=42ed6040a0948b6758bcbf48f035a48b)

![image](https://note.youdao.com/yws/api/personal/file/486DE575DEB14002929DB76B1C578C0A?method=download&shareKey=5d7381e665c2a468ea0f71b6d21391dd)

![image](https://note.youdao.com/yws/api/personal/file/1DA171A393D64A76B78D7B1560AB2B54?method=download&shareKey=e22d8c6edb3c1f82797b7b5035f0ff75)

此刻完成后，找到此任务，发现状态为 准备就绪

![image](https://note.youdao.com/yws/api/personal/file/2136C5A4A394477598D10FB4A88D5D07?method=download&shareKey=e15f45b04ba7962d96d22724fb9b6f9f)


到了触发的时间后，去指定的路径下，也就是bat文件中配置的路径【D:\db_backup\performance_%Ymd%.sql】下找到这个备份文件！


![image](https://note.youdao.com/yws/api/personal/file/53FFE7312A7041AC9F89D0948140C1B3?method=download&shareKey=80bc729d6abc66e484142e9ab26ca433)

 并且数据库的存储的数据，DDL  DML语句等都备份了下来
 
![image](https://note.youdao.com/yws/api/personal/file/EBC49DD16BA343AF996250715A8BB0A5?method=download&shareKey=528729b67b64502d85e684cc7400c65b)

参考文章:
https://www.cnblogs.com/sxdcgaq8080/p/6640420.html