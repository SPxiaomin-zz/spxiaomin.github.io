---
title: JavaScript中判定数组的方法
date: 2017-08-29 15:10:03
categories: ['技术', '前端技术']
tags: ['javascript']
---

## Object.prototype.toString.call

```js
Object.prototype.toString.call([]);
// "[object Array]"
```

## Array.isArray

```js
Array.isArray([]);
// true
```

## instanceof

```js
[] instanceof Array
// true
```

但是还是存在有缺陷的——<https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray#instanceof_vs_isArray>，不同全局作用域中的Array构造函数不同(Array是window的属性)。

## References

- [MDN javascript Array.isArray](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)
- [Javascript 判断变量类型的陷阱 与 正确的处理方式](http://www.cnblogs.com/pspgbhu/p/7149124.html#3734213)
- 红皮书

END.

<!-- more -->
