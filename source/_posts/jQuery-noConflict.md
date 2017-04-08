---
title: jQuery noConflict
date: 2017-04-08 11:53:39
categories: ['技术', '前端技术']
tags: ['jQuery']
---

## noConflict 出现的缘由

jQuery 使用 `$` 作为 jQuery 的简写，如果你将其他的框架或库和 jQuery 混在一起使用，并且其他的框架或库也是使用 `$` 作为简写的话，那么就会存在冲突。

jQuery 的团队考虑到了这个问题，并实现了 noConflict() 方法。

## noConflict 方法

noConflict 方法会释放对 `$` 标识符的控制，这样其他脚本就可以使用它了。

但是你仍然可以通过如下的三种方法来使用 jQuery。

### 全名

仍然可以通过全名替代简写的方式来使用 jQuery。

{% codepen SPxiaomin ryEdVN 0 js 265 %}

### 创建自己的简写

<!-- stop writing here 简介——noConflict 可返回 -->

###

## References

- [jQuery - noConflict() 方法](http://www.runoob.com/jquery/jquery-noconflict.html)
