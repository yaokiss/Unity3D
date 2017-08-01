## Lua工具安装下载

* 1,Lua的官网 lua.org
* 2,Luaforwindows
* http://luaforge.net/projects/luaforwindows/

* http://luaforwindows.luaforge.net/ (可安装的exe文件,一整套的Lua开发环境，有Lua的解释器，参考手册，范例和库，文档，和编辑器)
* 3,LuaStudio
* LuaStudio 是一款轻量级的优秀的可调试的Lua IDE,非常方便的用于lua代码的编写和调试.


## lua中的关键字

and、 break 、do 、else 、elseif、 end、 false、 for、 function 、if、 in 、local 、nil 、not、 or 、repeat、return、 then、 true、 until、while

这些关键字不可以被用作常量、变量、或者任何其他标识符  关键字不能当做标识符，Lua大小写敏感

## 注意事项

* print()是Lua内置的打印方法
* 在Lua中字符串""或''都可以表示
* Lua中语句后边没有  ;
* 单行注释是--注释内容
* 多行注释--[[ 注释内容]]--

https://github.com/andycai/luaprimer/blob/master/01.md


### Lua中定义变量

lua是一个弱类型语言,不具有强类型语言的特点,比如
num = 100
这里定义了一个全局变量叫做num,赋值为100
在Lua中定义变量是没有类型的，根据存储什么数据，来决定是什么类型
变量的命名不能以数字开头
尽量避免下划线加大写字母开头，这种格式Lua自身保留
推荐使用C#中的命名规范和驼峰命名

## Lua中5种变量类型

Lua中变量如下：

* 1，nil表示空数据，等同于null
* 2，boolean 布尔类型，存储true和false
* 3，string 字符串类型，字符串可以用双引号也可以使用单引号表示
* 4，number小数类型（Lua中没有整数类型）
* 5，table表类型
myTable = {34,,34,2,342,4}
myTable[3]
* 我们可以使用type()来取得一个变量的类型
```
m  =3
  print(type(m))

  o  = "32rer"
  print(type(o))

  n  =nil
  print(type(n))
```

局部变量和全局变量注意事项

默认定义的变量都是全局的，定义局部变量需要在前面加一个local；
在代码块中声明的局部变量，只会在当前作用域之类起作用,在lua中重复定义不会报错.
* temp = 34 – 全局
* local temp = 345 – 局部
````
condition = true
x = 10
if true then
    local x                -- local to the "then" body
    x = 20
    print(x + 2)
else
    print(x)                --> 10  (the global one)
end

if false then
    local x                -- local to the "then" body
    x = 20
    print(x + 2)
else
    print(x)                --> 10  (the global one)
end
print(x)                    --> 10  (the global one)

```

Lua中运算符有哪些：

* 1，算数运算符 + - * / % (Lua中没++ – 这样是运算符)

* 2，关系运算符 <= < > >= == ~=

* 3，逻辑运算符 and or not 分别表示 与 或 非（类似于C#中的 && || !）

a and b:当a为真时返回b,当a为假时,返回a <=> 条件表达式 a?b:a
　　a or b:当a为真时返回a, 当a为假时返回b <=>条件表达式 a?a:b
not a:当a为真时返回假,当a为假时返回真 <=>条件表达式 a?false:true
```
    local a = false
    b = 5
    local c = a and b
    print (tostring(c))
```

if语句的三种用法：

1，if语句
```
if [condition] then  -- 一定是与then 对应起来使用
end
```
```
2，if else语句
if [condition] then
else
end
```
```
3，if elseif else语句
if [condition] then
elseif [condition]
else
end
```
```
4，if not 语句
if not false then
print(“ 如果不是”)
end
```

循环结构while循环:

1，while语法结构
```
while [condition] do
end
```
2，输出1到100
3，实现1加到100
4，遍历1-100中所有的奇数的和


循环结构repeat循环:

（有点类似与C#中的do..while循环）

1，语法结构
```
  repeat
  [code to execute]
  until [condition]

  local a = 1
  repeat
  	a = a +1
  	print (tostring(a))
  until( a>10 )
```
2，输出1到100
3，实现1加到100
4，遍历1-100中所有的奇数的和

for循环结构：

1，语法结构
```
for index = [start],[end] do
[code to execute]
end
```
2，输出1到100
3，实现1加到100
4，遍历1-100中所有的奇数的和
break可以终止循环 没有continue语法

Lua中定义函数：

1，如何定义函数
function 关键字表示函数开始,后接函数名和函数体 end表示函数结束
```
 function [function name](/resource/k25/03_引擎高级进阶/项目发布/Lua/Lua语法介绍/param_1,param_2)
 [function code]
end
```

定义一个函数用来求得两个数字的和
```
 function add(num1,num2)
    return num1+num2
 end

 local d = add(3,4)
```
一个函数返回多个值
```
function tear(a,b)
	return a+1,b+1
end

x,y = tear(1,2)
print(x,y)

x,y,z = tear(1,2)
print(x,y,z)
```
标准库(标准函数)

内置标准函数

Lua内置提供了一些常用的函数帮助我们开发
1，数学处理的math相关函数
2，字符串处理的string相关函数
3，表处理的table相关函数
4，文件操作的io相关函数
```
  file = io.open("D:\\1\\1.txt","w+")
  file:write("32432","a")
  file:close()
```

数学运算函数

* math.abs(x) 返回x的绝对值。(整数/浮动)
* math.cos(x) 返回x的余弦值 (假定为弧度)
* math.max(x，…) 返回参数的最大值
* math.maxinteger(x) 一个整数的最大值为整数
* math.min(x,…) 返回参数的最小值
* math.sqrt (x) 返回x的平方根


字符串处理相关函数

string.len(s) 接受一个字符串,并返回它的长度。
string.lower(s) 接收一个字符串并返回该字符串的副本与所有大写字母改为小写
string.upper（s） 接收一个字符串并返回该字符串的副本与所有小写字母改为大写。
string.format(s)
```
str = string.format("字符串：%s\n整数：%d\n小数：%f\n十六进制数：%X","qweqwe",1,0.13,348)
```
string.match(s) 对目标字符串进行匹配，并找到匹配的字符段
```
print(string.match("hello lua", "lua"))
print(string.match("data :2017/6/2", "%d+/%d+/%d+"))  --按照模式进行匹配
print(string.match("lua2 lua3", "lua%d", 2)) -- 匹配后面这个字符串

```
.. 字符串相加
tostring() 把一个数字转化成字符串 如 local d = tostring(s)
tonumber() 把一个字符串转化成数字 local s = tonumber(d)
在lua中有默认的字符串和数字的自动转换:
```
print("10"+1)  --  11  number类型 ，字符串类型和数类型直接想加就转换成数字类型
local b = 10+"string" -- 错误  不能这样相加
```
table的赋值
```
myTable[3]=34  当键是一个数字的时候的赋值方式
myTable["name"]="newbieol" 当键是一个字符串的赋值方式
myTable.name = "shylock"当键是一个字符串的赋值方式
```
3，table的访问
```
myTable[3]  当键是数字的时候，只有这一种访问方式
myTable.name 当键是字符串的时候有两种访问方式
myTable["name"]
```
4，table的第一种创建方式
```
myTable = {name="shylock",age=18,isMan = true}--	（表创建之后依然可以添加数据） 数据访问
myTable.name
myTable["name"]
```
5，table的第二种方式(类似数组的使用)
```
  myTable = {34,34,34,3,4,"sdfdsf"}
```
当没有键的时候，编译器会默认给每一个值，添加一个数字的键，该键从1开始


表的遍历两种方式：

1,如果是只有数字键，并且是连续的可以使用下面的遍历
```
for index = 1,table.getn(myTable) do
	[code to execute]
end

local num = {1,3,43,43534,43,435,5} --默认是连续的
for index = 1,table.getn(num) do
	print ( tostring( num[index]) )
end

print ( "\n" )

local num = {[2]=1,[9]=3,43,43534,43,435,5} --非连续的


print ( "\n" )

```

表中通过pairs 和 ipairs进行遍历:
```
for index,value in pairs(myNames) do
    print(index,value)
end
print ( "\n" )

local tt =    
{    
    [1] = "test3",    
    [9] = "test4",    
    name = "test5"    
}    

for i,v in ipairs(tt) do    -- 当index不连续的时候或不是数字值时，不能完全遍历table中的值
    print( tt[i] )    
end  

for i,v in pairs(tt) do    --  当index不连续的时候，也可以完全遍历table中的值
    print( tt[i] )    
end
```

Lua中的table — 表

lua中表的特点

1.table 是 Lua 的一种数据结构用来帮助我们创建不同的数据类型，如：数字、字典等。

2.Lua table 使用关联型数组，你可以用任意类型的值来作数组的索引，但这个值不能是 nil。

3.Lua table 是不固定大小的，你可以根据自己需要进行扩容。

在Lua中的table类似C#中的字典，其实就是一个 key-value键值对的数据结构。

table的创建
```
  myTable = {}
  表名后面使用{}赋值，表示一个空的
```

```
Mytable = {"int","double","float","string","char","bool"}
Mytables = {1,8,6,2,4,7,9,3,2,3}
	--temp = table.concat(Mytable,".",1) --用符号把所有数据连成字符串
	--print(temp)

--	table.insert(Mytable,3,"long")		--在指定的位置插入一个值
--for index,value in pairs(Mytable) do
--	print(index,value)

--	table.remove(Mytable,4)				--移除指定位置的数据
--for index,value in pairs(Mytable) do
--	print(index,value)

--table.sort(Mytable)						--按字母顺序进行排序，遍历表打印
--for idex,value in pairs(Mytable) do
--print(idex,value)

--table.sort(Mytables)						--按顺序进行排序
--for index,value in pairs(Mytables) do
--print(index,value)


table.sort(Mytables,function(a,b) return a > b end) --按大到小排序
for i ,v in pairs(Mytables) do
print(i,v)

end
```

通过表来实现面向对象
```
Buff = {life = 100}

function Buff.getBuff(self,a)
	self.life = self.life+a
end

Buff.getBuff(Buff,10)
print(Buff.life)


function Buff:getBuff(a)
	self.life = self.life+a
end

Buff:getBuff(20)
print(Buff.life)
```























