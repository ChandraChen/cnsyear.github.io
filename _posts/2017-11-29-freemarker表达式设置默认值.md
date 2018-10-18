---
layout: post
title: freemarker表达式设置默认值
date: 2017-11-29
categories: freemarker
tags: [freemarker]
description: freemarker表达式设置默认值。
---

### freemarker表达式设置默认值
#### 有时候我想当一个value没有值时，就显示一个默认的值。

```Java
例子：

Hello,${user!}
Hello,${user!'我是默认值----zz'}

当user没有值时，显示
Hello,
Hello,我是默认值----zz
```











