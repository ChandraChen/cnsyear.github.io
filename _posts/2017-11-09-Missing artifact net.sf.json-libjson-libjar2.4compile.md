---
layout: post
title: Missing artifact net.sf.json-lib:json-lib:jar:2.4:compile
date: 2017-11-09
categories: maven
tags: [maven]
description:  Missing artifact net.sf.json-lib:json-lib:jar:2.4:compile。
---

### 今天在做一个maven项目时pom文件报红叉纠结了半天！！

#### pom文件引用json这个包，报错误：Missing artifact net.sf.json-lib:json-lib:jar:2.4:compile
```Java
<dependency>
		<groupId>net.sf.json-lib</groupId>
		<artifactId>json-lib</artifactId>
		<version>2.4</version>
	</dependency>
```
#### 去我本地的maven仓库看了一下，有几个lock的文件jar包没有下载下来。我就上网上手动下了一个，放到了里面。解决了错误，但是总是这么弄太low了。


#### 找了下度娘说json-lib是需要区分jdk版本的，pom.xml中的配置应加上标签classifier指定jdk版本，如用jdk15。

#### pom文件修改为：

```Java
<dependency>
		<groupId>net.sf.json-lib</groupId>
		<artifactId>json-lib</artifactId>
		<version>2.4</version>
		<classifier>jdk15</classifier><!--指定jdk版本-->
</dependency>
```
#### OK!!! 这样也可以解决问题
##### 最后代码上提交到审核部时没通过。最后放弃了这个jar包，换成了阿里的JSON。