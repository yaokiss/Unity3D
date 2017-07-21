
## 疯狂猜成语注册解析reg.php

```
using UnityEngine;
using System.Collections;
using System.Collections.Generic;
using LitJson;
using System.Xml;

public class UISignInHandler : UIHandler {

    private UIButton but;
    private UIButton button;
    private UILabel username;
    private UILabel password;
    private string URL = "http://localhost/crazyphrase/reg.php";
    void Start()
    {
        but = GetByName("back").GetComponent<UIButton>();
        EventDelegate.Add(but.onClick, denglu);
        button = GetByName("button").GetComponent<UIButton>();
        EventDelegate.Add(button.onClick, show);
        username = GetByName("NewName").GetComponent<UILabel>();
        password = GetByName("NewPwd").GetComponent<UILabel>();
    }
    void show()
    {
        print("111");
        StartCoroutine(Login(URL));

    }

    IEnumerator Login(string url)
    {
        WWWForm form = new WWWForm ();
        form.AddField ("username",username.text);
        form.AddField("password",password.text);
        //form.AddField("type","text");//text解析
        form.AddField("type", "json");
        form.AddField("type", "xml");

        WWW www = new WWW(url,form);
        
        yield return www;

        if(string.IsNullOrEmpty(www.error))
        {
            print(www.text);
            //string[] tmp = TextLoadStr(www.text);
            //UIAlertManager.instance.CreateAlert(this.gameObject, "UIAlert", "消息", tmp[1]);
            //List<string> tmp = JsonLoadStr(www.text);
            string[] tmpxml = XmlLoadstr(www.text);
            UIAlertManager.instance.CreateAlert(this.gameObject, "UIAlert",null, "消息", tmpxml[1]);
            
        }

    }

    //text解析
    //string[] TextLoadStr(string text)
    //{
    //    string[] str = text.Split('|');
    //    return str;
    //}

//json解析文件
    List<string> JsonLoadStr(string jsonstr)
    {
        List<string> liststr = new List<string>();
        JsonData jsondate = JsonMapper.ToObject(jsonstr);

        IDictionary idic = jsondate as IDictionary;
        foreach (var item in idic.Values)
        {
            liststr.Add(item.ToString());
        }
        return liststr;
    }

//xml解析
    string[] XmlLoadstr(string xmlstr)
    {
        string[] str = new string[2];
        XmlDocument xml = new XmlDocument();
        xml.LoadXml(xmlstr);
        for (int i = 0; i < xml.DocumentElement.ChildNodes.Count; i++)
        {
            str[i] = xml.DocumentElement.ChildNodes[i].InnerText;
        }
        return str;
    }
    void denglu()
    {
        UIGameManager.instance.Show(UIName.UILogin);
        UIGameManager.instance.Hide(UIName.UISignIn);
    }
}
```





















































