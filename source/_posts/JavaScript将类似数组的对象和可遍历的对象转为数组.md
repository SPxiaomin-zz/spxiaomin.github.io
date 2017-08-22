---
title: JavaScript将类似数组的对象和可遍历的对象转为数组
date: 2017-08-22 21:32:04
categories: ['技术', '前端技术']
tags: ['javascript']
---

## '只'类似数组的对象

类似数组的对象，本质就是有 `length` 属性。

可以使用如下的两种方式——

1. `[].slice.call(obj)`
2. `Array.from(obj)`

## '只'可遍历的对象

可遍历的对象，指具有 `iterator` 接口。

可以使用如下的两种方式——

1. `Array.from(obj)`
2. `[...obj]`

## 既类似数组又可遍历的对象

1. `[].slice.call(obj)`
2. `Array.from(obj)`
3. `[...obj]`

END.

<!-- more -->
