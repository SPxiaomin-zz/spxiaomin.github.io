---
title: React与传统前端开发的比较
date: 2017-03-25 21:53:51
categories: ['技术', '前端技术']
tags: ['react']
---

凡事都有动机，在开始使用 React 之前，首先要搞清楚一件事: React 到底给前端开发带来了什么改变，是什么支撑我们接受这样一个新事物的学习成本，把它的方案引入到工作中。

<!-- more -->

下面以一个可选列表(单选)为例，列表由多个列表项组成，每个列表项有选中状态和普通状态，单击某项则选中该项。最多可选中一项，即选中某项后先前的选中项变回普通状态。

## 传统做法

<https://github.com/SPxiaomin/React/blob/master/react-tab-selector/tab-selector-jquery/index.html>

从上面的代码可以看出，jQuery插件方式，开发者需要考虑两件事情：

1. 组件第一次 Render 出来时的 DOM 构建；
2. 如何切换 UI 上的选中状态；

## 全量更新

<https://github.com/SPxiaomin/React/blob/master/react-tab-selector/tab-selector-jquery/index-1.html>

这一种方法比上一种方法的优势在于，不需要自己去管理 UI 上的选中状态切换。

但是这么做的缺陷比第一种做法更突出：

1. 每次数据变动都要整体重新渲染，性能会非常差，尤其在数据变动频繁、界面复杂时；
2. 每次渲染都重新生成所有的 DOM 节点，那么在这些 DOM 节点上绑定的事件及外部持有的对这些 DOM 节点的引用都将失效；

## 使用 React

<https://github.com/SPxiaomin/React/blob/master/react-tab-selector/src/App.js>

### 和第一种方法的区别

从上面的代码可以看出，在 React 中，我们仅仅只需要考虑整体界面的 DOM 构建和声明数据到视图的转换逻辑，然后每次需要更新的时候调用 `setState` 方法，React 会为我们维护数据的变动，再次触发 `render` 来重构整个页面，自动更新视图。逻辑简单而直接，这一点就解决了第一种方法中存在的问题。

### 和第二种方法的区别

在具体分析之前，首先要说明一点: JSX 内容的渲染结果其实不是真实的 DOM 节点，本质上是 JavaScript 对象的虚拟 DOM 节点，它记录了这个节点的所有信息，可以依据一定的规则生成对应的真实 DOM 节点。

在第二种方法(全量更新)中，每次数据的变动都需要重新构建所有的 DOM。但是在 React 中，每次数据的变动，都只是重新生成虚拟的 DOM 节点(JavaScript 对象)，并且在将虚拟的 DOM 对应生成真实 DOM 节点之前，React 会将虚拟的 DOM 树与先前的进行比较(这里使用了 Diff 算法)，计算出变化的部分，再将变化的部分作用到真实 DOM 上，实现最终界面的更新。React 以额外的计算量换取了对于更新点的自动定位，提高了性能，解决了第二种方法中存在的第一个问题。

在事件绑定与读/写操作都被 React 通过抽象层屏蔽后，业务代码基本无须接触真实 DOM，需要持有引用的场景自然也不复存在，引用失效也就无从说起，这就解决了第二种方法中存在的第二个问题。

## References

- [颠覆式前端UI开发框架：React](http://www.infoq.com/cn/articles/subversion-front-end-ui-development-framework-react)
- 《React 全栈》
