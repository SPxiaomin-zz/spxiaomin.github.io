---
title: CSS 中的 specified/computed/used/actual value
date: 2017-04-08 10:32:54
categories: ['技术', '前端技术']
tags: ['css']
---

这四个值都是的计算都是发生在浏览器内部的，不过通过 `Window.getComputedStyle` 可以获取 `resolved value(computed or used value, depending on the property)`。

## specified value

一个 CSS 属性的 `specified value` 是通过如下的三种方式之一进行设置的:

- 如果文档的样式表为属性指定了值，那么将使用这个值作为 `specified value`；
- 如果文档的样式表没有为属性指定值，那么将从父元素继承（如果属性是可以继承的话），使用父元素的 `computed value` 作为 `specified value`；
- 如果上面的途径都不行，将会使用 CSS 规范为元素指定的初始值作为 `specified value`；

## computed value

一个 CSS 属性的 `computed value` 通过如下的方式从 `specified value` 计算得来：

- 处理特殊值 inherit 和 initial，然后
- 进行一定计算，进而变成——规范中属性描述中的 `computed value` 样子。

`computed value` 的计算典型包括将相对值(比如 em 单位)转换为绝对值。举个栗子: 如果一个元素的 `specified value` 中包括 `font-size: 16px; padding-top: 2em;`，那么 `padding-top` 的 `computed value` 为 `32px`。

但是 `computed value` 是 `pre-layout` 的，简单说就是页面布局之前的值，如果某些属性相对值转绝对值的计算依赖于布局，那么在 `computed value` 中相对值保持不变。

`computed value` 的主要用途就是用于 `继承`。

## used value

一个 CSS 属性的 `used value` 是进行完了所有的计算之后的最终值。

通过如下的四个步骤可以计算出任何 CSS 属性的最终使用值。

1. 通过 `cascading, inheritance, or the default` 得到 `specified value`；
2. 根据 `规范(specification)` 得到 `computed value`；
3. `post-layout(布局之后)` 得到 `used value`；
4. 根据运行环境的限制得到 `actual value`；

## actual value

<!-- TODO: stop writing here -->

## References

- [MDN specified value](https://developer.mozilla.org/en-US/docs/Web/CSS/specified_value)
- [MDN computed value](https://developer.mozilla.org/en-US/docs/Web/CSS/computed_value)
