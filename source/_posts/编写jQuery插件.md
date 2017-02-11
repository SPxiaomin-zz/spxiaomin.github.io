---
title: 编写jQuery插件
date: 2017-02-11 10:35:11
categories: ['技术', '前端技术']
tags: ['jquery']
---

## 定义，作用

## 使用，注意

编写jQuery插件，要设置默认值，并允许用户修改默认值，或者运行时传入其他值。

### 简单的jQuery插件——highlight:

#### 第一版

{% codepen SPxiaomin Xpyoow 0 js 265 %}

#### 第二版

此版和上一版的不同之处在于：这一版能够让用户通过运行时传入参数自定义高亮的颜色。

{% codepen SPxiaomin xgQBwX 0 js 265 %}

#### 第三版（最终版）

此版能够让用户修改默认值。

{% codepen SPxiaomin pRQYrE 0 js 265 %}

### 针对特定元素的扩展



### 注意

扩展jQuery对象的功能十分简单，但是我们要遵循jQuery的原则，编写的扩展方法能支持链式调用、具备默认值和过滤特定元素，使得扩展方法看上去和jQuery本身的方法没有区别。

```javascript
$.fn.highlight = function() {
    // this 已绑定为当前jQuery对象，因此jQuery对象的方法都可以在函数内运用。
    this.css('backgroundColor', '#fff');

    // 支持链式调用
    return this;
}
```

## 参考

[廖雪峰 JavaScript教程 jQuery扩展](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014356468967974219593d94f64d06b370c87fc38eade4000#0)
