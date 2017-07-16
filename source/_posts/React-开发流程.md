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
    npm i -D babel-core babel-loader babel-polyfill babel-p reset-env babel-preset-react react-hot-loader@next

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

  配置 webpack.config.js & .babelrc

  {% asset_img 'webpack.config.js-1.png' 'webpack.config.js-1' %}

  {% asset_img 'webpack.config.js-2.png' 'webpack.config.js-2' %}

  {% asset_img 'webpack.config.js-3.png' 'webpack.config.js-3' %}

  {% asset_img 'babelrc.png' '.babelrc.png' %}

4. 编写 package.json scripts

  ```
  {
    "build": "webpack",
    "dev": "webpack-dev-server --hot --progress --history-api-fallback --open"
  }
  ```

5. 编写 Hello World! 运行示例，测试能够正常运行＆hot load是否正常运行。

## 实际编码

### 文件内容顺序

1. 导入 node_modules 中的内容；
2. 导入 css；
3. 导入 自定义组件；
4. 导入自定义的一些东西，比如 utils；
5. class

  1. constructor

    1. this.state = {};
    2. this.customMethod = this.customMethod.bind(this);

  2. 自定义方法
  3. componentDidMount
  4. render

6. export

### Break The UI Into A Component Hierarchy

> 依据单一职责原理进行划分组件，也就是，一个组件理想状态下应该仅仅只做一件事。

分好组件，命好名称。并在components目录下建立好相应的目录＆文件。

{% asset_img 'step-1.png' '第一步' %}

### 写组件(静态数据)

1. 全部组件单独写，填充假数据。

  从下而上进行编写，然后组装到一起。

2. 通过 props 传递数据。

### 设置 state

#### 找出 state

Let's go through each one and figure out which one is state. Simply ask three questions about each piece of data:

1. Is it **passed in from a parent via props**? If so, it probably isn't state.
2. Does it **remain unchanged over time**? If so, it probably isn't state.
3. Can you **compute it based on any other state or props** in your component? If so, it isn't state.

#### 找出 state 的存放位置。

For each piece of state in your application:

1. **Identify every component that renders something based on that state.**
2. Find a common owner component (a single component above all the components that need the state in the hierarchy).
3. **Either the common owner or another component higher up in the hierarchy should own the state.**
4. If you can't find a component where it makes sense to own the state, create a new component simply for holding the state and add it somewhere in the hierarchy above the common owner component.

Cool, so we've decided that our state lives in FilterableProductTable. First, add an instance property this.state = {filterText: '', inStockOnly: false} to FilterableProductTable's constructor to reflect the initial state of your application. Then, pass filterText and inStockOnly to ProductTable and SearchBar as a prop. Finally, use these props to filter the rows in ProductTable and set the values of the form fields in SearchBar.

### 写交互

### 从后端拉取数据

通过在 `componentDidMount` 生命周期函数中向远程发送 ajax 请求，然后将获取的数据进行 `setState` 就可以了。

### 最终项目源码

<https://github.com/SPxiaomin/Thinking-in-React>

## References

- [Thinking in React - React](https://facebook.github.io/react/docs/thinking-in-react.html)

END.
