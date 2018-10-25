---
layout: post
title: MYSQL的binary解决mysql数据大小写敏感问题的方法
subtitle: 
date: 2018-02-22
categories: mysql
tags: [mysql]
description: MYSQL的binary解决mysql数据大小写敏感问题的方法。
---

MySQL不区分大小写，用户登录时查询密码的时候必须区分大小！


```Java
SELECT * FROM User WHERE username='zhangsan' AND password= binary '1Qaz23DDa';
```


如果想在查询时区分字段值的大小写，则：字段值需要设置BINARY属性，设置的方法有多种： 


```Java
A、创建时设置： 
    CREATE TABLE T( 
    name VARCHAR(10) BINARY 
    ); 

B、使用alter修改： 
ALTER TABLE `tablename` MODIFY COLUMN `cloname` VARCHAR(45) BINARY; 

C、mysql table editor中直接勾选BINARY项。

```



