## AssetBundle资源打包

AssetBundles 是有 Unity 编辑器在编辑环境中(enit-time)创建的一些列的文件，这些文件可以被用在项目的运行环境中(run-time)。 AssetBundles 可以包括的资源文件有模型文件（models）、材质（materials）、纹理（textures）和场景（scenes）。AssetBundles 不能包含脚本文件。具体来说，一个 AssetBundle 就是把一系列的资源文件或者场景文件以某种方式紧密保存的一个文件。这个 AssetBundle 文件可以被单独加载到可执行的应用程序中。AssetBundles 可以由被 Unity 构建的游戏或者应用按需加载使用。这允许对像模型、纹理、音频、甚至是整个的游戏场景这样的资源进行流式加载和异步加载。AssetBundles 可以预缓存（pre-cached）和存储在本地，这样在运行时就可以立即加载它们。但是 AssetBundles 技术的主要的目的是在需要的时候能够从远端的服务器上按需请求特定的资源，并加载到游戏中。AssetBundles 可以包含 Unity 可以识别的任何类型的资源，包括自定义的二进制数据。唯一的例外是，脚本资源是不被允许的。

## AssetBundle和Reoursrces的区别

其实Resources.Load()本质和AssetBundle相差不大，只不过是从一个缺省打进程序包里面的AssetBundle里加载资源。然而我们知道一旦游戏打包出来之后Resources文件夹就不存在了，而其中的资源也被打包到程序里面看不到了。所以要实现资源的热更不能采用这个方法。而且Resource这种方式为了保证Prefabs的依赖完整性会导致共同包含的依赖项重复，会大大增加游戏资源包的大小。而且AssetBundle支持动态下载替换，是Unity Web Caching License唯一可以缓存的内容。 

## AssetBundle工作流程

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/AssetBundle/images/Image1.png)

在开发过程中，开发人员需要准备AssetBundle资源和上传到服务器

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/AssetBundle/images/Image2.png)

在工作中，开发人员也可以根据需求在服务器上加载自己所需的AssetBundle资源，然后应用到自己的应用程序当中

## 安装注意

下载WAMP并安装。在安装完成后你需要设置一下默认浏览器，选择桌面的Internet或者他浏览器完成安装。运行WAMP，屏幕右下角的W图标即是WAPA软件，右键点击WAMP图标-language-chinese,可将语言设置为中文。
左键点击WAMP图标-启动所有服务，开启服务器。左键点击WAMP图标-切换到在线状态。
左键点击WAMP图标-www目录，新建一个文件夹并命名为Unity,拖入一张图片（这里以link.png为例）

如果安装完成之后显示为黄色，点击我的电脑——管理——服务和应用程序——服务——MySQL——调成手动——停止——确定。

## 资源指定

创建一个游戏物体，Cube或者Sphere,把它们拖拽成预制体，然后选中预制体，在Inspector窗口下的最下方有一个栏AssetBundle，用于设置将要导出的资源包

如图：

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/AssetBundle/images/Image3.png)

点击None下拉按钮，点击New...按钮，在输入栏中填写想要命名名称（比如modle），告诉unity这个资源需要打包到名为modle的AssetBundle中

## AssetBundle文件生成、上传

```
using UnityEngine;
using System.Collections;
using UnityEditor;

public class BundleAssets : MonoBehaviour {

	[MenuItem("Build/ModleAsset")]
    static void BundleAssetMainAsset()
    {
        //输出的路径
        string path = Application.dataPath;
        //打包的资源
        AssetBundleBuild[] AssetBundle = new AssetBundleBuild[1];
        //要打包的文件
        AssetBundle[0].assetBundleName = "modle";
        //要打包预制体的路径名
        string[] AssetName = new string[3] { "Assets/Prefab/Cube.prefab", "Assets/Prefab/Sphere.prefab", "Assets/Prefab/Terrain.prefab" };

        AssetBundle[0].assetNames = AssetName;
        //构建AssetBundles文件的方法                       //选择资源包的关系类型                            //打包的目标平台
        BuildPipeline.BuildAssetBundles(path,AssetBundle,BuildAssetBundleOptions.DeterministicAssetBundle,BuildTarget.StandaloneWindows64);
    }   
}
```
![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/AssetBundle/images/Image4.png)

点击菜单栏的Build/ModleAsset上传，然后再Project点击右键打开文件夹，将文件移动到unity文件夹中。

## 下载AssetBundle

```
using UnityEngine;
using System.Collections;

public class AssetsBundle : MonoBehaviour {

    public string URL = "http://localhost/UNity/modle";

    void Start()
    {
        StartCoroutine(DownLoadAsset(URL));
    }

    IEnumerator DownLoadAsset(string URL)
    {
        WWW www = new WWW(URL);

        yield return www;

        if(www.isDone)
        {
            GameObject go = www.assetBundle.LoadAsset("Terrain.prefab") as GameObject;
            GameObject.Instantiate(go);
        }
        www.Dispose();
    }
}
```

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/AssetBundle/images/Image6.png)


```WWW.LoadFromCacheOrDownload();```这个下载函数是AssetBundle专用的，可以很方便地处理AssetBundle文件的版本更新。在通过此函数下载AssetBundle后，资源会被缓存至本地储存起来；在下次调用此函数时，如果AssetBundle有新版本则下载新版本，如果没有新版本则不下载而直接从本地读取。
缓存的资源可以通过Caching.CleanCache()函数全部删除。































