---
title: CSS深入理解☞line-height
date: 2017-06-07 16:13:17
categories: ['技术', '前端技术']
tags: ['css']
---

## line-height的定义

line-height，行高，两行文字基线之间的距离。

### 什么是基线？

学习英语的时候，英语本子上的红线，那条红线就是这里的基线。

### line-height 200px与基线的关系

## line-height与行内框盒子模型

### 4种盒子

## line-height的高度机理

内联元素的高度是由 **line-height** 决定的。

内容区域高度(content area) + 行间距(vertical spacing) = 行高(line-height)

行间距在内容区域的上下进行均分。

## line-height各类属性值

normal

由于初始值 normal 在不同的浏览器中，表现都是不一致的，所以一般会在 body 进行全局设置。

<number>

<length>

<percent>

inherit

END.
