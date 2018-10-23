---
title: 关于html的知识介绍
date: 2018-10-18 17:46:56
tags:
---
## 一、W3C简介
**W3C，这个建立于 1994 年的组织，其宗旨是通过促进通用协议的发展并确保其通用型，以激发 web 世界的全部潜能。**
* **1.W3C 是什么？**
    * W3C 指万维网联盟（World Wide Web Consortium）
    * W3C 创建于1994年10月
    * W3C 由 Tim Berners-Lee 创建
    * W3C 是一个会员组织
    * W3C 的工作是对 web 进行标准化
    * W3C 创建并维护 WWW 标准
    * W3C 标准被称为 W3C 推荐（W3C Recommendations）
* **２.W3C 是如何创建的？**
万维网（World Wide Web）是作为欧洲核子研究组织的一个项目发展起来的，在那里 Tim Berners-Lee 开发出万维网的雏形。

Tim Berners-Lee - 万维网的发明人 - 目前是万维网联盟的主任。

W3C 在 1994 年被创建的目的是，为了完成麻省理工学院（MIT）与欧洲粒子物理研究所（CERN）之间的协同工作，并得到了美国国防部高级研究计划局（DARPA）和欧洲委员会（European Commission）的支持。
* **３.对 web 进行标准化**
W3C 致力于实现所有的用户都能够对 web 加以利用（不论其文化教育背景、能力、财力以及其身体残疾）。

W3C 同时与其他标准化组织协同工作，比如 Internet 工程工作小组（Internet Engineering Task Force）、无线应用协议（WAP）以及 Unicode 联盟（Unicode Consortium）。

W3C 由美国麻省理工学院计算机科学和人工智能实验室 (MIT CSAIL)，总部位于法国的欧洲信息数学研究联盟 (ERCIM) 和日本的庆应大学（Keio University）联合运作，并且在世界范围内拥有分支办事处。
* **４.W3C 会员**
正因为 Web 是如此的重要（不论在其影响范围还是在投资方面），以至于不应由任何一家单独的组织来对它的未来进行控制，因此 W3C 扮演者一个会员组织的角色：

一些知名的会员包括：

*IBM
*Microsoft
*America Online
*Apple
*Adobe
*Macromedia
*Sun Microsystems
W3C 的会员包括了：软件开发商、内容提供商、企业用户、通信公司、研究机构、研究实验室、标准化团体以及政府。
* **５.W3C Recommendations**
W3C 最重要的工作是发展 Web 规范（称为推荐，Recommendations），这些规范描述了 Web 的通信协议（比如 HTML 和 XHTML）和其他的构建模块。

每项 W3C 推荐的发展是通过由会员和受邀专家组成的工作组来完成的。工作组的经费来自公司和其他组织，并会创建一个工作草案，最后是一份提议推荐。一般来说，为了获得正式的批准，推荐都会被提交给 W3C 会员和主任。

## 二、MDN简介
**MDN Web Docs（旧称：Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一個汇集众多Mozilla基金会产品和网络开发文档的免费网站。**
* **1.历史**
该项目始于2005年，最初由Mozilla公司员工Deb Richardson领导。自2006年以来，文档工作由Eric Shepherd领导。

网站最初的内容是由DevEdge提供，但在AOL收购Netscape后，DevEdge网站也宣布关闭。为此Mozilla基金会向AOL获取了DevEdge发布的内容，同时将DevEdge内容搬移到mozilla.org。

MDN本身有一个论坛，并在Mozilla IRC网络上有一个IRC频道#mdn。MDN由Mozilla公司提供服务器和员工的资助。

2016年10月3日发表的Brave网页浏览器将MDN作为其搜索引擎选项之一。

## 三、HTML 所有标签列表
参看链接：[HTML5元素列表](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5/HTML5_element_list)
### 根元素
![](https://i.loli.net/2018/10/18/5bc860231c798.jpg)

### 文档元数据
![](https://i.loli.net/2018/10/18/5bc8605214f97.jpg)

### 脚本
![](https://i.loli.net/2018/10/18/5bc86084200ee.jpg)

### 章节
![](https://i.loli.net/2018/10/18/5bc860b6ba91d.jpg)

### 组织内容
![](https://i.loli.net/2018/10/18/5bc860ecda2c5.jpg)

### 文字形式
![](https://i.loli.net/2018/10/18/5bc86132a96d1.jpg)
![](https://i.loli.net/2018/10/18/5bc86160cc0c3.jpg)

### 编辑
![](https://i.loli.net/2018/10/18/5bc861929b460.jpg)

### 嵌入内容
![](https://i.loli.net/2018/10/18/5bc861c2449af.jpg)

### 表格
![](https://i.loli.net/2018/10/18/5bc861f2a28be.jpg)

### 表单
![](https://i.loli.net/2018/10/18/5bc86229783ff.jpg)

### 交互元素
![](https://i.loli.net/2018/10/18/5bc8626068354.jpg)

另请参阅：
[HTML5](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5)
[HTML元素大全](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element)，包括 HTML5 中不再有效的元素。

## 四、什么是空标签
**没有闭合的标签称为空标签，如：&lt;br/&gt;和&lt;img/&gt;等。一个空元素（empty element）可能是 HTML，SVG，或者 MathML 里的一个不可能存在子节点（例如内嵌的元素或者元素内的文本）的element。**
在 HTML 中，通常在一个空元素上使用一个闭标签是无效的。例如， &lt;input type="text"&gt; &lt;/input&gt;的闭标签是无效的 HTML。
在 HTML 中有以下这些空元素：
* [&lt;area&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/area)
* [&lt;base&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/base)
* [&lt;br&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/br)
* [&lt;col&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/col)
* [&lt;colgroup&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/colgroup)
* [&lt;command&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/command)
* [&lt;embed&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/embed)
* [&lt;hr&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/hr)
* [&lt;img&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img)
* [&lt;input&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input)
* [&lt;keygen&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/keygen)
* [&lt;link&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link)
* [&lt;meta&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta)
* [&lt;param&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/param)
* [&lt;source&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/source)
* [&lt;track&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/track)
* [&lt;wbr&gt;](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/wbr)

## 五、什么是可替换标签
**在CSS里，可替换元素(replaced element)的展现不是由CSS来控制的。这些元素是一类外观渲染独立于CSS的外部对象。**
**典型的可替换元素有&lt;img&gt;、&lt;object&gt;、&lt;video&gt;和表单元素，如&lt;textarea&gt;、&lt;input&gt;。某些元素只在一些特殊情况下表现为可替换元素，例如&lt;audio&gt;和&lt;canvas&gt;。通过CSS的content属性来插入的对象被称为匿名可替换对象(annoymous replaced elements)。**
**CSS在某些情况下会对可替换元素做特殊处理，比如计算外边距和一些auto值。**
**需要注意的是，一部分（并非全部）可替换元素，本身具有尺寸和基线(baseline)，会被想vertical-align之类的一些CSS属性用到。**
另可见：[css语法](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Syntax)

HTML的基础学习可以完成以下链接的题目：[W3schools 的 HTML 测试题](https://www.w3schools.com/quiztest/quiztest.asp?qtest=HTML)

