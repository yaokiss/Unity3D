## 认识unity中的www

WWW是一种unity开发中常用的工具类，主要提供一般http访问功能，以及动态从网上下载图片、声音、视频unity资源

主要支持的协议：
* http://
* https://
* file://
* ftp://(只支持匿名账号)

其中file:// 访问的是本地文件


## www加载网络资源

这里指的网络资源指图片，文本，视频，音频等各种格式的资源。实际上WWW类具有很多实用的属性与资源对应，如下 :
* assetbundle:
AssetBundle的数据流，可以包含项目文件夹中的任何类型资源。
* audioClip(声音) 从下载的数据，返回一个AudioClip。（只读）
* bytes(字节数组) 以字节组的形式返回获取到的网络页面中的内容(只读)。
* movie(视频) 从下载的数据，返回一个MovieTexture（只读）。
* text(文本,XML,Json) 通过网页获取并以字符串的形式返回内容(只读)。
* texture(图片) 从下载的数据返回一个Texture2D

## 使用WWW实现资源加载

图片地址：

[](https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo/bd_logo1_31bdc765.png)

使用UGUI在界面上添加一个RawImage组件，并创建一个LoadTexture脚本。   UI——RawImage

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/Http%E5%9C%A8Unity%E4%B8%AD%E4%BD%BF%E7%94%A8/images/20170116131040.jpg)

LoadTexture代码
```
using UnityEngine;
using System.Collections;
using UnityEngine.UI;

public class LoadTexture : MonoBehaviour {
    // 图片地址
    private string url = "https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo/bd_logo1_31bdc765.png";
    private RawImage img;
	// Use this for initialization
	void Start () {
        //获取RawImage组件
        img = this.transform.FindChild("RawImage").GetComponent<RawImage>();
        StartCoroutine(DoLoad());
	}


    IEnumerator DoLoad()
    {
        WWW www = new WWW(url);
        //挂起程序段，等资源下载完成后，继续执行下去  
        yield return www;

        //判断是否有错误产生  
        if (string.IsNullOrEmpty(www.error))
        {
            //把下载好的图片显示到RawImage中  
            img.texture = www.texture;
            //释放资源  
            www.Dispose();
        }
    }

}
```
运行后效果：![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/Http%E5%9C%A8Unity%E4%B8%AD%E4%BD%BF%E7%94%A8/images/20170116131544.jpg)

## WWW实现GET请求

代码：
```
using UnityEngine;
using System.Collections;

public class HttpGetDemo : MonoBehaviour
{

    //用于处理GET请求的页面地址
    private string url = "http://localhost/login_get.php?username=admin&password=123";

    // Use this for initialization
    void Start()
    {
        StartCoroutine(DoLoad());
    }


    IEnumerator DoLoad()
    {
        WWW www = new WWW(url);
        yield return www;

        //判断是否有错误产生  
        if (string.IsNullOrEmpty(www.error))
        {
            //输出服务器返回的内容
            print(www.text);

        }
    }
}
```
运行后效果：[](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/Http%E5%9C%A8Unity%E4%B8%AD%E4%BD%BF%E7%94%A8/images/20170116135746.jpg)

## WWW实现POST请求

代码：
```
using UnityEngine;
using System.Collections;

public class HttpPostDemo : MonoBehaviour
{

    //用于处理GET请求的页面地址
    private string url = "http://localhost/login_post.php";

    // Use this for initialization
    void Start()
    {
        StartCoroutine(DoLoad());
    }


    IEnumerator DoLoad()
    {
        //创建WWWForm对象
        WWWForm form = new WWWForm();
        //添加内容
        form.AddField("username", "admin");
        form.AddField("password", "123");

        //通过地址，表单构建WWW对象
        WWW www = new WWW(url,form);

        yield return www;

        //判断是否有错误产生  
        if (string.IsNullOrEmpty(www.error))
        {
            //输出服务器返回的内容
            print(www.text);

        }
    }
}
```
和get结果一样




```
using UnityEngine;
using System.Collections;
using UnityEngine.UI;

public class LoadTexture : MonoBehaviour {

    private string URL = "http://dl.bizhi.sogou.com/images/1440x900/2013/11/23/417539.jpg";

    private string phpurl = "http://localhost/UNity/login.php?username=admin&password=123";

    private string url_POST = "http://localhost/UNity/login.php";
    public RawImage image;

    private string music = "http://localhost/UNity/Fade.wav";
    public AudioSource audio;
	void Start () {
        audio = this.gameObject.GetComponent<AudioSource>();
       image = GameObject.Find("RawImage").GetComponent<RawImage>();
        StartCoroutine(LoadMusic(music));
        StartCoroutine(LoadDown(URL));
        //StartCoroutine(localLoad(phpurl));
        StartCoroutine(LoadPOST());
	}
    //使用WWW实现下载音乐   MP3不支持该平台，转换为mav格式
    IEnumerator LoadMusic(string url)
    {
        WWW www = new WWW(url);
        yield return www;

        if (www.isDone)
        {
            audio.clip = www.audioClip;
            audio.Play();
        }
        www.Dispose();
    }


    //使用WWW实现资源加载
    IEnumerator LoadDown(string url)
    {
        WWW www = new WWW(url);
        yield return www;

        if (www.isDone)
        {
            image.texture = www.texture;
        }
        www.Dispose();
    }

    //实现GET请求
    IEnumerator localLoad(string url)
    {
        WWW www = new WWW(url);
        yield return www;

        if(www.isDone)
        {
            print(www.text + "\n" + "GET");
        }
    }

    //实现POST请求
    IEnumerator LoadPOST()
    {
        WWWForm form = new WWWForm();

        form.AddField("username", "admin");
        form.AddField("password", "123");

        WWW www = new WWW(url_POST,form);
        yield return www;
        if(string.IsNullOrEmpty (www.error))
        {
            print(www.text + "\n" + "POST");
        }
    }
}
```


























