---
title: HTTP
tags:
  - HTTP
categories:
  - 后端
date: 2016-12-27 16:06:58
---
#### 1.OSI 七层模型定义
OSI（Open System Interconnection，开放系统互连）七层网络模型称为开放式系统互联参考模型 ，是一个逻辑上的定义，一个规范，它把网络从逻辑上分为了7层。
由下往上可分为：
![OSI 七层模型](http://upload-images.jianshu.io/upload_images/2321415-9f4ecd5b098175e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.HTTP 的工作原理
（1）客户端连接到Web服务器
一个HTTP客户端，通常是浏览器，与Web服务器的HTTP端口（默认为80）建立一个TCP套接字连接。
（2）发送HTTP请求
通过TCP套接字，客户端向Web服务器发送一个文本的请求报文，一个请求报文由请求行、请求头部、空行和请求数据4部分组成。
（3）服务器接受请求并返回HTTP响应
Web服务器解析请求，定位请求资源。服务器将资源复本写到TCP套接字，由客户端读取。一个响应由状态行、响应头部、空行和响应数据4部分组成。
（4）释放连接TCP连接
Web服务器主动关闭TCP套接字，释放TCP连接；客户端被动关闭TCP套接字，释放TCP连接。
（5）客户端浏览器解析HTML内容
客户端浏览器首先解析状态行，查看表明请求是否成功的状态代码。然后解析每一个响应头，响应头告知以下为若干字节的HTML文档和文档的字符集。客户端浏览器读取响应数据HTML，根据HTML的语法对其进行格式化，并在浏览器窗口中显示。

#### 3.URI
**格式：<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<hash>**
- **<scheme>协议方案名**，常见的协议有：
（1）http:应用最广泛的网络传输协议,主要用于传输网页资源 
（2）https:超文本传输安全协议,是一种网络安全传输协议，使用超文本传输协议进行通讯，但利用 SSL/TLS 协议来对封包进行加密 
（3）ftp:文件传输协议,主要用于传输文件 
（4）smtp:简单邮件传输协议,主要用于以推送方式传输邮件 
（5）imap:交互邮件访问协议,主要用于访问远程服务器上的邮件 
（6）ssh:计算机上的 Shell 提供安全的传输和使用环境的安全协议


- **<user>:<password>登录信息**：认证信息
- **<host>主机名**：IP地址或域名，用于确定要连接的对象的地址
- **<port>端口号**：用来区分主机上的进程，方便找到web服务器，一般不需要写（http默认80，https默认443，ftp默认21）
- **<path>路径**：带层次的资源路径，符合web服务器路由约定即可
- **<params>参数**：在一些协议中需要参数来访问资源，例如ftp是二进制还是文本传输，参数是名值对，用;隔开
- **<query>查询字符串**：主要用于 get 请求传递参数，name=value的形式
- **<hash>片段标识符**：用于标识文档的一部分，又称锚点，对server没用，协议不传输

#### 4.HTTP 协议和服务器交互的方法
- **GET**：最常用，通常用于请求服务器发送某个资源（平时在浏览器输入网页地址就是给服务器发送一个GET请求）
- **POST**：用于向服务器发送数据，通常用来支持HTML表单，将表单中的数据发送到服务器
- **HEAD**：和GET类似，但是在服务器的响应中没有资源的内容，只有资源的一些基本信息，主要用于： 1.在不获取资源的情况下获取资源信息（类型、大小等） 2.通过状态码产看资源是否存在 3.通过查看首部，测试资源是否被修改了
- **PUT**：和GET从服务器获取资源相反，PUT用于向服务器写入资源；PUT的语义就是让服务器用请求的主体部分创建一个请求URL命名的文档，如果存在就替换；出于安全原因不是所有的服务器都能实现
- **TRACE**：客户端发送一个请求的时候，这个请求可能会穿过防火墙、代理、网关和一些其它应用程序，每个中间节点都可能修改HTTP请求，TRACE方法允许客户端在最终请求发往服务器的时候，看看它变成了什么样子；TRACE请求会在目的服务器端发送一个“闭环”诊断，行程最后一站服务器会弹回一条TRACE响应，并在响应主题中携带它收到的原始请求报文
- **DELETE**：DELETE方法用于要求服务器删除请求的URL，和PUT一样，服务器可能会不支持（删除资源）
- **OPTIONS**：OPTIONS方法用于请求 web服务器告知其支持的各种功能（比如查看-服务器支持以上哪几种方法）

#### 5.状态码
- 200：OK；该请求被成功地完成，所请求的资源发送回客户端。
- 301：Moved Permanently；永久性定向，客户请求的文档在其他地方，新的URL在Location头中给出，浏览器应该自动地访问新的URL
- 304：Not Modified；上次的文档已经被缓存了， 还可以继续使用。
- 403：Forbidden；服务器收到请求，但是拒绝提供服务
- 404：Not Found；请求资源不存在（一般是输错了URL）
- 500：Internal Server Error；服务器发生了不可预期的错误
- 503：Server Unavailable；服务器当前不能处理客户端的请求，一段时间后可能恢复正常

#### 6.报文的组成
- 请求报文：
（1）起始行：请求方法、URI、协议版本
（2）首部：请求首部、通用首部 、实体首部及其他
（3）空行
（4）报文主体
- 响应报文：
（1）起始行：协议版本、状态码、状态码描述
（2）首部：响应首部、通用首部、实体首部及其他
（3）空行
（4）报文主体


#### 7.请求头的格式和作用
![请求头](http://upload-images.jianshu.io/upload_images/2321415-4c6ceb898ee8812f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Accept：浏览器能接收的资源类型
Accept-Encoding：告诉服务器能够发送哪些编码
Accept-Language：告诉服务器能够发送哪些语言
Cache-Control：缓存控制
Connection：客户端和服务器是否保持连接
Cookie：客户端字符串
Host：接受请求的服务器的主机号和端口号
User-Agent：发起请求的客户端应用程序

#### 8.首部的格式和作用
![首部](http://upload-images.jianshu.io/upload_images/2321415-e213f75163603c37.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
Request URL：请求的URL地址
Request Method：请求的方法
Status Code：状态码
Remote Address：远程地址即服务器地址

#### 9.主体的作用
![主体](http://upload-images.jianshu.io/upload_images/2321415-941d729e99e9368d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
主体就是客户端和服务器所传输的主要内容

#### 10.浏览器缓存是如何控制的
浏览器是否使用缓存、缓存多久，是由服务器控制的。准确来说，当浏览器请求一个网页（或者其他资源）时，服务器发回的响应的「响应头」部分的某些字段指明了有关缓存的关键信息。通过Expires,Cache-Contrll，Last-Modified/If-Modified-Since，Etag/If-None-Match控制。
- Expires：是Web服务器响应消息头字段，在响应http请求时告诉浏览器在过期时间前浏览器可以直接从浏览器缓存取数据，而无需再次请求。
- Cache-Control：与Expires的作用一致，都是指明当前资源的有效期，控制浏览器是否直接从浏览器缓存取数据还是重新发请求到服务器取数据，不过Cache-Control有多个参数，优先级高于Expires。
- Last-Modified/If-Modified-Since：Last-Modified/If-Modified-Since要配合Cache-Control使用。最后修改时间/除非在某个制定日期之后修改过，否则限制这个请求
- Etag/If-None-Match：Etag/If-None-Match也要配合Cache-Control使用。
Etag：web服务器响应请求时，告诉浏览器当前资源在服务器的唯一标识。
If-None-Match：当资源过期时（使用Cache-Control标识的max-age），发现资源具有Etage声明，则再次向web服务器请求时带上头If-None-Match（Etag的值）
[参考](http://www.cnblogs.com/skynet/archive/2012/11/28/2792503.html)

#### 11.下图各个参数是什么意思
![参数的意思](http://upload-images.jianshu.io/upload_images/2321415-4314e6b9baff008a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 12.POST 与 GET 的区别
（1）get和post都是数据提交的方式。
（2）get的数据是通过网址问号后边拼接的字符串进行传递的。post是通过一个HTTP包体进行传递数据的。
（4）get的传输量是有限制的，post是没有限制的。
（5）get的安全性没有post高，因为所发送的数据是URL的一部分。所以我们一般用get来获取数据，post一般用来修改数据。



