---
title: css深入理解のfloat
date: 2017-02-12 08:36:25
categories: ['技术', '前端技术']
tags: ['css', 'float']
---

!!!未完成

## float & containing box

float 的 containing box 是父 block 元素的 content-box。

{% codepen SPxiaomin YNRjdb 0 css 265 %}

## float & bfc

在同一个bfc中，正常流(normal flow)中生成bfc的元素不能够与float元素的 margin box 有重叠。可以用这个效果来实现一侧定宽的自适应布局，可复用性非常好。

{% codepen SPxiaomin zNeNqK 0 result 265 %}

## float & content reflow

{% codepen SPxiaomin jydBwm 0 result 265 %}

## float & stacking context

{% codepen SPxiaomin MJxazy 0 result 265 %}

## float & clear

{% codepen SPxiaomin EZMyxV 0 result 265 %}
