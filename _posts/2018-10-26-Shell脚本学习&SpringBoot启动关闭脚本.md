---
title: Shell脚本学习&SpringBoot启动关闭脚本
description: 
categories:
 - liunx
tags:
 - liunx
---

#### Shell脚本学习&SpringBoot启动关闭脚本

> Shell脚本学习手册 


[传送门](http://www.runoob.com/linux/linux-shell.html)

> SpringBoot Shell启动关闭脚本

```
springboot 启动脚本

#!/bin/sh
ps -ef |grep sell-0.0.1-SNAPSHOT.jar |grep -v grep
if [ $? -eq 0 ];then
  echo 'Server is running!!'
else
  echo 'Server starging...'
  nohup java -jar sell-0.0.1-SNAPSHOT.jar >/dev/null 2>&1 &
fi

springboot 停止脚本

#!/bin/sh
ps -ef | grep hrserver-1.0.0.jar| grep -v grep
if [ $? -eq 0 ];then
  PID_9050=$(ech
  o `netstat -apn |grep 9050 | awk '{print $NF}'|awk -F '/' '{print $1}'`)
  kill $PID_9050
  echo 'HRServer has shutdown!'
else
  echo 'Not Found HRServer!!!'
fi


```


*标记：听闻爱情，十人九悲，何不两清，做回甲乙丙。听闻回忆，十忆九伤,何不忘掉曾经，珍惜现在。听闻青春，十言九妄 ，何不放下，随风东南西北。听闻清楚,十有九错 ，何不疏狂,喜时饮酒逐月。听闻红坐,十有九故,何不淡泊。*