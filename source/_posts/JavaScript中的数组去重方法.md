---
title: JavaScript中的数组去重方法
date: 2017-08-22 22:04:33
categories: ['技术', '前端技术']
tags: ['javascript']
---

```js
let arr = [1, 1, 2, 3];

// 方法1
Array.from(new Set(arr));

// 方法2
[...new Set(arr)];

// 方法3
function dedup(arr) {
  let result = [];

  arr.forEach((item) => {
    result.indexOf(item) === -1 ? result.push(item) : '';
  });

  return result;
}
dedup(arr);
```

END.

<!-- more -->
