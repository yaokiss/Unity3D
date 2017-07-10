在XML中编写注释的语法与HTML的语法很相似
```
<!-- This is a comment -->
```

在XML中。空格会被保留。HTML中会把多个连续的空格字符裁减（合并）为一个
```
HTML:	Hello           my name is David.
输出:	Hello my name is David.

```
在XML中。文档中的空格不会被删节

## XML的语法规则

* XML文档必须有根元素
* 所哟XML元素都须有关闭标签
* XML标签对大小写敏感
* XML必须正确的嵌套
* XML的属性值须加引号

## XML文档必须有根元素

XMl文档必须有一个元素是所有其他元素的父元素，钙元素称为根元素
```
<root>
  <child>
    <subchild>.....</subchild>
  </child>
</root>
```
## 所有XML元素都须有关闭标签

在HTML经常会看到没有关闭标签的元素
```
<p>This is a paragraph
<p>This is another paragraph
```

在XML中，所有元素都必须有关闭标签，不能省略，
```
<p>This is a paragraph</p>
<p>This is another paragraph</p>
```

## XML标签对大小写敏感

XML元素使用XML标签进行定义

XML标签对大小写敏感，在XML中标签<Letter>与标签<letter>是不同的

必须使用相同的大小写来编写打开标签和关闭标签
```
<Message>这是错误的。</message>

<message>这是正确的。</message>
```
打开标签和关闭标签通常被称为开始标签和结束标签

## XML必须正确的嵌套

在HTML中，常会看到没有正确嵌套的元素
```
<b><i>This text is bold and italic</b></i>
```
在XML中所哟元素都必须彼此正确的嵌套
```
<b><i>This text is bold and italic</i></b>
```
在上例中，正确嵌套的意思是：由于```<i>```元素是在```<b>```元素内打开的，那么它必须在```<b>```元素内关闭。

## XML的属性值须加引号

与HTML类似，XML也可以拥有属性（名称，值的对）

在XML中，XML的属性值须加引号。

错误格式：
```
<note date=08/08/2008>
  <to>George</to>
  <from>John</from>
</note>
```

正确格式：
```
<note date="08/08/2008">
  <to>George</to>
  <from>John</from>
</note>
```
## XML中的特殊字符

所有XML文档中的文本均会被及解析器解析

在处理XML数据时，特殊符号要特殊处理，不能和节点字符混淆

在XML中。一些字符拥有特殊的意义

如果你把字符```"<"```放在XML元素中，会发生错误，这是因为解析器会把他当做新元素的开始

产生错误：
```
<message>if salary < 1000 then</message>
```

为了避免这个错误，用实体引用来代替```"<"``` 字符
```
<message>if salary &lt; 1000 then</message>
```

编码 | 对应字符 | 说明
-----|--------|-----|
```&lt;```|  ``` <``` | 小于|
```&gt;```|   ```>```  | 大于|
```&amp;```|  ```& ``` | 和号|
```&apos;```| ```'```  | 单引号|

```&quot;```“ |引号|注释：在 XML 中，只有字符 ”<“ 和 ”&" 确实是非法的。大于号是合法的，但是用实体引用来代替它是一个好习惯。

## CDATA区段

术语 CDATA 指的是不应由 XML 解析器进行解析的文本数据（Unparsed Character Data）。
在 XML 元素中，“<” 和 “&” 是非法的。
“<” 会产生错误，因为解析器会把该字符解释为新元素的开始。
“&” 也会产生错误，因为解析器会把该字符解释为字符实体的开始。
某些文本，比如 JavaScript 代码，包含大量 “<” 或 “&” 字符。为了避免错误，可以将脚本代码定义为 CDATA。
CDATA 部分中的所有内容都会被解析器忽略。
CDATA 部分由 “<![CDATA[“ 开始，由 ”]]>” 结束：

```
<script>
<![CDATA[
  function matchwo(a,b)
  {
  if (a < b && a < 0) then
    {
    return 1;
    }
  else
    {
    return 0;
    }
  }
]]>
</script>

```


# XML 数据操作

## 加载xml文件

```
<root>
  <data>
      <student id="1">
        <name>张三</name>
        <age>20</age>
      </student>
      <student id="2">
        <name>李四</name>
        <age>30</age>
      </student>
  </data>
</root>
```
当此文件放置在Assets目录下，加载代码如下

```
XmlDocument doc = new XmlDocument();
doc.Load(Application.dataPath + @"/data.xml");
```
## 通过字符串变量的形式穿件xmlDocument
```
XmlDocument doc = new XmlDocument();
string xmldata ="<root><data><student id='1'><name>张三</name><age>20</age></student><student id = '2'><name>李四</name><age>30</age></student></data></root>";
doc.LoadXml(xmldata);
```
## XML处理预备知识

在整个XML处理中，需要使用到的几个类的关系图

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C/images/20161205175000.jpg)

* XMLElement主要是针对节点的一些属性进行操作
* XMLDocument主要是针对节点的CUID操作
* XMLNode为抽象类，作为以上两类的基类，提供一些操作节点的方法

### 获取XML 根元素
```
XmlDocument doc = new XmlDocument();
doc.Load(Application.dataPath + @"/data.xml");

//获取到根元素
XmlElement root = doc.DocumentElement;
```

## 选取的结点

关于结点的选取常用的方法
* SelectSingleNode用于获取单个结点
* SelectNodes用于获取多个同名结点

假设我们想获取所有student的信息,那必须要先访问到data结点，此时需要使用的方法是```XmlElement.__SelectSingleNode__```(结点标记名)
```
   //选定students结点
   XmlNode data = root.SelectSingleNode("data");
```
当获取到data结点后，才能对所有的student信息进行访问。对于多个同名元素的访问，需要使用```XmlNode.__SelectNodes__```(结点名)
```
  XmlNodeList list=data.SelectNodes("student");
```
如果多个元素不同名，可以通过获取单个结点的方式单独访问，或者直接使用```XmlNode.__ChildNodes__ ```属性来获取所有的子结点。
```
  XmlNodeList list=data.ChildNodes;
```


## 元素及属性访问

1.获取元素

案例1：获取李四的年龄
```
//获取李四的年龄
XmlNode node = list[1].SelectSingleNode("age");
//输出此结点的xml内容
print(node.OuterXml);
//只获取age标签内的文本
print(node.InnerText);
```

2.获取属性

对于属性的获取，可以使用以下方式:
* XmlElement的GetAttribute方法
* XmlNode的Attributes属性数组

```
//获取李四的序号
XmlNode node2 = list[1];
//将结点转为XmlElement
XmlElement xl = (XmlElement)node2;
//通过GetAttribute方法
print(xl.GetAttribute("id"));

//通过属性方式
print(node2.Attributes[0].Value);
```









































