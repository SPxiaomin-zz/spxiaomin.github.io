---
title: JavaScript中任意类型转换为Boolean类型规则
date: 2017-08-08 15:18:17
categories: ['技术', '前端技术']
tags: ['javascript']
---

| 数据类型 | 转换为true的值 | 转换为false的值 |
| --- | --- | --- |
| Number 类型 | 任何非0数字值(包括无穷大) | 0和NaN |
| String 类型 | 任何非空字符串 | 空字符串 |
| Object 类型 | 任何对象 | null |
| undefined 类型 | n/a | undefined |

可以通过 `Boolean()` 来将一个值转换为对应的 Boolean 值。

END.

<!-- more -->
