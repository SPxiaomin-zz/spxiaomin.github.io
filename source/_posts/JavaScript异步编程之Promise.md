---
title: JavaScript异步编程之Promise
date: 2017-05-21 21:28:53
categories: ['技术', '前端技术']
tags: ['javascript']
---

在JavaScript的世界中，所有代码都是单线程执行的。由于这个 “缺陷”， 导致JavaScript的所有网络操作、浏览器事件，都必须是异步执行。

```javascript
function callback() {
  console.log('Done');
}

console.log('before setTimeout()');
setTimeout(callback, 1000); // 一秒钟后调用callback函数
console.log('after setTimeout()');

// 控制台输出结果
before setTimeout()
after setTimeout()
(等待1秒后)
Done
```

可见，异步操作会在将来的某个时间点触发一个函数调用。

<!-- more -->

## Promise 来了

Promise最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了。

{% asset_img 'promise.png' 'promise执行流程' %}

<!-- TODO: stop writing here -->

将异步操作全部放入到 `new Promise()` 中去，然后在将来的某个时间点触发的函数中调用 `resolve or reject`。

## Promise 的几大作用

###

###

###

## Promise 的应用

### 网易面试题



## References

- [廖雪峰Promise](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014345008539155e93fc16046d4bb7854943814c4f9dc2000)
