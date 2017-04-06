---
title: 使用 jQuery 发送 jsonp请求
date: 2017-04-06 12:08:42
categories: ['技术', '前端技术']
tags: ['jQuery']
---

## 示例和参数简介

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

## 实现原理

jQuery 实现 jsonp 跨域请求的原理是通过动态加载 script 实现的，允许用户传递一个 callback 参数给服务端，然后服务端返回数据时会将这个 callback 参数作为函数名来包裹住 JSON 数据。

END.
