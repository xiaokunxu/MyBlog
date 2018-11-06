---
title: BFC详解
tags:
  - HTML
  - CSS
categories:
  - 前端
date: 2016-12-23 17:32:18
---
#### 1.BFC定义
BFC(Block formatting context)是指"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

#### 2.BFC布局规则：
（1）内部的Box会在垂直方向，一个接一个地放置。
（2）Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。
（3）每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
（4）BFC的区域不会与float box重叠。
（5）BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
（6）计算BFC的高度时，浮动元素也参与计。

#### 3.那BFC是怎么形成的呢？
（1）float属性不为none；
（2）position为absolute或fixed；
（3）overflow: auto/hidden；
（4）display:inline-block、table-cells、table-captions、或inline-flex。

#### 4.作用：
（1）BFC会阻止垂直外边距（margin-top、margin-bottom）折叠
（2）BFC不会重叠浮动元素
（3）BFC可以包含浮动
（4）BFC可以形成一个独立的空间，和其他空间相互隔开，互不影响。

#### 5.下面就来了解浮动导致的父容器高度塌陷
当父容器没有设置高度，而子元素全部浮动时，子元素会脱离文档流，父容器就会视为内部没有任何子元素，也就是说父容器内没有任何子元素来支撑，所以父容器就为0，从而父容器高度塌陷。
解决方法：
（1）在父容器上设置display: inline-block;
（2）在父容器上设置overflow: auto/hidden;
（3）通过父容器浮动形成BFC；
（4）在浮动元素后面添加一个空元素，并对空元素进行清除浮动；
（5）在浮动元素的父容器上添加伪类元素，并设置：
```
.clearfix:after{ //在class="clearfix"上添加一个伪类
     content: ' '; 添加一个为空的字符
     display: inline-block; //设置为行内块级元素
     clear: both; //清除浮动
}
.clear{
     *zoom: 1; //兼容IE6/7
}
```