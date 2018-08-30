---
title: 如何在Windows上安装RabbitMQ
description: 
categories:
 - RabbitMQ
tags:
 - RabbitMQ
---


####  一、windows安装Erlang和RabbitMQ 
##### 先安装Erlang
- Erlang/OTP 20.3下载地址：http://erlang.org/download/otp_win64_20.3.exe
- Erlang/OTP其它版本下载地址：http://www.erlang.org/downloads
- 配置Erlang环境变量并在path后面追加 %ERLANG_HOME%\bin 
- erl -v回车检查是否配置成功
##### 再安装RabbitMQ Server
- RabbitMQ Server 3.7.4下载地址：
https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.4/rabbitmq-server-3.7.4.exe
- RabbitMQ其它版本下载地址：https://www.rabbitmq.com/download.html

 百度云下载链接：https://pan.baidu.com/s/18Zpeg7BpePTFs7rxQPoigw 密码：d62x
 
#### 二、启动RabbitMQ Server

RabbitMQ Server安装之后，会自动注册为windows服务，并以默认配置启动起来

![image](http://cnsyear.com/images/blog/20180709140141198.png)


#### 三、安装RabbitMQ管理页面（如有问题请重启一下电脑再安装！！！）

1.开启Web管理插件
进入rabbitmq安装目录的sbin目录，在此打开CMD命令窗口，执行以下命令

```
rabbitmq-plugins enable rabbitmq_management
```

出现如下提示，说明web管理插件安装成功

![image](http://cnsyear.com/images/blog/20180709140443957.png)

然后重新启动RabbitMQ 服务，打开浏览器并访问：http://localhost:15672/，并使用默认用户guest登录，密码也为guest，即可进入管理界面


#### Rabbit安装问题

#####  Rabbit安装问题一 ：计算机主机名不能有中文

注：erlang有个很坑的地方，你的计算机主机名不能有中文，不是安装会有问题。会有如下报错：

![image](http://cnsyear.com/images/blog/20180717203411418.png)

#####  Rabbit安装问题二 ： 安装完卸载在安装出现的问题 could not set correct interactive mode

```
Installing RabbitMQ service... 
RabbitMQ service is already present - only updating service parameters
C:\rabbitmq\erl9.3\erts-9.3\bin\erlsrv: Warning, could not set correct interactive mode. RabbitMQ
Error: 戮盲卤煤脦脼脨搂隆拢
C:\rabbitmq\erl9.3\erts-9.3\bin\erlsrv: Warning, could not set correct service description (comment) RabbitMQError: 戮盲卤煤脦脼脨搂隆拢
Starting RabbitMQ service...
服务名无效。
请键入 NET HELPMSG 2185 以获得更多的帮助。
Copy failed

```

解决方法：
删除注册表  HKLM/SOFTWARE/Ericsson/Erlang/ErlSrv 下安装的RabbitMQ

![image](http://cnsyear.com/images/blog/20180719204603395.png)

*标记：I don't want to survive. I want to live. 我想要的不仅仅是生存，而是生活。《为奴十二年》*