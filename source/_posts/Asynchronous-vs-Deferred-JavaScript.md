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

## References

- [Asynchronous vs Deferred JavaScript](https://bitsofco.de/async-vs-defer/)

END.
