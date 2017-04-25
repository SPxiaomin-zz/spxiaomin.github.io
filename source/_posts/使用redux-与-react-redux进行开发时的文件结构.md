---
title: 使用redux 与 react-redux进行开发时的文件结构
date: 2017-04-25 19:36:09
categories: ['技术', '前端技术']
tags: ['react', 'redux']
---

## 只使用redux进行开发

```
/actions
- /index.js
/reducers
- /index.js
/components
- /Counter.js
index.js
```

详细示例代码-<https://github.com/SPxiaomin/React/tree/master/react-redux-counter>

## 使用 redux & react-redux 进行开发

```
/actions
- index.js
/reducers
- index.js
/components
- App.js
- Change.js
- Hello.js
/ containers
- ClickChange.js
- VisibleHello.js
index.js
```

详细示例代码-<https://github.com/SPxiaomin/React/tree/master/react-redux-es6-quickstart>

END.
