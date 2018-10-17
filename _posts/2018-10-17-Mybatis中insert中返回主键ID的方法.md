---
title: Mybatis中insert中返回主键ID的方法
description: 
categories:
 - Mybatis
tags:
 - Mybatis
---

> Mybatis中insert中返回主键ID的方法


```
/**
 * 这里插入后需返回id
 */
int insert(EmployeeBusiness record);
	
	
<insert id="insert" parameterType="org.sang.bean.EmployeeBusiness" useGeneratedKeys="true" keyProperty="id">
insert into employeebusiness (id, empId, createDate, 
  updateDate, imgs, note
  )
values (#{id,jdbcType=INTEGER}, #{empId,jdbcType=INTEGER}, #{createDate,jdbcType=TIMESTAMP}, 
  #{updateDate,jdbcType=TIMESTAMP}, #{imgs,jdbcType=VARCHAR}, #{note,jdbcType=LONGVARCHAR}
  )
</insert>

```

*标记：岁月太过温柔，所以总能轻易相信和原谅一个人。 ——随侯珠 《别那么骄傲》*