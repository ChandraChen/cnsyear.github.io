---
title: 遍历HttpServletRequest获取请求参数
description: 
categories:
 - java
tags:
 - java
---

##遍历HttpServletRequest获取请求参数
###以方便我们排查错误

```Java
public List<Map<String, Object>> list(HttpServletRequest request) {
		Enumeration em = request.getParameterNames();
		 while (em.hasMoreElements()) {
		    String name = (String) em.nextElement();
		    String value = request.getParameter(name);
		    System.out.println(name+"\t"+value);
		}
}
```












