---
title: CSS 中的 specified/computed/used/actual value
date: 2017-04-08 10:32:54
categories: ['技术', '前端技术']
tags: ['css']
---

这四个值的计算都是发生在浏览器内部的，不过通过 `Window.getComputedStyle` 可以获取 `resolved value(computed or used value, depending on the property)`。

## specified value

一个 CSS 属性的 `specified value` 是通过如下的三种方式之一进行设置的:

- 如果文档的样式表为属性指定了值，那么将使用这个值作为 `specified value`；
- 如果文档的样式表没有为属性指定值，那么将从父元素继承（如果属性是可以继承的话），使用父元素的 `computed value` 作为 `specified value`；

    - 上面的规则适用于除了文档的根元素之外的元素；

- 如果上面的途径都不行，将会使用 CSS 规范为元素指定的初始值作为 `specified value`；

## computed value

一个 CSS 属性的 `computed value` 通过如下的方式从 `specified value` 计算得来：

- 处理特殊值 inherit 和 initial，然后
- 进行一定计算，进而变成——规范中属性描述中的 `computed value` 样子。

举几个 `computed value` 的例子：

- `computed value` 的计算典型包括将相对值(比如 em 单位)转换为绝对值。举个栗子: 如果一个元素的 `specified value` 中包括 `font-size: 16px; padding-top: 2em;`，那么 `padding-top` 的 `computed value` 为 `32px`。

- 还有就是 `<span style="position: absolute"></span>` 的 `display computed value` 为 `block`。

- 还有是 `computed value` 是 `pre-layout` 的，简单说就是页面布局之前的值。举个例子，如果某些属性的百分数相对值转绝对值的计算依赖于页面的布局情况，那么在 `computed value` 中还是保持百分数相对值不变。

- 无单位的 `line-height` 数值，`specified value` 和 `computed value` 相同，都是无单位的数值。

`computed value` 的主要用途就是用于 `继承`—— 父元素的 `computed value` 将是子元素的 `specified & computed value`。

## used value

一个 CSS 属性的 `used value` 是如下的第三步骤中的结果值。

通过如下的四个步骤可以计算出任何 CSS 属性的最终使用值。

1. 通过 `cascading, inheritance, or the default` 得到 `specified value`；
2. 根据 `规范(specification)` 得到 `computed value`；
3. `post-layout(布局之后)` 得到 `used value`；
4. 根据运行环境的限制，然后近似计算后得到 `actual value`；

举个例子：

```html
<div style="width: auto;">
    <p style="width: 50%;">width: 50%</p>
</div>
```

上面的 `p` 元素的 `specified & computed value` 都是 `50%`，因为 `p` 元素的宽度依赖于父元素 `div` 的宽度，但是 `div` 的宽度需要 `post-layout(布局之后)` 才能够确定，所以 `p` 元素的 `used value` 是布局之后父元素的宽度乘以50%之后的结果。

## actual value

一个 CSS 属性的 `actual value` 是 `used value` 根据实际运行的本地环境限制来改变后的近似值。比如，一个用户代理可能只能够渲染整数像素值的边框，因此边框的 `width used value` 要被近似估算。

## References

- [w3c css2.1](https://www.w3.org/TR/CSS2/cascade.html#value-stages)
- [MDN specified value](https://developer.mozilla.org/en-US/docs/Web/CSS/specified_value)
- [MDN computed value](https://developer.mozilla.org/en-US/docs/Web/CSS/computed_value)
- [MDN used value](https://developer.mozilla.org/en-US/docs/Web/CSS/used_value)
- [MDN actual value](https://developer.mozilla.org/en-US/docs/Web/CSS/actual_value)
