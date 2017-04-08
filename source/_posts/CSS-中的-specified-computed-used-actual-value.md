---
title: CSS 中的 specified/computed/used/actual value
date: 2017-04-08 10:32:54
categories: ['技术', '前端技术']
tags: ['css']
---

## specified value

一个 CSS 属性的 `specified value` 是通过如下的三种方式之一进行设置的:

- 如果文档的样式表为属性指定了值，那么将使用这个值作为 `specified value`；
- 如果文档的样式表没有为属性指定值，那么将从父元素继承（如果属性是可以继承的话），使用父元素的 `computed value` 作为 `specified value`；
- 如果上面的途径都不行，将会使用 CSS 规范为元素指定的初始值作为 `specified value`；

## computed value

<!-- TODO: stop writing here -->

## used value

## actual value

## References

- [MDN specified value](https://developer.mozilla.org/en-US/docs/Web/CSS/specified_value)
- [MDN computed value](https://developer.mozilla.org/en-US/docs/Web/CSS/computed_value)
