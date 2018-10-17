---
title: SQL一条insert语句批量插入多条记录
description: 
categories:
 - Mybatis
tags:
 - Mybatis
---

> SQL一条insert语句批量插入多条记录

常见的insert语句，向数据库中，一条语句只能插入一条数据：

```
insert into persons (id_p, lastname , firstName, city ) values(204,'haha' , 'deng' , 'shenzhen');
```

怎样一次insert插入多条记录呢？使用示例：

```
insert into persons (id_p, lastname , firstName, city )

values

(200,'haha' , 'deng' , 'shenzhen'),

(201,'haha2' , 'deng' , 'GD'),

(202,'haha3' , 'deng' , 'Beijing');
```

这样就批量插入数据了， 遵循这样的语法，就可以批量插入数据了。

*标记：To improve is change; to be perfect is to change often. 提高就是要改变,而要达到完美就要不断改变。 温斯顿·丘吉尔 *