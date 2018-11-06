---
title: JSONP
tags:
  - JavaScript
categories:
  - 前端
date: 2017-02-13 18:54:06
---
#### 一、JSONP 是什么？
JSONP 是利用在页面中创建 ``<script>`` 节点的方法向不同域提交HTTP请求的方法

#### 二、JSONP 是如何实现跨域的？
动态插入script标签，通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。 

#### 三、为什么能实现跨域
（1）``<script>`` 标签的src属性是可以跨域的 
（2）把跨域服务器写成调用本地的函数，回调数据回来就可以了
（3）json刚好被js支持（object）
（4）调用跨域服务器上动态生成的js格式文件（不管是什么类型的地址，最终生成的返回值都是一段js代码）
（5）传递一个callback参数给跨域服务端，然后跨域服务端返回数据时会将这个callback参数作为函数名来包裹住json数据即可。
（6）由于同源策略的限制，``XmlHttpRequest``只允许请求当前源（域名、协议、端口）的资源，为了实现跨域请求，可以通过script标签实现跨域请求，然后在服务端输出JSON数据并执行回调函数，从而解决了跨域的数据请求。

#### 四、与AJAX的区别？
（1）ajax 的核心是通过 XmlHttpRequest获取非本页内容
（2）jsonp 的核心是动态添加 ``<script>`` 标签来调用服务器提供的 js 脚本。

#### 五、JSONP 的数据格式是：jsonpCallback+"("+resultJson.toString()+")"，如：
```
jsonpCallback({

  "code": "aaa",

  "price": 1780,

  "tickets": 5

});
```







