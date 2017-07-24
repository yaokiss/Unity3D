## 常用JSON库简介

不推荐：
* Json.NET .NET自带的JSON库，缺点：比较臃肿
* MiniJson 缺点：不支持自定义的序列化
* LitJson 缺点：IOS平台支持不太友好 ，制作Android平台可以考虑

推荐
* MyJson
https://github.com/lightszero/myjson
* SimpleJson
http://blog.csdn.net/kakashi8841/article/details/21877131

强烈推荐
* JsonFX

## Litjson配置

将库脚本或动态库（Litjson.dll）置在Assets目录下的Plugins文件夹中，因为Plugins文件夹中的脚本会先运行

## Json的生成

使用JsonData生成普通Json

```
    JsonData data=new JsonData();
      data["name"] = "zhansan";
      data["age"] = 28;
      data["sex"] ="male";
      string  json1= data.ToJson();
      Debug.Log(json1);

      ---------------运行结果-----------------
      {"name":"zhansan","age":28,"sex":"male"}
```

使用JsonMapper生成Json

【player.cs】

```
using System.Collections;
public class Player {
    public string name { get; set; }
    public int age { get; set; }
    public string sex { get; set; }
}
```

将player对象转为Json格式

```
	  Player player = new Player();
    player.name = "peiandsky";
    player.age = 23;
    player.sex = "male";
    string json=JsonMapper.ToJson(player);

```

## 使用JsonWritter生成Json

对象类型json
```
 JsonWriter writer = new JsonWriter();
    writer.WriteObjectStart ();
    writer.WritePropertyName("name");
    writer.Write("xiayifan");
	writer.WritePropertyName("age");
	writer.Write (18);
	 writer.WritePropertyName("sex");
	writer.Write("男");
	writer.WriteObjectEnd ();

	Debug.Log(writer.ToString());

	------------输出结果----------
   {"name":"xiayifan","age":18,"sex":"男"}
```

数组类型json

```
JsonWriter writer = new JsonWriter();
writer.WriteArrayStart();
writer.Write("one");
writer.Write("two");
writer.Write("three");
writer.Write("four");
writer.WriteArrayEnd();

Debug.Log(writer.ToString());

------------输出结果----------
["one","two","three","four"]

```

## 解析JSON

使用JsonMapper解析上述json

```
JsonData jsonData2 = JsonMapper.ToObject(json2);
    Debug.Log(jsonData2["name"] + "  " + data2["info"]["sex"]);

    ---------------运行结果-----------------
    zhansan male

```

使用JsonMapper解析JSON数据给指定对象

```
   string json='{"name":"zhansan","age":28,"sex":"male"}';
   Player player=JsonMapper.ToObject<Player>(json);
   Debug.Log("name="+player.name+" age="+player.age);

   name=zhansan age=28

```

遍历JsonData的key和value
由于JsonData实现了IDictionary接口，所以可以使用Foreach进行遍历

```
JsonData jd = new JsonData();
jd["name"] = "张三";
jd["age"] = 35;
IDictionary dic=jd as IDictionary;
foreach (string key in dic.Keys)
{
	print(key);
}
```

```

using UnityEngine;
using System.Collections;
using LitJson;

public class CreateJson : MonoBehaviour {

    string str = @"{""name"":""xiaoer"",""Age"":20}";
    string play = "{'Name':'xiaoxiao','Age':25,'Sex':'男'}";
    string str1 = "{'游戏名字': 'World of Warcraft','游戏类型': '角色扮演','职业': 'DK','等级': 110,'成就点数': 17000,'坐骑数量': 200}";
    string str2 = @"{'电子称': [{'商品': '凯丰厨房秤电子称0.01g精准迷你珠宝秤0.1g家用称重烘焙食物克称','价格': 25,'运费': '免运费','付款人数': 44606,'地址': '金华'},
                     {'商品': '香山厨房称重烘焙电子称精准宝珠称迷你食物称0.1g厨房秤台秤克秤','价格': 49,'运费': '免运费','付款人数': 5243,'地址': '上海'},
                     {'商品': '精准迷你家用电子称0.1g厨房秤烘焙克称食物称重烘焙0.1小天平','价格': 25,'运费': '免运费','付款人数': 20311,'地址': '金华'}]}";
	void Start () {

        //JsonData date = JsonMapper.ToObject(str1);
        //print(date["游戏名字"]);
        //print(date["游戏类型"]);
        //print(date["职业"]);
        //print(date["等级"]);
        //print(date["成就点数"]);
        //print(date["坐骑数量"]);

        //遍历Key和Value
        JsonData date2 = JsonMapper.ToObject(str2);
        print(date2["电子称"].ToJson());
        print(date2["电子称"][0]["商品"]);
        print(date2["电子称"][1].ToJson());
        print(date2["电子称"][2].ToJson());

        IDictionary id = date2["电子称"][0] as IDictionary;
        foreach (var Key in id.Keys)
        {
            print(Key);
        }
        foreach (var Value in id.Values)
        {
            print(Value);
        }

        ////解析
        //JsonData date = JsonMapper.ToObject(str);
        //print(date["name"]);
        //print(date["Age"]);

        ////生成JSON
        //JsonData jd = new JsonData();
        //jd["name"] = "zhangsan";
        //jd["age"] = 20;
        //jd["sex"] = "男";
        //string jdstr = jd.ToJson();
        //print(jdstr);

        ////嵌套结构JSON
        //JsonData da = new JsonData();
        //da["name"] = "lisi";
        //da["info"] = new JsonData();
        //da["info"]["age"] = 10;
        //da["info"]["sec"] = "女";
        //string dastr = da.ToJson();
        //print(dastr);

        ////定义Player对象
        //Player player = new Player();
        //player.Name = "wangwu";
        //player.Age = 12;
        //player.SeX = "nan";
        //string players = JsonMapper.ToJson(player);
        //print(players);

        //JsonWriter jsonwriter = new JsonWriter();
        //jsonwriter.WriteObjectStart();
        //jsonwriter.WritePropertyName("Name");
        //jsonwriter.Write("小强");
        //jsonwriter.WritePropertyName("Age");
        //jsonwriter.Write(19);
        //jsonwriter.WritePropertyName("Sex");
        //jsonwriter.Write("男");
        //jsonwriter.WriteObjectEnd();
        //print(jsonwriter.ToString());
	}
	
	// Update is called once per frame
	void Update () {
	
	}
}

public class Player
{
    public string Name { get;set ;}
    public int Age { get; set; }
    public string SeX { get; set; }
}
```












































