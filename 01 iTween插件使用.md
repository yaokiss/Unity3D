## iTween的基本原理

iTween的核心数数值插值，简单说就是给iTween两个数值(开始值，结束值)，它会自动生成一些中间值，大概像这样子, 开始值->中间值 -> 中间值 …. -> 结束值。
这里的数值可以理解为: 数字，坐标点，角度，物体大小，物体颜色，音量大小等等

## 下载地址
```
http://itween.pixelplacement.com
```

## iTween类介绍
ITween 类的公共操作接口均以静态方法的形式提供，可分为三大类；

* 1.静态注册方法：提供注册动画效果的静态方法接口，如：MoveTo、CameraFadeTo等

* 2.Update静态方法：提供美珍改变属性值得环境，在Update或循环环境中调用，如：MoveUpdate、AudioUpdate

* 2.外部工具方法： 包括动画控制、路径绘制等

iTween类内部定义三种枚举类型

* 1.EaseType：缓动类型枚举

```示例
http://robertpenner.com/easing/easing_demo.html
```

* 2.LoopType : 动画的循环类型枚举

* 3.NamedValueColor：已命名颜色枚举

## 功能

* 1.Fade： 淡入淡出

* 2.Look：旋转对象使其面朝指定位置

* 3.Move：移动位置，

* 4.Rotate：旋转指定欧拉角度

* 5.Scale：缩放大小

* 6.Punch：添加摇晃力

* 7.Shake：摆动对象

* 8.CameraFade：摄像机的淡入淡出

两种音频方法：

* 1.Audio：音量和音调的变化

* 2.Stab ：播放AudioClip一次，不用手动加载AudioSource组件

一种颜色变化方法：

* 1.Color：变换颜色

一种值变化方法：

* 1，ValueTo：返回一个“from”和“to”之间的插值，用以改变属性

每个方法一般有两种重载方式：最小定制选项、完全定制项。

Update类方法：提供每帧改变属性值的环境。在Update或FixedUpdate方法或类似于循环的环境中调用。

动画控制：Pause（暂停），Resume（恢复），Stop（停止并销毁iTween）

绘制方法：DrawLine(绘制线条)，DrawLineGizmos（绘制线条），DrawPath（绘制弯曲的路径）DrawPathGizmos（与DrawPath相同）

其他方法：Count（返回iTween的数量），PathLength（返回路径长度），PutOnPath（根据提供的百分比将物体放置于所提供路径上），PointOnPath（返回路径上指定百分比处的Vector3）

iTweenPath类：用于在Scene试图中编辑路径。

```C#
using UnityEngine;
using System.Collections;

public class ItweenTest : MonoBehaviour {
    Hashtable hashtable;
    public GameObject go;
    //Vector3[] v = { new Vector3(0, 0, 10), new Vector3(-10, 0, 10), new Vector3(-10, 0, 0), new Vector3(0, 0, 0) };//创建数组
    void Awake()
    {
        hashtable = new Hashtable();
        //hashtable.Add("position", new Vector3(0,0, 30));//到达这个位置
        hashtable.Add("time", 0.1f);//移动到该位置的时间
        hashtable.Add("speed", 5f);//移动到该位置的速度
       // hashtable.Add("path", v);//按照数组的坐标移动
        go = GameObject.Find("Image");//寻找这个图片，淡入淡出显示

    }
	void Start () {
       // iTween.MoveTo(this.gameObject, new Vector3(1, 1, 10), 2f);//移动到该位置
        //添加摇晃力
        iTween.PunchRotation(this.gameObject, new Vector3(this.transform.rotation.x + 100, this.transform.rotation.y + 100, this.transform.rotation.z + 100), 10f);
        iTween.PunchPosition(this.gameObject, new Vector3(this.transform.position.x + 5, this.transform.position.y + 5, this.transform.position.z + 5), 5f);
        //摆动
        iTween.ShakePosition(GameObject.Find("Sphere").gameObject, new Vector3(gameObject.transform.position.x + 10, gameObject.transform.position.y + 10, gameObject.transform.position.z + 10), 2f);
        //iTween.MoveTo(this.gameObject, hashtable);
        //iTween.FadeTo(go,0.1f,2f);//淡入淡出显示图片
       // iTween.FadeFrom(go,1f,2f);
	}
	
	// Update is called once per frame
	void Update () {
       // iTween.MoveTo(this.gameObject, hashtable);
        
	}
}
```
























