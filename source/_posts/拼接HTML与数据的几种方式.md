---
title: 拼接HTML与数据的几种方式
date: 2017-03-25 20:33:27
categories: ['技术', '前端技术']
tags: ['javascript']
---

## 使用 `+` 拼接

```js
var a = 1;
var test = 'test';
var html = '<div class="' + test '">' +
           a +
           '</div>';
document.getElementById('container').innerHTML = html;
```

<!-- more -->

## 使用 `Array.push()` 和 `Array.join('')`

```js
var a = 1;
var test = 'test';
var html = [];
html.push('<div class="', test, '">', a, '</div>');
document.getElementById('container').innerHTML = html.join('');
```

## 使用 ES6 模板字符串

```js
var a = 1;
var test = 'test';
var html = `<div class="${test}">
            ${a}
            </div>`;
document.getElementById('container').innerHTML = html;
```

## YY一下

最后的一种方式肯定是最推荐的啦，为什么呢？

1. 看看最前面的两种方式，如果是标签带有属性的话，那么字符串和属性的两种引号混在一起看起来是很不爽的。
2. 不需要考虑引号转义的问题。
3. 暂时还没有其他感受～O__O "…

END.
