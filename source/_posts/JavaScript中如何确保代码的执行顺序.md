---
title: JavaScript中如何确保代码的执行顺序
date: 2017-07-16 08:34:57
categories: ['技术', '前端技术']
tags: ['javascript']
---

当我们想要确保某代码在谁谁之后执行时，我们可以使用如下的几种方式:

## 函数调用栈

可以利用函数调用栈，将我们想要执行的代码放入回调函数中。

```js
function want() {
  console.log('这是你想要执行的代码');
}

function fn(want) {
  console.log('这里表示执行了一大堆各种代码');

  // 其他代码执行完毕，最后执行回调函数
  want && want();
}

fn(want);
```

<!-- more -->

## 队列机制

```js
function want() {
  console.log('这是你想要执行的代码');
}

function fn(want) {
  // 将想要执行的代码放入队列中，根据事件循环的机制，我们就不用非得将它放到最后面了，由你自由选择
  want && setTimeout(want, 0);
  console.log('这里表示执行了一大堆各种代码');
}

fn(want);
```

## Promise 队列

```js
function want() {
  console.log('这是你想要执行的代码');
}

function fn(want) {
  console.log('这里表示执行了一大堆各种代码');

  return new Promise(function(resolve, reject) {
    if (typeof want === 'function') {
      resolve(want);
    } else {
      reject(`TypeError: ${want} is not a function`);
    }
  });
}

fn(want).then(function(want) {
  want();
});

fn('1234').catch(function(error) {
  console.log(error);
});
```

## References

- [前端基础进阶（十三）：透彻掌握Promise的使用，读这篇就够了](http://www.jianshu.com/p/fe5f173276bd)

END.
