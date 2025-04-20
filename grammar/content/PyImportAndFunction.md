### [Python 模块、包和函数](#)
`需要理解Python模块和包，还有基本单元 function的使用！`

-----

- [x] [`1. Python模块和包`](#1-)
- [x] [`2. 函数`](#2-函数)
- [x] [`3. Lambda 表达式`](#3-lambda-表达式)
- [x] [`4. 嵌套函数`](#4-嵌套函数)

-----

### [1. Python模块和包](#)
Python 提供了强大的模块支持，主要体现在，不仅 Python 标准库中包含了大量的模块（称为标准模块），还有大量的第三方模块，**开发者自己也可以创建自己的模块**。
**模块就是 Python 程序**。换句话说，任何 Python 程序都可以作为模块

**模块的的好处:**  模块可以理解为是 **对代码更高级的封装** 即把能够实现某一特定功能的代码编写在同一个 `.py` 文件中，并将其作为一个独立的模块，这样既可以方便其它程序或脚本导入并使用，同时还能有效避免函数名和变量名发生冲突。

* `第三方模板可以使用` `pip install 按照引用`
* `标准库可以直接引用`
* `关键在于你如何实现自己的模块！`


引入模块的方式，`有整体引入` 和 `部分引用` 两种方式
```python
import cnm  #引入整个cnm模块

factor = cnm.gcd(12, 36)  #使用模块里面的成员需要使用 模块名.成员名的方式
```

```python
from cnm import gcd #部分引入 只是引用模块中的一个 gcd 函数

factor = gcd(12, 36)
```

模块就是单独的每一个 python 源文件，而 **包** 就是包含这些源文件的目录， 如下目录结构！ **包中有一个特殊的py文件： __init__.py**
```
pkg
|---mysqldb.py
|---system.py
|---king.py
|---connector.py
|---__init__.py
```
`pkg 就是包` `mysqldb.py` `system.py` `king.py` `等就是模块`

**包是一种管理 Python 模块命名空间的形式** ，采用"点模块名称"。比如一个模块的名称是 `A.B`， 那么他表示一个包 `A` 中的子模块 `B` 。
如果一个源文件将作为可以被其他程序引用而存在的模块，那么推荐只是在这个模块里面存放 函数，类定义，变量等声明定义性质的代码。而不要在里面
写一些立即运行的代码！一个模块被另一个程序第一次引入时，将完整运行一次源文件里面的代码！

`__init__.py` 文件的作用是将文件夹变为一个Python包,Python 中的每个模块的包中，都有 `__init__.py`
最简单的情况，放一个空的 `__init__.py` 就可以了, 当然这个文件中也可以包含一些初始化代码或者为（将在后面介绍的）`__all__` 变量赋值。因此，如果我们想手动创建一个包，只需进行以下 2 步操作：

* `新建一个文件夹，文件夹的名称就是新建包的包名；`
* `在该文件夹中，创建一个 __init__.py 文件` `当然，也可以编写一些 Python 初始化代码，则当有其它程序文件导入包时，会自动执行该文件中的代码。`

**Python 3.3** 以后, 如果你不需要初始化或者执行一些操作，你就不需要在包目录下创建一个 `__init__.py`


#### [1.1 导入模块 import](#)
用于从另一个python源文件中的代码模块带入到当前文件中， 当解释器遇到 `import` 语句，如果模块在当前的搜索路径就会被导入。 `cnm.py`  和 当前源文件在同一个目录下面！ 使用 `as` 可以为导出的模块或者模块的成员取一个别名！

`整体导入语法` `import module_name`
```python
import 模块名1 [as 别名1], 模块名2 [as 别名2]
```
`使用这种语法格式的 import 语句，会导入指定模块中的所有成员（包括变量、函数、类等）。不仅如此，当需要使用模块中的成员时，需用该模块名（或别名）作为前缀，否则 Python 解释器会报错。`

`部分导入语法` `from module_name import what`
```python
from 模块名 import 成员名1 [as 别名1],成员名2 [as 别名2]
```

`使用 form 整体导入： 把一个模块的所有内容全都导入到当前的命名空间也是可行的`
```python
from modname import *
```
##### [1.1.1 导入下级模块](#)
`如果目录结构是如下关系`
```
pkg
|---god.py
main.py
```
`我们使用文件夹名称 和 . 号配合导入`
```python
import pkg.cnm as god

factor = cnm.gcd(12, 45)
print(factor)
```
`pkg是啥？` **pkg 就是包**

##### [1.1.2 导入上级模块](#)
`要导入上级目录下模块，可以使用sys.path`  
`sys.path的作用：当使用import语句导入模块时，解释器会搜索当前模块所在目录以及sys.path指定的路径去找需要import的模块，所以这里是直接把上级目录加到了sys.path里。`

```
import sys 
sys.path.append("..") 
import xxx
```

`如在file4.py中想引入import上级目录下的file1.py：`

```
-- dir0
　　| file1.py
　　| file2.py
　　| dir3
　　　| __init__.py
　　　| file3.py
　　| dir4
　　　| file4.py
```

```python
#file4.py
import sys 
sys.path.append("..") 
import file1
```

##### [1.1.3 __all__ 变量](#)
`模块提供的` `__all__` `量，该变量的值是一个列表，存储的是当前模块中一些成员（变量、函数或者类）的名称。通过在模块文件中设置 __all__ 变量，当其它文件以 ` 
`from 模块名 import *` `的形式导入该模块时，该文件中只能使用 __all__ 列表中指定的成员。`

```python
def say():
    print("人生苦短，我学Python！")
def CLanguage():
    print("C语言中文网：http://c.biancheng.net")
def disPython():
    print("Python教程：http://c.biancheng.net/python")
__all__ = ["say","CLanguage"]
```
`但是使用其他方式引入模块，则 __all__ 变量的设置是无效的`

`综上所述` **这是个废物变量**

#### [1.2 一个例子](#)
`每一个python文件就是一个 模块`

`cnm.py`
```python
# -*- coding: UTF-8 -*-
def gcd(am: int, bm: int):
    am = int(am); bm = int(bm);
    a = max([am, bm]);
    b = min([am, bm]);
    c = a % b;
    while c != 0:
        a = min([a, b]) #大的
        b = c  #a 为小的
        c = a % b
    #end while
    return b; # end def

#get least common multiple
def minMultiple(am: int , bm: int):
    am = int(am); bm = int(bm)
    return int(am * bm / gcd(am, bm))
```
`main.py`
```python
# -*- coding: UTF-8 -*-
from cnm import gcd as cgcd  #自己的模块
import datetime as dt  # 官方的库

now = dt.datetime(2022, 9, 15,20,12)

print(f"DateTime: {now:%Y/%m%d %H:%M:%S}")
#DateTime: 2022/0915 20:12:00

factor = cgcd(12, 36)
print(factor)
#12
```

#### [1.3 模块的属性](#)
一个模块被另一个程序第一次引入时，其主程序将运行。如果我们想在模块被引入时，模块中的某一程序块不执行，我们可以用 `__name__` 属性来使该程序块仅在该模块自身运行时执行。

##### [1.3.1 __name__](#)
`如果当前源文件是起始文件，那么会返回字符串` `__name__` `否则会返回 包.模块名称.模块名称`

```python
#!/usr/bin/python3
# Filename: using_name.py
if __name__ == '__main__':
   print('程序自身在运行')
else:
   print('我来自另一模块')
```
##### [1.3.2 __package__](#)
`返回当前源文件所属的包名`

##### [1.3.2 dir()](#)
`内置的函数 dir() 可以找到模块内定义的所有名称。以一个字符串列表的形式返回:`

```python
import fibo, sys
dir(fibo)
['__name__', 'fib', 'fib2']
```

#### [1.4 __init__.py 的真正作用](#)
**批量导入包中的模块** `用于整体导入当下包中的所有模块， 我们有如下的一个包的目录！`  `__init__.py中还有一个重要的变量，__all__, 它用来将模块全部导入。`

```
effects                  
|--__init__.py
|--echo.py
|--surround.py
|--reverse.py
```

```python
#  module description 
#  author and create datetime
__all__ = ["echo", "surround","reverse"]
```

`但是导入方式只能使用如下格式：`
```python
from effects import *

result = echo.start(0, 60)
dics = surround.run(result)

echo.db.store(reverse.sortByKey(dics))
```

### [2. 函数](#) 
函数是组织好的，可重复使用的，用来实现单一，或相关联功能的代码段。在Python中定一个函数需要使用关键字 **def** 。当然python 还 **支持lambda表达式** 以定义
匿名函数！ 当然作为一个动态编程语言，它还 **支持函数闭包**！ 当然我们还需要理解它传值的方式，按值传递，按引用传递！

**用函数的创建者看** 函数有以下几类
* `标准库内置函数`
* `第三方库定义的函数`
* `用户自定义函数`

**Python 没有JS中的函数变量提升，所以函数必须要先定义再使用！**

`首先我们定义一个 Python泛型函数 作为例子`
```python
# -*- coding: UTF-8 -*-
import typing

T1 = typing.TypeVar("T1", bound=typing.Union[list[int], list[float]])
T2 = typing.TypeVar("T2", bound=typing.Union[int, float])

def sum(numbers: T1) -> T2:
    total = 0
    for num in numbers:
        total += num
    return total

li1 = list([1, 2, 3])          # 整数型列表
li2 =list([1.1, 2.2, 3.3])     # 浮点数列表

print(f"total: {sum(li1)}") # total: 6
print(f"total: {sum(li2)}") # total: 6.6
```
#### [2.1 自定义一个标准函数](#) 
函数代码块以 **def** 关键词开头，后接函数 `标识符名称` 和圆括号 `()`。 任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数。 函数头以冒号结束，下一行缩进开始。
**函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。**  可以使用 `__doc__` 访问这个字符串。 `return [表达式]` 表示结束函数，选择性地返回一个值给调用方。 **不带return的函数相当于返回 None。**

**定义函数的语法：** `默认情况下，参数值和参数名称是按函数声明中定义的顺序匹配起来的。`
```
def functionname(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
   "函数_文档字符串"
   function_suite
   return [expression]
```

* `函数是按名调用！` 
* **python 所有的函数都有返回值，如果你没有指定return返回什么数据，那么默认返回None**

下面定义了一个函数用于获取两个整数的最大公因数， 另一函数获得最小公倍数！

```python
# -*- coding: UTF-8 -*-
def gcd(am: int, bm: int):
    am = int(am); bm = int(bm);
    a = max([am, bm]);
    b = min([am, bm]);
    c = a % b;
    while c != 0:
        a = min([a, b]) #大的
        b = c  #a 为小的
        c = a % b
    #end while
    return b; # end def

#get least common multiple
def minMultiple(am: int , bm: int):
    am = int(am); bm = int(bm)
    return int(am * bm // gcd(am, bm))

print( gcd(48, 24), gcd(17.15, 51), gcd(14, 24))
#14 17 2

print(minMultiple(48,13)) #624

print(f"2^4 = {2**8:d}");    
#256
# ---------------------------

print(10//4, 12//7, 15//18);
#2 1 0
```

**函数文档可以长一点**
```python
def my_function():
    """
    Do nothing, but document it.
    /....
    No, really, it doesn't do anything.
    """
    pass
```

#### [2.2 参数传递方式](#)
我们都知道Python内置了两大类型，不可变数据和可变数据。这使得对于Python函数的参数传递方式也具有了两种方式! 当然我们自己创建的类，一般来说都是可变数据类型！

* `不可变数据（3 个）：Number（数字）、String（字符串）、Tuple（元组）；`
* `可变数据（3 个）：List（列表）、Dictionary（字典）、Set（集合）。`

python 函数的参数传递：

* **不可变类型**：**类似 c++ 的按值传递** `如 整数、字符串、元组。如fun（a），传递的只是a的值，没有影响a对象本身。比如在 fun（a）内部修改 a 的值，只是修改另一个复制的对象，不会影响 a 本身。`
* **可变类型**：**类似 c++ 的引用传递**，`如列表，字典。如 fun（la），则是将 la 真正的传过去，修改后fun外部的la也会受影响!`

```python
student = { "lizhiming": 169,"jiangxing": 173,"huyu":172,"lijiakun":170,"lihangyong":169 }

count = 5
def changeCount(number):
    "修改 count的值"
    count = 0
    return None

changeCount(count)
print(count)
#5

def changeStudentValue(stuDictionary):
    "修改大家的值变成分数"
    for (key, value) in stuDictionary.items():
        stuDictionary[key] = value / 10.0
    return None

changeStudentValue(student)


for key,value in student.items():
    print(f"{key}:{value}")

# lizhiming:16.9
# jiangxing:17.3
# ...
```

#### [2.3 位置参数传递](#)
就是按照顺序传递参数, 一看就懂了！ Python由于是动态语言，所以 **传递给函数的参数可以是任何的类型**。 当然python现在也支持类型，甚至是泛型编程了，先按下不表！

```python
a,b = 10, 12
def maxValue(t1, t2):
    if t1 > t2:
        return t1
    else:
        return t2

#位置参数 
# a第一个 就赋给t1
# b第一个 就赋给t2
t3 = maxValue(a ,b)
```

#### [2.4 参数默认值](#)
为参数指定默认值是非常有用的方式。调用函数时，可以使用比定义时更少的参数，当然老样子， **默认值只能是从右往左！**
**python函数的默认值是在函数创建的时候绑定的，而不是在函数调用的时候每次都创建一个新的** 这导致python的默认值可以实现闭包的效果。
python的默认值如果是可变数据类型，并且函数体还修改了默认值，那么 **每次调用函数获得的默认值可能不一样**

**默认参数后面必须也是默认参数或者没有参数**
```python
#不被允许 c必须也赋予一个默认值，否则不允许b有默认值
def func(a, b = 10, c):
    pass
```

`以此为例：`
```python
def findMaxValue(values, start = 0, end = None):
    maxV = values[start]
    if end is None: end = len(maxV)
    for i in range(start + 1, end):
        if values[i] > maxV:
            maxV = values[i]
    return maxV
```

`默认值在定义作用域里的函数定义中求值，所以：` **默认值只会在函数定义的时候执行一次！**
```python
i = 5

def f(arg=i):
    print(arg)

f()  #上例输出的是 5。
i = 6
f()  #上例输出的是 5。
```

##### [2.4.1 默认值是一个可变类型](#)
如果默认值是一个可变类型，那将会是一件可怕的事情，如果总是使用默认值并且还修改了默认值，那么下一次调用函数的时候，得到的默认值将会和上一次不一样！

```python
def printValue(value, isShowHistory = False, history=[]):
    print(f"agr:{value}")
    history.append(value)
    if isShowHistory:
        i = 1
        for v in history:
            print(f"{i} :{v}")
            i = i + 1

printValue(10)
#agr:10  history=[10]
printValue(20)
#agr:20  history=[10,20]
printValue(30)
#agr:30  history=[10,20,30]
printValue(40, True)
#agr:40   history=[10,20,30,40]
#1 :10
#2 :20
#3 :30
#4 :40
```

**如果需要每次函数获得的默认参数都是一样的，如果默认参数是可变数据类型，需要先赋None，再给值！**
```python
def printValue(value, isShowHistory = False, history=None):
    if history is None:
        history = []
    print(f"agr:{value}")
    history.append(value)
    if isShowHistory:
        i = 1
        for v in history:
            print(f"{i} :{v}")
            i = i + 1

printValue(10)
#agr:10  history=[10]
printValue(20)
#agr:20  history=[20]
printValue(30)
#agr:30  history=[30]
printValue(40, True)
#agr:40   history=[40]
#1 :40
```

#### [2.5 关键字参数传递](#)
**name_arg=value** 形式的 关键字参数 也可以用于调用函数。使用关键字参数允许函数调用时参数的 **顺序与声明时不一致**，因为 Python 解释器能够用参数名匹配参数值。

`函数示例如下`
```python
scores = [45, 87, 99, 78, 77, 75, 15]

def findMaxValue(tlist, start, end):
    maxV = tlist[start]
    for i in range(start + 1, end):
        if tlist[i] > maxV:
            maxV = tlist[i]
    return maxV

#关键字参数
maxv = findMaxValue(tlist = scores, start=2, end= len(scores))

print(f"i find the max value: {maxv}")
#i find the max value: 99
```

#### [2.6 限定参数传递](#)
使用占位符 `*` 可限定在它位置之后的参数**只能**按照`关键字`参数传递！  
使用占位符 `\\` 可以限定在它位置之前参数**只能**按照`位置`参数传递！  

`keywordA` `keywordB` 不能使用位置传参数！ 只能使用如下形式， `*` 变成了一个占位符，说明后面的参数只能使用命名关键字传递！
```python
def getParameter(a, *, keywordA, keywordB):
    print(f"位置参数a:{a}")
    print(f"关键字参数:{keywordA}")
    print(f"关键字参数:{keywordA}")

val = 100
getParameter(val, keywordA=200, keywordB=300)
```
* `pos_only` **只能使用位置参数**
* `standard` **可以使用位置参数 也可以使用命名参数**
* `kwd_only1` `kwd_only2` **只能使用命名参数**

```python
def example(pos_only, /, standard, *, kwd_only1,kwd_only2):
    print(pos_only, standard, kwd_only1, kwd_only2)

example(29,standard=30, kwd_only1=300, kwd_only2=400)
```

#### [2.7 可变长参数 - 字典](#)
参数的长度不一定是固定的，如何处理，python提供了一种使用字典来接受可变长参数的方式。需要给参数加上 `**` 修饰符！
我们一般约定俗成，将参数名为: **kwargs** 
```python
def dicParameter(name, **kwargs):
    print(f"name:{name} has friends:")
    print(f"{kwargs}")

dicParameter("kicker", nick="nick", kicer="kicer", youmi="youmi")

# name:kicker has friends:
# {'nick': 'nick', 'kicer': 'kicer', 'youmi': 'youmi'}
```

#### [2.8 可变长参数 - 元组](#)
python提供了一种使用元组来接受可变长参数的方式。需要给参数加上 `*` 修饰符！

```python
def concat(*args):
    sep = '.'
    print(args) #('earth', 'mars', 'venus')
    return sep.join(args) #earth.mars.venus

vals = concat("earth", "mars", "venus")
```

#### [2.9 参数解包](#)
函数参数是字符串/列表/元祖/字典/集合的时候可以进行解包。**当然你需要保持其一一对应，数量相等！**

**解包字典** ： 使用符号 `**`
```python
##解包字典
#加个星号 效果一样！
#def PersonFactory(*,name, age, sex):
def PersonFactory(*, name, age, sex):
    print(f"name: {name}", end=" ")
    print(f"age: {age}", end=" ")
    sexName = ""
    if sex == True:
        sexName = "boy"
    elif sex == False:
        sexName = "girl"
    else:
        sexName = "type error"
    print(f"sex: {sexName}")

pardic = {"name": "remix", "age": 25, "sex": True }

PersonFactory(**pardic) #解包字典
#name: remix age: 25 sex: boy
```

**解包字符串 列表 元祖 集合**  使用符号 `*`

```python
#解包字符串
def createList(*args):
    print(list(args))

name = "kicker"
createList(*name)
#['k', 'i', 'c', 'k', 'e', 'r']

#解包列表
def Apolo(a,b,c,d):
    print([a,b,c,d])

names = {"Helios","Zeus","Jupiter","Hera"}
Apolo(*names)
#['Zeus', 'Jupiter', 'Hera', 'Helios']
#元祖 集合是一样的操作 不重复了
```

#### [2.10 返回值声明](#)
Pyhton 支持类似于C++，一样的语法，用来声明函数的返回值类型

**当前函数返回值类 为 int**
```python
def gcd(am: int, bm: int) -> int:
    am = int(am); bm = int(bm);
    a = max([am, bm]);
    b = min([am, bm]);
    c = a % b;
    while c != 0:
        a = min([a, b]) #大的
        b = c  #a 为小的
        c = a % b
    #end while
    return b; # end def
```

### [3. Lambda 表达式](#) 
**lambda** 关键字用于创建小巧的 **匿名函数**。 `lambda a, b: a+b` 函数返回两个参数的和。`Lambda` 函数可用于任何需要函数对象的地方。
在语法上，匿名函数只能是单个表达式。在语义上，它只是常规函数定义的语法糖。与嵌套函数定义一样，lambda 函数可以引用包含作用域中的变量：

* `lambda` 只是一个表达式，函数体比 `def` 简单很多。
* `lambda` 的主体是一个表达式，而不是一个代码块。仅仅能在 `lambda` 表达式中封装有限的逻辑进去。
* `lambda` 函数拥有自己的命名空间，且 **不能访问自己参数列表之外或全局命名空间里的参数**。
* **Python lambda 函数 只能写一行** 虽然 `lambda` 函数看起来只能写一行，却不等同于 `C` 或 `C++` 的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

```python
lambda [arg1 [,arg2,.....argn]]:expression
```

`一个例子，找到输入参数的最大值`
```python
def warpper(f, *args):
    return f(args)

maxv = warpper(lambda paramters: max(paramters), 56,98,78,48,56)
print(maxv) #98
```

### [4. 嵌套函数](#)
这是我自己起的名字，其实本质上就是函数返回函数，也就是闭包操作！

```python
#创造一个函数判断给定的set是否是一个完全剩余系
def CreateResidueSystemJudge(mod: int):
    if mod <= 0: 
        return None
    def judge(numbers):
        if len(numbers) != mod:
            return False
        rSet = set();
        for n in numbers:
            rSet.add(n % mod)
        if len(rSet) == abs(mod):
            return True
        else:
            return False
    return judge

v = 5
nm1 = [0,1,2,3,4]
nm2 = [7,12,2,3,4]

judger = CreateResidueSystemJudge(v)

print(f"{nm1} 是不是关于{v}完全剩余系?  judge:({judger(nm1)})")
print(f"{nm2} 是不是关于{v}完全剩余系?  judge:({judger(nm2)})")
```

-----
`时间`: `[]` 