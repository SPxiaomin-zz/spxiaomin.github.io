---
title: html/css + jQuery 的开发套路
date: 2017-04-13 12:08:32
categories: ['技术', '前端技术']
tags:
---

写好全局样式；

向分析好整个页面的布局方式，然后写好大块的容器 html 代码结构，并且通过样式布好局；

- div#header
- div#content
- div#nav
- div#main
- div#footer

然后写复用样式；

然后开始分块编写——写html，然后写css；

之后的每块：

- 递归——写好布局 html 代码和布局样式，然后分块编写 html、css；

---

如果要实现一个效果，但是不是很容易，这个时候可以借助于插件，插件也是 jQuery 的特色之一。
