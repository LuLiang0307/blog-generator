---
title: CSS的一般布局的实现
date: 2018-11-17 22:28:42
tags:
---
## 一、左右布局
### 1.table——tr+td 和 ul+li的两种形式
* **tr+td:**
tr代表行，td是列。先满足行，再满足列，还可以通过colspan来设置某一行的某一列。
html:
```
<table>
    <tr style="clearfix">
        <td>姓名</td>
        <td>Frank</td>
    </tr>
</table>```

css:
```
table{
    border: 1px solid red;
}
table tr td{
    border: 1px solid black;  
}```
效果：
![](https://i.loli.net/2018/11/18/5bf13a9db15c7.png)
* **ul+li**
设置ul的宽度不变，改变li的宽度就可以改变函数，ul的宽度和li的宽度之间的关系是倍数关系。
html:
```
<div class="my">
	<ul style="clearfix">
		<li>那些花儿</li>
		<li>那些花儿</li>
		<li>那些花儿</li>
		<li>那些花儿</li>
		<li>那些花儿</li>
		<li>那些花儿</li>
	</ul>
</div>
```

css:
```
.clearfix::after{
    content:"";
    display: block;
    clear: all;
}
.my ul {
	width: 210px;
}
.my li {
	width: 100px;   /*如果显示三列 则width改为70px*/
	float: left;
	display: block;
    border: 1px solid red;
}
```
效果：
![](https://i.loli.net/2018/11/18/5bf13a160e5a1.png)

### 2.display: inline-block
display:inline-block属性是介于行级元素(display:inline)和块级元素(display：block)之间的属性，它可以像行级元素一样水平布局，也可以像块级元素设置宽高属性，所以使用它可以进行左右布局。另：它不支持ie6、7浏览器，请注意，但是可以使用inline进行hack处理。
html:
```
<section class="section">
    <div class="wrap">
        <div class="col-4 c1">1</div>
        <div class="col-4 c2">2</div>
        <div class="col-4 c3">3</div>
        <div class="col-4 c4">4</div>
        <div class="col-4 c5">5</div>
        <div class="col-4 c6">6</div>
    </div>
</section>
```

css:
```
.col-4{
    display: inline-block;
    *display: inline;
    *zoom:1; //ie6、7hack
    width:25%;
    height:30px;
    border:1px solid #999;
    font-size: 14px;
}
.wrap{
    margin:10px auto;
    max-width:1280px;
    min-width:1024px;
    font-size: 0px;
}
```
效果：
![](https://i.loli.net/2018/11/21/5bf50f254bd9b.jpg)

### 3. float实现左右布局
float属性能使元素脱离文档流，left和right属性值能让元素靠左右排列，但是一般都有些bug，需要设置class属性为clearfix。
html:
```
<ul class="clearfix">
    <li><a href="#">关于</a></li>
    <li><a href="#">技能</a></li>
    <li><a href="#">作品</a></li>
    <li><a href="#">博客</a></li>
    <li><a href="#">日历</a></li>
    <li><a href="#">联系方式</a></li>
    <li><a href="#">其他</a></li>
</ul>
```

css:
```
.clearfix::after {
    content:"";
    display: block;
    clear: both;
}
ul { 
    list-style: none;
    margin: 0;
    padding: 0;
}
ul li {
    float: left;
    margin-left: 17px;
    margin-right: 17px;
}
```
效果为：
![](https://i.loli.net/2018/11/21/5bf512e3342e6.jpg)

### 4.基于css3中flexbox属性实现左右布局
box-flex 属性规定框的子元素是否可伸缩其尺寸。可伸缩元素能够随着框的缩小或扩大而缩写或放大。只要框中有多余的空间，可伸缩元素就会扩展来填充这些空间。语法为： box-flex: value;
value：元素的可伸缩行。柔性是相对的，例如 box-flex 为 2 的子元素两倍于 box-flex 为 1 的子元素。
目前没有浏览器支持 box-flex 属性。Firefox 支持替代的 -moz-box-flex 属性。Safari、Opera 以及 Chrome 支持替代的 -webkit-box-flex 属性。
html:
```
<section class="section">
    <div class="wrap">
        <div class="col-4 c1">1</div>
        <div class="col-4 c2">2</div>
        <div class="col-4 c3">3</div>
        <div class="col-4 c4">4</div>
    </div>
    <div class="wrap">
        <div class="col-4 c5">5</div>
        <div class="col-4 c6">6</div>
    </div>
</section>
```

css:
```
.wrap{
    margin:10px auto;
    max-width:1280px;
    min-width:1024px;
}
.wrap{
    display: -webkit-box;
    -webkit-box-orient: horizontal;
}
.col-4{
    height:30px;
    border:1px solid #999;
    -webkit-box-flex:1;
}
```

### 5.float+margin实现左右布局
float能够使得元素向左或者向右靠边布局，如果在同级元素中设置一个正常流的区域与浮动块并列，则浮动块会在该正常流同级区域的边界处，只是浮动块会影响该区域块的布局，所以要清除浮动块的影响，所以此时将正常流区域块的盒子设置margin等于浮动块的宽度既可以清除影响。
 补充：由margin→盒模型： css盒模型是css的基础环节，css盒子从内到外一次有内容-padding-border-margin组成，可以通过设置各个值来设置间距。 另：对于不同的文档模式其宽度和高度解析不同，
* 对于ie下怪异文档模式或者标准文档模式下定义了css3中的box-sizing：border-box的元素，css中设置的宽高都是内容区宽高+padding+border的；
* 标准文档下或者定义了css3中box-sizing:content-box的元素，css中定义的元素宽高就是内容区的宽高。
html:
```
<header class="header">
    <div class="wrap">
        <div class="hLeft">left</div>
        <div class="hRight">right</div>
    </div>
</header>
```

css:
```
.header{
    background-color: #ccc;
    padding:1px;
}   
.wrap{
    margin:10px auto;
    max-width:1280px;
    min-width:1024px;
}
.hLeft{
    float:left;
    border:1px solid #999;
    width:15%;
    height: 50px;
}
.hRight{
    /*overflow: hidden;
    zoom:1;*/
    height:50px;
    border:1px solid #999;
    margin-left:15%;
}
.box{
    height: 30px;
    background-color: red
}
```
效果：
![](https://i.loli.net/2018/11/21/5bf544d676b0e.jpg)

### 6.block formate context(float+overflow)实现左右布局
对于float对后面同级元素的影响，除了采用margin进行影响的清除，还可以在受影响的元素上添加overflow：hidden来清除浮动对该区域块带来的影响。
html:
```
<header class="header">
    <div class="wrap">
        <div class="hLeft">left</div>
        <div class="hRight">right</div>
        <!-- <div>hhh<br>hhh<br>jjj<br>sss</div> -->
    </div>
</header>
```

css:
 ```
 .header{
        background-color: #ccc;
        padding:1px;
    }   
    .wrap{
        margin:10px auto;
        max-width:1280px;
        min-width:1024px;
    }
    .hLeft{
        float:left;
        border:1px solid #999;
        width:15%;
        height: 90px
    }
    .hRight{
        overflow: hidden;
        zoom:1;
        height:50px;
        border:1px solid #999;
    }
    .box{
        margin:10px;
        border:1px solid #888;
    }
    .cbox{
        height:20px;
        background-color: #ccc;
        margin:25px;
        float:left;
        width:100%;
    }
    .clear{
        clear:both;
    }
```
效果：
![](https://i.loli.net/2018/11/21/5bf55b52af81a.jpg)

### 7. position:absolute左右布局
除了float可以产生脱离文档流的布局现象以外，position：absolute也可以，但是二者又有不同之处。不同之处在于absolute可以覆盖任何位置的元素且不会影响正常流的布局，但是会产生遮盖，所以要求正常流要躲避绝对布局的遮挡。躲避方式可以使用margin。
html:
```
<div class="works" style="height: 576px;">
    <div class="big" style="top: 0; left: 0;">
        <img src="./img/1.jpg" alt="作品1">
    </div>
    <div class="small" style="top: 0; left: 644px;">
        <img src="./img/2.jpg" alt="作品2">
    </div>
    <div class="small" style="top: 298px;left: 644px;">
        <img src="./img/3.jpg" alt="作品3">
    </div>
<div>
```

css:
```
.works{
    position: relative;
} 
.works .big,
.works .small{
    position: absolute;
}
```
效果：
![](https://i.loli.net/2018/11/21/5bf55d0a46970.jpg)

## 二、左中右布局
### 1.浮动布局 float
不设置中间的宽度,根据页面的变化中间会自动填充宽度。
html:
```
<div class="left">左边</div>
<div class="right">右边</div>
<div class="center"></div>
```

css:
```
*{
    margin: 0;
    padding: 0;
}
.left{
    float: left;
    border: 1px solid red;
    height: 100px;
    width: 100px;
    background: lightblue;
}
.right{
    float: right;
    border: 1px solid green;
    height: 100px;
    width: 100px;
    background: pink;
}
.center{
    border: 1px solid yellow;
    height: 100px;
    background: grey;
}
```
效果：
![左元素: float: left; 右元素: float: right; 中间元素:自动填充](https://i.loli.net/2018/11/21/5bf566c1a9745.jpg)

### 2.绝对定位 position
html:
```
<article class="left-center-right">
    <div class="left">左边</div>
    <div class="right">右边</div>
    <div class="center"></div>
</article>
```

css:
```
*{
  margin: 0;
  padding: 0;
}
.left-center-right{
  position: relative;
}
.left{
  left: 0;
  position: absolute;
  border: 1px solid red;
  height: 100px;
  width: 100px;
  background: lightblue;
}
.right{
  right: 0;
  position: absolute;
  border: 1px solid green;
  height: 100px;
  width: 100px;
  background: pink;
}
.center{
  left: 100px;
  right: 100px;
  position: absolute;
  border: 1px solid yellow;
  height: 100px;
  background: grey;
}
```
效果：
![左边元素: position: absolute; left: 0;右边元素: position: absolute; right:0; 中间元素: position: absolute;left:100px; right: 100px;](https://i.loli.net/2018/11/21/5bf57023466fd.jpg)

### 3.flex布局
html:
```
<article class="left-center-right">
    <div class="left">左边</div>
    <div class="center"></div>
    <div class="right">右边</div>
</article>
```

css:
```
*{
    margin: 0;
    padding: 0;
}
.left-center-right{
    display: flex;
}
.left{
    border: 1px solid red;
    height: 100px;
    width: 100px;
    background: lightblue;
}

.center{
    flex: 1;
    border: 1px solid yellow;
    height: 100px;
    background: grey;
}
.right{
    border: 1px solid green;
    height: 100px;
    width: 100px;
    background: pink;
}
```
效果：
![父元素display:flex; 左右子元素设置宽度100px; 中间子元素设置flex:1;](https://i.loli.net/2018/11/21/5bf57127da948.jpg)

### 4.表格布局
html:
```
<article class="left-center-right">
    <div class="left">左边</div>
    <div class="center"></div>
    <div class="right">右边</div>
</article>
```

css:
```
*{
  margin: 0;
  padding: 0;
}
.left-center-right{
    width: 100%; 
    display: table;
}
.left-center-right>div{
   display: table-cell;
}
.left{
  border: 1px solid red;
  height: 100px;
  width: 100px;
  background: lightblue;
}

.center{
  border: 1px solid yellow;
  height: 100px;
  background: grey;
}
.right{
  border: 1px solid green;
  height: 100px;
  width: 100px;
  background: pink;
}
```
效果：
![父元素width: 100%; display: table;左右子元素display: table-cell; width: 300px;](https://i.loli.net/2018/11/21/5bf573285801d.jpg)

### 5.网格布局
html:
```
<article class="left-center-right">
    <div class="left">左边</div>
    <div class="center"></div>
    <div class="right">右边</div>
</article>
```

css:
```
*{
  margin: 0;
  padding: 0;
}
.left-center-right{
  display: grid;
  width: 100%;
  grid-template-rows: 100px;
  grid-template-columns: 100px auto 100px;
}
.left{
  border: 1px solid red;
  height: 100px;
  width: 100px;
  background: lightblue;
}

.center{
  border: 1px solid yellow;
  height: 100px;
  background: grey;
}
.right{
  border: 1px solid green;
  height: 100px;
  width: 100px;
  background: pink;
}
```
效果：
![父元素宽度为100%,父元素width: 100%; display:grid; grid-template-rows: 100;grid-template-columns: 100px auto 100px](https://i.loli.net/2018/11/21/5bf573ee38974.jpg)

## 三、水平居中
### 1.最熟悉的方式是已知宽度，然后设置margin的左右为auto。
如：![已知宽度的情况](https://i.loli.net/2018/11/26/5bfbeb34721ba.jpg)

### 2.不知道准确的宽度的时候，用inline-block+ text-align 实现。
html:
```
<div class="pagination">
  <ul>
    <li><a href="#">Prev</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">Next</a></li>
  </ul>
</div>
```

css:
```
*{
  list-style: none;
  text-decoration: none;
  margin: 0;
  padding: 0;
}
.pagination ul li a{
  border: 1px solid black;
}
.pagination ul li{
  border: 1px solid red;
  display: inline-block;
}
.pagination ul{
   text-align: center;
}
```
效果：
![](https://i.loli.net/2018/11/26/5bfbf41037202.png)

### 3.浮动实现水平居中。配合position使用。
html:
```
<div class="pagination">
<ul>
    <li><a href="#">Prev</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">Next</a></li>
</ul>
</div>
```

css:
```
*{
  list-style: none;
  text-decoration: none;
  margin: 0;
  padding: 0;
}
.pagination ul li a{
  border: 1px solid black;
}
.pagination ul li{
  border: 1px solid red;
  position: relative;
  display: block;
  right: 50%;
  float: left;
  margin: 0 5px;
}
.pagination ul{
  float: left;
  clear: left;
  position: relative;
  left: 50%;
  text-align: center;
}
.pagination{
  position: relative;
}
```
效果：
![](https://i.loli.net/2018/11/26/5bfbf70b34f3c.jpg)

### 4.绝对定位实现水平居中
html:
```
<div class="pagination">
  <ul>
    <li><a href="#">Prev</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">Next</a></li>
  </ul>
</div>
```

css:
```
*{
  list-style: none;
  text-decoration: none;
  margin: 0;
  padding: 0;
}
.pagination ul li a{
  border: 1px solid black;
}
.pagination ul li{
  border: 1px solid red;
  position: relative;
  right: 50%;
  float: left;
  margin: 0 5px;
}
.pagination ul{
  position: absolute;
  left: 50%;
}
.pagination{
  position: relative;
}
```
效果：
![](https://i.loli.net/2018/11/26/5bfbf8f765e60.jpg)

### 5.flex实现水平居中方法
兼容性比较差！
CSS：
```
*{
  list-style: none;
  text-decoration: none;
  margin: 0;
  padding: 0;
}
.pagination ul li a{
  border: 1px solid black;
}
.pagination ul li{
  border: 1px solid red;
  float: left;
  margin: 0 5px;
}
.pagination ul{
}
.pagination{
  display: -webkit-box; 
  -webkit-box-orient: horizontal;
  -webkit-box-pack: center;
  display: -moz-box; 
  -moz-box-orient: horizontal;
  -moz-box-pack: center; 
  display: -o-box; 
  -o-box-orient: horizontal;
  -o-box-pack: center;
  display: -ms-box;
  -ms-box-orient: horizontal;
  -ms-box-pack: center; 
  display: box;
  box-orient: horizontal; 
  box-pack: center;
}
```
效果：
![](https://i.loli.net/2018/11/26/5bfbfa0cc9cf6.jpg)

### 6.CSS3的fit-content实现水平居中方法
css:
```
*{
  list-style: none;
  text-decoration: none;
  margin: 0;
  padding: 0;
}
.pagination ul li a{
  border: 1px solid black;
}
.pagination ul li{
  border: 1px solid red;
  float: left;
  margin: 0 5px;
}
.pagination ul{
  width: -moz-fit-content; 
  width:-webkit-fit-content;
  width: fit-content;
  margin-left: auto;
  margin-right: auto;
}
```
效果：
![](https://i.loli.net/2018/11/26/5bfbfac273526.jpg)

## 四、垂直居中
### 1.相对定位+margin
html:
```
<div class="orange"></div>
```

css:
```
*{
  list-style: none;
  text-decoration: none;
  margin: 0;
  padding: 0;
}
.orange{
  width: 100px;
  height: 100px;
  background: orange;
  position: relative;
  margin: 0 auto;
  top: 50%;
  margin-top: -50px;
}
html,body{
  width: 100%;
  height: 100%;
}
```
效果：
![](https://i.loli.net/2018/11/26/5bfbfd74dd6a9.jpg)

除了可以使用margin-top把div往上偏移之外，CSS3的transform属性也可以实现这个功能，通过设置div的transform: translateY(-50%)，意思是使得div向上平移（translate）自身高度的一半(50%)。

### 2.CSS3的弹性布局（flex）
使用CSS3的弹性布局很简单，只要设置父元素（这里是指body）的display的值为flex即可。
css:
```
*{
  list-style: none;
  text-decoration: none;
  margin: 0;
  padding: 0;
}
.orange{
  width: 100px;
  height: 100px;
  background: orange;
}
html,body{
  width: 100%;
  height: 100%;
}
body {
  display: flex;
  align-items: center; /*定义body的元素垂直居中*/
  justify-content: center; /*定义body的里的元素水平居中*/
}
```

## 五、等其他小技巧
### 1.解决float的bug
在float的父级元素上添加class="clearfix";
```
.clearfix::after{
    content: '';
    display: block;
    clear: both;
}
```
### 2.list-style用在ul上，因为ul是list，而li是list-item,列表项。

### 3.解决display：inline-block的bug
会在页面中出现缝隙，要加vertical-align：top；以消除出现的额缝隙。

### 4.在列表中，选中奇数或者是偶数进行设置
nth-child(even)     选中偶数
nth-child(odd)      选中奇数
nth-child(1)        选中列表的第一个项