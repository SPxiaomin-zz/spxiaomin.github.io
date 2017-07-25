---
title: JavaScript异步编程之Generator
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
