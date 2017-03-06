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

浮动盒子会在 `其当前所在的行` ，向左或右侧(取决于float属性的值)浮动，直到浮动盒子的 `margin edge(看文章开头的图片)` 触碰到 `包含块的边缘(containing box edge)`或者另一个浮动盒子的 `margin edge`。如果当前行存在行盒，那么浮动盒子的 `top margin edge(看文章开头的图片)` 会与当前行盒的顶部对齐。如果当前行没有足够的空间来容纳浮动盒子，那么浮动盒子会向下移动，直到空间合适或者没有浮动出现了。

{% codepen SPxiaomin QdXxPp 0 result 265 %}

这里补充一下和浮动相关的包含块(containing block)知识，float 的 containing box 是父 block 元素的 content-box。

<!-- TODO: 稍后再插入，相关的知识点对于我来说存在有难度 -->
<https://www.w3.org/TR/CSS2/visudet.html#containing-block-details>
<https://www.w3.org/TR/CSS2/visuren.html#block-boxes>

浮动最有趣的特性就是文字环绕效果(除非被 `clear` 属性禁止了)，文字会环绕在左浮动盒的右侧排列、右浮动盒的左侧排列。

顺带讲解一下文字环绕效果相关的原理知识：因为浮动盒不在流内，在浮动盒子之前和之后创建的非定位(non-positioned) `块盒(block boxes)` 会照旧垂直排列，表现得就好像浮动不存在一样。但是在浮动盒子旁边的 `行盒(line box)` 会进行必要的缩短，为浮动盒子的 `margin box` 留出空间，进而就产生了文字环绕的效果了。

{% codepen SPxiaomin ggyrgr 0 result 265 %}

注意是 `块盒(block boxes)` 而不是 `block-level box` (e.g. block img replaced element) 或者 `block container box`(inline-block)；

{% codepen SPxiaomin EZBXNM 0 result 265 %}
<!-- TODO: 插入这些box的解释 -->

但是在文字环绕效果中，也有一点需要注意的事情，当行盒被缩短到无法容纳任何内容的时候，那么行盒就会被向下移动，直到可以容纳内容或者不再有浮动出现为止。

{% codepen SPxiaomin ggNRVX 0 result 265 %}

还有一种比较少见的情况，那就是当浮动的 `outer height` 为0或者负值的时候，浮动盒子旁边的行盒就不会缩短，进而也就不会产生文字环绕效果了。

{% codepen SPxiaomin YNmwEx 0 result 265 %}

## float & float

{% codepen SPxiaomin Bpbgor 0 result 265 %}

## float & content reflow

在一个行盒中，任何在浮动盒子之前(比如在左浮动的左边或者在右浮动的右边)的内容，都会被移动到浮动盒子之后。

{% codepen SPxiaomin jydBwm 0 result 265 %}

## float & bfc

在同一个bfc中，正常流(normal flow)中生成bfc的元素(比如说一个带有 overflow 属性值为非 visible的元素)的 `border box` 不能够与float元素的 `margin box` 有重叠。可以用这个效果来实现一侧定宽的自适应布局，可复用性非常好。

{% codepen SPxiaomin zNeNqK 0 result 265 %}

## float & margin collapse

浮动元素是不会和父元素发生 `margin collapse` 的，因为 `margin collapse` 的前提是在同一个bfc中的流内块级元素。

{% codepen SPxiaomin OpNmep 0 result 265 %}

## float & stacking context

浮动的内容堆叠得就好像浮动生成了新的堆叠上下文，除了定位元素和实际上生成了新的堆叠上下文的元素参与浮动的父堆叠上下文。当浮动元素和正常流(normal flow)中的其它元素重叠的时候，浮动元素会被渲染在非定位流内块(non-positioned in-flow blocks)之上，但是在流内内联(in-flow inlines)之下。

{% codepen SPxiaomin MJxazy 0 result 265 %}

## float & clear

可以使用 clear 属性来清除浮动，这样被清除浮动的盒子的 `top border edge` 会与浮动盒子的 `bottom margin edge` 对齐，这是通过在被清除浮动的盒子的 `top margin edge` 上方添加 `clearance` 来实现的。

{% codepen SPxiaomin EZMyxV 0 result 265 %}

## 参考

[w3c css2 floats](https://www.w3.org/TR/CSS2/visuren.html#floats)
