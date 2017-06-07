---
title: CSS absolute的位置跟随特性&应用
date: 2017-06-06 14:39:33
categories: ['技术', '前端技术']
tags: ['css']
---

## 跟随性讲解

如果元素本身就是 `block` 和其他元素不在一行，那么 `absolute` 之后也不会在同一行。如果元素本身是 `inline or inline-block` 和其他元素在一行，那么 `absolute` 之后也是在同一行的。简单就是说原来在什么位置，绝对定位之后还是在什么位置。

<http://www.imooc.com/code/4403>

## 跟随性应用

### 文字后面跟随图片

一般的方式是通过在父元素上设置 `position: relative`，图片上设置 `position: absolute` 然后进行定位。两者有什么区别呢？张大大在视频上面说是下面的方式更加简洁&并且灵活，然后我并没有觉得有非常大的改善。

{% codepen spxiaomin GEgVjP 0 result 265 %}

### 原地不动，覆盖别人

{% codepen spxiaomin PjqevY 0 result 265 %}

### 尾部跟随，不占空间

{% codepen spxiaomin RgPJrX 0 result 265 %}

## References

- [张鑫旭 imooc](http://www.imooc.com/video/4461)

END.
