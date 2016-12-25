---
title: css权重
date: 2016-11-27 20:17:30
categories: ['技术', '前端技术']
tags: ['css', '权重']
---

## 权重定义

权重决定了哪一条规则会被浏览器应用在元素上。当很多的规则被应用到某一个元素上时，权重是一个决定哪种规则生效，或者是优先级的过程。

## 权重的用处

有时候你会发现自己辛辛苦苦写的CSS样式不起作用，文件引入了，浏览器也加载了，但就是不按照你想要的方式显示，这个时候你就要考虑CSS权重的问题。

## 权重的计算

1. 权重的级别根据选择器被划分为四个分类:

    1. 行内样式
    2. id
    3. 类、属性、伪类
    4. 元素、伪元素（伪元素选择器只包含: ::after, ::before, ::first-letter, ::first-line, ::selection）

2. 权重的计算方法

    A: 如果规则是写在标签的style属性中（内联样式），则 A=1，否则，A=0。（对于内联样式，由于没有选择器，所以 B、C、D 的值都为0，即 A=1，B=0，C=0，D=0，简写为1,0,0,0)

    B: 计算该选择器中 ID 的数量。（例如，#header 这样的选择器，计算为 0，1，0，0）。

    C: 计算该选择器中伪类及其它属性的数量（包括类选择器、属性选择器等，不包括伪元素）。（例如，.logo[id='site-logo'] 这样的选择器，计算为 0，0，2，0）。

    D: 计算该选择器中伪元素及标签的数量。（例如，p:first-letter 这样的选择器，计算为 0，0，0，2）。

3. 权重值的比较

    根据上面的权重计算方法，分为 A、B、C、D 四组值，从左到右，分组比较，比较同一组的个数，数量多的优先级高。如果同一组的数量相同，则比较下一组的值。如果全部组的数量都相同，则后定义的优先。

    举例如下:

    ```css
        /* 样式一 */
        body header div nav ul li div p a span em {
            color: red;
        }

        /* 样式二 */
        .count {
            color: blue;
        }

        样式一的四组值分别是 0,0,0,11，样式二的四组值分别是 0,0,1,0 。样式二和样式一的 A、B 相同，而样式二的 C 大于样式一，所以，不管 D 的值如何，样式二权重值都大于样式一。所以应用了上面样式的元素应该是蓝色的。
    ```

4. 权重的级别

    根据鬼哥的文章说道，权重比较的级别可以分为: `important > 内联 > ID > 类|伪类|属性选择 > 标签|伪元素 > 通配符 > 继承。

    其实上面的权重比较还可以这样解释: 比较同一级别的个数，数量多的优先级高，如果相同即比较下一级别的个数。

## 注意

1. 通配符选择器、继承来的样式，他们的权重以 0，0，0，0 来计算。不过通配符选择器的样式权重级别要高于继承来的样式。

    如下例:

    {% codepen SPxiaomin aZvLqV 0 css 265 %}

    其实简单的就是说，继承而来的属性值，权重永远低于明确指定到元素的定义。只有当一个元素的某个属性没有被指定时，才会继承父级元素的值。

2. 否定伪类选择器 `:not()` 的权重:

    它的权重是由括号内的内容决定。

    code:

    {% codepen SPxiaomin RRWpOM 0 css 265 %}

3. 如果两个选择器作用在同一元素上，则权重高者生效。

4. 如果两个选择器权重值相同，则最后定义的规则被计算到权重中:

    ```css
    p {
        color: red;
        background: yellow;
    }

    p {
        color: green;
    }
    ```

    段落会呈现绿色的文字，当然背景颜色还会是黄色的，就是因为第一条规则只是被覆盖了 color 属性。

5. 与元素“挨得近”的规则生效:

    规则1(位于css文件中)

    ```css
    #content h1 {
        padding: 5px;
    }
    ```

    规则2(位于html文件中)

    ```html
    <style>
        #content h1 {
            padding: 10px;
        }
    </style>
    ```

    在上面的两个规则中，因为规则2(位于html文件中)跟元素挨得比较近，所以生效。

6. 特殊的 !important

    CSS2 规范中规定: !important 用于单独指定某条样式中的单个属性。对于被指定的属性，有 !important 指定的权重值大于所有未用 !important 指定的规则。

    举例如下:

    ```css
    /* 样式一 */
    #header nav ul li.current {
        color: red;
        font-weight: bold;
    }

    /* 样式二 */
    li:hover {
        color: blue !important;
        font-weight: normal;
    }
    ```

    样式一的权重为 0,1,1,3，然而样式二的权重是 0,0,1,1，所以当两条样式规则应用于同一个元素的时候，应该是样式一生效。但是对于 color 这个属性，由于样式二中用 !important 做了指定，因此 color 将应用样式二的规则。而 font-weight 仍将使用样式一的规则。

    但是值得注意的是: 如果在多条规则中对同一属性指定了 !important 的话，这时候 !important 的作用相互抵消，仍然按照 ABCD 四组计算比较。

### References

[重新认识CSS的权重](http://blog.cssforest.org/2011/05/19/%E9%87%8D%E6%96%B0%E8%AE%A4%E8%AF%86CSS%E7%9A%84%E6%9D%83%E9%87%8D.html)

[你应该知道的一些事情——CSS权重](http://www.w3cplus.com/css/css-specificity-things-you-should-know.html)

[css2.1 specification](https://www.w3.org/TR/CSS2/cascade.html#specificity)

[深入解析CSS样式层叠权重值](http://ofcss.com/2011/05/26/css-cascade-specificity.html)

[CSS 中的权重问题](http://zhanglun.github.io/2014/09/26/css%E4%B8%AD%E7%9A%84%E6%9D%83%E9%87%8D%E9%97%AE%E9%A2%98/)

[CSS 选择器的权重详解](http://www.cnblogs.com/rubylouvre/archive/2010/03/17/1687786.html)
