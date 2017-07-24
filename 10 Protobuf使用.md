## Protobuf简介

Protocol Buffers是 Google公司开发的一种 数据描述语言，类似于 XML能够将结构化数据序列化，可用于数据存储、 通信协议等方面。它不依赖于语言和平台并且可扩展性极强。现阶段官方支持C++、JAVA、Python等三种编程语言，但可以找到大量的几乎涵盖所有语言的第三方拓展包。

protobuf-net地址：https://github.com/mgravell/protobuf-net


## Protobuf的优点

同XML相比，Protocol buffers在序列化结构化数据方面有许多优点：
* 1. 更简单

* 2. 数据描述文件只需原来的1/10至1/3

* 3. 解析速度是原来的20倍至100倍

* 4. 减少了二义性

* 5. 生成了更容易在 编程中使用的数据访问类

* 6. 支持多种编程语言

## Protobuf性能分析

如下列图所示，Protobuf性能相对较好，应用领域包括：网络传输，配置文件，数据存储等

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image.png)

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image1.png)

## Protobuf语法规则

###　指定字段类型

所有的字段都是标量类型：string、bool类型、int类型等等，当然，你也可以为字段指定其他的合成类型，包括枚举（enumerations）或其他消息类型。

### 分配标识号

在消息定义中，每个字段都有唯一的一个标识符。这些标识符是用来在消息的二进制格式中识别各个字段的，一旦开始使用就不能够再改。

* 注：[1,15]之内的标识号在编码的时候会占用一个字节。[16,2047]之内的标识号则占用2个字节。所以应该为那些频繁出现的消息元素保留 [1,15]之内的标识号

*切记：要为将来有可能添加的、频繁出现的标识号预留一些标识号。
最小的标识号可以从1开始，最大到229 - 1, or 536,870,911。不可以使用其中的[19000－19999]的标识号， Protobuf协议实现中对这些进行了预留。如果非要在.proto文件中使用这些预留标识号，编译时就会报警。

### 指定字段规则

所指定的消息字段修饰符必须是如下之一：
* required：不可增加或删除的字段，必须初始化；
* optional：可选字段，可删除，可以不初始化；
* repeated：可重复字段(对应C#里面的List)。

### 标量数值类型

一个标量消息字段可以含有一个如下的类型——该表格展示了定义于.proto文件中的类型，以及与之对应的、在自动生成的访问类中定义的类型：

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image3.png)

向.proto文件添加注释，也跟C#语法一样(//)的语法格式，如：
```
message SearchRequest
{
    required string query =1;
    optional int32 page_number =2; //最终返回的页数
    optional int32 result_per_page =3; //每页返回的结果数   
}
```

### 枚举类型

```cs
message SearchRequest
{
required string query = 1;
optional int32 page_number = 2;
optional int32 result_per_page = 3 [default = 10];
enum Corpus {
UNIVERSAL = 0;
WEB = 1;
IMAGES = 2;
LOCAL = 3;
NEWS = 4;
PRODUCTS = 5;
VIDEO = 6;
}
optional Corpus corpus = 4 [default = UNIVERSAL];
}

```

### 嵌套类型

```
package Cmd;
	message Person
	{
	    message Address
	    {
	         required string Line1 = 1;
	         required string Line2 = 2;
	    }
    	required int32 Id = 1;
	    required string Name = 2;
	    required Address address = 3;
  }
```


### 多重嵌套

```
package Cmd;
message Outer {
  message MiddleAA{
    message Inner {
      required int64 ival = 1;
      optional bool  booly = 2;
    }
  }
  message MiddleBB {
    message Inner {
      required int32 ival = 1;
      optional bool  booly = 2;
    }
  }
}
```

### 引用外部定义的消息类型

```
UserData.proto
	message UserItem
	{
		required string userId = 1;
		required string userName = 2;
	}
Test.proto
	package Cmd;
	import "UserData.proto";
	message Test
	{
		optional string name = 1;
		required UserItem userItem = 2;
	}
```

## Protobuf例子

protobuf应用于C#Model的实际案例,代码：

```
Package Cmd;
message Person
{
	optional string Child = 1;
	repeated string Parent = 2;
	required string Name = 3;
	required bool Gender = 4;
	required string Msg = 5;
}
```

然后将Protobuf格式的问价转化成我们熟知的C#的Modl

首先在dos下cd到protogen.exe然后再输入

protogen.exe -i:PersonInfo.proto -o:PersonInfo.cs  （可以手动拖动）

效果如下图：

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image2.png)


## Protobuf的序列化和反序列化

序列化是指将结构化的数据俺一定的编程规范转成指定格式的过程。

反序列化是指将转成指定格式的数据解析成原始的结构化数据的过程


创建一个Person类

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image4.png)

```
using System.IO;
using System.Text;
using ProtoBuf;
namespace protobuf_test
{
    class ProtobufHelper
    {
        /// <summary>
        /// 序列化成string
        /// </summary>
        /// <typeparam name="T"></typeparam>
        /// <param name="t"></param>
        /// <returns>返回字符串</returns>
        public static string Serialize<T>(T t)
        {
            using (MemoryStream ms = new MemoryStream())
            {
                Serializer.Serialize<T>(ms, t);
                return Encoding.UTF8.GetString(ms.ToArray());
            }
        }
        /// <summary>
        /// 序列化到文件
        /// </summary>
        /// <typeparam name="T"></typeparam>
        /// <param name="path"></param>
        /// <param name="data"></param>
        public static void Serialize<T>(string path, T data)
        {
            using (Stream file = File.Create(path))
            {
                Serializer.Serialize<T>(file, data);
                file.Close();
            }
        }
        /// <summary>
        /// 根据字符串反序列化成对象
        /// </summary>
        /// <typeparam name="T"></typeparam>
        /// <param name="content"></param>
        /// <returns></returns>
        public static T DeSerialize<T>(string content)
        {
            using (MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(content)))
            {
                T t = Serializer.Deserialize<T>(ms);
                return t;
            }
        }
        /// <summary>
        /// 根据文件流返回对象
        /// </summary>
        /// <typeparam name="T"></typeparam>
        /// <param name="filestream"></param>
        /// <returns></returns>
        public static T DeSerialize<T>(Stream filestream)
        {
            return Serializer.Deserialize<T>(filestream);
        }

    }
}
```

利用以上代码进行序列化和反序列化

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image5.png)

控制台输出结果

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image6.png)

Unity中使用Protobuf序列化和反序列化

创建一个PersonInfo.proto文件

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image7.png)

 把PersonInfo.proto文件生成PesonInfo.cs文件，再将生成PersonInfo.cs文件打开浏览  然后拖到unity中

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image8.png)

完成Unity中代码，效果图如下：（注意：（ProtobufHelper类如上）此过程是序列化到文本中）

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image9.png)

Unity输出内容：

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Protobuf/images/Image10.png)


需要把protobuf-net.dll拖到unity中引用
















































