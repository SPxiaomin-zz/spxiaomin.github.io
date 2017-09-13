---
title: JavaScript实现之二分查找
date: 2017-09-11 17:21:59
categories: ['技术']
tags: ['javascript', '算法']
---

## 二分查找法的基本实现

在二分查找法的基本实现中，取 **mid** 值的时候，向上取整和向下取整都是可以的，没有问题。

二分查找法的递归实现:

```js
/**
 * let left = 0;
 * left right = arr.length - 1;
 */
function binarySearch(arr, left, right, target) {
  if (left > right) return -1;

  let mid = Math.floor((left + right) / 2);

  if (arr[mid] < target) {
    return binarySearch(arr, mid + 1, right, target);
  } else if (arr[mid] === target) {
    return mid;
  } else {
    return binarySearch(arr, left, mid - 1, target);
  }
}
```

二分查找法的非递归实现:

```js
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;
  let mid;

  while (left <= right) {
    mid = Math.floor((left + right) / 2);

    if (arr[mid] < target) {
      left = mid + 1;
    } else if (arr[mid] === target) {
      return mid;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```

## 用二分查找法找寻边界值

### 用二分查找法找寻上界值

严格上界:

在用二分查找法找寻上界值的时候，取 **mid** 值的时候，**只能** 够向下取整(如果进行向上取整的话，当left==right-1的时候，并且arr[mid]>target就会进入死循环；e.g. '1 2 3 4 5' 取3的严格上界可以向上取整试试，会进入死循环的)。

```js
function binarySearchUpperBound(arr, target) {
  // 先判断上界是否存在
  if (arr[arr.length - 1] <= target) return -1;

  let left = 0;
  let right = arr.length - 1;
  let mid;
  while (left < right) {
    mid = Math.floor((left + right) / 2);

    if (arr[mid] > target) {
      right = mid;
    } else {
      left = mid + 1;
    }
  }

  return left;
}
```

### 用二分查找法找寻下界值

严格下界

在用二分查找法找寻下界值的时候，取 **mid** 值的时候，**只能** 够向上取整(如果进行向下取整的话，当left==right-1的时候，并且arr[mid] < target就会进入死循环；e.g. '1 2 3 4 5' 取2的严格下界可以向下取整试试，会进入死循环的)。

```js
function binarySearchLowerBound(arr, target) {
  // 检测是否存在严格下界
  if (arr[0] >= target) return -1;

  let left = 0;
  let right = arr.length - 1;
  let mid;
  while (left < right) {
    mid = Math.ceil((left + right) / 2);

    if (arr[mid] < target) {
      left = mid;
    } else {
      right = mid - 1;
    }
  }

  return right;
}
```

### 用二分查找法找寻区域

```js
function searchRange(arr, target) {
  const results = [-1, -1];

  // 1. 先找到严格下界，然后进行判断看是否存在 target；
  let lower = binarySearchLowerBound(arr, target);
  lower += 1;

  // 判断看是否存在 target
  if (arr[lower] === target) {
    results[0] = lower;
  } else {
    return results;
  }

  // 2. 然后找到严格上界，进行取值
  let upper = binarySearchUpperBound(arr, target);
  upper = upper < 0 ? arr.length - 1 : upper - 1;

  // 上面已经判断过是否存在 target 了
  results[1] = upper;

  return results;
}
```

## References

- [segmentfault 二分查找](https://segmentfault.com/a/1190000008584438)
- [常用二分查找模板](http://blog.csdn.net/u012280578/article/details/56844778)
