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

## 遍历

### 遍历数组

each，为每一个匹配的元素运行指定的函数，如果 `return false` 的话，可以提早终止循环。

Syntax
```javascript
$(selector).each(function(index, element));
// 如果想要获得当前元素的话，也可以通过 `this`，不过这是DOM对象，转换为jQuery对象需要这样 `$(this)`。
```

{% codepen SPxiaomin NdeyOe 0 js 265 %}
