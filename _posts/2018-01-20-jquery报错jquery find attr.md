---
layout: post
title: jquery报错jquery find attr 
subtitle: 
date: 2018-01-20
categories: js
tags: [js]
description: jquery报错jquery find attr 。
---

![image](https://note.youdao.com/yws/api/personal/file/C25CC843477A432297CA602E6181CC96?method=download&shareKey=db63e330f2f3daca84f40b5f0fadea36)

```Javascript
($('#form1').find("span"))这是一个对象的集合，可以用jQuery的val方法
($('#form1').find("span"))[0]这是对象集合中的第一个对象，只能用js的value属性，而不是jQuery的val方法

所以可以这样用：$(($('#form1').find("span"))[0]).text()
将转换成jquery对象：$(($('#form1').find("span"))[0])
也可以$('#form1').find("span").get(0)
$('#form1').find("span").eq(0)
```

原文链接：http://blog.sina.com.cn/s/blog_7768d2210102v00r.html
