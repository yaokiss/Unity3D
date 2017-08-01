## 在C#中执行访问lua代码

```
//Lua lua = new Lua();
            //lua["name"] = "小兰";
            //lua["age"] = 26;
            //lua["girl"] = true;
            //lua.NewTable("table");

            //string name = (string)lua["name"];
            //double age = (double)lua["age"];
            //bool girl = (bool)lua["girl"];

            //Console.WriteLine("姓名:" + name +"\n" + "年龄:" + age + "\n" + "女生:" + girl);

```

```
//Lua lua = new Lua();
/lua.DoFile("C:/Users/Administrator/Desktop/Lua/test.lua");  //在C#中执行Lua脚本
```

```
Lua lua = new Lua();
lua.DoString("name = 'aa'");//不能使用中文。中文需要luainterface2.0才可以
lua.DoString("age = 20");
lua.DoString("sex = 'nan'");

lua.DoString("function show(name,age,sex) print(name,age,sex) end show(name,age,sex)");
```

### lua和C#中类型的对应
```
Lua中            C#中
nil 		     null
string 		     System.String
number 	            System.Double
boolean 	     System.Boolean
table		    LuaInterface.LuaTable
function 	    LuaInterface.LuaFunction
```


















