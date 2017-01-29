---
title: css深入理解之marginの学习笔记
date: 2017-01-06 07:26:27
categories: ['技术', '前端技术']
tags: ['css', 'margin']
---

!!!未完成

## 1-1 css margin与容器的尺寸

css margin可以改变容器的尺寸。

标准的盒模型——

{% asset_img margin-1.png '标准的盒模型' %}

元素尺寸

1. 可视尺寸-clientWidth（标准）——就是上图中的border box包含的尺寸。

2. 占据尺寸-outerWidth（YY，jQuery里面是有这个方法的）——就是上图中的margin box包含的尺寸。

### margin与可视尺寸

1. 适用于 `没有设定width/height` 的 `普通` `block水平` 元素。

    ~~float元素~~ ~~absolute/fixed元素~~ ~~inline水平，table-cell元素~~，...

2. 只适用于水平方向的尺寸。

示例代码如下：

{% codepen SPxiaomin QdOzKM 0 html 265 %}

适用场景：

1. 一侧定宽的自适应布局

    {% codepen SPxiaomin Ndweyw 0 html 265 %}

2. 两端对齐布局

### margin与占据尺寸

1. block/inline-block水平元素的适用；
2. 与有没有设定width/height值无关；
3. 适用于水平方向和垂直方向；

示例代码如下：

{% codepen SPxiaomin mRqaKO 0 html 265 %}
