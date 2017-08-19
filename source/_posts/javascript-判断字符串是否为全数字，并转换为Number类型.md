---
title: javascript 判断字符串是否为全数字，并转换为Number类型
date: 2017-08-19 10:34:30
categories: ['技术', '前端技术']
tags: ['javascript']
---

```js
function checkStringIsNumberAndConvertToNumber(str) {
  return /^\d+\.?\d*$/.test(str) ? Number(str) : false;
}
```

END.

<!-- more -->
