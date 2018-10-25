---
layout: post
title: jQueryUI拖动（Draggable）
subtitle: 
date: 2018-04-21
categories: jquery
tags: [jquery]
description: jQueryUI拖动（Draggable）。
---

#### jQueryUI拖动（Draggable）
> 需求

实现可拖动不同的元素的位置实现位置的排序。

![image](http://cnsyear.com/images/blog/TIM截图20180421142604.png?233)

---

```Html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>jQuery UI 拖动（Draggable）</title>
  <script src="jquery.min.js"></script>
  <script src="jquery-ui-1.10.4.min.js"></script>
  <style>
  ul { list-style-type: none; margin: 0; padding: 0; margin-bottom: 10px; }
  li { margin: 5px; padding: 5px; width: 150px; border: 1px solid red;<!-- float:left;--> }
  </style>
  <script>
  $(function() {
    $( "#sortable" ).sortable({
      revert: true
    });
    $( "ul, li" ).disableSelection();
  });
  //获取排序的位置
  function getIndex(){
	$("#sortable li").each(function(index,elem){
		var id = $(elem).data("id");//Id==>可以是数据库的id
		 console.log(id+"======index:"+index );
	});
  }
  </script>
</head>
<body>
<ul id="sortable" >
  <li class="ui-state-default" data-id="1">Item 1</li>
  <li class="ui-state-default" data-id="2">Item 2</li>
  <li class="ui-state-default" data-id="3">Item 3</li>
  <li class="ui-state-default" data-id="4">Item 4</li>
  <li class="ui-state-default" data-id="5">Item 5</li>
  <li class="ui-state-default" data-id="6">Item 6</li>
  <li class="ui-state-default" data-id="7">Item 7</li>
  <li class="ui-state-default" data-id="8">Item 8</li>
  <li class="ui-state-default" data-id="9">Item 9</li>
  <li class="ui-state-default" data-id="10">Item 10</li>
</ul>
 <button onclick="getIndex()">获取位置</button>
</body>
</html>
```

要想横着排列，float:left即可。

[源码地址](https://github.com/cnsyear/tools/tree/master/jQuery%20UI%20%E6%8B%96%E5%8A%A8%EF%BC%88Draggable%EF%BC%89)
[参考链接](http://www.runoob.com/try/try.php?filename=jqueryui-example-draggable-sortable)

*标记：我的意思是说呀，你关心错地方了，是别的地方，你以为没有问题的地方，反而出了大问题了，而且就在你眼前。
——贺涵 《我的前半生》*