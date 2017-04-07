---
title: 使用 jQuery 发送 jsonp请求
date: 2017-04-06 12:08:42
categories: ['技术', '前端技术']
tags: ['jQuery']
---

## 示例和参数简介

### 示例一 $.ajax()

{% codepen SPxiaomin mWYJgx 0 js 265 %}

```
示例请求url: https://api.douban.com/v2/movie/subject/26260853?callback=jsonpCallback&_=1491451234603
url: 设置发送请求的 url；
type: 请求使用的 HTTP 方法；
dataType: 你期待从服务器返回的数据的类型；
jsonp: 设置上面示例url中 query string 的 callback；
jsonpCallback: 设置上面示例url中 query string 的 jsonpCallback；
success: 请求成功时调用的函数；
```

### 示例二 $.getJSON()

{% codepen SPxiaomin NpVRMg 0 js 265 %}

### 上面两种方式的区别

其实 `$.getJSON` 本质上如下——

```
$.ajax({
    url: url,
    dataType: 'json',
    data: data,
    success: success
    });
```

当在 url 中添加了 `?callback=?` 等类似的 `query string` 之后，请求就变为了 jsonp。那和 `$.ajax` 进行 jsonp 请求的区别何在呢？在 `$.ajax` 中可以通过 `jsonpCallback` 参数自定义回调函数的名称(不然的话就是 jQuery 每次请求时随机生成的函数名)，再通过设置 `cache: true` 之后，就可以进行 `GET` 缓存了，但是这在 `$.getJSON` 方式中是做不到的。

## 实现原理

jQuery 实现 jsonp 跨域请求的原理是通过动态加载 script 实现的，允许用户传递一个 callback 参数给服务端，然后服务端返回数据时会将这个 callback 参数作为函数名来包裹住 JSON 数据。

### 原生 js 实现示例

{% codepen SPxiaomin ryEBbN 0 js 265 %}

## ajax 与 jsonp

从上面的代码可以看出，jQuery 将 ajax & jsonp 都封装在了一个 api 中了。但是，ajax 和 jsonp 其实本质上是不同的东西，ajax 的核心是通过 XMLHttpRequest 获取非本页的内容，而 jsonp 的核心则是动态添加 `<script>` 标签来调用服务器提供的 js 脚本。

所以说，其实 ajax 与 jsonp 的区别不在于是否跨域，ajax 通过服务器端的配置一样可以实现跨域，jsonp 本身也不排斥同域的数据的获取。

## 参考

- [说说JSON和JSONP，也许你会豁然开朗，含jQuery用例](http://www.cnblogs.com/dowinning/archive/2012/04/19/json-jsonp-jquery.html)
- [jQuery.ajax()](http://api.jquery.com/jquery.ajax/)
- [jQuery.getJSON()](http://api.jquery.com/jQuery.getJSON/)

END.
