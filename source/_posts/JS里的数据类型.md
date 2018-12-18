---
title: JS里的数据类型
date: 2018-12-18 22:40:39
tags:
---
## JS的七种数据类型
数字（number） 字符串（string） 布尔（boolean） 符号（symbol） null undefined 对象（object）

### 1.number
1. 1.整数和浮点数
JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的，是同一个数。
2. 2.数值精度
根据国际标准 IEEE 754，JavaScript 浮点数的64个二进制位，从最左边开始，是这样组成的。
* 第1位：符号位，0表示正数，1表示负数
* 第2位到第12位（共11位）：指数部分
* 第13位到第64位（共52位）：小数部分（即有效数字）
3. 3.数值范围
 JavaScript 能够表示的数值范围为21024到2-1023（开区间），超出这个范围的数无法表示。
 如果一个数大于等于2的1024次方，那么就会发生“正向溢出”，即 JavaScript 无法表示这么大的数，这时就会返回Infinity。如果一个数小于等于2的-1075次方（指数部分最小值-1023，再加上小数部分的52位），那么就会发生为“负向溢出”，即 JavaScript 无法表示这么小的数，这时会直接返回0。
4. 4.数值的进制
* 十进制：没有前导0的数值。
* 八进制：有前缀0o或0O的数值，或者有前导0、且只用到0-7的八个阿拉伯数字的数值。
* 十六进制：有前缀0x或0X的数值。
* 二进制：有前缀0b或0B的数值。
5. 5.特殊值
* 1）+0和-0
这两者基本上是一样的，唯一有区别的是+0或-0当作分母，返回的值是不相等的。
`(1 / +0) === (1 / -0) // false`
上面的代码之所以出现这样结果，是因为除以正零得到+Infinity，除以负零得到-Infinity，这两者是不相等的
* 2)NaN
表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。
*NaN不等于任何值，包括它本身。
* 3)Infinity
Infinity表示“无穷”，用来表示两种场景。一种是一个正的数值太大，或一个负的数值太小，无法表示；另一种是非0数值除以0，得到Infinity。
* Infinity的四则运算，符合无穷的数学计算规则。
```
5 * Infinity // Infinity
5 - Infinity // -Infinity
Infinity / 5 // Infinity
5 / Infinity // 0
```

0乘以Infinity，返回NaN；0除以Infinity，返回0；Infinity除以0，返回Infinity。
```
0 * Infinity // NaN
0 / Infinity // 0
Infinity / 0 // Infinity
```

Infinity加上或乘以Infinity，返回的还是Infinity。
```
Infinity + Infinity // Infinity
Infinity * Infinity // Infinity
```

Infinity减去或除以Infinity，得到NaN。
```
Infinity - Infinity // NaN
Infinity / Infinity // NaN
```

Infinity与null计算时，null会转成0，等同于与0的计算。
```
null * Infinity // NaN
null / Infinity // 0
Infinity / null // Infinity
```

Infinity与undefined计算，返回的都是NaN。
```
undefined + Infinity // NaN
undefined - Infinity // NaN
undefined * Infinity // NaN
undefined / Infinity // NaN
Infinity / undefined // NaN
```

6. 6.parseInt()  parseFloat()   isNaN()  isFinite()
前三个都很好理解，主要介绍第四个
isFinite方法返回一个布尔值，表示某个值是否为正常的数值
```
isFinite(Infinity) // false
isFinite(-Infinity) // false
isFinite(NaN) // false
isFinite(undefined) // false
isFinite(null) // true
isFinite(-1) // true
```
除了Infinity、-Infinity、NaN和undefined这几个值会返回false，isFinite对于其他的数值都会返回true。

### string
1. 1.定义
字符串就是零个或多个排在一起的字符，放在单引号或双引号之中。
如果要在单引号字符串的内部，使用单引号，就必须在内部的单引号前面加上反斜杠，用来转义。
```
'a \'name\' '
```

如果要写成多行字符串
```
'a\
b\
c'
```
或者是
```
'a'+
'b'+
'c'
```
推荐使用第二种
2. 2.转义
* \0 ：null（\u0000）
* \b ：后退键（\u0008）
* \f ：换页符（\u000C）
* \n ：换行符（\u000A）
* \r ：回车键（\u000D）
* \t ：制表符（\u0009）
* \v ：垂直制表符（\u000B）
* \' ：单引号（\u0027）
* \" ：双引号（\u0022）
* \\ ：反斜杠（\u005C）
特殊写法：
```
'\251' // "©"
'\xA9' // "©"
'\u00A9' // "©"
```
3. 3.Base64 转码
* btoa()：任意值转为 Base64 编码
* atob()：Base64 编码转为原来的值

4. 4.
空字符串 ""或者是''        length = 0
空格字符串 " "或者是 ' '    length = 1

### null
表示空
### undefined
表示未被定义
* null和undefined的区别
定义了一个变量，但是没有给变量赋值   ---------undefined（语法）
定义了一个对象（object），但是没有给对象赋值  ----------null（惯例）
定义了一个非对象，但是没有赋值           ----------undefined（惯例）

* 两种重新定义key和value的方式的区别
```
delete person['name']
person.name           //undefined
'name' in person      //false
```
无key 无value

```
person.name = undefined
person.name             //undefined
'name' in person        //true
```
有key 无value

* 死记两个bug
>typeof null      //'object'
>typeof function  //'function'
注意：没有'function'这个数据类型！！
