---
layout: post
title: java-source 1.5 中不支持 diamond 运算符
subtitle: 
date: 2018-03-19
categories: maven
tags: [maven]
description: java-source 1.5 中不支持 diamond 运算符。
---

#### java: -source 1.5 中不支持 diamond 运算符 (请使用 -source 7 或更高版本以启用 diamond 运算符)

> 背景

今天创建了一个maven工程，使用了jdk1.7以后才有的新特性发现报错。。以为是项目配置的问题找了半天，最后一想我直接在构建的时候指定一想jdk版本不就好了。

```Java

<!--构建-->
<build>
<pluginManagement>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.1</version>
      <configuration>
        <source>1.8</source>
        <target>1.8</target>
      </configuration>
    </plugin>
  </plugins>
</pluginManagement>
</build>


```

*标记：不明白任何情况就劝你一定要大度的人，这种人你要离他远一点，因为雷劈他的时候会连累到你。
——郭德纲*
