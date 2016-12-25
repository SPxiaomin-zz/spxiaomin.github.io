---
title: 使用gulp实现nodejs自动化运行
date: 2016-12-13 20:48:26
categories: ['技术', '前端技术']
tags: ['nodejs', 'gulp']
---

## 编写自动化脚本

```javascript gulp.js
const gulp = require('gulp');
const shell = require('gulp-shell');
const nodemon = require('gulp-nodemon');

gulp.task('node', shell.task([
    'clear',
    'echo \n',
    'node index.js',
    'echo \n'
]));

gulp.task('watch', () => {
    gulp.watch('index.js', ['node']);
});

gulp.task('default', ['watch']);

gulp.task('server', () => {
    nodemon({
        script: server.js
    });
});
```

```json package.json
{
    ...
    "scripts": {
        "start": "gulp",
        "server": "gulp server"
    }
    ...
}
```

## 运行

```shell
$ npm run start
or
$ npm run server
```
