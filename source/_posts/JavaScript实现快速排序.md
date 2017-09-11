---
title: JavaScript实现快速排序
date: 2017-02-16 07:46:11
categories: ['技术']
tags: ['javascript', '算法', '排序']
---

```js
function quickSort(arr) {
  if (arr.length <= 1) return arr;

  const tempArr = arr.concat();

  /**
   * 中间数的索引值有两种获取的方式(下面的两种方式都是可行的，可以通过从 arr.length = 0 or 偶数 or 奇数 三个方面进行对比):
   * 1. Math.floor(arr.length / 2);
   * 2. Math.floor((left + right) / 2); left = 0; right = arr.length - 1;
   */
  const mid = Math.floor(tempArr.length / 2);
  const midItem = tempArr.splice(mid, 1);

  const left = [];
  const right = [];
  tempArr.forEach((item) => {
    if (item < midItem) {
      left.push(item);
    } else {
      right.push(item);
    }
  });

  return quickSort(left).concat(midItem, quickSort(right));
}
```

References

- [JavaScript算法详解——快速排序](https://segmentfault.com/a/1190000000669157)

<!-- more -->
