---
layout: post
title: svn cleanup failed to process the following paths
subtitle: 
date: 2018-03-15
categories: svn
tags: [svn]
description: svn cleanup failed to process the following paths。
---

#### SVN检出报错

![image](http://cnsyear.com/images/blog/TIM截图20180315133643.jpg)

#### 解决方法

> 下载sqlite3.exe，并将其放到.svn文件夹中

> 直接将.svn文件夹中的wc.db拖到sqlite3.exe

这个时候我们就会看到一个命令行工具了，首先我们可以通过.table命令查看到底有什么表在这个数据库文件中。

之后就是最关键的步骤了！
执行
 
```Java
delete from wc_lock;

delete from work_queue;

```

这两句话，将表中的内容清空，这样就可以愉快的update,commit啦，O(∩_∩)O哈哈~


*标记：人类花费了几千年才从神话的朦胧走向理性的澄明
——史蒂芬·霍金*