---
title: HTML5离线缓存
tags:
  - HTML
categories:
  - 前端
date: 2017-02-13 17:47:18
---
#### 1、使用：
（1）创建 manifest 文件
``
cache manifest
# version n.n


cache:
// 需要缓存的文件﻿​
/css/style.css
/images/image.jpg


network:
// 每次重新拉取的文件
* （除了以上的所有文件）


fallback:
// 离线状况下代替的文件
/offline.html 
`` 
 
（2）在 HTML 页面中引用 manifest 文件
```
<htmlmanifest="sample.appcache">
<html>
<head>
  //todo
</head>
<body>
  //todo
</body>
</html>
```
 
（3）在服务器添加 mime-type text/cache-manifest
 
（4）如何更新：如果有修改资源文件，必须通过修改manifest文件来刷新被缓存的文件列表。
 
#### 2、优势：
（1）完全离线
（2）资源被缓存，加载更快
（3）降低 server 负载
 
#### 3、缺陷：
（1）含有 manifest 属性的当前请求页无论如何都会被缓存
（2）更新需要建立在manifest文件的更新，文件更新后是需要页面再次刷新的（需要2次刷新才能获取新资源）
（3）更新全局性的，无法单独更新某个文件（无法单点更新）
（4）对于链接的参数变化是敏感的，任何一个参数的修改都会被（master）重新缓存（重复缓存含参页面）index.html 和 index.html?renew=1 会被认为是不同文件，分别缓存。
 
#### 4、使用场景
（1）单地址的页面
（2）对实时性能要求不高的业务 （修改不频繁）
（3）离线 webapp  