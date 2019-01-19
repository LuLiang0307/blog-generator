---
title: JS里的数据类型转换及一些面试题的坑
date: 2018-12-20 19:04:49
tags:
---
## 一、七种数据类型
number string boolean symbol null undefined object

## 二、任意类型转换成字符串的三种常用方法
1.toString
null和undefined没有这个API，出错的提示是 cannot read property 'toString' of null/undefined。不能读取null和undefined的属性。
object的toString方法得到  `"[object Object]"`。
2.string()
这种方法下，null和undefined就不会出现不能变成字符串的情况。
3.''+任意类型
比如 1+'1'      //输出的结果是'11'，优先转变成字符串

## 三、任意类型转换成布尔类型的两种方法
1.Boolean()
2.!!任意类型的数据

* 五个falsy值：0    NaN    ''    null    undefined  
* 所有的object都是true。

## 四、内存
1.内存是计算机中重要的部件之一，它是与CPU进行沟通的桥梁。计算机中所有程序的运行都是在内存中进行的，因此内存的性能对计算机的影响非常大。内存(Memory)也被称为内存储器，其作用是用于暂时存放CPU中的运算数据，以及与硬盘等外部存储器交换的数据。只要计算机在运行中，CPU就会把需要运算的数据调到内存中进行运算，当运算完成后CPU再将结果传送出来，内存的运行也决定了计算机的稳定运行。 内存是由内存芯片、电路板、金手指等部分组成的。
* 特点是断电就丢失存储的数据。
2.数据区分为栈（Stack）和堆（Heap）。
3.ECMAScript规定：数字以64位存储，ES3中的字符以16位存储。
4.简单的数据类型直接存入stack中，复杂的数据类型（obj）存Heap地址存入stack中。
5.垃圾回收：如果一个对象没有被引用，那么它就是垃圾，将被会搜。

## 五、面试题
这些题目需要画内存图既能很容易的分析出来。
```
javascript
var a = 1
var b = a
b = 2
请问 a 显示是几？  
```
a=1;

```
javascript
var a = {name: 'a'}
var b = a
b = {name: 'b'}
请问现在 a.name 是多少？
```
a;

```
javascript
var a = {name: 'a'}
var b = a
b.name = 'b'
请问现在 a.name 是多少？
```
b; //浅拷贝的很好的例子，改变b的值同时影响到了a的值。

```
javascript
var a = {name: 'a'}
var b = a
b = null
请问现在 a 是什么？
```
`a=｛name : 'a'｝`;

![1545306360(1).png](https://i.loli.net/2018/12/20/5c1b813a131fd.png)