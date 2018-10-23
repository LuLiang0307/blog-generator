---
title: HTML常用标签注意的地方
date: 2018-10-22 21:42:33
tags:
---
上次的博客已经把常用的标签总结了一下，这篇博客把某些标签使用的地方需要注意的东西总结一下，也是我课堂上的笔记。

## 1.iframe标签
   &nbsp;&nbsp; iframe标签在现代的前端中使用得不多，但是也是优缺并存，不少人都是中立的看法。
1）常见的用法是： `<iframe src="路径" frameborder="0"></iframe> `
一般都把frameborder设置为0，为了美观。
2）iframe标签和a标签一起使用的情况
 `<iframe name=xxx src="#" frameborder="0"></iframe>  `
 `<a target=xxx href="路径"></a> `
点击标签a定义的链接时，会在iframe的窗口中打开。

##　2.a标签
1）a标签的打开方式
&nbsp;&nbsp;_blank：在新的空页面打开
&nbsp;&nbsp;_self：在自己本身的页面打开
&nbsp;&nbsp;_parent：在父代窗口打开
&nbsp;&nbsp;_top：在顶层窗口打开（三级以上的窗口有明显效果）
2）下载一个文件
 `<a href="路径" download>下载</a> `或者 `Content-type:application/octet-stream; `
3)设置href="路径"时，只有#锚点不发起请求，因为锚点是在页面内跳转，其他的形式都发起请求。
4）JavaScript伪协议
例如： `<a href="javascript:alert(1);" ></a> `
在a标签内执行JavaScript命令，有时候用来实现一些比较奇葩的效果，比如说点击a标签的时候页面不会发生跳转。
 `<a href="javascript=;"></a> `
5)跳转页面
a标签：HTTP GET
form标签：HTTP POST

## 3.form标签
1）注意：form标签里面一定要有一个提交按钮，不然里面的数据无法提交。
2）submit和button
 `<button>button</button> `这种写法会将button按钮自动升级成提交按钮。
但是如果加上 `type="button" `， `<button type="button">button</button> `或者是 `<input type="button"> `就没有提交功能了。
**注意：submit是form表单中唯一能提交的按钮，而button只是普通按钮。**

## 4.checkbox标签
怎么设置选中文字即可勾选或者点击文字自动选中文本框的功能？
有两种方式。
&nbsp;&nbsp;1. `<input type="checkbox" id=xxx><label for=xxx>文字</label> `
&nbsp;&nbsp;2. `<label><input type="checkbox"></label> `这种形式就可以不写id和for了，但是label标签里面只能有一个input标签。

## 5.radio标签
要使单选框只能选中一个，那么要在各个选项使用同一个name属性。
 `<input type="radio" name="loveme">yes `
 `<input type="radio" name="lveme">no `

## 6.select标签
 `<select name=xxx> `
   &nbsp;` <option value="..." disabled></option> `
  &nbsp;`<option value="..." selected></option> `
   &nbsp;` <option value="..." multiple></option> `
 `</select> `
disabled:不让勾选
selected：默认选中
multiple：按下shift键可以多选

## 7.textarea标签
一般textarea在页面中可以拖动，但是容易将提交按钮弄到下一行去，容易出bug，所以可以用cSS样式控制文本域不能拉动。
 `style="resize:none;" `
width在textarea中不能精确的设置宽度，所以可以用CSS样式精确的设置宽和高。

## 8.table标签
  `<table border=1> `
     &nbsp;`<colgroup> `
        &nbsp;&nbsp; `<col width=200>`
        &nbsp;&nbsp;`<col width=100> `
       &nbsp;&nbsp; `<col width=100>`
       &nbsp;&nbsp; `<col width=100>`
   &nbsp; `</colgroup>`
   &nbsp; `<thead>`
     &nbsp;&nbsp; `<tr>`
       &nbsp;&nbsp;&nbsp; `<th>项目</th><th>姓名</th><th>班级</th><th>分数</th>`
     &nbsp;&nbsp; `</tr> `
   &nbsp;`</thead>`
   &nbsp; `<tbody>`
      &nbsp;&nbsp;  `<tr>`
          &nbsp;&nbsp;&nbsp;  `<td>1</td><td>小明</td><td>二年一班</td><td>94</td>` 
       &nbsp;&nbsp; `</tr>`
       &nbsp;&nbsp; `<tr>`
        &nbsp;&nbsp;&nbsp;    `<td>2</td><td>小红</td><td>二年二班</td><td>96</td>`
     &nbsp;&nbsp;   `</tr>`
   &nbsp; `</tbody>`
    &nbsp;`<tfoot>`
       &nbsp;&nbsp; `<tr>`
          &nbsp;&nbsp;&nbsp;  `<th>总分</th><td></td><td></td><td>190</td>`
       &nbsp;&nbsp; `</tr>`
       &nbsp;&nbsp; `<tr>`
          &nbsp;&nbsp;&nbsp;  `<th>平均分</th><td></td><td></td><td>95</td>`
       &nbsp;&nbsp; `</tr>`
  &nbsp; `</tfoot>`
  `</table>`
上面的代码把table基本的框架都描述出来了，一些属性很容易。