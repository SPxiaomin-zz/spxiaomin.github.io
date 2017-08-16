---
title: Asynchronous vs Deferred JavaScript
date: 2017-08-08 15:47:00
categories: ['技术', '前端技术']
tags: ['javascript']
---

## Normal Execution

```html
<html>
<head> ... </head>
<body>
  ...
  <script src="script.js">
  ...
</body>
</html>
```

{% asset_img 'Normal-Execution.png' 'Normal Execution' %}

## The async Attribute

```html
<script async src="script.js">
```

{% asset_img 'Async-Execution.png' 'Async Execution' %}

`script` 会和文档解析并行下载，并在一下载完成了之后立刻执行，并且并不会按照文档中的js文件引入顺序执行(如果存在多个js文件的话)。

## The defer Attribute

```html
<script defer src="script.js">
```

{% asset_img 'Defer-Execution.png' 'Defer Execution' %}

`script` 会和文档解析并行下载，但是就算在文档解析完毕之前下载完成了，也不会立刻执行，而是等到文档解析完毕、按照原文中的js文件引入顺序按序执行(如果存在多个js文件的话)。

## 如果同时使用的

The defer attribute may be specified even if the async attribute is specified, to cause legacy Web browsers that only support defer (and not async) to fall back to the defer behavior instead of the synchronous blocking behavior that is the default.

不过要理解这句话的潜在含义：为了 fallback async 可以连用 defer，但反过来是不成立的。

## References

- [Asynchronous vs Deferred JavaScript](https://bitsofco.de/async-vs-defer/)
- [defer和async的区别](https://segmentfault.com/q/1010000000640869)

END.
