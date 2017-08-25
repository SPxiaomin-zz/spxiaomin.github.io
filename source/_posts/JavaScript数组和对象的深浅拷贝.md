---
title: JavaScript数组和对象的深浅拷贝
date: 2017-08-23 10:17:02
categories: ['技术', '前端技术']
tags: ['javascript']
---

浅拷贝指的是——对于基本类型，就会拷贝一份，互不影响；但是对于引用类型的话，就 **只会拷贝引用**。

深拷贝指的是——对于基本类型，就会拷贝一份，互不影响；对于引用类型的话，**完全的进行拷贝，互不影响**。

<!-- more -->

## 数组

### 数组的浅拷贝

ES5:

```js
let arr = [{ old: 'old' }, ['old']];

// 1.
let newArr = arr.concat();

// 2.
let newArr = arr.slice();
```

ES6:

```js
let arr = [{ old: 'old' }, ['old']];

// 1.
let newArr = [...arr];

// 2.
let newArr = Array.from(arr);

// 3.
let newArr = [...arr.values()];
```

## 数组和对象

### 数组和对象的浅拷贝

```js
function shallowCopy(obj) {
  // 如果不是 object 类型，就不进行拷贝
  if (typeof obj !== 'object') return;

  // 根据obj的类型判断是新建一个数组还是对象
  let newObj = Array.isArray(obj) ? [] : {};

  // 遍历obj，并且判断是obj的属性才拷贝
  for (let prop in obj) {
    if (obj.hasOwnProperty(prop)) {
      newObj[prop] = obj[prop];
    }
  }

  return newObj;
}
```

### 数组和对象的深拷贝

```js
function deepCopy(obj) {
  if (typeof obj !== 'object') return;

  let newObj = Array.isArray(obj) ? [] : {};

  for (let prop in obj) {
    if (obj.hasOwnProperty(prop)) {
      newObj[prop] = typeof obj[prop] === 'object'
        ? deepCopy(obj[prop])
        : obj[prop];
    }
  }

  return newObj;
}
```

除了通过上面的方式进行深拷贝，还可以通过如下的方式(但是缺点是 **不能拷贝函数**)——

```js
let arr = [{ old: 'old' }, ['old']];
let newArr = JSON.parse( JSON.stringify(arr) );
```

## References

- [JavaScript专题之深浅拷贝](https://juejin.im/post/59658504f265da6c415f3324)

END.
