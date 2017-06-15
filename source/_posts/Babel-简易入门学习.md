---
title: Babel 简易入门学习
date: 2017-06-15 17:29:38
categories: ['技术', '前端技术']
tags:
---

## 认识 Babel

作为一种语言，JavaScript 在不断发展，各种新标准和提案层出不穷，但是由于浏览器的多样性导致有可能几年之内都无法广泛普及，而 Babel 可以让你提前使用这些语言特性，它是一种多用途的 JavaScript 编译器，它把最新版本的 JavaScript 编译成当下可以执行的版本。简而言之，利用 Babel 就可以让我们在当前的项目中随意地使用这些最新的 ES6 语法特性。

<!-- more -->

### Babel CLI

通过使用Babel CLI可以在命令行中使用Babel编译。

```bash
$ npm install babel-cli -g
$ babel es6.js -o compiled.js
```

## 配置

Babel 是通过安装插件(plugin)或者预设(preset, 就是一组设定好的插件)来编译代码的。

```json
{
  "presets": ["es2015"],
  "plugins": ["transform-object-rest-spread"]
}
```

Babel 的核心概念就是利用一系列的 plugin 来管理编译规则，通过不同的 plugin，它不仅可以编译 ES6 代码，还可以编译 React JSX 语法或者是 CoffeeScript 等，甚至可以使用还在提案阶段的一些特性，这就足以看出它的可扩展性和易用性等魔力。

## References

- 《React 全栈》

END.
