## HTTP概念

超文本传输协议（HTTP、HyperText Transfer Protocol）是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个标准

## HTTP请求响应模型

1. HTTP是一个客户端和服务器端请求和应答的标准

2. 通过HTTP或者HTTPS协议请求的资源由统一资源标识符（Uniform Resource Identifiers）（或者更标准一些，URLs）来标识。

3. 在浏览器的地址栏输入网址叫做URL（Uniform Resource Locator，统一资源定位符），就像每家每户都有一个门牌地址一样，
每个网页也都有一个Internet地址，挡在浏览器的地址框中输入一个URL或者单击一个超级链接时，URL就确定了浏览的地址，浏览器通过超文本传输协议（HTTP），
将Web服务器上站点网页代码提取出来。并翻译成网页。

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/Http/images/20161215215617.jpg)

**HTTP协议永远都是客户端发起请求，服务器端会送响应**

## 常用请求方式

GET和POST是HTTP协议所规定的两种通讯方式（客户端向服务器传递数据的两种方式）

**GET**

把数据放到HTTP协议的URL里，对多只能传输1024字节

格式：http://127.0.0.1:80/1405A/test.php ?name=testUser&pwd=123

特点：安全性低、传输量小、速度快

**POST**

以表单提交数据，数据在HTTP的协议体中，理论上没有传输数据的最大限制

特点： 数据量大、安全性高

## POST和GET对比

**GET**
优点：便于测试 、简洁明了    缺点：信息量比较小。安全性相对低

**POST**
优点：信息量大、安全性相对高    缺点：测试不方便

## 通过网页认识HTTP请求

通过模拟用户登录操作来演示Get和POST请求的不同，由于采用的服务器端为php语言，所以需要安装一个支持php的web服务器。

[下载地址](http://www.wampserver.com/)

[安装WampServer参考](http://jingyan.baidu.com/article/2d5afd69efe9cf85a3e28e54.html)

案例：请求

1.创建一个能够输入用户名和密码的Html页面login_get.html,本次案例采用get方式请求
```
<html>
<head>
  <meta charset="utf-8">
  <title>模拟用户登录</title>
</head>
<body>
  <span>模拟用户登录GET</span>

  <!--
  创建一个表单，用于向服务器传递用户名和密码、

  form为表单对象
  action对应的表单需要由哪个网页处理
  method 数据请求的方式
  -->
  <form action="login_get.php" method="get">
     <span>账号: <input type="text" value=""  id="username" name="username"></span><br />
     <span>密码: <input type="password" value=""  id="password" name="password"></span><br />
     <input type="submit" value="登录"/>
  </form>
</body>
<html>
```
将编写好的文件，复制到Wamp安装目录下WWW文件夹中，通过浏览器访问此文件 http://localhost/login.html

页面效果：
![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/Http/images/20161229213924.jpg)

在编写服务器php脚本，用来接收html页面传递的用户名和密码，经过处理后，输出一些提示信息

login_get.php
```
<?php
//接收传递过来的变量name
  $name=$_GET["username"];

//接收到的密码
  $pwd=$_GET["password"];

  echo  "用户名是".$name.","."密码是:".$pwd."<br/>";
  if($name=="admin"){
    if($pwd=="123"){
      echo "欢迎管理员登录!";
    }else{
      echo "密码不正确，回去想想吧！";
    }
  }else{
    echo "普通用户，我也不知道密码对不对！";
  }
?>
```
将编写好的login.php文件放在login.html相同目录下

在HTML在页面中输入用户名和密码，点击登录按钮将会自动将用户名和密码传递给login_get.php处理

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/Http/images/20161229214418.jpg)


案例：post

当采用post方式传递数据时，需要将表单中的method属性改为post

login_post.html
```
<html>
<head>
  <meta charset="utf-8">
  <title>模拟用户登录</title>
</head>
<body>
  <span>模拟用户登录 POST</span>

  <!--
  创建一个表单，用于向服务器传递用户名和密码、

  form为表单对象
  action对应的表单需要由哪个网页处理
  method 数据请求的方式
  -->
  <form action="login_post.php" method="post">
     <span>账号: <input type="text" value=""  id="username" name="username"></span><br />
     <span>密码: <input type="password" value=""  id="password" name="password"></span><br />
     <input type="submit" value="登录"/>
  </form>
</body>
<html>
```

login_post.php
```
<?php

//接收传递过来的变量name
  $name=$_POST["username"];

//接收到的密码
  $pwd=$_POST["password"];

  echo  "用户名是".$name.","."密码是:".$pwd."<br/>";
  if($name=="admin"){
    if($pwd=="123"){
      echo "欢迎管理员登录!";
    }else{
      echo "密码不正确，回去想想吧！";
    }
  }else{
    echo "普通用户，我也不知道密码对不对！";
  }

?>
```
浏览器显示

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E6%95%B0%E6%8D%AE%E5%A4%84%E7%90%86%E5%8F%8AHTTP%E5%BA%94%E7%94%A8/Http/images/20161229215401.jpg)















































