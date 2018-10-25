---
layout: post
title: JS实现复制Div(span)的内容到剪切板
subtitle: 
date: 2018-03-16
categories: js
tags: [js]
description: JS实现复制Div(span)的内容到剪切板。
---

#### JS实现复制Div(span)的内容到剪切板


```Javascript
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>JS实现复制Div(span)的内容到剪切板</title>
<script>
/**
 * 执行浏览器的Copy
 */
function execClick(){
    document.execCommand("copy");
}

/**
 * execCopy
 */
function execCopy(event,thisDiv){
    if(isIE()){
        if(window.clipboardData){
            window.clipboardData.setData("Text", thisDiv.textContent);
            alert(window.clipboardData.getData("Text"));
        }
    }else{
        event.preventDefault();
        if (event.clipboardData) {
            event.clipboardData.setData("text/plain", thisDiv.textContent);
            alert(event.clipboardData.getData("text"));
        }
    }
}

/**
 * 判断IE的版本
 */
function isIE(){
    var input = window.document.createElement ("input");
    //"!window.ActiveXObject" is evaluated to true in IE11
    if (window.ActiveXObject === undefined) return null;
    if (!window.XMLHttpRequest) return 6;
    if (!window.document.querySelector) return 7;
    if (!window.document.addEventListener) return 8;
    if (!window.atob) return 9;
    //"!window.document.body.dataset" is faster but the body is null when the DOM is not
    //ready. Anyway, an input tag needs to be created to check if IE is being
    //emulated
    if (!input.dataset) return 10;
    return 11;
}
</script>
</head>
<body>

<p onclick="execClick();" oncopy="execCopy(event,this);">这里是DIV的内容</p>
<span onclick="execClick();" oncopy="execCopy(event,this);">这里是DIV的内容2</span>
<div onclick="execClick();" oncopy="execCopy(event,this);">这里是DIV的内容3</div>
<div onclick="execClick();" oncopy="execCopy(event,this);">这里是DIV的内容4</div>
<div onclick="execClick();" oncopy="execCopy(event,this);">这里是DIV的内容5</div>

</body>
</html>

```

[参考链接](https://www.cnblogs.com/zhangjianqiang/articles/6654362.html)

[参考链接](http://blog.csdn.net/qq1332479771/article/details/78007905)

*标记：如果连死的勇气都有，还有什么能阻挡你的成功？
《不要让未来的你，讨厌现在的自己》*
