---
layout: post
title: JSONP解决跨域请求(示例java版)
date: 2017-11-29
categories: jsonp
tags: [jsonp]
description: JSONP解决跨域请求(示例java版)。
---


### JSONP解决跨域请求----示例java版

##### JS
```JavaScript
  $(function(){
	    var url="http://localhost:8080/find.do?jsoncallback=success_jsonpCallback";
	    $.ajax({
	       type : "get",
	       async : false,
	       dataType : 'jsonp',
	       url : url,
	       data :{
	       	"name":"test"
	       },
	       jsonp : "callbackparam",
	       jsonpCallback : "success_jsonpCallback",
	       success: function(data){
	    	   alert(data);
	           console.log(data);
	       }
	     });
  });
```

##### JAVA

```Java
  /**
	 * 
	 * @Description :查询
	 * @author : jie.zhao
	 * @Date: 2017年8月2日
	 */
	@RequestMapping(value="find.do", method={RequestMethod.GET, RequestMethod.POST})
	public void findAction(HttpServletRequest request,HttpServletResponse response) throws Exception{
		Map<String , Object> map=new HashMap<String , Object>();
		map.put("result", 0);
		try {
			webService.find(request);
			map.put("result", 1);
		} catch (Exception e) {
			e.printStackTrace();
			map.put("result", 0);
		}
		StringBuffer sb  = new StringBuffer(request.getParameter("jsoncallback"));
		sb.append("(");
		sb.append(JsonDecoder.toJSON(map));
		sb.append(")");
		response.getWriter().print(sb.toString());
	}
```


----------












