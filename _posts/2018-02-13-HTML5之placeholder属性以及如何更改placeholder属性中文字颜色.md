---
layout: post
title: HTML5之placeholder属性以及如何更改placeholder属性中文字颜色
date: 2018-02-13
categories: html
tags: [html]
description: HTML5之placeholder属性以及如何更改placeholder属性中文字颜色。
---

##### placeholder这个属性是HTML5中新增的属性，该属性的作用是规定可描述输入字段预期值的简短的提示信息，该提示会在用户输入之前显示在输入字段中，会在用户输入字段后消失，有些浏览器则是获得焦点后该提示便消失（如Safari、IE）

- 适用范围：placeholder 属性适用于下面的 input 类型：text、search、url、tel、email 和 password。

- 因为是HTML5中新增的属性，所以会存在兼容性问题。下面说说浏览器的支持情况：
IE10+、Firefox、Opera、Chrome 和 Safari 均支持 placeholder 属性。IE9及以下版本不支持input的placeholder属性。

- placeholder的用法，举例：


```Html
　　 <input type="text" placeholder="请输入您要搜索的内容！"> 
```

该提示文字会有自己默认的颜色，然而有时候，我们并不希望用该默认颜色，而是想自定义颜色。那么该怎么处理呢?不废话，上代码。　


```Html
<style>
        input::-webkit-input-placeholder{
            color:red;
        }
        input::-moz-placeholder{   /* Mozilla Firefox 19+ */
            color:red;
        }
        input:-moz-placeholder{    /* Mozilla Firefox 4 to 18 */
            color:red;
        }
        input:-ms-input-placeholder{  /* Internet Explorer 10-11 */ 
            color:red;
        }
    </style>
```
针对不同浏览器或不同版本的浏览器会有不同的写法，会添加相应的前缀。

　　注意：

　　1、WebKit, Blink, Edge浏览器等需要带上-webkit-前缀，且是双冒号，写的时候还要带上input

　　2、针对火狐浏览器则有两种写法，一种是针对低版本的，一种是针对高版本的，二者都需要带上-moz-前缀。要点1：火狐低版本的使用冒号（：），而高版本的使用双冒号（：：）；要点2：火狐浏览器不需要像webkit内核那样要带上input。

　　3、由于placeholder属性只在IE10+才支持，因此，针对IE10、IE11的写法是加上-ms-前缀，使用的是冒号（：），需要带上input

　　

　　特别强调：冒号与双冒号的问题，还有是否需要加上input


[原文链接](https://www.cnblogs.com/jf-67/p/7241252.html?utm_source=tuicool&utm_medium=referral)







