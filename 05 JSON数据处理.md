## JSON简介

JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。它基于ECMAScript的一个子集。 JSON采用完全独立于语言的文本格式，但是也使用了类似于C语言家族的习惯（包括C、C++、C#、Java、JavaScript、Perl、Python等）。这些特性使JSON成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成(一般用于提升网络传输速率)。

## JSON语法规则

* 数据在键值对中
* 数据由逗号分隔
* 花括号保存对象
* 方括号保存数组

## JSON键值对

JSON数据的书写格式是：键/值对

键/值对组合中的键写在前面（在双引号中）,值写在后面（在双引号中），中间用冒号隔开

```
"firstName":"John"
```
等价于JavaScipt语句
```
firstName="John"
```

## JSON值

* 数字（整数或者浮点数）
* 字符串（在双引号中）
* 逻辑符 （true 或 false）
* 数组（在方括号中）
* 对象（在花括号中）

## JSON基础结构

JSON结构有两种结构，这两种结构就是对象和数组两种结构，通过这两种结构可以表示各种复杂的结构。

1.对象

对象在js中表示为"{}"括起来的内容，数据结构为```{key;value,key:value,....}的键值对的结构，在面向对象的语言中，key为对象的属性，value为对应属性值
，所以很容易理解，取值方法为对象，key获取属性值，这个属性值得类型可以是数字、字符串、数组、对象几种。

案例
```
{"name" : "iphone","price" : 3000}
```

具体形式：

对象是一个无序的"键/值"对集合。
* 一个对象以"{"(左括号)开始， "}"(右括号)结束
* 每个"键"后边跟一个":"(冒号)
* “‘键/值’ 对”之间使用“,”（逗号）分隔。

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/JSON/JSON%E7%AE%80%E4%BB%8B/images/20161206174643.jpg)

例子
```
{
  "姓名":"大憨"，
  "年龄":24
}
```

案例
```
{"firstName":"Brett","lastName":"McLaughlin"}
```
firstName和lastName是键（key），而Brett和McLaughlin是值（value）

2.数组

数组在js中是中括号"[]"括起来的内容，数据结构为[“java”,“javascript”,“vb”,…]，取值方式和所有语言中一样，使用索引获取，字段值的数据类型可以是数字、字符串、数组、对象几种，

当需要表示一组值时，JSON不但能够提高可读性。而且可以减少复杂性，如果使用JSON，就只需要将多个花括号的记录分组在一起。

案例：通过JSON数据存储三位外国人的名字及邮箱
```
{
    "people":[
        {"firstName":"Brett","lastName":"McLaughlin","email":"aaa@163.com"},
        {"firstName":"Jason","lastName":"Hunter","email":"bbbb@163.com"},
        {"firstName":"Elliotte","lastName":"Harold","email":"cccc@163.com"}
    ]
}
```

具体形式

数组是值（value）的有序集合
* 一个数组以“[”（左中括号）开始，“]”（右中括号）结束。
* 值之间使用“,”（逗号）分隔。

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/JSON/JSON%E7%AE%80%E4%BB%8B/images/20161206174805.jpg)

```
{
    "学生": [
        {"姓名":"小明","年龄":23},
        {"姓名":"大憨","年龄":24}
    ]
}
```




























