---
layout: post
title: Apache配置中的ProxyPass和ProxyPassReverse
subtitle: 
date: 2018-03-30
categories: apache
tags: [apache]
description: Apache配置中的ProxyPass和ProxyPassReverse。
---


#### Apache配置中的ProxyPass和ProxyPassReverse

> Apache代理（ProxyPass）转发

apache中的mod_proxy模块用于url的转发，即具有代理的功能。应用此功能，可以很方便的实现同tomcat等应用服务器的整合，甚者可以很方便的实现web集群的功能。 

> 例子：客户端请求http://app.highset.com/save.do 后台实际保存的接口是http://b.com/save.do

```Java

#Tomcat_8084
#
<VirtualHost *:80>
ServerName app.highset.com
#代理请求
ProxyPass /save.do http://b.com/save.do
ProxyPassReverse /save.do http://b.com/save.do

ProxyPass / http://app.highset.com:8084/
ProxyPassReverse / http://app.highset.com:8084/
ErrorLog "|bin/rotatelogs.exe logs/app.highset.com-error_%Y_%m_%d.log 86400 480"
</VirtualHost>

```
> 注意——ProxyPassReverse 的配置总是和ProxyPass 一致

ProxyPassReverse 的配置总是和ProxyPass 一致，它的作用在于反向代理，如果响应中有302重定向，ProxyPassReverse就派上用场。


[参考地址](https://www.cnblogs.com/milton/p/4215125.html)

*标记：贪婪和爱情，可能只是同一个欲望的两种说法罢了。
——Nietzsche*