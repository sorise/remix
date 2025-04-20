### [Python 变量和基本数据类型](#)
**介绍**： 理解变量的声明赋值，了解一些基本简单数据类型，数值类型、字符串类型。区分不可变数据类型和可变类型。

-----
-  [1. 变量](#1-变量)
-  [2. 标准数据类型](#2-标准数据类型)
-  [3. 数值类型](#3-数值类型)
-  [4. 字符串类型](#4-字符串类型)
-  [5. None](#5-none)
-  [6. 脚本属性](#6-脚本属性)

----
### [1. 变量](#)
**Python 中的变量不需要声明。** 每个变量在使用前都 **必须赋值** ，变量赋值以后该变量才会被创建。在 Python 中，变量都可以看成是内存中某个对象的引用，它没有类型，我们所说的 "类型" 是变量所指的内存中对象的类型。

Python同时声明多个变量和其他语言有所不同，有点JavaScript解构赋值的味道！
```python
# coding=utf-8
#单变量声明
score = 95.512      # average score
UID = "2016110418"  # user ID
sex = True          # sex

#多个变量声明
machineType, machineName =  12, "air-condition"
```

#### [1.1 赋值、解构赋值](#)
在Python中，只要是可迭代的对象，都可以用来解构，例如元祖、字典、列表...  ，需要注意的是字典在进行迭代操作时，只会返回键，而不会返回值。

**元祖的解构赋值:**

```python
def get_tuple():
    tpl = (25, True, 'New World New Life!')
    return tpl


age, sex, slogan = get_tuple()  #解构
print(f"年龄: {age} 性别: {sex}, 口号: {slogan}")

project_name, salary = ('上海区块链', 1500) #解构
print(f"项目名称:{project_name}\n薪水:{salary}/月")
```

**列表解构赋值**: [如果想要使用少数的变量来接收更多的元素，就需要使用 * 来将最后面的多个元素进行聚合 !](#)

```python
a, b, c = [23, 25, 25]
print(a, b, c,sep=" ")

# 如果想要使用少数的变量来接收更多的元素，就需要使用 * 来将最后面的多个元素进行聚合
quora, know, *scores = [23, 45, 56, 67, 78, 87, 12]
print(quora, know, scores, sep="\n")
# 23
# 45
# [56, 67, 78, 87, 12]
```

**字典解构赋值**： [字典在进行迭代操作时，只会返回键，而不会返回值](#)

```python
a, b = {"key": 1, "key2": 2}
print(a)  # key
print(b)  # key2
```

#### [1.2 删除变量](#)
在python中可以删除一个变量，当然这本质是解除变量名对内存中变量的引用，回收内存！ 

您也可以使用 **del**语句删除一些对象的引用。**del**语句的语法是：
```python
del var1[,var2[,var3[....,varN]]]
```
您可以通过使用del语句删除单个或多个对象的引用。例如：
```python
del var
del var_a, var_b
```

**作用于变量名**
```python
a = 12
del a
print(a); #报错 a已经不存在了
```

**作用于list**: [del语句用于list列表操作，可以删除一个列表，还可以删除列表里面一个或连续几个元素](#)

```python
valuesArray = [95, 87, 85, 79, 78];
ref_vals = valuesArray;

del ref_vals; #解引用
del valuesArray[1] #删除第二个元素
print(valuesArray);
# [95, 85, 79, 78];

del valuesArray[0:2] #删除0-2下标的元素！
```

#### [1.3 常量](#)
**常量类似于变量，** 但其值在程序的整个生命周期内保持不变。 **Python没有内置的常量类型** ，但Python程序员会使用全大写来指出应将某个变量视为常量，其值应始终不变：

```python
#const variables
DAYS_OF_YEAR = 35  #一年35天 某颗星球
MAX_COUNT = 500000 #最大数量
```

> python 的常量是一种约定，并不是真的不能够修改！并没有 **const** 修饰符，相比于C++的const ，python这样可以少很多事情!

#### [1.4 变量和类型](#)
需要铭记的重要内容是：[**在python中，只有对象才有类型，变量是没有类型的！**](#) 

```python
a = [1,2,3]  # [1,2,3] 是 List 类型, 变量 a 是没有类型, 它是引用
b = "Runoob" # "Runoob" 是 String 类型, 变量 b 是没有类型, 它是引用
```
以上代码中，[1,2,3] 是 List 类型，"Runoob" 是 String 类型，而变量 a 是没有类型，她仅仅是一个对象的引用（一个指针），可以是 List 类型对象，也可以指向 String 类型对象。

### [2. 标准数据类型](#)
Python3 中有**六** 个内置的标准的基本数据类型： Number（数字） String（字符串） List（列表） Tuple（元组） Set（集合） Dictionary（字典）。它们又可以分为可更改(mutable)对象与不可更改(immutable)对象。

* 不可变数据（3 个）：Number（数字）、String（字符串）、Tuple（元组）、Bytes字节序列；
* 可变数据（3 个）：List（列表）、Dictionary（字典）、Set（集合）。

**解释两种数据**

* 不可变数据，类似于值类型，一旦修改/重新赋值，原对象被抛弃，会新开辟一个内存空间存储新值，变量会指向一个全新的对象。
* 可变数据，可以进行更改，并且更改后内存地址不会发生改变！ 类似于Java、C#的引用类型！

| 类型名称     | 类型      | 是否可变 | 例子                                   |
| ------------ | --------- | -------- | -------------------------------------- |
| 布尔值       | bool      | 否       | True,False                             |
| 整数         | int       | 否       | age = 45                               |
| 浮点数       | float     | 否       | PI = 3.1415926                         |
| 复数         | complex   | 否       | 5+9j, 5j                               |
| 文本字符串   | str       | 否       | "message"                              |
| 元祖         | tuple     | 否       | ("remix", True, 29, 3.1415)            |
| 列表         | list      | 是       | ["red", "green", "yellow"]             |
| **字节序列** | bytes     | 否       | b'ab\xff'                              |
| **字节数组** | bytearray | 是       | bytearray(...)                         |
| 集合         | set       | 是       | set([3, 5, 7, 8])                      |
| **冻结集合** | frozenset | 否       | frozenset(['Elas', 'Otto', 'Kote'])    |
| 字典         | dict      | 是       | {"cicier": 23, "mike": 27, "umix": 21} |

#### [2.1 对象](#)
在Python中数据都是对象，一个对象是至少包含一下内容的数据块：

* **类型**，定义了可以执行哪些操作，决定了值是可变的，还是不变的
* 唯一的**id**，用于区分于其他对象
* 和类型一直的**值**
* **引用计数**，用于跟踪该对象的使用频率

#### [2.2 类型判断](#)
我们有**type**和**isinstance**操作符来判断数据类型，他们的区别如下：

- type() 不会认为子类是一种父类类型。
- isinstance() 会认为子类是一种父类类型。

```python
a = 111
isinstance(a, int)  #True
```

**类型判断例子：**

```python
>>> class A:
...     pass
... 
>>> class B(A):
...     pass
... 
>>> isinstance(A(), A)
True
>>> type(A()) == A 
True
>>> isinstance(B(), A)
True
>>> type(B()) == A
False
```

#### [2.3 id(__obj)](#)
通过**id**获得变量的标识符**Id**，通过**type**获取变量的类型 多次赋值以后变量名会指向新的空间 说明他们是值类型。

```python
name = "jxkicker"
age = 18

print("标识", id(name), "类型", type(name),"值",name)
name = 'zjr'
print("标识", id(name), "类型", type(name),"值",name)

#多次赋值以后变量名会指向新的空间 说明他们是值类型
print("标识", id(age), "类型", type(age),"值",age)
# 标识 1280218759088 类型 <class 'str'> 值 jxkicker
# 标识 3272803140144 类型 <class 'str'> 值 zjr
# 标识 1280217738064 类型 <class 'int'> 值 18
```

### [3. 数值类型](#)
数字包括几种基本类型，首先是整型，然后是浮点型(小数)！ Python还支持复数(complex numbers) 类型！ 布尔类型也算整型！

数字数据类型用于存储数值。他们是不可改变的数据类型，这意味着改变数字数据类型会分配一个新的对象。

#### [3.1 整数类型](#)
整型有两种：int（有符号整型）、bool  **当然一个用于科学计算的语言怎么可能只有这两个整型呢！** ，一些其他的库提供了很多其他整型，例如 numpy提供了 int64、int128;

**int(value, o) 可以用于强制类型转换，使其转换为整数,  这个函数有两个参数**，第一个参数是要转换为整形的对象，第二个是使用的进制。

```python
# -*- coding: UTF-8 -*-
countOfStudent = 56
score = int("95");

print(countOfStudent + score); #151

miner = int("2130", 8)  # 八进制

print("miner: %d" % miner)   # 1112
```
**整数字面量：**如果数字字面量过于长，可以使用下划线`_`来作为**数位分隔符**。

```python
score = 123_34_79
MAX_COUNT = 100_100_100_100

print(score)	  # 123_34_79	
print(MAX_COUNT)  # 100100100100
```

**注意点：Python的整数除法运算比较奇特!**  `/` 运算符是浮点数除法，`//` 这才是其他程序语言的整数除法！

```python
val = 100

result = val / 3
rel = val // 3

print(result)  # 33.333333333333336
print(rel)  # 33
```

##### [3.2.1 小整数池](#)
在 Python 中，整数可以表示的范围很大，但是常用的整数可能都集中在 -1000 到 1000 之间，如考试分数，一般在 0 到 100 之间，年龄也在 0 到 100 之间。

基于整数对象分布不均匀的特性，Python做了一些优化来提升运行效率。

在 Python 解释器的内部实现中，对于 -5 到 256 内的整数建立了一个小整数池。如果要使用的整数对象在该范围内，其不会自动新建一个整数对象，而是看小整数池中是否有值相同的整数对象：

- 如果有，则返回这个现有的整数对象；
- 如果没有，则创建一个新的整数对象，这个新建的整数对象在以后也可能被共享使用。

我们可以使用函数 id() 来查看对象的地址

```python
count = 25
save = 27

print(id(count), id(save))  # 140714610124328 140714610124392

count = count + 2
# 此时count 和 save 指向同一个对象
print(id(count))  # 140714610124392
```

#### [3.2 布尔类型 bool](#)
Python3 中，**bool** 是 int 的子类，True 和 False 可以和数字相加，**True==1**、False==0 会返回 True，但可以通过 is 来判断类型。

* True 值为 1
* False 值为 0

```python
flag = True
if flag == 1:
    print("True is 1")
else:
    print("True is not 1")
```

**bool()** 函数可以接受任何值作为参数并且返回等价的布尔值。

支持的布尔运算：**and 、or、not**

```python
tr_t, tr_f = True, False

print(tr_t and tr_f)  # False
print(tr_t or tr_f)  # True
print(not tr_f)  # True
```

#### [3.3 进制转换](#)
本质上将数字转换为各个进制的字符串表示，这个Python也可以支持进制转换！

**进制：**

* 二进制 : 0b 开头
* 八进制 : 0o 开头
* 十六进制 ：0x 开头

**进制转换函数:**


* **bin(__number)**:  将其转换为二进制数
* **oct(__number)**: 将其转换为八进制数
* **int(__number)**: 将其转换为十进制数
* **hex(__number)**: 将其转换为十六进制数

```python
val = 32
val2 = 0o142

print('二进制', 0b1101)  # 13
print('二进制', bin(val))  # 0b100000
print('八进制', oct(val))  # 0o40
print("十进制", int(val2))  # 98
print("十六机制", hex(val2))  # 0x62
```

#### [3.4 浮点类型](#)
Python支持的浮点类型是 float` `在计算机中表示一个浮点数，其结构如下： **浮点数国际标准：IEEE 754**

<table log-set-param="table_view" data-sort="sortDisabled">
    <tbody>
        <tr>
            <td align="left" width="87">
                <div class="para" label-module="para">阶符±</div>
            </td>
            <td align="left" width="87">
                <div class="para" label-module="para">阶码e</div>
            </td>
            <td align="left" width="87">
                <div class="para" label-module="para">数符±</div>
            </td>
            <td align="left" width="87">
                <div class="para" label-module="para">尾数m</div>
            </td>
        </tr>
    </tbody>
</table>
* 尾数是小数，其位数n+1决定了浮点数的精度，如果尾数采用小数且位数n足够长，则当浮点数运算需要对尾数运算结果舍入时，造成的数据精度损失会比较小。即尾数越长，所能表示的精度越高。
* 阶码是整数，其位数k+1决定了浮点数表示的数值范围，也就是决定了数据的大小，或小数点在数据中的真实位置。阶符决定阶码的正负。即阶码越长，所能表示的范围越大。
* 尾数的符号表示浮点数的正负。

```python
# -*- coding: UTF-8 -*-
score = 98.564;
height = float("173.154");

print("height: %5.3f" % (height + score));
#271.718

PI = 3.912342e4  #科学计数法
print(PI)  # 39123.42
```

浮点数由整数部分和小数部分组成，其实不精确地，小数位数不确定，需要确定的小数位数可以使用 **decimal** ,不推荐使用浮点数进行等于比较。

```python
from decimal import Decimal

val_dec = Decimal('1.2152') + Decimal('2.3')

print(val_dec)
val_flo = 1.2152 + 2.3
val_flo2 = 1.2152 + 2.3

print(val_flo)
print(val_dec == val_flo) #false
```

##### 3.4.2 浮点数方法
Python内置了一些浮点数方法

* eval(str) , 独立方法，将字符串转换为浮点数 
* is_integer()，对象方法，判断一个浮点数是否是整数
* as_integer_ratio, 将浮点数转换成近似的两个整数的商

```python
PI = eval("3.142")
val = 4.0
print(PI.is_integer())  # False
print(val.is_integer())  # True

a = 0.2
tpl = a.as_integer_ratio()
print(tpl)  # (3602879701896397, 18014398509481984)
```

#### [3.5 复数类型](#)
先来看复数的定义： 我们把形如`z=a+bj（a,b均为实数）`的数称为复数，其中`a`称为实部，`b`称为虚部，`j`称为虚数单位。**python**中可以直接使用**complex**类构造复数。

```python
cpla = complex(-2,2)
cplb = complex(5,-1)

print(cpla, cplb)
print(cpla + cplb)

value = -2+4j

print(value) #(-2+4j)
```

type(x)，python中复数类型为complex；
```python
cpla = complex(-2,2)
print(type(cpla))  #<class 'complex'>
```

* **x.real** 获取复数x的实部
* **x.imag** 获取复数x的虚部，使用`x.imag`

```python
cpla = complex(-2,2)
print(cpla.real, cpla.imag);
```

* x.conjugate(): 返回共轭复数
* 两个复数支持加减乘除操作

### [4. 字符串类型](#)
Python中的字符串用单引号 `'` 或双引号 `"` 括起来，同时使用反斜杠 `\` 转义特殊字符。几乎在每一门编程语言中，字符串都是一块比较多的知识内容，这里我们先介绍一些字符串的基本用法。

* 反斜杠可以用来转义，使用`r`可以让反斜杠不发生转义。
* 字符串可以用`+`运算符连接在一起，用 **`*`** 运算符重复。
* Python中的字符串有两种索引方式，从左往右以0开始，从右往左以-1开始。
* Python中的字符串不能改变。

```python
# -*- coding: UTF-8 -*-
name = "remix"
message = 'this is a message!'
introduce = "you are a master!"

print(name, message, introduce, sep="  ");
```

**双三引号可以多行字符串**
```python
said = """jx kicker that 
want go there
let us to dead
"""
```
`与 C 字符串不同的是，Python 字符串不能被改变。向一个索引位置赋值，比如 word[0] = 'm' 会导致错误`

**字符串乘法**

```python
# -*- coding: UTF-8 -*-
name = "remix"

print(name * 2); #remixremix
```
**字符串拼接**
```python
# -*- coding: UTF-8 -*-
name = "remix"
message = 'this is a message!'
introduce = "you are a master!"

print(name * 2); #remixremix
print(name + ": \"" + message + "\""); #remix: "this is a message!"
```

#### [4.1 字符串编码](#)
字符串编码方式有ASCII，UTF-8, UTF-16, UTF-32。Python默认采用的是可变长字符串编码方式 **UTF-8**，编码不同，占用的字节就不同，不同编码之间不能相互识别，编码与解码必须一样。

python给 **str** 类型提供了两个方法，用于字符串编码和解码： **可以实现str类型和bytes类型相互转换！ **

* **encode**(*encoding='utf-8'*, *errors='strict'*)  **将字符串编码为二进制字节流**
  * 默认的错误处理方案 `'strict'` 表示编码错误将引发 [`ValueError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ValueError) (或更特定编解码器相关的子类，例如 [`UnicodeEncodeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#UnicodeEncodeError))
* **decode**(*obj*, *encoding='utf-8'*, *errors='strict'*) **将二进制字节流转换为字符串**
  * 默认的错误处理方案 `'strict'` 表示编码错误将引发 [`ValueError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ValueError) (或更特定编解码器相关的子类，例如 [`UnicodeDecodeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#UnicodeDecodeError))。

```python
message = b'your father is me, do you know that?'  # 二进制字节流
print(type(message))  # <class 'bytes'>

result = message.decode("ascii")  # 重新解析为字符串
print(type(result), result)  # <class 'str'>

# 使用字符串创建一个使用utf-8编码的字节流
message_bytes = "我是老傻逼了".encode("utf-8")
message_bytes_utf32 = "我是老傻逼了".encode("utf_32")
print(message_bytes)
# b'\xe6\x88\x91\xe6\x98\xaf\xe8\x80\x81\xe5\x82\xbb\xe9\x80\xbc\xe4\xba\x86'
print(message_bytes_utf32)
# b'\xff\xfe\x00\x00\x11b\x00\x00/f\x00\x00\x01\x80\x00\x00\xbbP\x00\x00<\x90\x00\x00\x86N\x00\x00'
print(type(message_bytes))  # <class 'bytes'>

error = "__error__happen__23_15"
message_str = message_bytes.decode("utf-8", error)

print(message_str)  # 我是老傻逼了
```

#### [4.2 字符串切片](#)
Python 提供了很多截取字符串的方法，被称为“切片（slicing）”,  **由于Python的字符串是不可变数据，所以截取后的字符串和原来的字符串是完全不同的两个对象。** 
```python
str[start: end: step]
```
索引值以 0 为开始值，-1 为从末尾的开始位置。

* **start** ：起点位置，子字符串的起始索引。该索引处的字符包含在子字符串中。start 为空时则默认为 0。
* **end** ：终点位置，子字符串的终止索引。该索引处的字符不包括在子字符串中。end 为空时，或者指定的值超过字符串的长度，则默认它等于字符串的长度。
* **step** ：步长，当前字符之后和目标字符之间的距离。step 为空时，则默认值为 1。

```python
# -*- coding: UTF-8 -*-
message = '1234567890!'

print(message[0:5])   #12345
print(message[:5])    #12345  
print(message[0:-5])  #123456
print(message[2:])    #34567890!
slistr = message[0:8:2] #1357

del message
print(slistr) #1357
```

#### [4.3 空字符串和 len( ) 函数](#)
Python允许空字符串的存在，不包含任何字符且长度为0， **len( )**  用于计算字符串含有多少个字符。

```python
# -*- coding: UTF-8 -*-
message = '1234567890!'

print("string length: %d" % len(message))
#string length: 11
```

#### [4.4 字符串操作](#)
Python字符串支持很多操作，替换、查找... **python的字符串是一个类，它有很多的方法，需要的时候查询API就可以了**

**replace** 替代字符串

```python
message = '1234567890!'

print(message.replace('456',"--"))
#123--7890!
```
**str(x)**: 将对象 x 转换为字符串

* capitalize(): 返回原字符串的副本，其首个字符大写，其余为小写。
* count(sub[, start[, end]]): 返回子字符串 sub 在 [start, end] 范围内非重叠出现的次数。
* format(*args, **kwargs): 执行字符串格式化操作。 调用此方法的字符串可以包含字符串字面值或者以花括号 {} 括起来的替换域。 每个替换域可以包含一个位置参数的数字索引，或者一个关键字参数的名称。 返回的字符串副本中每个替换域都会被替换为对应参数的字符串值。

```python
"The sum of 1 + 2 is {0}".format(1+2)
#'The sum of 1 + 2 is 3'
```
* upper(): 返回原字符串的副本，其中所有区分大小写的字符均转换为大写。
* lower(): 返回原字符串的副本，其中所有区分大小写的字符均转换为小写。
* startswith(prefix[, start[, end]]): 如果字符串以指定的 prefix 开始则返回 True，否则返回 False
* endswith(prefix[, start[, end]]): 如果字符串以指定的 prefix 结束则返回 True，否则返回 False
* split(sep=None, maxsplit=- 1): 返回一个由字符串内单词组成的列表，使用 sep 作为分隔字符串。
* find(sub[, start[, end]]): 返回子字符串 sub 在 [start, end] 范围内出现的位置。
* **isalpha()**  如果字符串中的所有字符都是字母，并且至少有一个字符，返回 True ，否则返回 False 。
* **isascii()**  如果字符串为空或字符串中的所有字符都是 ASCII ，返回 `True` ，否则返回 `False`  
* **isdigit()**  如果字符串中的所有字符都是数字，并且至少有一个字符，返回 `True` ，否则返回 `False` 

#### [4.5 ASCII相关接口](#)
Python内置了两个函数，用于将字符串转换为 ASCII码，或者ASCII转换为字符串。

* ord(str) 获取单个字符的ASCII码
* chr(num) ASCII码转换为字符 num范围必须在 0-255 之间！

```python
code_number = ord('a')
print(code_number, chr(code_number))  # 97 a
```

#### [4.6 字符串输出格式语法](#)
Python 3中引进了这种新式的语法。新式语法丢掉了原先的%符号，改用format()方法在字串中插入变量，使用时需要搭配花括号进行标识。 **详细操作，请查阅后续！**

最开始使用 % 来进行格式化输出
```
"%[(name)][flags][width][.precison]type" % 待格式化数据
```
然后引入了 format！

```
"{[index][:[[fill]align][sign][#][0][width][grouping_option][.precision][type]]}".format()
```

```python
first_name = 'John'
last_name='Snow'
city = 'Winterfell'
print("Hi, My name is {0} {1}. I am from {2} ".format(first_name, last_name,city ))


# .3表示一共三个数 运行结果:3.14
print('{0:.3}'.format(3.14159))

# .3f表示三位小数  运行结果:3.142
print('{0:.3f}'.format(3.14159))

# 宽度为10 保留三位小数 运行结果:     3.142
print('{0:10.3f}'.format(3.14159))

# 0是占位符的顺序, 可以省略 默认为0
```
还可以访问参数属性
```python
c = 3-5j
>>> ('The complex number {0} is formed from the real part {0.real} '
...  'and the imaginary part {0.imag}.').format(c)
```
它还支持一些格式化参数
```python
"int: {0:d};  hex: {0:x};  oct: {0:o};  bin: {0:b}".format(42)
'int: 42;  hex: 2a;  oct: 52;  bin: 101010'
```

可以看到花括号{ }取代了xxx，而.format(person)可以将person变量的值插入到花括号中。

**Python3.6** 提供了 **f-string** 作为字串格式化的方式。f-strings又称为·string interpolation(字符串插值)·

```python
# -*- coding: UTF-8 -*-
age = 25.5321
print(f"my age is {age:-10.5}!");
#my age is     25.532!

first_name = 'John'
last_name='Snow'
city = 'Winterfell'
print(f"Hi, My name is {first_name} {last_name}. I am from {city}!")
#Hi, My name is John Snow. I am from Winterfell!
```

**控制浮点数精度**
```python
import math
pi = math.pi
print(f'{pi: .3f}')
print(f'{pi:.8f}')
 
#输出
3.142
3.14159265
```

**标准化显示宽度:**
```python
for x in range(1,11):
    print(f'{x:02}|{x**2:3}/{x**5:6}')

#输出
01|  1/     1
02|  4/    32
03|  9/   243
04| 16/  1024
05| 25/  3125
06| 36/  7776
07| 49/ 16807
08| 64/ 32768
09| 81/ 59049
10|100/100000
```

**修改为左对齐:**
```python
for x in range(1,11):
    print(f'{x:<2}|{x**2:<3}|{x**5:<6}')

#输出
1 |1  |1     
2 |4  |32    
3 |9  |243   
4 |16 |1024  
5 |25 |3125  
6 |36 |7776  
7 |49 |16807 
8 |64 |32768 
9 |81 |59049 
10|100|100000
```

**设置科学计数法格式:**
```python
import math
pi = math.pi
print(f'{pi*100:.10e}')

#输出
3.1415926536e+02
```

**控制有效数字位数**
`通过下面的方式，我们还可以控制所显示数字的有效数字位数，即从左开始第一个不为0的数字往右一共显示的个数，当位数低于整数部分时会自动变成科学计数法格式：`

```python
a=1312.3123123123123
print(f'{a:.10g}')
#输出：1312.312312

a=1312.3123123123123
print(f'{a:.3g}')
#输出：1.31e+03
```

**将小数百分比输出！**

```python
lf = 0.56;
print(f"{lf:.2%}"); #56%
```

**推荐使用 f-string 字符串插值的方式**

### [5. bytes类型](#)
Pythond 使用bytes 类型用来表示一个 **字节串** ，在Python3以后，字符串和bytes类型彻底分开了。字符串是以字符为单位进行处理的，bytes类型是以字节为单位处理的。  **\x表示后面的字符是十六进制数！** 

bytes数据类型在所有的操作和使用甚至内置方法上和字符串数据类型基本一样，也是不可变的序列对象。

bytes对象只负责以二进制字节序列的形式记录所需记录的对象，至于该对象到底表示什么（比如到底是什么字符）则由相应的编码格式解码所决定
> Python3中，bytes通常用于网络数据传输、二进制图片和文件的保存等等

```python
class bytes([source[, encoding[, errors]]])
```

表示 bytes 字面值的语法与字符串字面值的大致相同，只是添加了一个 `b` 前缀：

```
bitcoin = b"come on edit!"
```

**bytes 字面值中只允许 ASCII 字符（无论源代码声明的编码为何）**，任何超出 127 的二进制值必须使用相应的转义序列形式加入 bytes 字面值。

#### [5.1 创建 bytes 对象](#)

创建bytes数据使用`b''`创建，也可以使用 **bytes( )** 创建不可变序列。

```python
b = b''         # 创建一个空的bytes
b = byte()      # 创建一个空的bytes
string_asc = "come on edit! ————蒋—————"
b = bytes(string_asc, encoding='utf-8')

print(b.decode('utf-8'))
# come on edit! ————蒋—————
```

使用 **bytearray( )** 创建可变序列。

```python
names = bytearray("google is good company!", encoding="utf-8")
names.append(98)
print(names.decode("utf-8"))
# google is good company!b
```

#### [5.2 还原 bytes 数据](#)

使用 **bytes.decode( )** 还原不可变序列。

```python
byte_str = bytes('Python', encoding='utf-8')
utf_str = bytes.decode(byte_str)
print(utf_str)  # 'Python'
```

在UTF-8中，每个汉字用3个 **Byte** 表示

```python
byte_str = bytes('我是', encoding='utf-8')
print(byte_str)
>>> b'\xe6\x88\x91\xe6\x98\xaf'
```

#### [5.3 bytes 类型切片迭代](#)

通过 bytes[index] 方式返回的是底层 **int** 类型。

```python
byte_str = b'abc'
print(type(byte_str[2]))
print(byte_str[2])
>>> <class 'int'>
>>> 99
```

通过**for ... in bytes**方式返回的是底层 **int** 类型。

```python
names = bytearray("google is good company!", encoding="utf-8")

for byte in names:
    print("[%d]:%c" % (byte, byte))
```

通过 **bytes[start:end]** 方式返回的是底层 **bytes** 类型。

```python
for byte in names[0:6]:
    print("[%d]:%c" % (byte, byte))
```

### [6. None](#)

在 Python 中，有一个特殊的常量 None（N 必须大写）。和 False 不同，它不表示 0，也不表示空字符串，而表示没有值，也就是空值。


```python
you = None
if you is None:
    print("i love you!")
else:
    print("yes me too!")
```

```python
>>> None is []
False
>>> None is ""
False
```
None 有自己的数据类型，我们可以在 IDLE 中使用 type() 函数查看它的类型，执行代码如下：
```python
type(None)  #<class 'NoneType'>
```

None 常用于 assert、判断以及函数无返回值的情况。举个例子，在前面章节中我们一直使用 print() 函数输出数据，其实该函数的返回值就是 None。因为它的功能是在屏幕上显示文本，根本不需要返回任何值，所以 print() 就返回 None。

另外，对于所有没有 return 语句的函数定义，Python 都会在末尾加上 return None，使用不带值的 return 语句（也就是只有 return 关键字本身），那么就返回 None。

```python
>>> spam = print('Hello')
Hello
>>> None == spam
True
```

**如何一个函数没有返回值，那么如果你用一个变量去接受函数返回值，那么这个变量得到的返回就是None**

### [7. 脚本属性](#)
脚本文件自身有两个属性， `__name__`、 `__file__`，在很多 Python程序里，经常会看到这样的一段代码。

```python
if __name__ == '__main__':
    main()
```
但很多人对这个内置变量的具体含义并不清楚。作为 Python 的内置变量，`__name__` 变量还是挺特殊的。它是每个 `Python` 模块必备的属性，但它的值取决于你是如何执行这段代码的。

#### 7.1 \_\_name\_\_
一个模块被另一个程序第一次引入时，其主程序将运行。如果我们想在模块被引入时，模块中的某一程序块不执行，我们可以用__name__属性来使该程序块仅在该模块自身运行时执行。

每个模块都有一个\_\_name\_\_属性，当其值是'\_\_main\_\_'时，表明该模块自身在运行，否则是被引入。

```python
# 如果当前脚本文件是入口文件则执行该函数
if __name__ == '__main__':
    name, age = get_information()
    time_str = time.strftime("%Y/%m/%d %H:%M:%S", time.localtime())
```

-----
`时间`: `[2023年2月15日15:21:28]` 