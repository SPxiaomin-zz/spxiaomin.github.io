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

Promise 最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了。

{% asset_img 'promise.png' 'promise执行流程' %}

```js
function ajax(method, url) {
  return new Promise(function(resolve, reject) {
    // 创建 xml 对象
    let xml = new XMLHttpRequest();

    // onreadystatechange
    xml.onreadystatechange = function() {
      if (xml.readyState === 4) {
        if (xml.status === 200) {
          resolve(xml.responseText);
        } else {
          reject(xml.status);
        }
      }
    };

    // open
    xml.open(method, url);

    // send
    xml.send();
  });
}

let p = ajax('GET', 'http://api.test.com/movies/123');
p.then(function(result) {
  console.log(result);
}).catch(function(code) {
  console.log(`Error: ${code}`);
});
```

将异步操作全部放入到 `new Promise()` 中去，然后在将来的某个时间点触发的函数中调用 `resolve or reject`。

## Promise 的几大作用

### 串行执行一系列异步任务

比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。

要串行执行这样的异步任务，不用 Promise 需要写一层一层的嵌套代码。

```js
let filename = '1.js';

readFileAsync(filename, function(error, result) {
  readFileAsync(result, function(error, result) {
    readFileAsync(result, function(error, result) {
      console.log(result);
    });
  });
});
```

通过 Promise 处理了之后。

```js
function readFileAsyncPromise(fileName) {
  return new Promise(funtion(resolve, reject) {
    readFileAsync(fileName, function(err, result) {
      if (err) {
        reject(err);
      }

      resolve(result);
    });
  });
}

let p = new Promise(function(resolve, reject) {
  resolve('1.js');
});

p.then(readFileAsyncPromise)
  .then(readFileAsyncPromise)
  .then(readFileAsyncPromise)
  .then(function(result) {
    console.log(result);
  })
  .catch(function(error) {
    console.log(error);
  });
```

#### 串行过程中的返回值问题

```js
let fileName = '1.js';

let p = new Promise(function(resolve, reject) {
  readFileAsync(fileName, function(error, result) {
    if (error) {
      reject(error);
    }

    resolve(result.name);
  });
});

p.then(function(fileName) {
  // 1
  return new Promise(function(resolve, reject) {
    readFileAsync(fileName, function(error, result) {
      resolve(result);
    });
  });

  // 2
  readFileAsync(fileName, function(error, result) {
    return result;
  });

  // 3
  return undefined;
}).then(function(result) {
  console.log(result);
});
```

<!-- TODO: stop 分析三种返回值的 event loop 队列 -->

1. return 另一个 new Promise()

  这个用来再执行一个异步任务。

2. 间接 return 一个简单的值

  这个 return 的值是得不到处理的，因此也差不多是多此一举的样子。

3. 直接 return 一个简单的值

  这个暂时我觉得没有什么实际的用处，有多此一举的嫌疑。

### 并行执行一系列异步任务

###

## Promise 的应用

### 网易面试题



## References

- [廖雪峰Promise](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014345008539155e93fc16046d4bb7854943814c4f9dc2000)
