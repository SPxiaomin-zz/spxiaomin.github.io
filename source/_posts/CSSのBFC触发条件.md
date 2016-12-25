---
title: CSSのBFC触发条件
date: 2016-12-16 07:40:47
categories: ['技术', '前端技术']
tags: ['css', 'bfc']
---

## 前言

BFC这个东西可是非常强大的哈，借用张大大的一句话——BFC元素中的内部子元素再怎么翻江倒海、翻云覆雨都不会影响外部大的元素，可以用来避免margin穿透，清除浮动等。

## bfc触发条件

1. `float` 的值不为 `none`
2. `position` 的值不为 `static` or `relative`
3. `overflow` 的值为 `auto` or `hidden` or `scroll`
4. `display` 的值为 `table-cell` or `table-caption` or `inline-block`

END.
