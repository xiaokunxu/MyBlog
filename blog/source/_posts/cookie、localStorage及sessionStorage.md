---
title: cookie、localStorage及sessionStorage
tags:
  - HTML5
categories:
  - 前端
date: 2017-02-13 17:52:07
---
#### 一、cookie
（1）cookie 是web浏览器存储的少量数据，最早设计为服务器端使用，作为HTTP协议的扩展实现。cookie 数据会自动在浏览器和服务器之间传输。
（2）通过读写 cookie 检测是否支持
（3）cookie 属性有名，值，max-age，path, domain，secure；
（4）cookie默认有效期为浏览器会话，一旦用户关闭浏览器，数据就丢失，通过设置max-age=seconds 属性告诉浏览器 cookie 有效期
（5）cookie作用域通过文档源和文档路径来确定，通过path和domain进行配置，web页面同目录或子目录文档都可访问
（6）通过cookie保存数据的方法为：为document.cookie 设置一个符合目标的字符串如下
（7）读取 document.cookie 获得'; '分隔的字符串，key=value,解析得到结果
```
document.cookie = 'name=qiu; max-age=9999; path=/; domain=domain; secure';
document.cookie = 'name=aaa; path=/; domain=domain; secure'; 
  // 要改变cookie的值，需要使用相同的名字、路径和域，新的值 
  // 来设置cookie，同样的方法可以用来改变有效期
  // 设置max-age为0可以删除指定cookie
  //读取cookie，访问document.
cookie返回键值对组成的字符串， //不同键值对之间用'; '分隔。通过解析获得需要的值 `﻿
```
#### 二、localStorage和sessionStorage
（1）使用方法
在使用之前首先需要判断浏览器是否支持localStorage和sessionStorage属性
```
if(！window.localStorage){
  alert("浏览器支持localstorage");
    return false;
  }else{
    //主逻辑业务
}
```

- 存储：localStorage.setItem(key,value)如果key存在时，更新value

- 获取：localStorage.getItem(key)如果key不存在返回null

- 删除：localStorage.removeItem(key)一旦删除，key对应的数据将会全部删除

- 全部清除：localStorage.clear()
某些时候使用removeItem逐个删除太麻烦，可以使用clear,执行的后果是会清除所有localStorage 对象保存的数据


（2）可以存什么：数组、json数据、图片、脚本以及样式文件

（3）使用限制
- 存储更新策略，过期控制。
- 子域名之间不能共享存储数据。
- 超出存储大小之后如何存储（LRU、FIFO）。
- server 端如何取到。

（4）使用场景：
- 利用本地数据。减少网络传输。
- 弱网络环境下，高延迟，低带宽，尽量把数据本地化。

（5）区别：
- localStorage有效期为永久，sessionStorage有效期为顶层窗口关闭前，sessionStorage 存储的数据在浏览器关闭后自动删除。
- 同源文档可以读取并修改 localStorage 数据，sessionStorage 只允许同一个窗口下的文档访问，如通过 iframe 引入的同源文档。
- Storage对象通常被当做普通javascript对象使用：通过设置属性来存取字符串值，也可以通过 setItem(key, value) 设置，getItem(key)读取，removeItem(key)删除，clear()删除所有数据，length表示已存储的数据项数目，key(index)返回对应索引的key。

#### 三、localStorage,sessionStorage,cookie 区别
- 都会在浏览器端保存，有大小限制，同源限制。
- cookie 会在请求时发送到服务器，作为会话标识，服务器可修改cookie；web storage 不会发送到服务器。
- cookie 有path概念，子路径可以访问父路径 。cookie，父路径不能访问子路径cookie。
- 有效期：cookie 在设置的有效期内有效，默认为浏览器关闭；sessionStorage在窗口关闭前有效，localStorage 长期有效，直到用户删除。
- 共享：sessionStorage不能共享，localStorage在同源文档之间共享，cookie在同源且符合path规则的文档之间共享。
- localStorage的修改会促发其他文档窗口的 update 事件。
- cookie有secure属性要求HTTPS传输。
- 浏览器不能保存超过300个cookie，单个服务器不能超过20个，每个cookie不能超过4k。web storage大小支持能达到5M。
- cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应当使用session。
- session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用cookie。
- 所以个人建议：将登陆信息等重要信息存放为session，其他信息如果需要保留，可以放在cookie中。




