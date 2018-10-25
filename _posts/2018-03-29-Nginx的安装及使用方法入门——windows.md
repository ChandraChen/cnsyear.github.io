---
layout: post
title: Nginx的安装及使用方法入门——windows
subtitle: 
date: 2018-03-29
categories: Nginx
tags: [Nginx]
description: Nginx的安装及使用方法入门——windows。
---
#### Nginx的安装及使用方法入门——windows
> 简介

Nginx (engine x) 是一个高性能的HTTP和反向代理服务器，也是一个IMAP/POP3/SMTP服务器。

> 一. 下载

- 下载nginx [>>> 传送门](http://nginx.org/)

![image](http://cnsyear.com/images/blog/TIM截图20180331202912.png)

> 二. 修改配置文件

nginx配置文件在 conf\nginx.conf

```Java
http {
     gzip  on;

    #静态文件
    server {
        listen       80;
        server_name  static.cnblog.com;

        location / {
            root   G:/source/static_cnblog_com;
        }
    }

    #html文件
    server {
        listen       80;
        server_name  127.0.0.1 localhost;

        location / {
            root   G:/source/html/mobile/dist;
            index  index.html index.htm;
        }
    }
}
```

如上可以配置多个server，这样访问localhost即访问到了  G:/source/html/mobile/dist  目录， 还可以开启gzip，压缩html

> 三. 启动

***注意不要直接双击nginx.exe，这样会导致修改配置后重启、停止nginx无效，需要手动关闭任务管理器内的所有nginx进程***
 
在nginx.exe目录，打开命令行工具，用命令 启动/关闭/重启nginx 
 
```Java
start nginx : 启动nginx
nginx -s reload  ：修改配置后重新加载生效
nginx -s reopen  ：重新打开日志文件
nginx -t -c /path/to/nginx.conf 测试nginx配置文件是否正确

关闭nginx：
nginx -s stop  :快速停止nginx
nginx -s quit  ：完整有序的停止nginx
```

如果遇到报错：

```Java
bash: nginx: command not found
```

有可能是你再linux命令行环境下运行了windows命令，
如果你之前是允许 nginx -s reload报错， 试下 ./nginx -s reload
或者用windows系统自带命令行工具运行

> 四.测试是否启动成功

访问http://localhost

![image](http://cnsyear.com/images/blog/TIM截图20180331203623.png)

[原文链接](https://www.cnblogs.com/saysmy/p/6609796.html)

*标记：杏花，春雨，江南。六个方块字，或许那片土就在那里面。
——余光中 《听听那冷雨》*