---
title: css深入理解のfloat
date: 2017-02-12 08:36:25
categories: ['技术', '前端技术']
tags: ['css', 'float']
---

!!!未完成

先借用一下w3c的盒子模型图片，下文将会用到。

{% asset_img boxdim.png '盒子模型' %}

## float & line box、containing box

浮动盒子会在 `其当前所在的行` ，向左或右侧(取决于float属性的值)浮动，直到浮动盒子的 `margin edge(看文章开头的图片)` 触碰到 `包含块的边缘(containing box edge)`或者另一个浮动盒子的 `margin edge`。如果当前行存在行盒，那么浮动盒子的 `top margin edge(看文章开头的图片)` 会与当前行盒的顶部对齐。如果当前行没有足够的空间来容纳浮动盒子，那么浮动盒子会向下移动，直到空间合适或者没有更多地浮动出现了。

{% codepen SPxiaomin EZJgKX 0 result 265 %}

这里补充一下和浮动相关的包含块(containing block)知识，
<!-- TODO: 稍后再插入，相关的知识点对于我来说存在有难度 -->
<https://www.w3.org/TR/CSS2/visudet.html#containing-block-details>
<https://www.w3.org/TR/CSS2/visuren.html#block-boxes>

浮动最有趣的特性就是文字环绕效果(除非被 `clear` 属性禁止了)，文字会环绕在左浮动盒的右侧排列、右浮动盒的左侧排列。

顺带讲解一下文字环绕效果相关的原理知识：因为浮动盒不在流内，在浮动盒子之前和之后创建的非定位 `块盒(block boxes)` 会照旧垂直排列，表现得就好像浮动不存在一样。但是在浮动盒子旁边的 `行盒(line box)` 会进行必要的缩短，为浮动盒子的 `margin box` 留出空间，进而就产生了文字环绕的效果了。

{% codepen SPxiaomin ggyrgr 0 result 265 %}

但是在文字环绕效果中，也有一点需要注意的事情，当行盒被缩短到无法容纳任何内容的时候，那么行盒就会被向下移动，直到可以容纳内容或者不再有浮动出现为止。

{% codepen SPxiaomin ggNRVX 0 result 265 %}

注意是 `块盒(block boxes)` 而不是 `block-level box` (block img replaced element) 或者 `block container box`(inline-block)；

{% codepen SPxiaomin EZBXNM 0 result 265 %}
<!-- TODO: 插入这些box的解释 -->

## float & containing box

float 的 containing box 是父 block 元素的 content-box。

## float & float

{% codepen SPxiaomin Bpbgor 0 result 265 %}

## float & content reflow

{% codepen SPxiaomin jydBwm 0 result 265 %}

## float & bfc

在同一个bfc中，正常流(normal flow)中生成bfc的元素不能够与float元素的 margin box 有重叠。可以用这个效果来实现一侧定宽的自适应布局，可复用性非常好。

{% codepen SPxiaomin zNeNqK 0 result 265 %}

## float & margin collapse

## float & stacking context

{% codepen SPxiaomin MJxazy 0 result 265 %}


## float & clear

{% codepen SPxiaomin EZMyxV 0 result 265 %}

## 参考

[w3c css2 floats](https://www.w3.org/TR/CSS2/visuren.html#floats)
