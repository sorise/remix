### [Python 语言基础入门](#)

**介绍**： 入门Python的一些基础知识, 例如如何注释、打印输出、编码、转移、类型判断等等，这些是这门语言的基石，也是一门语言最基础的部分。

-----
* [1. 语言基础部分](#1-语言基础部分)
* [2. 基本输入输出](#2-基本输入输出)

----

### [1. 语言基础部分](#)
Python是面向对象的解释型计算机程序设计语言，也是强类型的动态脚本语言，Python语言的标识符、注释、缩进和语句规则，还有对于字符串的引号。

Python 被认为是**强类型**（strongly typed）和**动态类型**（dynamically typed）的脚本语言，这涉及到两个不同的概念：类型强度（strength of typing）和类型检查的时间（time of type checking）。
1. **强类型**：这意味着 Python 在变量使用时会严格遵守数据类型的规则。你不能在不进行显式转换的情况下将一个类型的数据当作另一个类型来处理。例如，在强类型语言中，你不能直接将字符串与整数相加，因为它们是不同类型的数据。尝试这样做会导致 TypeError 错误。这与弱类型语言形成对比，后者允许隐式类型转换，并可能自动将一种类型转换为另一种类型以完成操作。

2. **动态类型**：指的是在运行时确定变量的数据类型，而不是在编译时。这意味着你可以先定义一个变量而不声明它的类型，然后在程序的任何地方给它赋值为不同类型的数据。例如，你可以在程序的一处将变量 `x` 设定为整数，而在另一处将其设定为字符串。Python 解释器会在每次赋值时记住该变量的最新类型。

因此，Python 是强类型的，因为它`不会自动转换不同类型的数据进行操作`；同时它也是动态类型的，因为变量的类型是在运行时根据所赋的值来决定的，而不是在编写代码时静态指定的。这种组合使得 Python 既安全又灵活，但同时也要求程序员对类型有清晰的理解，以避免运行时错误。

#### [1.1 标识符](#)
标识符用于标识用于用户自定义的变量，而**变量存在的意义： 给内存空间起一个别名，方便管理和使用内存空间**。在Python 中，所有标识符可以包括 **英文、数字以及下划线(_)**，但不能以数字开头，区分大小写的。 这和C，Java, C#, C++... 是一致的！

[**声明变量的方式是直接命名，不需要说明变量的类型，这不同于其他语言。**](#)
```python
userScores = [56.89, 75.56, 98.12, 98.5]
userId = "2016110418"
userAge = 25
```

**为了代码的可读写**，有时候需要知道变量的数据类型，Python现在也是支持的，**但是这种声明对实际代码执行并无影响，仅仅是为了代码的可读写**。
```python
_userScores: list = [56.89, 75.56, 98.12, 98.5]  #类型为列表
_userId: str = "2016110418"  #类型为 字符串
_userAge: int = 25  #类型为整形
```

#### [1.2 Python 保留字符](#)
用户自定义的标识符不能和系统定义的关键字相冲突，比如不能将标识符定义为 if，else, class 等这些系统保留关键字。

下面的列表显示了在Python中的保留字。这些保留字不能用作常数或变数，或任何其他标识符名称，所有 Python 的关键字只包含小写字母。
```python
and    exec   not     assert    finally  or   
class  from   print   continue  global   raise
def    if     break   return    del      import
try    elif   in      while     for      pass
else   is     with    except    lambda   yield
```
Python提供了[**keyword**](https://docs.python.org/zh-cn/3/library/keyword.html#module-keyword)包可以查看和输出保留字。

```python
import keyword
print('保留字数量：', len(keyword.kwlist));
print(keyword.kwlist) #以列表的形式打印
```
#### [1.3 注释](#)
注释的最大作用是提高程序的可读性，没有注释的程序简直就是天书，让人吐血！ Python 支持两种类型的注释，分别是单行注释和多行注释。

Python 单行注释 使用注释符号 `#`， Python 多行注释 使用三对双引号或者单引号 `""" 注释内容 """`  `'''注释'''`

```python
# user age and id 单行注释
userId = "2016110418";
userAge = 25;

"""
print user information! 多行注释
"""
def inputUserInfo(id, age):
    print("ID: %s, Age: %d" % (userId, userAge));
    return;

inputUserInfo(userId, userAge);

'''
this is a notes information 多行注释
'''
```

#### [1.4 缩进规则](#)
Python 与其他语言最大的区别就是，Python 的代码块不使用大括号 {} 来控制类，函数以及其他逻辑判断。Python 最具特色的就是用**缩进**来代替大括号实现代码块。

**缩进**的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量，这个必须严格执行。

```python
if userAge > 18:
    print("your age is so big!");
else:
    print("just ok!");
```

**没有严格缩进，在执行时会报错！**

**`IndentationError`**: **`unindent does not match any outer indentation level`** 错误表明，你使用的缩进方式不一致，有的是 tab 键缩进，有的是空格缩进，改为一致即可
**`IndentationError`**: **`unexpected indent`** 错误 则 python 编译器是在告诉你"Hi，老兄，你的文件里格式不对了，可能是 tab 和空格没对齐的问题

在 Python 的代码块中必须使用相同数目的行首缩进空格数。建议你在每个缩进层次使用 单个制表符 或 两个空格 或 四个空格 , 切记不能混用

Python 中实现对代码的缩进，可以使用空格或者 Tab 键实现。但无论是手动敲空格，还是**使用 Tab 键**，通常情况下都是**采用4个空格**长度作为一个缩进量（默认情况下，一个 Tab 键就表示 4 个空格）。
```python
status: str = input("please input your status:")
state = int(status)

match state:
    case 404:
        print("not found!")
    case 200:
        print("normal")
    case 100:
        print("danger")
    case _:
        print("error")
```

#### [1.5 语句规则](#)
**Python**语句中一般以新行作为语句的结束符。所以一般不需要分号`;`结尾！ 我们可以使用斜杠（ `\`）将一行的语句分为多行显示，如下所示：

```python
scores = [56.89, 75.56, 98.12, 98.5]
total_machine = sum(scores)
total_manual = scores[0] + \
        scores[1] + \
        scores[2] + \
        scores[3] 

print("machine sum: %d , manual: %d" % (total_machine, total_manual))
#sum: 329 , manual: 329
```

语句中包含**[]**, **{}** 或 **()** 括号就不需要使用多行连接符。如下实例：

```python
days: list = ['Monday', 'Tuesday', 'Wednesday',
        'Thursday', 'Friday', 'Saturday', 'Sunday']

for v in days:
    print(v)
```

**分号作用(不推荐使用了):** 一般而言，一行结束是不需要加上分号的。` `同一行显示多条语句, Python可以在同一行中使用多条语句，语句之间使用分号(;)分割，以下是一个简单的实例：

```python
scores = [56.89, 75.56, 98.12, 98.5]; total = sum(scores);print("sum: %d" % total);
```

当然目前Python脚本的推荐写法为一行一条语句！

#### [1.6 语句引号](#)
Python 可以使用引号( `'` )、双引号(` "` )、三引号(` '''` 或` """` ) 来表示字符串，引号的开始与结束必须是相同类型的。

```
word = 'word'
sentence = "这是一个句子。"
paragraph = """这是一个段落。
包含了多个语句"""
```

#### [1.7 中文编码](#)
在早期版本中，Python 文件中如果未指定编码，在执行过程会可能会因为编码问题出现报错。 Python中默认的编码格式是 ASCII 格式，在没修改编码格式时无法正确打印汉字，所以在读取中文时会报错！

解决方法为只要在文件开头加入 # -*- coding: UTF-8 -*- 或者 # coding=utf-8 就行了

```python
# -- coding: UTF-8 --
print( "我是一条中文语句哦！" );
```

但是自从**Python3.X 源码文件默认使用utf-8编码，所以可以正常解析中文，无需指定 UTF-8 编码。**

#### [1.8 脚本执行顺序](#)
Python没有一个main函数作为整个程序的入口，它就是一个脚本语言！ 从入口文件的第一行代码从上至下开始执行！

```python
import time #导入标准库模块

print("将会打印个人信息！ 代码从此开始运行！")

# 输入个人信息
def get_information() -> (str, int):
    _name: str = input("please input your name:")
    _age: int = int(input("please input your age:"))
    return _name, _age

# 如果当前脚本文件是入口文件则执行该函数
if __name__ == '__main__':
    name, age = get_information()
    time_str = time.strftime("%Y/%m/%d %H:%M:%S", time.localtime())
    print(f"my name is {name}, age is {age}!  ---- {time_str}")
```

Python可以导入外部模块文件，一般而言一个脚本文件就对应一个程序模块。使用import导入其他模块，例如标准库文件或者第三方、用户自定义模块，每个 import 语句只导入一个模块，尽量避免一次导入多个模块。

```python
#推荐
import os
import sys
#不推荐
import os,sys
```
#### [1.9 转义字符](#)
Python 转义字符！和其他语言基本上是大同小异！转义字符的定义：由反斜杠加上一个字符或数字组成，它把反斜杠后面的字符或数字转换成特定的意义。

<table>
  <tbody>
    <tr>
      <th>转义字符</th><th>说明</th>
    </tr>
    <tr>
      <td>\n</td><td>换行符，将光标位置移到下一行开头。</td>
    </tr>
    <tr>
      <td>\r</td><td>回车符，将光标位置移到本行开头。</td>
    </tr>
    <tr>
      <td> \t</td><td>水平制表符，也即 Tab 键，一般相当于四个空格。</td>
    </tr>
    <tr>
      <td> \a</td><td>蜂鸣器响铃。注意不是喇叭发声，现在的计算机很多都不带蜂鸣器了，所以响铃不一定有效。</td>
    </tr>
    <tr>
      <td>\b</td><td>退格（Backspace），将光标位置移到前一列。</td>
    </tr>
    <tr>
      <td>\\</td> <td>反斜线</td>
    </tr>
    <tr>
      <td>\'</td><td>单引号</td>
    </tr>
    <tr>
      <td>\"</td> <td>双引号</td>
    </tr>
  </tbody>
</table>


### [2. 基本输入输出](#)
Python提供了print和input两个函数用于和屏幕交互，打印信息或者获得用户输入！

#### [2.1 print() 函数](#)
可以输出信息到屏幕上面，也可以输出信息到文件中！ 它有如下几个参数

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

* **objects** -- 复数，表示可以一次输出多个对象。输出多个对象时，需要用 , 分隔。
* **sep** -- 用来间隔多个对象，默认值是一个空格。
* **end**  -- 用来设定以什么结尾。默认值是换行符 \\n，我们可以换成其他字符串。
* **file** -- 要写入的文件对象。
* **flush** -- 输出是否被缓存通常决定于 file，但如果 flush 关键字参数为 True，流会被强制刷新。

**说明：**

* print 函数可以输出：字符串、数字、含有运算符的表达式。
* print 函数输出目的地有：文件，显示器[命令行] 可以通过修改 `file` 参数来实现。

```python
# 将消息输出到文件中
fp = open('./append.txt','a+')
print("this is a message !!", file=fp)

fp.close()
```
**分隔符参数使用**
```python
age = 25
print("your age is ", age, "! yes i know!", sep="-");
#your age is -25-! yes i know!
```
**end 结束参数！不换行！**
```python
# coding=utf-8
age = 25

print("your age is ", age, "! yes i know!", end="");
print("asdasdasd");
#your age is  25 ! yes i know!159asdasdasd
```
#### [ 2.2 input() 函数](#)
**input**输入函数，所有用户输入都是当做字符串处理 格式为： variable = input(prompt)这个输入格式 prompt为输出文本，以回车结束。配合**split**函数可以完成列表输入：

**split()**: 能根据设定的分割点分割字符串并返回分割后的字符串列表。

```python
name = input("please input your name：")
print('name:', name)

age = int(input("please input your age："))
print('age:', age)

scores = input("please input your scores[split by \"，\"]：").split(",")
print('scores', scores)

# 输出输入内容
"""
please input your name：jxkicker
name: jxkicker
please input your age：15
age: 15
please input your scores[split by "，"]：78,56,56,234,234,12
scores ['78', '56', '56', '234', '234', '12']
"""
```

#### [2.3 格式化输出](#)
我们可以输出指定的数据类型和长度精度规范，基本与C语言printf遵循的规范差不多！ 这是对输出到屏幕上面的信息格式化，要和字符串格式化分开理解！

**数据类型占位符**
* **%c**	 格式化字符及其ASCII码
* **%s**	 格式化字符串
* **%d**	 格式化整数
* **%u**	 格式化无符号整型
* **%o**	 格式化无符号八进制数
* **%x**	 格式化无符号十六进制数
* **%X**	 格式化无符号十六进制数（大写）
* **%f**	 格式化浮点数字，可指定小数点后的精度
* **%e**	 用科学计数法格式化浮点数
* **%E**	 作用同%e，用科学计数法格式化浮点数
* **%g**	`%f`和`%e`的简写
* **%G**	 `%f`和`%E` 的简写
* **%p**	 用十六进制数格式化变量的地址

**格式化操作符辅助指令**
* **.** 定义宽度或者小数点精度
* **-**	用做左对齐
* **+**	在正数前面显示加号( + )
* **<sp>**	在正数前面显示空格
* **\#**	在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X')
* **0**	显示的数字前面填充'0'而不是默认的空格
* **%**	'%%'输出一个单一的'%'
* **(var)**	映射变量(字典参数)
* **m.n.**	m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)

```python
# coding=utf-8
name,age,average_scores = "remix",24, 92.15

print("姓名: %s  年龄: %#o  平均分数: %5.2f" % (name, age, average_scores));
#姓名: remix  年龄: 0o30  平均分数: 92.15
```

#### [2.4 时间输出](#)
Python提供了多个内置模块用于操作日期时间，像calendar，time，datetime。

**datetime中包含三个类date ,time,datetime**
* 函数datetime.combine(date,time) 可以得到dateime，datetime.date()、datetime.time()可以获得date和time
* datetime模块定义了两个常量：datetime.MINYEAR和datetime.MAXYEAR，分别表示datetime所能表示的最 小、最大年份。其中，MINYEAR = 1，MAXYEAR = 9999。

**格式化输出世间**

```python
import datetime as pk_dt;
now = pk_dt.datetime.now();
birthDt = pk_dt.datetime(1998,6,27,12,00,00);

print(f"{now:%y/%m/%d %H:%M:%S %a}");
print(f"{birthDt:%Y/%m/%d %H:%M:%S %a}");
# 22/10/25 18:54:30 Tue
# 1998/06/27 12:00:00 Sat
```

**datetime**模块定义了下面这几个类：

* **datetime.date**：表示日期的类。常用的属性有year, month
* **datetime.time**：表示时间的类。常用的属性有hour, minute, second, microsecond；
* **datetime.datetime**：表示日期时间。
* **datetime.timedelta**：表示时间间隔，即两个时间点之间的长度。
* **datetime.tzinfo**：与时区有关的相关信息。

注 ：上面这些类型的对象都是不可变（immutable）的。

**Python中时间日期格式化符号：**

* %y 两位数的年份表示（00-99）
* %Y 四位数的年份表示（000-9999）
* %m 月份（01-12）
* %d 月内中的一天（0-31）
* %H 24小时制小时数（0-23）
* %I 12小时制小时数（01-12）
* %M 分钟数（00-59）
* %S 秒（00-59）
* %a 本地简化星期名称
* %A 本地完整星期名称
* %b 本地简化的月份名称
* %B 本地完整的月份名称
* %c 本地相应的日期表示和时间表示
* %j 年内的一天（001-366）
* %p 本地A.M.或P.M.的等价符
* %U 一年中的星期数（00-53）星期天为星期的开始
* %w 星期（0-6），星期天为星期的开始
* %W 一年中的星期数（00-53）星期一为星期的开始
* %x 本地相应的日期表示
* %X 本地相应的时间表示
* %Z 当前时区的名称
* %% %号本身
