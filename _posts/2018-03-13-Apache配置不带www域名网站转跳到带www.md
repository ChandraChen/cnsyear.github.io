---
layout: post
title: Apache配置不带www域名网站转跳
subtitle: 
date: 2018-03-13
categories: apache
tags: [apache]
description: Apache配置不带www域名网站转跳。
---

#### Apache配置不带www域名网站转跳到带www

> Windows服务器 -- 亲测Ok

```Java
#Tomcat_8084
#
<VirtualHost *:80>
ServerName www.cgmtchina.com
ProxyPass / http://www.cgmtchina.com:8084/
ProxyPassReverse / http://www.cgmtchina.com:8084/
ErrorLog "|bin/rotatelogs.exe logs/www.cgmtchina.com-error_%Y_%m_%d.log 86400 480"
</VirtualHost>
# 这里配置非www转向的
<VirtualHost *:80>
ServerName cgmtchina.com
RedirectMatch permanent ^/(.*) http://www.cgmtchina.com/$1 
</VirtualHost>
```


> CentOS下Apache环境 -- 未测试！

一般我们设置两个虚拟主机，一个为带www的域名一个为不带www域名
这里我们一般使用301重定向，服务器端301重定向对用户体验对搜索SEO是有利的，不建议的做法就是echo javascript进行转跳

```Java
<virtualhost *:80>
    ServerName tahenniu.com
    #301永久重定向，302临时重定向
    Redirect 301 / http://www.tahenniu.com/
</virtualhost>

<virtualhost *:80>
    ServerName www.tahenniu.com
    #你的网站配置
</virtualhost>
```

将下面代码片段编辑写入.htaccess文件

```Java
RewriteEngine On
RewriteBase /
RewriteCond %{HTTP_HOST} !^www. 
RewriteRule ^(.*)$ http://www.%{HTTP_HOST}/$1 
```

至此,我们已经完成了不带www的域名网站跳到带www域名的网站项目上.

如果未生效,重启一下web即可.

对于带www的重定向到不带www的例如本站www.tahenniu.com重定向到tahenniu.com你只需将上面配置文件域名部分和.htaccess部分找葫芦画瓢修改下即可

[原文链接](https://tahenniu.com/news/14)

*标记：天命之谓性，率性之谓道。
——孟子 《中庸》*