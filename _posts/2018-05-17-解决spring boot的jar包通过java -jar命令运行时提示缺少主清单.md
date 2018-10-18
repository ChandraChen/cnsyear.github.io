---
title: 解决spring boot的jar包通过java -jar命令运行时提示缺少主清单
date: 2018-05-17
categories: Springboot
tags: [Springboot] 
---

#### 解决spring boot的jar包通过java -jar命令运行时提示"缺少主清单..."

> 问题

![image](http://blog.cnsyear.com/assets/share/TIM图片20180517180211.jpg?1)

> 解决方法

- pom文件中引入如下配置


```
<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

- 运行 mvn package,查看target下是否存在一个.jar.original后缀的文件,有,就ok了, 因为maven项目的创建一般都是父子项目的结构,我们在打包时,有的子项目没有主函数,会抛出找不到主函数异常,解决方案见[http://blog.csdn.net/qq_33547169/article/details/78259685](http://blog.csdn.net/qq_33547169/article/details/78259685)

*标记：四月最残忍，从死了的土地滋生丁香，混杂着回忆和欲望，让春雨挑动着呆钝的根。
《荒原》*
