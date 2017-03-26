---
title: React与传统前端开发的比较
date: 2017-03-25 21:53:51
categories: ['技术', '前端技术']
tags: ['react']
---

凡事都有动机，在开始使用 React 之前，首先要搞清楚一件事: React 到底给前端开发带来了什么改变，是什么支撑我们接受这样一个新事物的学习成本，把它的方案引入到工作中。

<!-- more -->

以一个可选列表(单选)为例，列表由多个列表项组成，每个列表项有选中状态和普通状态，单击某项则选中该项。最多可选中一项，即选中某项后先前的选中项变回普通状态。

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

<!-- stop writing here -->
