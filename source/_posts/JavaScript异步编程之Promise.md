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

要串行执行这样的异步任务，不用 Promise 需要写一层一层的嵌套代码（也就是俗称的回调地狱）。

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

通过 Promise 处理了之后，就 **将回调地狱的问题解决了**。

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
  return result;
}).then(function(result) {
  console.log(result);
});
```

1. return 另一个 new Promise()

  这个用来再执行一个异步任务。**这也是解决回调地狱的主要方式**。

2. 间接 return undefined

  这个异步中 return 的值是得不到处理的。

3. 直接 return 一个简单值

  这个暂时我觉得没有什么实际的用处，有多此一举的嫌疑。

其实上面的三种方式也是传递数据的几种方式——resolve、reject、return；

- 开头的Promise

  必须通过resolve、reject返回值；

- then

  可以通过 `return new Promise() + resolve|reject` 的方式返回值，这是用来顺序执行多个异步任务的方式，也即用来解决回调地狱的主要方式。

  也可以通过 `return result;` 的方式返回值。

### 并行执行一系列异步任务

除了串行执行若干异步任务外，Promise还可以并行执行异步任务。

#### 同时返回多个异步任务的返回结果

试想一个页面聊天系统，我们需要从两个不同的URL分别获得用户的个人信息和好友列表，这两个任务是可以并行执行的，用 `Promise.all()` 实现如下：

```js
let p1 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 500, 'P1');
});

let p2 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 600, 'P2');
});

// 同时执行p1和p2，并在它们都完成后执行then:
Promise.all([p1, p2]).then(function(results) {
  console.log(results); // 获得一个Array: ['P1', 'P2']
});
```

注意：

1. Promise.all() 的参数是一个 **数组**，并且数组中的项都是 **new Promise() 对象**。

2. `Promise.all([p1, p2]).then(function(results) {});` results 是一个 **数组**。

3. 即then的执行方式，

  如果都是 resolve，那么就调用then方法中的第一个参数。

  如果仅仅存在一个reject，那就只会处理那一个reject，resolve的部分不会处理。

  - {% asset_img 'promise.all-1.png' '仅仅存在一个reject时' %}

  如果两个都是reject，

  1. 当返回的时间不同的时候，那就只会处理先返回的那个reject，后一个reject不会处理。

    {% asset_img 'promise.all-2.png' '两个reject，返回时间不同' %}

  2. 当返回的时间相同的时候，也只会处理一个，但是是处理源代码中位置靠前的那一个(和在all参数中的位置无关)。

    {% asset_img 'promise.all-3.png' '三个reject，返回时间相同，在源码中的位置不同' %}

    {% asset_img 'promise.all-4.png' '三个reject，返回时间相同，在源码中的位置不同' %}

    {% asset_img 'promise.all-5.png' '三个reject，返回时间相同，在源码中的位置不同' %}

4. then的执行时间，

  1. 当两个都是 resolved 的时候，那就要等到都变为 resolved 才会执行 then 方法。

  2. 当一个是 rejected、一个是 resolved 的时候，

    - 如果rejected那个先执行，那么就立刻执行 then 方法。
    - 如果resolved那个先执行，那么就等到 rejected 那个执行完再执行 then 方法。

  3. 当都是 rejected 的时候，

    - 返回时间不同的话，当有一个先 rejected 了就立刻执行 then 方法；
    - 返回时间相同的话，先执行源码中位置靠前的。

#### 容错的多个异步任务

有些时候，多个异步任务是为了容错。比如，同时向两个URL读取用户的个人信息，只需要获得先返回的结果即可。这种情况下，用 `Promise.race()` 实现:

```js
let p1 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 500, 'P1');
});

let p2 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 600, 'P2');
});

Promise.race([p1, p2]).then(function(result) {
  console.log(result); // 'P1'
});
```

注意：

1. then 的执行方式——

  无论都是两个 resolve，还是都是两个 reject，或者是一个是 resolve、一个是 reject，

  - 看谁先返回就先处理谁。
  - 如果同时返回的话，就处理源代码中位置靠前的。

2. then 的执行时间——

  如果有先返回的，就立刻执行 then 进行相关的处理，不用等待。

  如果相同时间的话，就处理源代码中位置靠前的。

## Promise 的应用

### Promise 的适用场景

Promise 因回调地狱的问题而出现，因此Promise适用来解决回调地狱的问题。

### 网易面试题

> 现在有三个 [异步接口]，分别是
1. getTodayUser： 获取当天用户id，callback返回userId
2. getTodayMovie: 获取当天的电影id，callback返回movieId
3. bookMovieForUser 为用户预定电影，参数是userId和movieId
现在要实现，一个接口bookTodayMovieForTodayUser，为当天用户预定当天电影

> getTodayUser(function(userId) {
  // 获得当天的预定客户
});

> getTodayMovie(function(movieId) {
  // 获得当天的电影
});

> bookMovieForUser(userId, movieId, function(isDone) {
});

> // 根据以上接口封装这个函数
bookTodayMovieForTodayUser(function(isDone) {
  // 为今天预定客户预定当天影片
  alert('预定成功');
});

解答(传统解答):

```js
function bookTodayMovieForTodayUser(callback) {
  let ids = {};

  function check() {
    if (typeof ids.userId !== 'undefined' && typeof ids.movieId !== 'undefined') {
      bookMovieForUesr(ids.userId, ids.movieId, function(isDone) {
        callback(isDone);
      });
    }
  }

  getTodayUser(function(userId) {
    ids.userId = userId;
    check();
  });

  getTodayMovie(function(movieId) {
    ids.movieId = movieId;
    check();
  });
}

bookTodayMovieForTodayUser(function(isDone) {
  alert('预定成功');
});
```

解答2:

```js
function bookTodayMovieForTodayUser(callback) {
  let userPromise = new Promise(function(resolve, reject) {
    getTodayUser(function(userId) {
      resolve(userId);
    });
  });

  let moviePromise = new Promise(function(resolve, reject) {
    getTodayMovie(function(movieId) {
      resolve(movieId)
    });
  });

  Promise.all([userPromise, moviePromise]).then(function([userId, movieId]) {
    return new Promise(function(resolve, reject) {
      bookMovieForUser(userId, movieId, function(isDone) {
        resolve(isDone);
      });
    });
  })
  .then(callback)
  .catch(e => console.log(e));
}

bookTodayMovieForTodayUser(function(isDone) {
  alert('预定成功');
});
```

解答2优化:

```js
function convertToPromise(fn) {
  return function() {
    let args = [].slice.call(arguments);

    return new Promise(function(resolve, reject) {
      let callback = function(result) {
        resolve(result);
      };
      args.push(callback);

      fn.apply(undefined, args);
    });
  };
}

function bookTodayMovieForTodayUser(callback) {
  let userPromise = convertToPromise(getTodayUser);
  let moviePromise = convertToPromise(getTodayMovie);
  let bookPromise = convertToPromise(bookTodayMovieForTodayUser);

  Promise.all([userPromise(), moviePromise()]).then(function([userId, movieId]) {
    return bookPromise(userId, movieId);
  }).then(callback);
}

bookTodayMovieForTodayUser(function(isDone) {
  alert('预定成功');
});
```

## References

- [廖雪峰Promise](http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014345008539155e93fc16046d4bb7854943814c4f9dc2000)
- [前端基础进阶（十三）：透彻掌握Promise的使用，读这篇就够了](http://www.jianshu.com/p/fe5f173276bd)
- [5个经典的前端面试题-网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1003674021#/learn/live?lessonId=1004206346&courseId=1003674021)
