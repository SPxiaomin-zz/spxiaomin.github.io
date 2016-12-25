---
title: inline-block 元素的基线
date: 2016-11-24 07:15:40
categories: ['技术', '前端技术']
tags: ['css', '基线']
---

`inline-block` 元素的基线是分两种情况的：

1. `inline-block` 元素中存在有文字内容；
2. `inline-block` 元素中不存在有文字内容；

## 存在有文字内容

当 `inline-block` 元素中存在有文字的时候，`inline-block` 元素的基线是最后一行文字的基线，无论文字在什么子对象容器内、在什么位置都没有关系。

{% codepen SPxiaomin LbLPgz 0 html 265 %}

## 不存在有文字内容

当 `inline-block` 元素中不存在文字内容的时候，`inline-block` 元素的基线是 `容器的margin-bottom` 底边缘，与容器内的元素没有半毛钱关系，就算和内部元素发生了外边距合并也没有任何影响。

{% codepen SPxiaomin dORbrm 0 html 265 %}

<br>

END.
