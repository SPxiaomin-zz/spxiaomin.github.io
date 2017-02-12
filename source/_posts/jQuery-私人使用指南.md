---
title: jQuery 私人使用指南
date: 2017-02-02 09:14:05
categories: ['技术', '前端技术']
tags: ['jQuery']
---

## 创建元素的方式

```js
$('<p>test</p>');

or

var tmp = 'test';
$('<p>' + tmp + '</p>');
```

## 添加新元素或内容的方式

after/before
```js
var body = $('body');

body.after($('<p>test</p>'));
body.after('test');
```

append/prepend
```js
var body = $('body');

body.append($('<p>test</p>'));
body.append('test');
```

appendTo/prependTo
```js
var body = $('body');

$('<p>test</p>').appendTo(body);
// 注意，此方法不能够添加纯文本内容，例如 'test'
```

## attr

### 设置或获取属性

设置 `所有匹配` 的DOM元素

```javascript
$('img').attr('width', '10');

$('img').attr({width: '10', height: '10'});
```

获取 `第一个匹配` 的DOM元素

```javascript
$('img').attr('width');
```

### 删除属性

removeAttr

```javascript
$('p').removeAttr('id class')
```
