---
layout: post
title: java中replaceAll方法替换字符串中的反斜杠
subtitle: 
date: 2018-03-09
categories: java
tags: [java]
description: java中replaceAll方法替换字符串中的反斜杠。
---

#### java中replaceAll方法替换字符串中的反斜杠
```Java

/**
 * 如果把\替换成别的字符
 */
String s="C:\\盘";
s=s.replaceAll("\\","/");

System.out.println(s);


/**
 * 报错

Exception in thread "main" java.util.regex.PatternSyntaxException: Unexpected internal error near index 1
\
 ^
	at java.util.regex.Pattern.error(Pattern.java:1955)
	at java.util.regex.Pattern.compile(Pattern.java:1702)
	at java.util.regex.Pattern.<init>(Pattern.java:1351)
	at java.util.regex.Pattern.compile(Pattern.java:1028)
	at java.lang.String.replaceAll(String.java:2223)
	at demo.test.main(test.java:10)
 */


错误的原因：
在regex中"\\"表示一个"\"，在java中一个"\"也要用"\\"表示。
这样，前一个"\\"代表regex中的"\"，后一个"\\"代表java中的"\"。
所以要想使用replaceAll方法将字符串中的反斜杠("\")替换成空字符串("")，则需要这样写：str.replaceAll("\\\\","");


String s="C:\\盘";
s = s.replaceAll("\\\\","/");

System.out.println(s);

```


*标记：人的一生，都有一些说不出的秘密，挽不回的遗憾，触不到的梦想，忘不了的爱。*




[原文链接](http://blog.csdn.net/lcczzu/article/details/46862405)
 