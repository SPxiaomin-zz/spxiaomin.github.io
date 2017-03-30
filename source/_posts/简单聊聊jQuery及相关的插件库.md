---
title: 简单聊聊jQuery及相关的插件库
date: 2017-03-28 16:34:39
categories: ['技术', '前端技术']
tags: ['jQuery']
---

在本文将先简单地介绍一下 jQuery 所包含的知识分支及相关分支的用途，然后介绍一下 jQuery UI/jQuery EasyUI/jQuery Mobile 和 jQuery 的关系，以及 zepto 与 jQuery 的关系。

<!-- more -->

## jQuery 知识分支

jQuery 主要的话，包含如下的六大部分：

1. 选择器和样式、属性；

    这一块的话，负责一些基础性的操作——获取元素的引用，然后进行样式和属性的操作。

2. DOM；

    这一块包含 DOM 的创建、插入、删除、复制和替换、遍历。

3. 事件；

    这一块是处理用户交互的关键，包括鼠标事件、表单事件、键盘事件、事件的绑定和解绑、事件对象的使用、事件的触发。

4. 动画；

    这一块包含的是动画效果——显示和隐藏、上卷和下拉、淡入和淡出、自定义动画和停止动画。

5. Ajax；

    这一块包含的是Ajax的相关操作。

6. 插件和一些核心方法。

    插件方法有 `$.plugin` & `$.fn.plugin`。

## 谈谈 jQuery 的相关插件库

### jQuery UI

jQuery UI 是建立在 jQuery 之上的一个库，主要分为 3 个部分，交互、微件和效果库：

- 交互：这里都是一些与鼠标交互相关的内容。
- 微件：这里主要是一些界面的扩展。
- 效果库：此库用于提供丰富的动画效果。

### jQuery EasyUI

jQuery　EasyUI 是一个基于 jQuery 的框架，集成了各种用户界面插件。

### jQuery Mobile

jQuery Mobile 是一个基于 jQuery 的移动应用界面开发框架。

### 以上三者的区别

UI & EasyUI 和 Mobile 的定位不同：前两者常用于开发桌面 Web 应用，后者用于开发移动应用。

UI 和 EasyUI 的区别：前者是由 jQuery 官方进行开发的，后者是第三方开发的，并且对私免费、对公收费的。后者的组件比前面的组件要更加全面和丰富。

## zepto 与 jQuery

<!-- stop writing here -->

END.
