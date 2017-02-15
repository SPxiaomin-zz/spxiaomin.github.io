---
title: JavaScript性能优化のthrottle及实战应用
date: 2017-02-14 21:20:12
categories: ['技术', '前端技术']
tags: ['javascript', '性能优化']
---

## 需要节流(throttle)的缘由

浏览器中某些计算和处理要比其它的昂贵很多。比如，DOM操作比起非DOM交互需要更多的内存和CPU时间。连续尝试进行过多的DOM相关操作可能会导致浏览器挂起，有时候甚至会崩溃。尤其在IE中使用 onresize 事件处理程序的时候容易发生，当调整浏览器大小的时候，该事件会连续触发。在 onresize 事件处理程序内部如果尝试进行DOM操作，其高频率的更改可能会让浏览器崩溃。为了绕开这个问题，你可以使用定时器对该函数进行节流。

## 节流(throttle)背后的基本思想

函数节流背后的基本思想是指，某些代码不可以在没有间断的情况连续重复执行。第一次调用函数，创建一个定时器，在指定的时间间隔之后运行代码。当第二次调用该函数时，它会清除前一次的定时器并设置另一个。如果前一个定时器已经执行过了，这个操作就没有任何意义。然而，如果前一个定时器尚未执行，其实就是将其替换为一个新的定时器。目的是只有在执行函数的请求停止了一段时间之后才执行。

## 节流的使用方式

```javascript
function throttle(method, context) {
    clearTimeout(method.tId);
    method.tId = setTimeout(function () {
        method.call(context);
    }, 100); // 100 可以根据实际情况自己改成其他值
}
```

throttle() 函数接受两个参数: 要执行的函数以及在哪个作用域中执行。如果没有给出第二个参数，那么就在 `全局作用域内` 执行该方法。

## 使用节流解决resize事件的问题

假设有一个 `<div />` 元素需要保持它的高度始终等同于宽度。那么实现这一功能的JavaScript如下:

```javascript
window.onresize = function() {
    var div = document.getElementById('myDiv');
    div.style.height = div.offsetWidth + 'px';
};
```

这段非常简单的例子有两个问题可能会造成浏览器运行缓慢。首先，要计算 offsetWidth 属性，如果该元素或者页面上其它元素有非常复杂的CSS样式，那么这个过程将会很复杂。其次，设置某个元素的高度需要对页面进行回流来令改动生效。如果页面有很多元素同时应用了相当数量的CSS的话，这又需要很多计算。因此，如果在极短的时间内进行过多的计算，就可能导致浏览器挂起，有时候甚至会崩溃。

用throttle()函数来解决如下:

```javascript
function resizeDiv() {
    var div = document.getElementById('myDiv');
    div.style.height = div.offsetWidth + 'px';
}

window.onresize = function() {
    throttle(resizeDiv);
};
```

## 节流的实战应用

{% codepen SPxiaomin WRLWEj 0 result 265 %}

## 参考

- JavaScript高级程序设计(第3版)

END.
