---
title: 常用Apache的httpd.conf配置
description: 
categories:
 - Apache
tags:
 - Apache
---

> 备份：常用Apache的httpd.conf配置

- 静态目录
- 请求转发
- www跳转
- ....

<!-- more -->

```
#指向一个静态目录 该目录下有index.html
<VirtualHost *:80>
	ServerName dsshow.xxx.com
    DocumentRoot "D:\projects\cms_pc_close"   
</VirtualHost>

#转发配置
<VirtualHost *:80>
	ServerName trends.xxx.com
	ProxyPass /wechat/sign http://hset-wechat-share.xxx.com:8093/wechat/sign
	ProxyPassReverse /wechat/sign http://hset-wechat-share.xxx.com:8093/wechat/sign

	ProxyPass / http://localhost:8080/
	ProxyPassReverse / http://localhost:8080/
	ErrorLog "|bin/rotatelogs.exe logs/trends.xxx.com-error_%Y_%m_%d.log 86400 480"
	CustomLog "|bin/rotatelogs.exe logs/trends.xxx.com-access_%Y_%m_%d.log 86400 480" common
</VirtualHost>

#配置不带www域名网站转跳到带www
<VirtualHost *:80>
	ServerName www.cgmtxxx.com
	ProxyPass / http://www.cgmtxxx.com:8084/
	ProxyPassReverse / http://www.cgmtxxx.com:8084/
	ErrorLog "|bin/rotatelogs.exe logs/www.cgmtxxx.com-error_%Y_%m_%d.log 86400 480"
</VirtualHost>
#这里配置非www转向的
<VirtualHost *:80>
	ServerName cgmtxxx.com
	RedirectMatch permanent ^/(.*) http://www.cgmtxxx.com/$1 
</VirtualHost>

```

*标记：猛兽总是独行，牛羊才成群结队。——鲁迅《鲁迅杂文精选》*