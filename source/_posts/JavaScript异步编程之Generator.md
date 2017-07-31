---
title: JavaScript异步编程之Generator&async/await
date: 2017-07-25 22:22:04
categories: ['技术', '前端技术']
tags: ['javascript']
---

## Generator 入门示例

```javascript
function* gen(x) {
  let y = yield x + 2;
  return y;
}

let g = gen(1);
g.next(); // { value: 3, done: false }
g.next(2); // { value: 2, done: true }
```

## Generator 异步实例

```javascript
const fetch = require('node-fetch');

function* gen() {
  const url = 'https://api.github.com/users/github';
  let result = yield fetch(url);
  console.log(result.bio);
}

let g = gen();
let result = g.next();

result
  .value
  .then(data => data.json())
  .then(result => g.next(result));
```

```javascript
// await 版
const fetch = require('node-fetch');

async function gen() {
  const url = 'https://api.github.com/users/github';
  let temp = await fetch(url);
  let result = await temp.json();
  console.log(result.bio);
}

gen();
```

## Async 入门示例

```javascript
function foo() {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, 3000, 30);
  });
}

async function fn() {
  try {
    let t = await foo();
    console.log(t);
    console.log('next code');
  } catch (e) {
    console.log(e);
  }
}

fn();
// 30
// next code
```
