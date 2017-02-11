---
title: 编写jQuery插件
date: 2017-02-11 10:35:11
categories: ['技术', '前端技术']
tags: ['jquery']
---

```javascript
$.fn.highlight = function() {
    // this 已绑定为当前jQuery对象，因此jQuery对象的方法都可以在函数内运用。

    // 保证链式
    return this;
}
```
