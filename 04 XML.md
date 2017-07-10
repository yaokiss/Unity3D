## XML的起源和目的

XML是Extensible Markup Language的缩写，即可扩展标记语言。它是一种用来创建的标记的标记语言。1996年，万维网协会（或者叫W3C，http://www.w3c.org ）开始设计一种可扩展的标记语言，1998年2月，XML1.0成为了W3C的推荐标准。

使用XML标记语言可以做到数据或数据结构在任何编程语言环境下的共享。例如我们在某个计算机平台上用某种编程语言编写了一些数据或数据结构，然后用XML标记语言进行处理，那样的话，其他人就可以在其他的计算机平台上来访问这些数据或数据结构，甚至可以用其他的编程语言来操作这些数据或数据结构了。这就是XML标记语言作为一种数据交换语言存在的价值。
       
## 什么事XML

* XML 指可扩展标记语言（EXtensible Markup Language）
* XML 是一种标记语言，很类似 HTML
* XML 的设计宗旨是传输数据，而非显示数据
* XML 标签没有被预定义。您需要自行定义标签。
* XML 被设计为具有自我描述性。
* XML 是 W3C 的推荐标准

案例:
下面是 John 写给 George 的便签，存储为 XML格式数据.
```
<?xml version="1.0" encoding="ISO-8859-1"?>
<note>
  <to>George</to>
  <from>John</from>
  <heading>Reminder</heading>
  <body>Don't forget the meeting!</body>
</note>
```
## XML特点

* XML仅仅是纯文本
* 通过XML可以发明自己的标签
* XML不是对HTML的代替，而是对HTML的补充

## XML和HTML的区别

XML和HTML都是用于操作数据或者数据结构，在结构上大致是相同的，但它们在本质上却存在明显的区别：

主要区别：

* 语法要求不同，HTML中不区分大小写，在XML中对大小写要求非常严格

* 标记不同，HTML使用固有的标记，而XML没有固有标记

* 作用不同，XML被设计用来传输和存储数据，HTML被设计用来显示数据

## XML的优势

每种语言的产生都有能完成某些特定的功能，XML作为一种标记语言也不例外，XML最大的优势在于它能对各种编程语言编写的数据进行管理，是的在任何平台下都能
通过解析器来读取XML数据

优势：

* 数据的搜索，在XML中可以提取文档中任何位置的数据
* 数据的显示，XML将数据的结构和数据的显示形式分开，根据需要使数据呈现出多种显示方式，比如：HTML，PDF格式
* 数据的交换，XML标记语言的语法非常简单，可以通过解析器在任何机器上解读，并可以在各种计算机平台上使用，逐渐成为一种数据交换语言。

# XML文档结构

XML文档形成一种树结构，从根开始，然后扩展到枝叶。

案例

XML使用简单的具有自我描述的语法；
```
<?xml version="1.0" encoding="ISO-8859-1"?>
<note>
<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
</note>
```
第一行是 XML 声明。它定义 XML 的版本 (1.0) 和所使用的编码 (ISO-8859-1 = Latin-1/西欧字符集)。

下一行描述文档的根元素（像在说：“本文档是一个便签”）：
```
<note>
```
接下来 4 行描述根的 4 个子元素（to, from, heading 以及 body）：
```
<to>George</to>
<from>John</from>
<heading>Reminder</heading>
<body>Don't forget the meeting!</body>
```
最后一行定义根元素的结尾
```
</note>
```

## XML的树形结构

XML 文档必须包含根元素，钙元素是所有其他元素的父元素

XML 文档中的元素形成了一颗文档树，这棵树从根部开始，并扩展到树的最低端

所有元素均可以拥有子元素
```
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```

父、子以及同胞等术语用于描述元素之间的关系。父元素拥有子元素。相同层级上的子元素成为同胞（兄弟或姐妹）。
所有元素均可拥有文本内容和属性（类似 HTML 中）

## 案例分析
```
<bookstore>
  <book category="COOKING">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
    <year>2005</year>
    <price>30.00</price>
  </book>
  <book category="CHILDREN">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
    <year>2005</year>
    <price>29.99</price>
  </book>
  <book category="WEB">
    <title lang="en">Learning XML</title>
    <author>Erik T. Ray</author>
    <year>2003</year>
    <price>39.95</price>
  </book>
</bookstore>
```

如果使用树形的结构图去描述XMl的方式，将会得到下面的一张图.

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E7%AE%80%E4%BB%8B/images/20161205131929.jpg)

例子中的根元素是bookstore。文档中的所有 book 元素都被包含在 bookstore 中。
book 元素有 4 个子元素：
```
* <title>
* <author>
* <year>
* <price>
```























































