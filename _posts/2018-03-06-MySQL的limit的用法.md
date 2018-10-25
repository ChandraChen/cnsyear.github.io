---
layout: post
title: MySQL的LIMIT的用法
subtitle: 
date: 2018-03-06
categories: blog
tags: [mysql]
description: MySQL的LIMIT的用法。
---

#### MySQL的limit的用法

LIMIT是MySQL内置函数，其作用是用于限制查询结果的条数。

- 1)其语法格式如下:

LIMIT[位置偏移量,]行数

其中，中括号里面的参数是可选参数，位置偏移量是指MySQL查询分析器要从哪一行开始显示，索引值从0开始，即第一条记录位置偏移量是0，第二条记录的位置偏移量是1,依此类推...，第二个参数为“行数”即指示返回的记录条数。

位置偏移量可以理解为跳过前xx条记录(元组).

- 2)基本用法

```Java
/*当没有指定位置偏移量时，只取4条时，可以这样写*/
SELECT * FROM YourTableName LIMIT 4;
 
/*当指定了位置偏移量时，从第3条起取4条时，可以这样写*/
/*因为索引是从0开始计数的，所以第3条对应的索引就是2*/
SELECT * FROM YourTableName LIMIT 2,4;

```

- 3)应用场合:分页


```Java

SELECT * FROM YourTableName LIMIT startRow,pageSize;


 // 后台计算出页码、页数(页大小)
 int curPage = 2;
 int pageSize = 10;
 int startRow = (curPage - 1) * pageSize;

```

原文链接：https://zhidao.baidu.com/question/266421833.html