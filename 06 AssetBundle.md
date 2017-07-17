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







































