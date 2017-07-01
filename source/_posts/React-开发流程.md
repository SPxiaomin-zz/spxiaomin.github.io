---
title: React 开发流程
date: 2017-06-12 19:32:54
categories: ['技术', '前端技术']
tags: ['react']
---

## 准备工作

1. npm init -y

2. 构建目录

  {% asset_img 'directory.png' '初始化目录结构' %}

3. 配置 webpack && babel

  安装依赖:

  - webpack

    ```
    npm i -D webpack webpack-dev-server
    ```

  - es6 & react

    ```
    npm i -D babel-core babel-loader babel-polyfill babel-p reset-env babel-preset-react react-hot-loader

    npm i -S react react-dom
    ```

  - css

    ```
    npm i -D css-loader style-loader sass-loader node-sass
    ```

  - html

    ```
    npm i -D html-webpack-plugin
    ```

4. 编写 Hello World! 运行示例。

###

### 目录结构

### 文件内容顺序

1. 导入 node_modules 中的内容；
2. 导入 css；
3. 导入 自定义组件；
4. 导入自定义的一些东西，比如 utils；

## 实际编码

### Break The UI Into A Component Hierarchy

> 依据单一职责原理进行划分组件，也就是，一个组件理想状态下应该仅仅只做一件事。

分好组件，命好名称。

### 写组件(静态数据)

1. 全部组件单独写，填充假数据。

2. 组合组件，通过 props 传递数据。

### 设置 state

#### 找出 state

Let's go through each one and figure out which one is state. Simply ask three questions about each piece of data:

1. Is it passed in from a parent via props? If so, it probably isn't state.
2. Does it remain unchanged over time? If so, it probably isn't state.
3. Can you compute it based on any other state or props in your component? If so, it isn't state.

#### 找出 state 的存放位置。

For each piece of state in your application:

1. Identify every component that renders something based on that state.
2. Find a common owner component (a single component above all the components that need the state in the hierarchy).
3. Either the common owner or another component higher up in the hierarchy should own the state.
4. If you can't find a component where it makes sense to own the state, create a new component simply for holding the state and add it somewhere in the hierarchy above the common owner component.

Cool, so we've decided that our state lives in FilterableProductTable. First, add an instance property this.state = {filterText: '', inStockOnly: false} to FilterableProductTable's constructor to reflect the initial state of your application. Then, pass filterText and inStockOnly to ProductTable and SearchBar as a prop. Finally, use these props to filter the rows in ProductTable and set the values of the form fields in SearchBar.

### 写交互

### 从后端拉取数据

---



---

# webpack

npm init --yes

npm i -g webpack webpack-dev-server

## 安装配置 Babel

```bash
$ npm i --save-dev babel-core babel-loader
$ npm i --save-dev babel-preset-es2015 babel-preset-react
```

```json
{
  "presets": ["es2015", "react"]
}
```

## 安装配置 ESLint

```bash
$ npm i --save-dev eslint eslint-loader
$ npm i --save-dev eslint-plugin-import eslint-plugin-react eslint-plugin-jsx-a11y
$ npm i --save-dev eslint-config-airbnb
```

```json
{
  "extends": "airbnb"
}
```
