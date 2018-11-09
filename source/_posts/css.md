---
title: css
date: 2018-11-09 16:21:08
tags:
---
## 层叠样式表（英语：Cascading Style Sheets，简写CSS），又称串樣式列表、级联样式表、串接样式表、階層式樣式表，一种用来为结构化文档（如HTML文档或XML应用）添加样式（字体、间距和颜色等）的计算机语言，CSS 描述了在屏幕、纸质、音频等其它媒体上的元素应该如何被渲染的问题。由W3C定义和维护。


## 一、CSS的选择器有哪些？
1. 1.id选择器（ # myid）
2. 2.类选择器（.myclassname）
3. 3.标签选择器（div, h1, p）
4. 4.相邻选择器（h1 + p）
5. 5.子选择器（ul > li）
6. 6.后代选择器（li a）
7. 7.通配符选择器（ * ）
8. 8.属性选择器（a[rel ="external"]）
9. 9.伪类选择器（a:hover,li:nth-child）

## 二、CSS position 有哪些取值？
**absolute**
生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。 
元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。 
**fixed** 
生成绝对定位的元素，相对于浏览器窗口进行定位。 
元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。 
**relative** 
生成相对定位的元素，相对于其正常位置进行定位。 
因此，”left:20” 会向元素的 LEFT 位置添加 20 像素。 
**static** 
默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。 
**inherit** 
规定应该从父元素继承 position 属性的值。

## 三、1、介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同的？
（1）有两种， IE 盒子模型、W3C 盒子模型；
（2）盒模型：内容(content)、填充(padding)、边界(margin)、边框(border)；
（3）区 别： IE的content部分把 border 和 padding计算了进去;

**border-box**
![](https://i.loli.net/2018/11/09/5be568cd398af.png)
**content-box**
![](https://i.loli.net/2018/11/09/5be568fe78395.png)

## 四、position的值relative和absolute定位原点是？
**absolute**
生成绝对定位的元素，相对于值不为 static的第一个父元素进行定位。

**fixed** （老IE不支持）
生成绝对定位的元素，相对于浏览器窗口进行定位。

**relative**
生成相对定位的元素，相对于其正常位置进行定位。

**static**
默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）。

**inherit**
规定从父元素继承position 属性的值。

## 五、文档流的定义和脱离文档流的方式
**文档流**是文档内元素的流动方向。内联元素从左往右流动，遇到阻碍会换行继续流动；块级元素从上往下流动。
**float:left**、**position:fixed**、**position:absolute** 都能使元素脱离文档流。

## 六、关于 display: inline 元素
 给 display: inline 元素设置宽高是无效的
 给 display: inline 元素设置 margin-top margin-bottom 是无效的

## 七、display有哪些值？说明他们的作用。
**block** 块类型。默认宽度为父元素宽度，可设置宽高，换行显示。
**none** 缺省值。象行内元素类型一样显示。
**inline** 行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示。
**inline-block** 默认宽度为内容宽度，可以设置宽高，同行显示。
**list-item** 象块类型元素一样显示，并添加样式列表标记。
**table** 此元素会作为块级表格来显示。
**inherit** 规定应该从父元素继承display 属性的值。

## 八、如何用CSS做一个直角三角形
`triangle{` 
&nbsp;`border: 20px solid transparent;` 
&nbsp;`border-left-color:red ;` 
&nbsp;`width: 0;` 
&nbsp;`border-top-width: 0px;` 
`}` 
其他图形参考：[css-tricks](https://css-tricks.com/the-shapes-of-css/)
学习链接：[css篇的面试题](https://zhuanlan.zhihu.com/p/25355029)