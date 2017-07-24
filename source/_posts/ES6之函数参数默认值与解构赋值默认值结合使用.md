---
title: ES6之函数参数默认值与解构赋值默认值结合使用
date: 2017-07-24 10:43:44
categories: ['技术', '前端技术']
tags: ['javascript']
---

## 知识点详解

```js
// 写法一
function m1({x = 0, y = 0} = {}) {
  console.log([x, y]);
}

// 写法二
function m2({x, y} = {x: 0, y: 0}) {
  console.log([x, y]);
}

// 函数没有参数的情况
m1(); // [0, 0]
m2(); // [0, 0]

// x和y都无值的情况
m1({}); // [0, 0]
m2({}); // [undefined, undefined]

// x有值，y无值的情况
m1({x: 3}); // [3, 0]
m2({x: 3}); // [3, undefined]

// x和y都有值的情况
m1({x: 3, y: 3}); // [3, 3]
m2({x: 3, y: 3}); // [3, 3]
```

上面两种写法的区别：上面两种写法都对函数的参数设定了默认值，区别是写法一函数参数的默认值是空对象，但是设置了对象解构赋值的默认值；写法二函数参数的默认值是一个有具体属性的对象，但是没有设置对象解构赋值的默认值。

<!-- more -->

## 实际应用

```js
class Dialog {
  constructor({title = '这是标题', content = '这是内容'} = {}) {
    this.title = title;
    this.content = content;
    this.html = `
      <div class="dialog">
        <div class="dialog-container">
          <div class="dialog-header">${this.title}</div>
          <div class="dialog-content">${this.content}</div>
          <div class="dialog-footer">
            <button class="dialog-button dialog-button-cancel">取消</button>
            <button class="dialog-button dialog-button-confirm">确认</button>
          </div>
        </div>
      </div>
    `;
  }

  // ...
}
```

上面是一个对话框的组件，这是采用的写法一。因为使用组件的人，可能

1. 什么都不传入 `new Dialog()`；
2. 可能传入一个空对象 `new Dialog({})`；
3. 可能只传一个值 `new Dialog({title: '天气'})`；
4. 可能两个值都传 `new Dialog({title: '天气', content: '39.9°'})`；

，但是无论什么情况都必须保证使用组件的人没有明确设置的参数，必须有默认值，不能是 `undefined`，所以只能使用写法一。

```js
// 如果使用es5的写法如下：

class Dialog {
  constructor(config) {
    !config && (config = {});

    this.title = config.title ? config.title : '这是标题';
    this.content = config.content ? config.content : '这是内容';
  }

  // ...
}
```

## References

- [阮一峰es6——函数参数的默认值](http://es6.ruanyifeng.com/#docs/function#函数参数的默认值)

END.
