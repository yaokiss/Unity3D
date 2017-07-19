## SQL语句

SQL 是一门 ANSI 的标准计算机语言，用来访问和操作数据库系统。SQL 语句用于取回和更新数据库中的数据。SQL 可与数据库程序协同工作，比如 MS Access、DB2、Informix、MS SQL Server、Oracle、Sybase 以及其他数据库系统。

说明:
* SQL 指结构化查询语言
* SQL 使我们有能力访问数据库
* SQL 是一种 ANSI 的标准计算机语言

不幸地是，存在着很多不同版本的 SQL 语言，但是为了与 ANSI 标准相兼容，它们必须以相似的方式共同地来支持一些主要的关键词（比如 SELECT、UPDATE、DELETE、INSERT、WHERE 等等）。

## SQL能做什么

* SQL 面向数据库执行查询
* SQL 可从数据库取回数据
* SQL 可在数据库中插入新的记录
* SQL 可更新数据库中的数据
* SQL 可从数据库删除记录
* SQL 可创建新数据库
* SQL 可在数据库中创建新表

## RDBMS关系型数据库管理系统

RDBMS 指的是关系型数据库管理系统。
RDBMS 是 SQL 的基础，同样也是所有现代数据库系统的基础，比如 MS SQL Server, IBM DB2, Oracle, MySQL 以及 Microsoft Access。

RDBMS 中的数据存储在被称为表（tables）的数据库对象中。

表是相关的数据项的集合，它由列和行组成。

## SQL DML 和DDL

可以把 SQL 分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。

SQL (结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。

**查询和更新指令构成了 SQL 的 DML 部分：**
* SELECT - 从数据库表中获取数据
* UPDATE - 更新数据库表中的数据
* DELETE - 从数据库表中删除数据
* INSERT INTO - 向数据库表中插入数据

SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

**SQL 中最重要的 DDL 语句:**
* CREATE DATABASE - 创建新数据库
* ALTER DATABASE - 修改数据库
* CREATE TABLE - 创建新表
* ALTER TABLE - 变更（改变）数据库表
* DROP TABLE - 删除表
* CREATE INDEX - 创建索引（搜索键）
* DROP INDEX - 删除索引

## 常用SQL语句

### 1.SELECT 语句

SELECT语句用于从表中选取数据，结果被存储在一个结果表中（称为结果集）

语法格式

**SQL语句对大小写不敏感，SELECT等效select

```
SELECT 列名称 FROM 表名称
SELECT * FROM 表名称
```

如需获取名为 “LastName” 和 “FirstName” 的列的内容（从名为 “Persons” 的数据库表），请使用类似这样的 SELECT 语句：
```
SELECT LastName,FirstName FROM Persons
```

“Persons” 表:

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144430.jpg)

查询结果：

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144642.jpg)

【SELECT案例二】

现在我们希望从 “Persons” 表中选取所有的列。
请使用符号 * 取代列的名称，就像这样：
```
SELECT * FROM Persons
```
提示：星号是选取所有列的快捷方式。
结果：

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144709.jpg)

### 2.WHERE 语句

如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句。
```
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
```
如果只希望选取居住在城市 “Beijing” 中的人，我们需要向 SELECT 语句添加 WHERE 子句：
```
SELECT * FROM Persons WHERE City='Beijing'
```
“Persons” 表

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144000.jpg)

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144256.jpg)

###　3.INSERT INTO 语句

INSERT INTO 语句用于向表格中插入新的行。
语法格式
```
INSERT INTO 表名称 VALUES (值1, 值2,....)
```
我们也可以指定所要插入数据的列：
```
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
```
【插入案例1】

“Persons” 表：

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144752.jpg)

SQL 语句：
```
INSERT INTO Persons VALUES ('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
```

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144818.jpg)

【插入案例2】
在指定的列中插入数据

“Persons” 表

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144844.jpg)

SQL 语句：
```
INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
```
![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209144859.jpg)


### 4.UPDATE

Update 语句用于修改表中的数据。

语法：
```
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```
Person表

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209145745.jpg)

【更新案例1】
更新某一行中的一个列
我们为 lastname 是 “Wilson” 的人添加 firstname：
```
UPDATE Person SET FirstName = 'Fred' WHERE LastName = 'Wilson'
```

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209145843.jpg)

更新案例2】
更新某一行中的若干列
我们会修改地址（address），并添加城市名称（city）：
```
UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing'
WHERE LastName = 'Wilson'
```
![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209150001.jpg)


### 4.DELETE语句

DELETE语句用于删除表中的行

语法格式
```
DELETE FROM 表名称 WHERE 列名称 = 值
```
![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209150220.jpg)

删除某行
“Fred Wilson” 会被删除：
```
DELETE FROM Person WHERE LastName = 'Wilson'
```
![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/%E5%8D%8F%E5%90%8C%E5%BC%80%E5%8F%91%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%9F%BA%E7%A1%80/%E6%95%B0%E6%8D%AE%E5%BA%93/%E6%95%B0%E6%8D%AE%E5%BA%935%E6%95%B0%E6%8D%AE%E5%BA%93SQL%E6%93%8D%E4%BD%9C/images/20161209150338.jpg)



```
using UnityEngine;
using System.Collections;
using MySql.Data;
using MySql.Data.MySqlClient;
public class MySQLtest : MonoBehaviour {
    //连接数据库的IP
    public string ServerIP = "localhost";
    //数据库的名字
    public string dataName = "yao";
    //用户名
    public string userID = "root";
    //密码
    public string Password = "yaojian";

    MySqlConnection mysqlconnetion;

    //连接数据库的字符串
    string connetionStr = "";

    string CmdText = "Select * From account;";
    string insert = "Insert into account values('xiaoqiang',1212,'男',12,'xiaoqiang@163.com');";
    string delete = "Delete From account Where 用户名 = 'xiaoqiang'";
    //string update = "Update account Set 用户名 ='小小' Where 用户名 = 'qqq';";
    string update = "Update account Set 年龄 = 111 where 用户名 = '小小'";
    string chazhao = "Select * From account Where 年龄 >=20;";
    void Start()
    {

        connetionStr = string.Format("Server = {0};Database= {1};user ID = {2};Password = {3}", ServerIP, dataName, userID, Password);
        mysqlconnetion = new MySqlConnection(connetionStr);
        if (mysqlconnetion != null)
        {
            mysqlconnetion.Open();
        }
        Insert(insert);
        Delete(delete);
        upData(update);
        ChaZhao(chazhao);

        //MySqlCommand commdan = new MySqlCommand(CmdText, mysqlconnetion);
        //MySqlDataReader reader = commdan.ExecuteReader();//反馈信息调用ExecuteReader
        //if (reader.HasRows)//判断是否有行数
        //{
        //    while (reader.Read())
        //    {
        //        string dataStr = "";
        //        dataStr += reader["用户名"] + ",";
        //        print(dataStr);
        //    }
        //}

        
    }

    void Insert(string insert)
    {
        //插入
        MySqlCommand command = new MySqlCommand(insert, mysqlconnetion);
        int hasRows = command.ExecuteNonQuery();//修改函数时调用ExecuteNonQuery
        print(hasRows + " 插入");
    }

    void Delete(string delete)
    {
        //删除
        MySqlCommand delet = new MySqlCommand(delete, mysqlconnetion);
        int del = delet.ExecuteNonQuery();
        print(del + " 删除");
    }
    void upData(string update)
    {
        //改
        MySqlCommand gai = new MySqlCommand(update, mysqlconnetion);
        int ga = gai.ExecuteNonQuery();
        print(ga + " 改");
    }
    void ChaZhao(string chazhao)
    {
        //查找
        MySqlCommand cz = new MySqlCommand(chazhao, mysqlconnetion);
       // int cha = cz.ExecuteNonQuery();
       // print(cha + " 查找");

        MySqlDataReader reader = cz.ExecuteReader();//反馈信息调用ExecuteReader
        if (reader.HasRows)//判断是否有行数
        {
            while (reader.Read())
            {
                string dataStr = "";
                dataStr += reader["用户名"] + "," + reader["密码"] + "," + reader["性别"] + "," + reader["年龄"] + "," + reader["年龄"];
                print(dataStr);
            }
        }  
    }
}
```














