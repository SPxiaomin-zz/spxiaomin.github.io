---
title: 深入理解のBootstrap3-网格系统
date: 2016-12-20 18:52:55
categories: ['技术', '前端技术']
tags: ['css', 'Bootstrap']
---

!!! 未完成

> Bootstrap includes a responsive, mobile first fluid grid system that appropriately scales up to 12 columns as the device or viewport size increases.
> Bootstrap 包含一个响应式的，移动设备优先的流体网格系统，包含12列，并且随着设备或者视口的尺寸不断增加每一列的宽度。

### 网格系统-基础知识简介

<!-- TODO: 画出线状图出来理解、查一下有什么线状图工具 -->

> `*` 代表的是占用的网格数量，Bootstrap 中一行的网格数量默认最多是 12 个。

使用网格系统，首先需要注意视口的3个断点——768px、992px、1200px

#### css 权重基础知识简介

css，英文全称cascading style sheet，层叠(cascading)一词就说明了css的核心——当多个选择器选择的是同一个元素的时候，如果样式规则存在冲突，就通过层叠规则来规定样式的覆盖，进而决定使用哪个样式规则。

层叠规则简言之就是通过计算每个选择器权重的数值大小，进而权重值大的覆盖权重值小的，权重值相同就后面的覆盖前面的。当然这是不全面的，还要考虑来源、重要性等特殊情况，不过这里用不到，就不展开了。（这里有一篇关于权重的好文-<http://www.jianshu.com/p/6f5d10343c28>）

<!-- TODO: 日后通过css权威指南进行权重知识的完善 -->

这个特性也是Bootstrap网格系统的核心关键所在——当选择器的权重值相同的时候，后面的样式规则覆盖前面的样式规则。

<!-- TODO: stop writing here -->

Bootstrap 是移动设备优先的，因此在设置 `col-xs-*` 的样式的时候是没有使用媒体查询的，而是直接写样式的，其它的都是通过设置相应宽度的媒体查询实现 `@media (min-width: *) {}`。

- col-xs-*

    xs即extra small，是为手机准备的网格类，也就是在视口 `< 768px` 的时候应用的样式。

- col-sm-*

    sm即small，用在小尺寸屏幕上，比如说平板电脑，在视口 `>= 768px` 的时候应用的样式。

- col-md-*

    md即middle，用在中等设备上，在视口 `>= 992px` 的时候应用的样式。

- col-lg-*

    lg即large，用在大尺寸设备上，在视口 `>= 1200` 的时候应用的样式。

### 让页面居中显示的容器－.container

通过为元素多添加一个带有 `class="container"` 的父元素，就可以实现让页面居中显示。

`.container` 的具体样式规则如下:

```css
.container {
    padding-left: 15px;
    padding-right: 15px;
    margin-left: auto;
    margin-right: auto;
}

@media (min-width: 768px) {
    .container {
        width: 750px;
    }
}

@media (min-width: 992px) {
    .container {
        width: 970px;
    }
}

@media (min-width: 1200px) {
    .container {
        width: 1170px;
    }
}
```

从上面的样式就可以看出来，是通过 `css` 样式层叠特性 & `media` 来实现在不同屏幕尺寸上使用不同的宽度。

上面的样式规则中，先针对移动设备设置默认的样式规则，然后再通过使用媒体查询来根据屏幕不断增大的情况来设置样式，可以看出来采用了移动设备优先的思想。

### 网格类 & 混合使用网格类

网格类Bootstrap样式规则源码

使用一个类——`.col-xs-6`

```css
.col-xs-6 {
    width: 50%;
}

.col-xs-6 {
    float: left;
}
```

混合使用网格类Bootstrap样式规则源码

使用类——`.col-xs-6.col-sm-8`

```css
.col-xs-6 {
    width: 50%;
}

.col-xs-6 {
    float: left;
}

.col-sm-8 {
    width: 66.66666667%;
}

.col-sm-8 {
    float: left;
}
```

其实混合使用网格类布局的核心原则是——权重相同的样式规则，位置越靠后的覆盖位置靠前的。

### 内容列的顺序－push与pull

在不改变代码结构的情况下，改变元素的左右显示位置。使用这个样式的目的是便于SEO搜索优化。

`push` 是向右推，`pull` 是向左拉。

Bootstrap 使用的是以下方式实现效果 `position: relative;` & push `left: *%` & pull `right: *%`

<!-- TODO: left 的百分比值也是相对父元素的宽度计算吗 -->

### 嵌套的布局-nesting

嵌套布局简单来说，就是在 `.col-*-*` 中嵌套 `.col-*-*`，但是要注意将嵌套的 `.col-*-*` 包裹一层 `.row`。

<!-- TODO: 插入本子上的图——有无row，可以考虑用工具画 -->

但是容易造成如下的现象——

<!-- TODO: 插入图片 -->
产生了混排的现象。

解决方案有两种——

1. 分别放在单独的一个 `row`;
2. 增加一个无语义的 `div.clearfix`，来修复元素的浮动问题。

### 偏移的空间-offset

<!-- TODO: 正则表达式1-12的符号怎么表示 -->

使用 `.col-(xs|sm|md|lg)-offset-[1-12]` 对元素进行水平方向的偏移。

Bootstrap 实现的方式是借助 `margin-left` 进行偏移的，这里其实是借助了 `margin` 的百分比值是相对于宽度计算的特性。

### 隐藏与显示的响应式工具类

`visible-(xs|sm|md|lg)` 表示分别在不同尺寸的设备上进行显示。

`hidden-(xs|sm|md|lg)` 表示分别在不同尺寸的设备上进行隐藏。

上面的样式规则已经被弃用了，虽然现在还在支持，

`visible|hidden-xs|sm|md|lg-block|inline|inline-block`


Grid classes apply to devices with screen widths greater than or equal to the breakpoint sizes, and override grid classes targeted at smaller devices. Therefore, e.g. applying any .col-md-* class to an element will not only affect its styling on medium devices but also on large devices if a .col-lg-* class is not present.

Horizontal at all times	Collapsed to start, horizontal above breakpoints
