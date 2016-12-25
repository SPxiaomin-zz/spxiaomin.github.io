---
title: css避免margin穿透的方式
date: 2016-12-20 07:39:14
categories: ['技术', '前端技术']
tags: ['css', 'margin穿透']
---

## 使用BFC

通过生成BFC可以避免margin穿透问题，具体[css spec2.1](https://www.w3.org/TR/CSS2/box.html#collapsing-margins) 是这样说的 Two margins are adjoining if and only if: both belong to in-flow block-level boxes that participate in the same block formatting context，简单的说呢，就是只有在同一个bfc中才能够发生外边距合并。

所以我可通过在父元素上设置生成bfc的属性，这样就可以为子元素生成一个新的bfc，然而和父元素是不在同一个bfc中的，这样就可以避免margin穿透问题了

{% codepen SPxiaomin MbdQgN 0 html 265 %}

END.
