### [Python 运算符和控制流程](#)
**介绍：** 运算符和控制流程就好比一个程序的骨架，用于构建数据处理的流程，是一门编程语言最基础的部分！

-----
-  [1. 运算符](#1-运算符)
-  [2. 条件控制](#2-条件控制)
-  [3. 循环控制](#3-循环控制)
-  [4. Python 封装](#4-python-封装)

-----

### [1. 运算符](#)
Python 语言支持以下类型的运算符: **算术运算符**、比较（关系）运算符、赋值运算符、逻辑运算符、位运算符、成员运算符、身份运算符、运算符优先级。

表达式有几个核心要素:  操作数类型和个数、优先级。

#### [1.1 算术运算符](#)
最常用的运算符！Python 没有`++` 和`--` 用以恶心人的自增自减运算符！
|运算符|描述|实例|
|:--:|:---|:---|
|+|加|两个对象相加	a + b 输出结果 31|
|-|减|得到负数或是一个数减去另一个数	a - b 输出结果 -11|
|*| 乘     |不同类型的乘法不相同|
|/|浮点数除|x 除以 y	b / a 输出结果 2.1|
|%|取模|返回除法的余数	b % a 输出结果 1|
|**|幂|返回x的y次幂	a**b 为10的21次方|
|//|整数除|向下取接近商的整数|

**使用例子：** 区分浮点数除法和整数除法！
```python
#python
rlt = 9 / 2
rlt_int = 9 // 2

print(rlt)  # 4.5
print(rlt_int)  # 4
print(2**6)  # 64
```

**乘法：** 乘法在数值类型、字符串类型、列表类型上面的运算结果各有差异！
```python
scores = [1, 2, 4, 5] * 2
result = "success !" * 2
count = 20 * 2
tpl = ("Hello", "world") * 2

print(scores)  # [1, 2, 4, 5, 1, 2, 4, 5]
print(result)  # success !success !
print(count)  # 40
print(tpl)  # ('Hello', 'world', 'Hello', 'world')
```
#### [1.2 比较运算符](#)
常用于条件表达式、逻辑判断, 是很常见的运算符。

|运算符|描述|实例 (a = 10, b = 20)|
|:---|:---|:---|
|==|等于|比较对象是否相等	(a == b) 返回 False。|
|!=|不等于|比较两个对象是否不相等	(a != b) 返回 True。|
|>|大于|返回x是否大于y	(a > b) 返回 False。|
|<|小于|返回x是否小于y。	(a < b) 返回 True。|
|>=|大于等于|返回x是否大于等于y。	(a >= b) 返回 False。|
|<=|小于等于|返回x是否小于等于y。	(a <= b) 返回 True。|

```python
# -*- coding: UTF-8 -*-
age = int(input("please input your age: "));

if age <= 17 & age >= 0:
    print("teenager!")
elif age > 18 and age < 65:
    print("young man!")
elif age >= 65:
    print("the old!")
else:
    print("what happen!")
#end if
```


#### [1.3 赋值运算符](#)
很简单的， 也比较常用！ **一些运算符可以简写赋值和运算！**

|运算符|描述|实例|
|:---|:---|:---|
|=|简单的赋值运算符|c = a + b 将 a + b 的运算结果赋值为 c|
|+=|加法赋值运算符|c += a 等效于 c = c + a|
|-=|减法赋值运算符|c -= a 等效于 c = c - a|
|*=|乘法赋值运算符|c *= a 等效于 c = c * a|
|/=|除法赋值运算符|c /= a 等效于 c = c / a|
|%=|取模赋值运算符|c %= a 等效于 c = c % a|
|**=|幂赋值运算符|c \*\*= a 等效于 c = c \*\* a|
|//=|取整除赋值运算符|c //= a 等效于 c = c // a|

```python
val = 2;
val *= 15;

print(val);#30 
```

#### [1.4 逻辑运算符](#)
等同于Java、C++、C# 里面的 &&、||、! 运算符 Python将他们语义化为了 and  or not！

* **and**	x and y 布尔"与"
* **or**	x or y	布尔"或"
* **not**	not x	布尔"非" 

```python
if a > 20 and b< 60:
    print("you are loser")
else:
    print('success!')
```

#### [1.5 位运算符](#)
我也很少用到，Python还没有底层到需要操作位这种数据粒度！

* &	按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0	
* |	按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。	
* ^	按位异或运算符：当两对应的二进位相异时，结果为1	
* ~	按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1 。~x 类似于 -x-1	
* <<	左移动运算符：运算数的各二进位全部左移若干位，由 << 右边的数字指定了移动的位数，高位丢弃，低位补0。	
* **>>**	右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，>> 右边的数字指定了移动的位数	

```python
# -*- coding: UTF-8 -*-
count = 64;
count = count << 2;

print(count); #256

a = 0b00111100 #60
b = 0b00001100 #12

print(a & b) #12
print(a | b) #60
print(a^b)   #48
```

#### [1.6 成员运算符](#)
身份运算符用于比较两个对象的存储单元 id() 函数用于获取对象内存地址。 **字符串，列表或元组都支持成员运算符**

|运算符|描述|
|:---|:---|
|**in**|如果在指定的序列中找到值返回 True，否则返回 False。|
|**not in**|如果在指定的序列中没有找到值返回 True，否则返回 False。|

```python
# -*- coding: UTF-8 -*-
a = 78; scores = [89,78,54,65,23,12,85,98]
if a in scores:
    print('exist')  #exist
# end if    

user = ("remix", 56, bool)
print(56 in user) #true

nstr = "2016110418"
print("18" in nstr); #true
```


#### [1.7 身份运算符](#) 
身份运算符用于比较两个对象的存储单元 等于 id(obj1) == id(obj2)

* **is**	    is 是判断两个标识符是不是引用自一个对象	x is y, 类似 id(x) == id(y) , 如果引用的是同一个对象则返回 True，否则返回 False
* **is not**	is not 是判断两个标识符是不是引用自不同对象 x is not y ， 类似 id(x) != id(y)。如果引用的不是同一个对象则返回结果 True，否则返回 False。

```python
age = 10
apper = 10

if age is apper:
    print('same numbers')
else:
    print('different numbers')
```

#### [1.8 运算符优先级](#) 
以下表格列出了从最高到最低优先级的所有运算符：

|运算符|解释|
|--|--|
|**|指数 (最高优先级)|
|~ + -	|按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@)|
|* / % //	|乘，除，取模和取整除|
|+ -	|加法减法|
|>> <<	|右移，左移运算符|
|&	|位 'AND'|
|^\||位运算符|
|<= < > >=	|比较运算符|
|<> == !=|等于运算符|
|= %= /= //= -= += *= **=	|赋值运算符|
|is is not|身份运算符|
|in not in|成员运算符|
|not and or|逻辑运算符|

#### [1.9 isinstance(instance, type)](#)
Python 中的isinstance()函数，isinstance()是Python中的一个内建函数。是用来判断一个对象的变量类型。

```python
age = 32
print(isinstance(age, int))  #True
```

### [2. 条件控制](#)
Python条件语句是通过一条或多条语句的执行结果（True或者False）来决定执行的代码块，它总共有三个部分: 

* **if condition:**  
* **elif condition:**  
* **else:**

```python
import math
import random as rand

#test your lucky value
lucky = int(input("input a lucky number: "))

rnumber = rand.randint(lucky - 10, lucky + 10)

if lucky == rnumber:
    print("you are super lucky person!")
elif math.fabs(rnumber - lucky) < 5:
    print(f"{rnumber}: you are lucky person!")
else:
    print(f"{rnumber}: today is not a good day!")
#end if
```

只有一段的 **if** 语句！
```python
if ( value  == 100 ): print("变量 var 的值为100" )
```

#### [2.1 match](#)
用来替代 `switch`  配合 | 和`_` 一起使用！

```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case 401 | 403 | 404:
            return "Not allowed"
        case _:
            return "Something's wrong with the internet"
```


### [3. 循环控制](#) 
Python 提供了 for 循环和 while 循环 **（在 Python 中没有 do..while 循环）:**

* break 语句	在语句块执行过程中终止循环，并且跳出整个循环
* continue 语句	在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环。
* pass 语句	pass是空语句，是为了保持程序结构的完整性。

**class range(start, stop[, step])函数:**  range 类型表示不可变的数字序列，通常用于在 for 循环中循环指定的次数。
```python
for i in range(0, 5):
    print(i)
#0 1 2 3 4
```

#### [3.1 for循环](#)
for循环可以遍历任何序列的项目，如一个列表或者一个字符串。 比较奇葩还可以带一个 else用于for循环结束后执行的语句！ 当然这个else可以省略！

```
for iterating_var in sequence:
   statements(s)
else:
   statements(s1)
```

**遍历列表：**

```python
# -*- coding: UTF-8 -*-
fruits = ['banana', 'apple',  'mango']
for index in range(len(fruits)):
   print ('当前水果 : %s' % fruits[index])
else:
    print ("Good bye For!")
# 当前水果 : banana
# 当前水果 : apple
# 当前水果 : mango

for fruit in fruits:
   print ('当前水果 : {0}'.format(fruit))
else:
    print("End For")
# 当前水果 : banana
# 当前水果 : apple
# 当前水果 : mango
```

#### [3.2 while](#)
 while 语句用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务。

```
while 判断条件(condition)：
    执行语句(statements)……
else:
    执行语句(statements)……
```

```python
# -*- coding: UTF-8 -*-
numbers = [65, 78, 97, 45 ,95 ,75 ,56, 12]

even = []
odd = []

while len(numbers) >0:
    val = numbers.pop();
    if val % 2:
        even.append(val)
    else:
        odd.append(val)
    #end if
else:
    print("while end !") #while end !
#end while

print(even)
print(odd)
```

### [4. Python 封装](#)
前面讲了封装，并且还介绍了很多具有封装特性的结构，比如说：

* 诸多容器，例如列表、元组、字符串、字典等，它们都是对数据的封装；
* 函数是对 Python 代码的封装；
* 类是对方法和属性的封装，也可以说是对函数和数据的封装。



```python
class EDBlock:
    def __init__(self,
                 before_hash: bytes,
                 timestamp: str,
                 root: bytes,
                 version: int,
                 randon_v_r_f: float,
                 ):
        self.before_hash = before_hash
        self.timestamp = timestamp
        self.root = root
        self.version = version
        self.randon_v_r_f = randon_v_r_f
```






-----
时间: [2022年10月28日15:32:58] 