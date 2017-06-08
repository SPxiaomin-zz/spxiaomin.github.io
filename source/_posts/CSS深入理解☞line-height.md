---
title: CSS深入理解☞line-height
date: 2017-06-07 16:13:17
categories: ['技术', '前端技术']
tags: ['css']
---

## line-height的定义

line-height，行高，两行文字基线之间的距离。

{% asset_img 'line-height_baseline.png' 'line-height与基线的关系' %}

### 什么是基线？

学习英语的时候，英语本子上的红线，那条红线就是这里的基线。

{% asset_img 'baseline.png' '英语本中的基线' %}

或者可以说是微软雅黑字体中字母 **x** 下边缘的位置。

{% asset_img 'x-baseline.png' '基线可以说是微软雅黑字体中字母x的下边缘' %}

如果是其他的字体的话，那就不一定是字母 **x** 下边缘的位置。

{% asset_img 'baseline_font.png' '基线的具体位置和字体也是有关系的' %}

## line-height与行内框盒子模型

行内框盒子模型是非常重要的一个东西，因为所有内联元素的样式表现都与行内框盒子模型有关！！！

{% asset_img 'inline-box-model.png' '一个包含4种盒子的例子' %}

总共四种盒子:

1. 内容区域(content area)；
2. 内联盒子(inline boxes)；
3. 行框盒子(line boxes)；
4. 包含盒子(containing box)；

其中4包含3，3包含2，2和1的关系说不清。

### 4种盒子

1. "内容区域" (content area)，是一种围绕文字看不见的盒子。"内容区域" (content area)的大小与 `font-size` 大小相关，与 `line-height` 无关。

  那么既然看不见，我们还怎么学习呢？张大大将其理解为选中文字时候的区域就是 "内容区域"。

  {% asset_img 'content-area.png' '内容区域' %}

2. "内联盒子" (inline boxes)

  {% asset_img 'inline-boxes.png' '内联盒子' %}

3. "行框盒子" (line boxes)

  {% asset_img 'line-boxes.png' '行框盒子' %}

  上面图片中的 `p` 元素，如果其中有一个 `<br>` 换行或者是当前行容纳不了这么多文字，那么就会换行，这个时候就有两个 `line box` 了。

  上面的行框盒子包括了三个 "内联盒子" (inline boxes)。

4. "包含盒子" (containing box)

  {% asset_img 'containing-box.png' '包含盒子' %}

## line-height的高度机理

内联元素的高度是由 **line-height** 决定的。不是由字体撑开的。

{% codepen SPxiaomin bRVojB 0 result 265 %}

但是有一点是要注意的，内联元素的高度是由 **line-height** 决定的，但是就算line-height的值为0，也不会改变字体的基线位置，它只是改变了两行文字基线之间的距离&内联元素的高度而已。

{% codepen SPxiaomin zzvppN 0 result 265 %}

这个时候问题就来了——line-height明明是两行文字基线距离，单行文字哪来行高，都没有两个基线，还控制了高度？其实啊：

{% asset_img 'behind.png' '高度的真正表现' %}

也就是说只不过刚好如下的公式成立：

```
内容区域高度(content area) + 行间距(vertical spacing) = 行高(line-height)
```

行间距在内容区域的上下进行均分，因此就有了 “半行间距”。简言之，行间距墙头草，可大可小(甚至负值)，保证高度正好等同于行高。

### 内容区域(content area)

关于 "内容区域" (content area) 的讲解如下图：

{% asset_img 'content-area-height.png' '内容区域(content area)高度的决定因素' %}

看两个关于 "内容区域" (content area) 的例子：

{% asset_img 'content-area-example1.png' '内容区域(content area)示例1' %}

{% asset_img 'content-area-example2.png' '内容区域(content area)示例2' %}

### 行框盒子的高度与内联盒子高度的关系

如果行框盒子(line box)里面有多个不同行高的内联盒子，那么高度表现会是什么样？是由行高最高的那个内联盒子决定吗？

答案是似是而非。看下面的例子就知道了：

{% codepen SPxiaomin GEpQrV 0 result 265 %}

### 包含盒子(containing box)

含多个行框盒子的包含容器的高度，多行文本的高度就是单行文本高度累加。

## line-height各类属性值

### normal

默认属性值。跟着用户的浏览器走，且与元素字体关联。

由于初始值 normal 在不同的浏览器中，表现都是不一致的，具有非常的不确定性，所以实际开发的时候一般会在 body 进行全局设置，保证各个浏览器一致。

### `<number>`

使用数值作为行高值，例如 `line-height: 1.5;`。

根据 **当前元素** 的font-size大小计算。

### `<length>`

使用具体长度值作为行高值，例如 `line-height: 1.5em;`(相对单位) or `line-height: 15px`(固定单位)。

如果是相对单位的话，是相对于 **设置了该line-height属性的元素** 的font-size大小计算。

### `<percent>`

使用百分比值作为行高值。例如 `line-height: 150%;`。

相对于 **设置了该line-height属性的元素** 的font-size大小计算。

### inherit

行高继承。

input框等元素默认行高是normal，使用inherit可以让文本框样式可控性更强。

### 来个对比吧！

line-height: 1.5，line-height: 150%，line-height: 1.5em，三者有什么区别？

如果从计算上面来讲是没有什么差别的，假设设置了该line-height属性的元素的font-size:20px，那么都计算出来30px。那么差别在什么地方呢？

1. `line-height: 1.5` 所有可继承元素根据font-size重计算高度；
2. `line-height: 150%/1.5em` 当前元素根据font-size计算行高，继承给下面的元素；

## line-height与图片的表现

行高 **不会** 影响图片实际占据的高度！！！实际上line-height改变的是文字的高度，然后基线对齐，就产生了空隙。简单就是说 line-height&vertical-align 共同起了作用，图片所占据的高度还是它原本的高度。

因为inline水平元素默认 `vertical-align: baseline`，也就是基线对齐，所以图片和包含盒子之间会有空隙。

但是后面没有文字呀？是什么情况？其实呢，存在看不见的隐匿文本节点，其实在规范当中是称为 `strut`。

{% asset_img 'line-height_hidden-text.png' '隐匿文本节点' %}

### 如何消除图片底部间隙？

1. 图片块状化 — 无基线对齐

  ```css
  img {
    display: block;
  }
  ```

  因为 `vertical-align` 属性只是适用于 `inline` or `inline-block` 的元素，所以就没有什么基线对齐的情况，进而也就没有了间隙的问题。

2. 图片底线对齐

  ```css
  img {
    vertical-align: bottom;
  }
  ```

3. 行高足够小

  ```css
  .box {
    line-height: 0;
  }
  ```

## line-height 的应用

### 单行文本垂直居中

END.
