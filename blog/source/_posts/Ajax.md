---
title: Ajax
tags:
  - JavaScript
categories:
  - 前端
date: 2017-02-13 22:35:17
---
#### 一、Ajax 的定义
AJAX全称为“Asynchronous JavaScript and XML”（异步JavaScript和XML），是一种创建交互式网页应用的网页开发技术。数据通常以JSON的格式来进行传送，是一种创建快速动态网页的技术。它使用：
1. 使用XHTML+CSS来标准化呈现；
2. 使用XML和XSLT进行数据交换及相关操作；
3. 使用XMLHttpRequest对象与Web服务器进行异步数据通信； 
4. 使用Javascript操作Document Object Model进行动态显示及交互； 
5. 使用JavaScript绑定和处理所有数据。 

#### 二、Ajax 的实现原理及创建过程
1. 首先，由客户端事件触发Ajax事件；
2. 创建XMLHttpRequest对象,也就是创建一个异步调用对象；
3. 创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息；
4. 设置响应HTTP请求状态变化的函数；
5. 发送HTTP请求；
6. 获取异步调用返回的数据；
7. 使用JavaScript和DOM实现局部刷新。
```
var xhr =null;//创建对象 
if(window.XMLHttpRequest){
  xhr = new XMLHttpRequest();
}else{
  xhr = new ActiveXObject("Microsoft.XMLHTTP");
}
xhr.open(“方式”,”地址”,”标志位”);//初始化请求 
xhr.setRequestHeader(“”,””);//设置http头信息 
xhr.onreadystatechange =function(){}//指定回调函数 
xhr.send();//发送请求 
```

#### 三、Ajax 的优点和缺点？
1. 优点：
- 最大的一点是页面无刷新，用户的体验非常好。
- 使用异步方式与服务器通信，具有更加迅速的响应能力。
- 前端和后端负载平衡。
- 基于标准化的并被广泛支持的技术，不需要下载插件或者小程序。
- 界面与应用分离。

2. 缺点：
- ajax不支持浏览器back按钮。
- 安全问题 AJAX暴露了与服务器交互的细节。
- 对搜索引擎的支持比较弱。
- 破坏了程序的异常机制。
- 不容易调试。

#### 四、下面是封装的一个 Ajax 函数：
```
function ajax(objs){
  var xhr = new XMLHttpRequest();
  xhr.onreadystatechange = function(){
    if(xhr.readyState == 4 && xhr.status == 200){
      console.log(xhr.responseText);
    }
    if(xhr.readyState == 4 && xhr.status == 404){
      console.log("Error!");
    }
  }
  var dataSens = "";
  for(var key in objs.data){
  dataSend += key + "=" + objs.data[key] + "&";
  }
  dataSend = dataSend.substr(0, dataSend.length - 1);
  if(objs.type.toLowerCase() == "get"){
  xhr.open("GET", objs.url + dataSend, false);
  xhr.send();
  }
  if(objs.type.toLowerCase() == "post"){
  xhr.open("POST", objs.url, false);
  xhr.setRequestHeader("Content-type", "application/x-www-from-urlencoded");
  xhr.send(dataSend);
  }
}
```

相信大家都遇到过这样的一个场景，当我们点击按钮时，如果在短时间内重复点击的话，就会不断的向后台发出请求，从而结果就是执行完上一个请求后又将继续执行下一个请求直至点击最后的那个，这时候该如何在数据到来之前防止重复点击呢？
答案是通过设置状态锁的方法来防止重复点击，下面是代码：
```
var isLoading = false;
btn.addEventListener('click', function(){
  if(isLoading){
    return ;
  }else{
    isLoading = true;
      // to do......
    isLoading = false;
  }
}, false)
```














