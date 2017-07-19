# XML操作案例及序列化和反序列化


### XML创建内容

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image.png)

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image1.png)

点击CrateXml会在Assets路径中创建一个Xml文件，并且写入相应内容
```
using System.Xml;
public class CreateXml : MonoBehaviour {
  public string filepaht;
  void Start () {
   	filepaht = Application.dataPath+"/xiayifan.xml";    //xml文本存放路径
  }
  void OnGUI()
	{
		if (GUI.Button (new Rect (0, 0, 100, 40),"CreatXml"))
		{	 
		    CrateXmlFile();
		}
  }

  void CrateXmlFile()
  {
    XmlDocument xmldoc = new XmlDocument ();           //创建XmlDocument对象
		XmlElement root = xmldoc.CreateElement ("root");   //创建本文的节点对象（root）
    XmlElement Book = xml.CreateElement ("book");
		XmlElement Title = xml.CreateElement ("title");
    XmlElement Author = xml.CreateElement ("author");
		XmlElement Year = xml.CreateElement ("year");
    XmlElement Price = xml.CreateElement ("price");

    Book.SetAttribute ("category", "悬疑");      //设置book节点的属性
		Title.InnerText =  "盗墓笔记";                    //定义title节点内容
		Author.InnerText = "南派三叔";
		Year.InnerText = "2007";
		Price.InnerText = "198.99";

		Book.AppendChild (Title);                    //让book成为title的父节点
		Book.AppendChild (Author);
		Book.AppendChild (Year);
		Book.AppendChild (Price);
		root.AppendChild (Book);
    xml.AppendChild (root);

		xml.Save (filepaht);                          //保存XML到指定路径
  }

}

```

### XML添加内容

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image2.png)

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image3.png)


点击AddXml会在原有的基础上添加一段新内容：
```
void OnGUI()
{
    if (GUI.Button (new Rect (0, 50, 100, 40), "AddXml"))
    {
     AddXmlFile();   
    }
}
void AddXmlFile()
{
    XmlDocument xmldoc = new XmlDocument ();
		xmldoc.Load (filepaht);                     //读取以保存的Xml文件
		XmlElement root = xmldoc.SelectSingleNode ("root") as XmlElement; //选择root根节点
    XmlElement Book = xml.CreateElement ("book");  //创建本文的节点对象(book)
    XmlElement Title = xml.CreateElement ("title");
    XmlElement Author = xml.CreateElement ("author");
    XmlElement Year = xml.CreateElement ("year");
    XmlElement Price = xml.CreateElement ("price");

    Book.SetAttribute ("category", "历史");      //设置book节点的属性
    Title.InnerText =  "三国演义";                    //定义title节点内容
    Author.InnerText = "罗贯中";
    Year.InnerText = "1366";
    Price.InnerText = "298";

    Book.AppendChild (Title);                    //让book成为title的父节点
    Book.AppendChild (Author);
    Book.AppendChild (Year);
    Book.AppendChild (Price);
    root.AppendChild (Book);
    xml.AppendChild (root);

    xml.Save (filepaht);                          //保存XML到指定路径
}
```

### XML更新内容

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image4.png)

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image5.png)

点击UpdateXml会更新Xml文件里的year选项：
```
void OnGUI()
{
  if (GUI.Button (new Rect (0, 100, 100, 40), "UpdateXml"))
  {
  	 UpdateXmlFile();   
  }

}
void UpdateXmlFile()
	{
		XmlDocument xmldoc = new XmlDocument ();
		xmldoc.Load (filepaht);
		XmlNodeList nodelist = xmldoc.SelectSingleNode("root").SelectNodes("book"); //获取root下的所有book节点
		/*
		for (int i = 0; i < nodelist.Count; i++)
		{
			for (int j= 0; j < nodelist[i].ChildNodes.Count; j++) {
				if(nodelist[i].ChildNodes[j].Name == "price")
				{
					nodelist[i].ChildNodes[j].InnerText = "998";
				}
			}
		}*/
		foreach (XmlNode node in nodelist)
    {
			foreach (XmlNode item in node.ChildNodes)
		  {
  	    if(item.Name=="year")
				{
           item.InnerText = "2017";  
           print(item.InnerText);
				}
			}
		}
		xmldoc.Save (filepaht);
	}
 ```

### XML删除内容

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image6.png)

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/XML%E7%BC%96%E5%86%99%E8%A7%84%E8%8C%83/XML%E6%95%B0%E6%8D%AE%E6%93%8D%E4%BD%9C%E5%8F%8A%E5%BA%8F%E5%88%97%E5%8C%96%E5%92%8C%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96/images/Image7.png)

点击DeleXml会删除掉Xml文件里的year选项中的内容

```
void OnGUI()
{
  if (GUI.Button (new Rect (0, 150, 100, 40), "DeleXml"))
  	{
  		DeleXmlFile();   
  	}
}
void DeleXmlFile()
	{
		XmlDocument xmldoc = new XmlDocument ();
		xmldoc.Load (filepaht);
		XmlNodeList nodelist = xmldoc.SelectSingleNode("root").SelectNodes("book");
		foreach (XmlNode node in nodelist)
		{
			foreach (XmlNode item in node.ChildNodes) {
				if(item.Name == "year")
				{
					item.RemoveAll();   //删除节点内容
					//item.RemoveChild(item);//删除节点
				}
			}
		}
		xmldoc.Save (filepaht);
	}
```

## XML序列化和反序列化

### 序列化的实质

序列化是吧一个对象持久化到一个磁盘中的过程。应用程序的一部分，甚至另一个应用程序都可以反序列化对象。是他们的状态序列化之前相同，

其中会用到System.Xml.Serialization命名空间，反序列化可以理解为把这个过程倒过来再来一遍

### XML 序列化过程的描述：

System.Xml.Serialization命名空间中最重要的类是Xmlserializer.要序列化对象，首先需要实例化一个XmlSerializer对象，指定要序列化的对象类型，
然后实例化一个流/写入器对象，以把文件写入流/文档中，最后一步是在XmlSerializer上调用Serializer()方法，给他传递流/写入器和要序列化的对象
 被序列化的数据可以为基本类型的数据、字段、数组、以及XmlElement和XmlAttribute对象格式的内嵌XML。
 
### XML反序列化过程的描述

从XML文档中反序列化对象，应执行上述逆向过程，创建一个流/读取器对象和一个XmlSerializer对象，然后给DeSerializer()方法传递该流/读取器对象，这个方法返回序列化的对象。尽管他需要强制转换为正确的类型。

1.实际代码演示：序列化一个游戏物体（例如：玩家，怪物，NPC等）对象的实例，可以将它的数据（例如：位置，名字, 等级，血量，经验）序列化到XML中。


## XML序列化实例

* 首先创建一个PlayerData类。

```
public class PlayerData   //  需要序列化的玩家数据类   
{
    public struct _Pos   // 结构类型
    {
        public float x,y,z;   // 表示位置的坐标点X,Y,Z;
    }
    public _Pos pos;

    private string name;
    public string Name      // 人物名称
    {
        get{ return name;}
        set{name =value ;}
    }
}
```
2.创建一个TestXmlSerializer类操作序列化过程，
```
using System.Xml;
using System.Xml.Serialization;
using System.IO;
public class TestXmlSerializer : MonoBehaviour
{
public GameObject Player;        //定义玩家对象
PlayerData data;                       // 定义玩家数据
string filepath;                         // 路径
void Start()
   {
      data = new PlayerData(）;      // 实例化对象
      filepath =  Application.dataPath+"/PlayerData.xml";   // 创建XML文件的路径
   }
void OnGUI()
    {
         if(GUI.Button(new Rect(10,10,100,20),"SaveData"))    
        {
            data.pos.x = Player .transform.position.x;
            data.pos.y = Player .transform.position.y;    
            data.pos.z = Player .transform.position.z;
            data.Name = Player .name;                                   // 将Plyer信息赋给玩家数据的对象；
            XmlSerializerData(data);                                        // 然后将数据序列化
        }
    }
void XmlSerializerData(data)
   {
        StreamWriter sr;                                                       //流/写入器对象
        FileInfo info = new FileInfo (filepath);                       //创建filepath路径下的文件对象
        print (info);
        if (!info.Exists) {                                              // 判断路径是否存在，不存在则创建，存在则删除再创建
            sr = info.CreateText ();
        }else
        {
            info.Delete();
            sr = info.CreateText();
        }
        XmlSerializer xs = new XmlSerializer (typeof(PlayerData));       // XmlSerializer对象并且指定序列化类型
        xs.Serialize (sr, data);                                         //  序列化方法（传递流/写入器对象，和玩家数据对象）
        sr.Close ();                                                                              //  关闭流
       }
}

```

## XML反序列化实例

.创建一个TestXmlDeSerializer类，那么其实反序列化的关键就在于DeSerializer方法的使用。

```
using System.Xml;
using System.Xml.Serialization;
using System.IO;
public  class TestXmlDeSerializer: MonoBehaviour
{
public GameObject Player;        //定义玩家对象
PlayerData data;                       // 定义玩家数据
string filepath;                         // 路径
Vector3 TempPos;
void Start()
   {
      data = new PlayerData(）;      // 实例化对象
      filepath =  Application.dataPath+"/PlayerData.xml";   // 创建XML文件的路径
   }
void OnGUI
   {
     if (GUI.Button (new Rect (10, 40, 100, 20), "LoadData"))
        {
           data = DeSerializerData();                                // 接受返回的反序列化出来的的对象
           TempPos = new Vector3(data.pos.x,data.pos.y,data.pos.z);   // 将反序列化出来的数据（坐标）赋给临时坐标
           Player .transform.position = TempPos;             
           Player .name = data.Name;                             //  然后把该数据再转给现在的玩家
        }
    }
PlayerData DeSerializerData()
   {
         PlayerData playerdata = new PlayerData ();
         FileStream f = new FileStream (filepath,FileMode.Open);      //  打开filepath路径中的XML文件（文件流对象）
         XmlSerializer xs = new XmlSerializer (typeof(PlayerData));     // 指定需要操作的对象类型
         playerdata = (PlayerData)xs.Deserialize (f);           //  反序列化成一个object对象然后强制转化成PlyerData类型
         print (playerdata.pos.x+","+ playerdata.pos.y+","+ playerdata.pos.z); // 打印出序列化之前（反序列化之后）的 玩家数据
         return playerdata;          // 返回这个对象
     }
}

```


## 课上代码

```
using UnityEngine;
using System.Collections;
using System.IO;
using System.Xml;
using System.Xml.Serialization;
public class TestXmlSerializer : MonoBehaviour {

    public GameObject Player;//定义玩家对象
    PlayerDate date;//定义玩家数据
    string filepath;//路径
	void Start () {
        filepath = Application.dataPath + "/PlayerDate.xml";//创建Xml文件路径
        date = new PlayerDate();//实例化对象
        Player = GameObject.Find("Cube");

	}
    void OnGUI()
    {
        if(GUI.Button(new Rect(0,0,100,40),"SaveDate"))
        {
            
            date.name = "aaa";
            date.HP = 1000;
            date.MP = 100;
            date.Attack = 45;
            date.Armor = 10;
            date.Crit = 1.1;
            date.pos.X = Player.transform.position.x;
            date.pos.Y = Player.transform.position.y;
            date.pos.Z = Player.transform.position.z;
            SaveDate(date);
        }
        if(GUI.Button(new Rect(0,40,100,40),"LoadDate"))
        {
            date = LoadDate();
            Vector3 v3 = new Vector3(date.pos.X, date.pos.Y, date.pos.Z);
            Player.transform.position = v3;

        }
    }
    void SaveDate(PlayerDate player)
    {
        StreamWriter sw; //流/写入器对象
        FileInfo info = new FileInfo(filepath);//创建filepath路径下的文件对象
        
        //判断路径是否存在，不存在就创建，存在就删除在创建
        if(!info.Exists)
        {
            sw = info.CreateText();
        }
        else
        {
            info.Delete();
            sw = info.CreateText();
        }
        XmlSerializer xs = new XmlSerializer(typeof(PlayerDate));
        xs.Serialize(sw, date);//  序列化方法（传递流/写入器对象，和玩家数据对象
        sw.Close();//关闭流
    }
    PlayerDate LoadDate()
    {
        PlayerDate play = new PlayerDate();
        FileStream fs = new FileStream(filepath, FileMode.Open);//打开filepath路径中的xml文件
        XmlSerializer xs = new XmlSerializer(typeof(PlayerDate));//指定需要操作的对象
        play = (PlayerDate)xs.Deserialize(fs);

        return play;

    }
}
public class PlayerDate  //需要序列化的玩家数据
{
    //玩家数据
    public string name;
    public int HP;
    public int MP;
    public int Attack;
    public int Armor;
    public double Crit;

    public Pos pos;
    public struct Pos   //结构类型
    {
        public float X, Y, Z;//坐标
    }

}
```




























