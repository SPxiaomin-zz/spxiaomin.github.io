---
title: 使用CSS控制页面的四种方式
date: 2017-04-14 10:39:04
categories: ['技术', '前端技术']
tags: ['css']
---

使用 CSS 控制页面的四种方式，分别为行内样式(内联样式)、内嵌式、链接式、导入式。

## 行内样式(内联样式)——inline style

行内样式(内联样式)即写在 HTML 标签中的 style 属性中控制元素样式，如下列的代码所示:

```html
<div style="width: 100px; height: 100px;"></div>
```

## 内嵌式——embedded style

内嵌样式即写在 style 标签中，如下代码示例:

```html
<style>
    div {
        width: 100px;
        height: 100px;
    }
</style>
```

## 链接式——linked style

链接式即为用 link 标签引入 css 文件，如下代码示例:

```html
<link rel="stylesheet" href="/static/css/main.css" />
```

## 导入式——import style

导入式即为用 import 导入 css 文件，如下代码示例:

```html
@import url("/static/css/main.css");
```

## References

- [原生JavaScript获取css样式](http://www.cnblogs.com/wjx91/p/5645464.html)
