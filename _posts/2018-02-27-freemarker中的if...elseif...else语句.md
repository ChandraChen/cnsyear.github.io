---
layout: post
title: freemarker中的if...elseif...else语句
subtitle: 
date: 2018-02-27
categories: freemarker
tags: [freemarker]
description: freemarker中的if...elseif...else语句。
---


### freemarker中的if...elseif...else语句



1、设计示例



```Java
<#if student.studentAge lt 12>  
    ${student.studentName}不是一个初中生  
<#elseif student.studentAge lt 15>  
    ${student.studentName}不是一个高中生  
<#elseif student.studentAge lt 18>  
    ${student.studentName}不是一个大学生  
<#else>  
    ${student.studentName}是一个大学生  
</#if>  

```



2、运行结果
student.studentAge为20,student.studentName为张三丰


```Java
张三丰是一个大学生  

```

[原文转载地址：http://blog.csdn.net/you23hai45/article/details/27239369](http://blog.csdn.net/you23hai45/article/details/27239369)

