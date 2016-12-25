---
title: javascript函数的作用域链
date: 2016-11-27 15:20:24
categories: ['技术', '前端技术']
tags: ['javascript']
---

最近在做项目，由于好久没有写js了，一直在练习css，遇到了关于函数的作用域链问题，我就一脸懵逼了。

## 问题

函数的作用域链中，当离开了本函数作用域范围往上面查找时，这时是从调用函数的位置开始查找？还是从定义函数的位置开始查找？

## 解决过程

### 权衡利弊思考

由于暂时没有时间系统的学习，那么就先用最快的方式知道答案吧——直接写脚本进行测试就好了。

### 动手

写了如下的两段代码进行测试,

#### 不存在闭包时

```javascript test1.js
var a = 1;

function called() {
    console.log(a);
}

function call() {
    var a = 2;

    called();
}

call();
```

测试结果:

{%  asset_img test1result.png test1.js测试结果 %}

#### 存在闭包时

```javascript test2.js
var a = 1;
var b = 1;

var called = function () {
    var b = 2;
    return function() {
        console.log('a', a);
        console.log('b', b);
    };
}();

function call() {
    var a = 2;

    called();
}

call()
```

测试结果:

{% asset_img test2result.png test2.js测试结果 %}

### 测试结果分析

从 `test1.js` 中的结果 `a=1`，可以知道作用域链离开本函数往上查找的时候，是从函数定义的位置开始沿着作用域链向上查找的。从 `test2.js` 的结果中也可以验证这个结论。

## 结论

函数的作用域链中，当离开了本函数作用域范围往上面查找时，这时是从定义函数的位置开始沿着作用域链继续往上查找的。

END.
