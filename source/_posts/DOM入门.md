---
title: DOM入门
date: 2019-01-19 13:00:31
tags:
---
## DOM简介
### 1.文档对象模型（Document Object Model，简称DOM）
是W3C组织推荐的处理可扩展标志语言的标准编程接口。在网页上，组织页面（或文档）的对象被组织在一个树形结构中，用来表示文档中对象的标准模型就称为DOM。Document Object Model的历史可以追溯至1990年代后期微软与Netscape的“浏览器大战”，双方为了在JavaScript与JScript一决生死，于是大规模的赋予浏览器强大的功能。微软在网页技术上加入了不少专属事物，既有VBScript、ActiveX、以及微软自家的DHTML格式等，使不少网页使用非微软平台及浏览器无法正常显示。DOM即是当时蕴酿出来的杰作。

### 2.节点
根据 DOM，HTML 文档中的每个成分都是一个节点。
DOM 是这样规定的：
整个文档是一个文档节点
每个 HTML 标签是一个元素节点
包含在 HTML 元素中的文本是文本节点
每一个 HTML 属性是一个属性节点
注释属于注释节点

### 3.Node层次
节点彼此都有等级关系。
HTML 文档中的所有节点组成了一个文档树（或节点树）。HTML 文档中的每个元素、属性、文本等都代表着树中的一个节点。树起始于文档节点，并由此继续伸出枝条，直到处于这棵树最低级别的所有文本节点为止。
![节点树示意图](https://i.loli.net/2019/01/19/5c42b1359999b.jpg)

### 4.优点和缺点
DOM的优势主要表现在：易用性强，使用DOM时，将把所有的XML文档信息都存于内存中，并且遍历简单，支持XPath，增强了易用性。

DOM的缺点主要表现在：效率低，解析速度慢，内存占用量过高，对于大文件来说几乎不可能使用。另外效率低还表现在大量的消耗时间，因为使用DOM进行解析时，将为文档的每个element、attribute、processing-instruction和comment都创建一个对象，这样在DOM机制中所运用的大量对象的创建和销毁无疑会影响其效率。

## Node类型
Node是一个接口，许多DOM类型从这个接口继承，并允许类似地处理（或测试）这些各种类型。
以下接口都从Node继承其方法和属性：
Document, Element, Attr, CharacterData (which Text, Comment, and CDATASection inherit), ProcessingInstruction, DocumentFragment, DocumentType, Notation, Entity, EntityReference。
在方法和属性不相关的特定情况下，这些接口可能返回null。它们可能会抛出异常 - 例如，当将子节点添加到不允许子节点存在的节点时。

### 属性
从其父类EventTarget继承属性。
1. Node.childNodes（只读）
返回一个包含了该节点所有子节点的实时的NodeList。NodeList 是“实时的”意思是，如果该节点的子节点发生了变化，NodeList对象就会自动更新。
2. Node.firstChild （只读）
返回该节点的第一个子节点Node，如果该节点没有子节点则返回null。
3. Node.isConnected（只读）
返回一个布尔值用来检测该节点是否已连接(直接或者间接)到一个上下文对象上，比如通常DOM情况下的Document对象，或者在shadow DOM情况下的ShadowRoot对象。
4. Node.lastChild （只读）
返回该节点的最后一个子节点Node，如果该节点没有子节点则返回null。
5. Node.nextSibling （只读）
返回与该节点同级的下一个节点 Node，如果没有返回null。
6. Node.nodeName （只读）
返回一个包含该节点名字的DOMString。节点的名字的结构和节点类型不同。比如HTMLElement的名字跟它所关联的标签对应，就比如HTMLAudioElement的就是 'audio' ，Text节点对应的是 '#text' 还有Document节点对应的是 '#document'。
7. Node.nodeType（只读）
返回一个与该节点类型对应的无符号短整型的值，后面作为重点详细介绍。
8. Node.parentNode （只读）
返回一个当前结点 Node的父节点 。如果没有这样的结点,，比如说像这个节点是树结构的顶端或者没有插入一棵树中， 这个属性返回null。
9. Node.parentElement （只读）
返回一个当前节点的父节点 Element 。 如果当前节点没有父节点或者说父节点不是一个元素(Element), 这个属性返回null。
10. Node.previousSibling （只读）
返回一个当前节点同辈的前一个结点( Node) ，或者返回null（如果不存在这样的一个节点的话）。

### nodeType
nodeType 属性可用来区分不同类型的节点，比如 元素, 文本 和 注释。
```
var type = node.nodeType;
```
返回一个整数，其代表的是节点类型。

| 常量 |	值	| 描述 |
| :------| :------: | :------: |
| Node.ELEMENT_NODE |	1	| 一个 元素 节点，例如 `<p>` 和 `<div>`。|
| Node.TEXT_NODE    |	3	|  Element 或者 Attr 中实际的 文字 |
| Node.PROCESSING_INSTRUCTION_NODE |	7	| 一个用于XML文档的 ProcessingInstruction ，例如 `<?xml-stylesheet ... ?>` 声明。|
| Node.COMMENT_NODE  |	8	| 一个 Comment 节点。|
| Node.DOCUMENT_NODE |	9	| 一个 Document 节点。|
| Node.DOCUMENT_TYPE_NODE  |	10	| 描述文档类型的 DocumentType 节点。例如 `<!DOCTYPE html> ` 就是用于 HTML5 的。|
| Node.DOCUMENT_FRAGMENT_NODE  |	11	| 一个 DocumentFragment 节点。|

## 节点创建API
节点创建API主要包括 createElement 、 createTextNode 、 cloneNode 和 createDocumentFragment 四个方法。
### createElement
```
let element = document.createElement(tagName[, options]);
```
（1）参数
* tagName
指定要创建元素类型的字符串,创建元素时的nodeName使用tagName的值为初始化,该方法不接受使用限定名称(如:"html:a"),在HTML文档上调用createElement()方法创建元素之前会将tagName转化成小写,在Firefox, Opera 和 Chrome内核中. createElement(null) 等同于 createElement("null")
* options(可选)
一个可选的参数 ElementCreationOptions 是包含一个属性名为 is的对象, 该对象的值是用 customElements.define()方法定义过的一个自定义元素的标签名。 为了向前兼容较老版本的 Custom Elements specification, 有一些浏览器会允许你传一个值为自定义元素的标签名的字符串作为该参数的值. 可以看 Extending native HTML elements 仔细了解如何使用该参数。
这个新元素会有一个 is 属性，该属性值为自定义元素的标签名。注意，自定义元素是一项只在某些浏览器可用的实验性特性。

（2）返回值
The new Element.
* element 是创建的Element对象。
* tagName 指定将要创建的元素类型的字符串。创建的element的nodeName会被初始化为tagName的值。该方法不接受带条件的元素名字(例如: html:a)。
* options 是一个可选的 ElementCreationOptions 对象. 如果这个对象被定义并赋予了一个 is 特性，则创建的element的 is 属性会被初始化为这个特性的值. 如果这个对象没有 is 特性，则值为空.

### createTextNode
创建一个新的文本节点.
```
var text = document.createTextNode(data);
```
(1)参数
* text 是一个文本节点.
* data 是一个字符串,包含了放在文本节点中的内容.

### cloneNode
Node.cloneNode() 方法返回调用该方法的节点的一个副本.
```
var dupNode = node.cloneNode(deep);
```
**node**
将要被克隆的节点
**dupNode**
克隆生成的副本节点
**deep** (可选)
是否采用深度克隆,如果为true,则该节点的所有后代节点也都会被克隆,如果为false,则只克隆该节点本身.

### createDocumentFragment
创建一个新的空白的文档片段( DocumentFragment)。
```
let fragment = document.createDocumentFragment();
```
fragment 是一个指向空DocumentFragment对象的引用。

## 页面修改型API
修改页面内容的api主要包括：appendChild，insertBefore，removeChild，replaceChild。
### appendChild
Node.appendChild() 方法将一个节点添加到指定父节点的子节点列表末尾。
```
var child = node.appendChild(child);
```
node 是要插入子节点的父节点.
child 即是参数又是这个方法的返回值.

### insertBefore
insertBefore用来添加一个节点到一个参照节点之前.
```
parentNode.insertBefore(newNode,refNode);
```
parentNode表示新节点被添加后的父节点
newNode表示要添加的节点
refNode表示参照节点，新节点会添加到这个节点之前

### removeChild
Node.removeChild() 方法从DOM中删除一个子节点。返回删除的节点。
```
let oldChild = node.removeChild(child);
//OR
element.removeChild(child);
```
child 是要移除的那个子节点.
node 是child的父节点.
oldChild保存对删除的子节点的引用. oldChild === child.
被移除的这个子节点仍然存在于内存中,只是没有添加到当前文档的DOM树中,因此,你还可以把这个节点重新添加回文档中,当然,实现要用另外一个变量比如上例中的oldChild来保存这个节点的引用. 如果使用上述语法中的第二种方法, 即没有使用 oldChild 来保存对这个节点的引用, 则认为被移除的节点已经是无用的, 在短时间内将会被内存管理回收.

### replaceChild
用指定的节点替换当前节点的一个子节点，并返回被替换掉的节点。
```
replacedNode = parentNode.replaceChild(newChild, oldChild);
```
newChild 用来替换 oldChild 的新节点。如果该节点已经存在于DOM树中，则它会被从原始位置删除。
oldChild  被替换掉的原始节点。
replacedNode 和oldChild相等。

## 节点查找API
### 1. document.getElementById ：
（1）参数
* 根据ID查找元素，大小写敏感，如果有多个结果，只返回第一个；
* element是一个 Element 对象。如果当前文档中拥有特定ID的元素不存在则返回null.
（1）返回值
* 返回一个匹配到 ID 的 DOM Element 对象。若在当前 Document 下没有找到，则返回 null。

由于元素的 ID 在大部分情况下要求是独一无二的，这个方法自然而然地成为了一个高效查找特定元素的方法。不同于其他 Element 查找方法（如Document.querySelector() 以及 Document.querySelectorAll()），getElementById() 只有在作为 document 的方法时才能起作用，而在DOM中的其他元素下无法生效。这是因为 ID 值在整个网页中必须保持唯一。因此没有必要为这个方法创建所谓的 “局部” 版本。
```
var element = document.getElementById(id);
```

### 2. document.getElementsByClassName ：
根据类名查找元素，多个类名用空格分隔，返回一个 HTMLCollection 。注意兼容性为IE9+（含）。另外，不仅仅是document，其它元素也支持 getElementsByClassName 方法；
```
var elements = document.getElementsByClassName(names); // or:
var elements = rootElement.getElementsByClassName(names);
```
elements 是一个实时集合，包含了找到的所有元素。
names 是一个字符串，表示要匹配的类名列表；类名通过空格分隔
getElementsByClassName 可以在任何元素上调用，不仅仅是 document。 调用这个方法的元素将作为本次查找的根元素.

### 3. document.getElementsByTagName ：
根据标签查找元素， * 表示查询所有标签，返回一个 HTMLCollection 。
```
var elements = document.getElementsByTagName(name);
```
elements 是一个由发现的元素出现在树中的顺序构成的动态的HTML集合 HTMLCollection 。
name 是一个代表元素的名称的字符串。特殊字符 "*" 代表了所有元素。
**注意：**当在一个HTML 文件上执行时， getElementsByTagName() 会在执行前把参数转换为小写字母。这是试着在一个HTML文件的子树匹配驼峰命名法的 SVG 元素时不希望的。 document.getElementsByTagNameNS() 在那种情况下会有用. 

### 4. document.getElementsByName ：
根据元素的name属性查找，返回一个 NodeList 。

```
elements = document.getElementsByName(name);
```

elements 是一个实时更新的 NodeList 集合。
name 是元素的 name 属性的值。
**注意：**
* getElementsByName  在不同的浏览器其中工作方式不同。在IE和Opera中， getElementsByName()  方法还会返回那些 id 为指定值的元素。所以你要小心使用该方法，最好不要为元素的 name 和 id 赋予相同的值。 
* IE 和 Edge 都返回一个 HTMLCollection, 而不是NodeList 。

### 5. document.querySelector ：
返回单个Node，IE8+(含），如果匹配到多个结果，只返回第一个。如果找不到匹配项，则返回null。

```
element = document.querySelector(selectors);
```

（1）参数
* selectors包含一个或多个要匹配的选择器的 DOM字符串DOMString。 该字符串必须是有效的CSS选择器字符串；如果不是，则引发SYNTAX_ERR异常。
**提示:**必须使用反斜杠字符转义不属于标准CSS语法的字符。 由于JavaScript也使用退格转义，因此在使用这些字符编写字符串文字时必须特别小心。
（2）返回值
* 表示文档中与指定的一组CSS选择器匹配的第一个元素的 html元素Element对象。
（3）异常
* SYNTAX_ERR指定selectors的语法无效。

### 6. document.querySelectorAll ：
返回一个 NodeList ，IE8+(含）。

```
elementList = parentNode.querySelectorAll(selectors);
```

（1）参数
* 一个 DOMString 包含一个或多个匹配的选择器。这个字符串必须是一个合法的 CSS selector 如果不是，会抛出一个 SyntaxError 错误。
（2）返回值
* 一个静态 NodeList，包含一个与至少一个指定选择器匹配的元素的Element对象，或者在没有匹配的情况下为空NodeList。
（3）异常
* SyntaxError如果指定的 选择器 不合法，会抛出错误。如$("##div")


### 7. document.forms ：
获取当前页面所有form，返回一个 HTMLCollection ；

```
let collection = document.forms; 
```

## 节点关系API
DOM中的节点相互之间存在着各种各样的关系，如父子关系，兄弟关系等。
### 父关系API
* parentNode：每个节点都有一个parentNode属性，它表示元素的父节点。Element的父节点可能是Element，Document或DocumentFragment。
* parentElement：返回元素的父元素节点，与parentNode的区别在于，其父节点必须是一个Element，如果不是，则返回null

### 子关系API
* childNodes：返回一个即时的NodeList，表示元素的子节点列表，子节点可能会包含文本节点，注释节点等。
* children：一个即时的HTMLCollection，子节点都是Element，IE9以下浏览器不支持。
* firstNode：第一个子节点
* lastNode：最后一个子节点
* hasChildNodes方法：可以用来判断是否包含子节点。

### 兄弟关系型API
previousSibling：节点的前一个节点，如果该节点是第一个节点，则为null。注意有可能拿到的节点是文本节点或注释节点，与预期的不符，要进行处理一下。
previousElementSibling：返回前一个元素节点，前一个节点必须是Element，注意IE9以下浏览器不支持。

nextSibling：节点的后一个节点，如果该节点是最后一个节点，则为null。注意有可能拿到的节点是文本节点，与预期的不符，要进行处理一下。
nextElementSibling：返回后一个元素节点，后一个节点必须是Element，注意IE9以下浏览器不支持。

## 元素属性型API
### setAttribute
设置指定元素上的一个属性值。如果属性已经存在，则更新该值; 否则将添加一个新的属性用指定的名称和值。要获取属性的当前值，使用 getAttribute(); 要删除一个属性，调用removeAttribute()。
```
element.setAttribute(name, value);
```
name 是表示属性名称的字符串
value 是属性的新值

### getAttribute
getAttribute() 返回元素上一个指定的属性值。如果指定的属性不存在，则返回  null 或 "" （空字符串）
```
let attribute = element.getAttribute(attributeName);
```
attribute 是一个包含 attributeName 属性值的字符串。
attributeName 是你想要获取的属性值的属性名称。

## 元素样式API
### window.getComputedStyle
Window.getComputedStyle()方法返回一个对象，该对象在应用活动样式表并解析这些值可能包含的任何基本计算后报告元素的所有CSS属性的值。 私有的CSS属性值可以通过对象提供的API或通过简单地使用CSS属性名称进行索引来访问。
```
let style = window.getComputedStyle(element, [pseudoElt]);
```
**element**
 用于获取计算样式的Element。
**pseudoElt** (可选)
指定一个要匹配的伪元素的字符串。必须对普通元素省略（或null）。

返回的style是一个实时的 CSSStyleDeclaration 对象，当元素的样式更改时，它会自动更新本身。

### getBoundingClientRect
Element.getBoundingClientRect()方法返回元素的大小及其相对于视口的位置。
```
rectObject = object.getBoundingClientRect();
```
返回值是一个 DOMRect 对象，这个对象是由该元素的 getClientRects() 方法返回的一组矩形的集合, 即：是与该元素相关的CSS 边框集合 。

DOMRect 对象包含了一组用于描述边框的只读属性——left、top、right和bottom，单位为像素。除了 width 和 height 外的属性都是相对于视口的左上角位置而言的。
![示意图](https://i.loli.net/2019/01/19/5c42ced469f7d.png)
空边框盒会被忽略。如果所有的元素边框都是空边框，那么这个矩形给该元素返回的 width、height 值为0，left、top值为第一个css盒子（按内容顺序）的top-left值。

当计算边界矩形时，会考虑视口区域（或其他可滚动元素）内的滚动操作，也就是说，当滚动位置发生了改变，top和left属性值就会随之立即发生变化（因此，它们的值是相对于视口的，而不是绝对的）。如果你需要获得相对于整个网页左上角定位的属性值，那么只要给top、left属性值加上当前的滚动位置（通过window.scrollX和window.scrollY），这样就可以获取与当前的滚动位置无关的值。