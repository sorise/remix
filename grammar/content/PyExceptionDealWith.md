### [Python 异常处理](#)

` 错误和异常处理，断言使用！几乎是程序设计的必须， 让我们来学习它吧！`

-----

- [ ] [`1. 错误和异常概述`](#1-)
- [ ] [`2. 异常类`](#2-异常类)
- [ ] [`3. traceback`](#3-traceback)
- [ ] [`4. 断言`](#4-断言)

-----

### [1. 错误和异常概述](#)

Python中导致程序错误的原因有两大类：**语法错误**和**异常**！句法错误又称解析错误！如下所示就是一个语法错误，第一条语句缺少冒号（`':'`）作为结束！

```python
while True
	print('Hello world')

#SyntaxError: invalid syntax
```

即使语句或表达式使用了正确的语法，执行时仍可能触发错误。例如：传入无效的参数、除数为0、数值运算超出最大限制..... 这错误往往不会被语法解析器检测出来，只会在程序运行中的某个特定时刻暴露出来。**大多数异常不会被程序处理，如果程序员不自己捕获处理，将导致程序运行失败！**

```python
name = "message"

def Mod(value: int,p: int):
    return value % p

print(Mod(name, 7))
#TypeError: not all arguments converted during string formatting
```

**异常是Python对象**，表示一个错误。当Python脚本发生异常时我们需要捕获处理它，否则程序会终止执行。我们也可以自定义异常对象，**Python也内置了许多异常类型。**



#### [1.1 异常处理](#)

Python中捕捉异常可以使用 **try/except** 语句。**try/except**语句用来检测**try语句块**中的错误，从而让**except语句**捕获异常信息并处理。

- 首先执行try， 如果当try后的语句执行时发生异常，python就跳出try并执行第一个匹配该异常的except子句，异常处理完毕，控制流就通过整个try语句。
- 如果在try后的语句里发生了异常，却没有匹配的except子句，异常将被递交到上层的try，或者到程序的最上层（这样将结束程序，并打印默认的出错信息）。
- 如果在try子句执行时没有发生异常，python将执行else语句后的语句（如果有else的话），然后控制流通过整个try语句。
- finally 以后的语句，一定会执行！

```python
try:
	#运行可能抛出异常的代码
except 异常类型： #异常类型 和 异常参数
	#处理异常语句
except 异常类型 as 别名: #别名就是 抛出的异常对象
	#处理异常语句
except:
    #如果上面没有匹配项，那么我捕获任何类型异常！
else:
	#如果没有异常发生 执行的语句
finally: 
    #无论如何都要执行的语句
```

**try** 语句可以有多个 **except** 子句 来为不同的异常指定处理程序。 但最多只有一个处理程序会被执行。 

**except 子句** 可以用带圆括号的元组来指定多个异常，例如:

```python
except (RuntimeError, TypeError, NameError):
	pass
```

一个参数错误的小例子：

```python
name = "message"

def Mod(value: int,p: int):
    return value % p  #字符串 用于除法 错误

try:
    print(Mod(name, 7))
except TypeError:
    print("传递的参数类型错误！")
else:
    print("running  normally")
finally: 
    print("无论如何都要执行")
    #一般用于文件关闭，释放数据库链接，网络请求后续处理
```



#### [1.2 异常不可避免 ](#)

即使是知识最渊博的程序员，也无法写出完全没有异常的程序，因为操作系统本身会发生错误，网络也可能发生异常，文件未必如你所愿，用户输入并发完美无缺，人的思维也非毫无漏洞！所以作为一个程序员，懂得为自己的代码套一层 **try-except** 是一个良好且必须的习惯！



#### [1.3 异常类之间的父子关系](#)

如果发生的异常与 **except** 子句中的类是同一个类或是它的基类时,则该类与该异常相兼容!  **口诀: 子类在上父类在下**

```python
class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in [B, C, D]:
    try:
        raise cls()
    except D:
        print("D") #孙类
    except C:
        print("C") #子类
    except B:
        print("B") #父类
```



#### [1.4 获取异常对象](#)

**as**用在异常中，获得捕获的异常对象！如下所示 **zero** 是异常对象，**ZeroDivisionError** 是异常类型！

```python
try:
    a = 10 / 0
except TypeError as ty:
    print(ty.args)
except ZeroDivisionError as zero:
    print(zero.args) #('division by zero',)
    print(ZeroDivisionError.args) #<attribute 'args' of 'BaseException' objects>
```



#### [1.5 抛出异常](#)

Python 使用 **raise** 语句抛出一个指定的异常，支持强制触发指定的异常。

```
raise [Exception [, args [, traceback]]]
```

```python
age = input("请输入你的年龄: ")

try:
    ageReal = int(age)
    if ageReal < 18:
        raise Exception(f"your age ({ageReal:+4} < 18) is not legal!")
except TypeError as ty:
    print(f"TypeError {ty.with_traceback()}")
except Exception as ex:
    print(f"{ex.args[0]}")
except:
    print(f"i dont know what except")

```



#### [1.6 异常类的参数](#)

异常参数是指传递给异常对象的参数，获取异常参数使用as获取异常对象，访问 **args** 属性！

```python
try:
    raise ZeroDivisionError(10, 0) #抛出异常，给两个参数
except ZeroDivisionError as zero:
    print(zero.args) #(10, 0)
```



### [2. 异常类](#) 

在 Python 中，所有异常必须为一个派生自 [**BaseException**](https://docs.python.org/zh-cn/3/library/exceptions.html#BaseException) 的类的实例, 不能被用户定义的异常直接继承。

|`方法`|`说明`|
|:---|:---|
|**SystemExit(BaseException)**|此异常由 sys.exit() 函数引发, 在执行期间，会定期检测中断信号。 该异常继承自 BaseException 以确保不会被处理 Exception 的代码意外捕获|
|**KeyboardInterrupt(BaseException)**|当用户按下中断键 (通常为 Control-C 或 Delete) 时将被引发, 在执行期间，会定期检测中断信号。 该异常继承自 BaseException 以确保不会被处理 Exception 的代码意外捕获|
|`Exception(BaseException)`|`所有内置的非系统退出异常都派生自此类,所有用户定义的异常也应从此类派生 `|
|`ArithmeticError(Exception)`|`所有算术类错误而引发的内置异常都派生自此类: OverflowError, ZeroDivisionError, FloatingPointError`|
|`BufferError(Exception)`|`与缓冲区相关的操作无法执行时将被引发`|
|`LookupError(Exception)`|`用于派生当映射或序列所使用的键或索引无效时引发的异常: IndexError, KeyError`|

**详细的异常有一大堆：** [异常类层次关系图](https://docs.python.org/zh-cn/3/library/exceptions.html#exception-hierarchy)

**BaseException**的构造函数支持传递 列表参数 **\*args**

**args**: `传给异常构造器的参数元组。`

**with_traceback**(*tb*): `此方法会将 *tb* 设为新的异常回溯信息并返回异常对象。 `



#### [2.1 常用内置异常](#)

`一下都是常用的内置异常类型！`

| 序号 | 异常类型            | 描述                                      |
| ---- | ------------------- | ----------------------------------------- |
| 1    | ZeroDivisionError   | 除（或取模）零（所有数据类型）            |
| 2    | IndexError          | 序列中没有此索引（index）                 |
| 3    | KeyError            | 映射中没有这个键                          |
| 4    | SyntaxError         | Python语法错误                            |
| 5    | ValueError          | 传入无效的参数                            |
| 6    | OSError             | 操作系统错误                              |
| 7    | IOError             | 输入/输出操作失败                         |
| 8    | AssertionError      | 断言语句失败, 断言语句返回为 false        |
| 9    | ImportError         | 导入模块/对象失败                         |
| 10   | MemoryError         | 内存溢出错误(对于Python 解释器不是致命的) |
| 11   | NameError           | 未声明/初始化对象 (没有属性)              |
| 12   | NotImplementedError | 尚未实现的方法                            |
| 13   | TypeError           | 对类型无效的操作                          |
| 14   | ZeroDivisionError   | 除(或取模)零 (所有数据类型)               |
| 15   | OverflowError       | 数值运算超出最大限制                      |
| 1    | FloatingPointError  | 浮点计算错误                              |
| 17   | StandardError       | 所有的内建标准异常的基类                  |



#### [2.2 用户自定义异常](#)

你可以通过创建一个新的异常类来拥有自己的异常。**异常类继承自 Exception 类**，可以直接继承，或者间接继承，例如:

```python
class MyError(Exception):
    def __init__(self, value):
        self.value = value
    def __str__(self):
        return repr(self.value)
```

**自定义异常的使用**

```python
age = input("请输入你的年龄: ")

try:
    ageReal = int(age)
    if ageReal < 18:
        raise MyError(f"your age ({ageReal:+4} < 18) is not legal!")
except ValueError as vy:
    print("---- 输入数据不可以转换为整型 ----")
    vy.with_traceback();
    #打印堆栈信息
except MyError as ke:
     print("触发自定义异常！")
     print(ke)
except Exception as ex:
    print(f"{ex.args[0]}")
except:
    print(f"i dont know what except")
```

### [3. traceback](#) 

在日常开发中，我们会做一些基本的异常处理，但是有时候只能打印我们处理的结果或者将异常打印出来，不能直观的知道在哪个文件中的哪一行出错。而使用Python中traceback模块来进行处理可以直观异常信息, **该模块提供了一个标准接口，用于提取，格式和打印Python程序的堆栈痕迹。它完全模仿了Python解释器在打印堆栈跟踪时的行为。 当您想在程序控制下打印堆栈迹线时，这非常有用**

```python
import traceback

def func(num1, num2):
    try:
        x = num1 * num2
        y = num1 / num2
        return x, y
    except:
        traceback.print_exc()

func(1, 0)

"""
Traceback (most recent call last):
  File "E:\Codes\vccode\cs-paper\test.py", line 6, in func
    y = num1 / num2
ZeroDivisionError: division by zero
"""
```

**Python中的traceback信息均来源于一个叫做traceback object的对象，而这个traceback object通常是通过函数sys.exc_info()来获取的**

```
import sys


def func1(num1, num2):
        x = num1 * num2
        y = num1 / num2
        return x, y
def func2():
    func1(1, 0)


if __name__ == '__main__':
    try:
        func2()
    except Exception as e:
        exc_type, exc_value, exc_traceback = sys.exc_info()
        print("exc_type:",exc_type)
        print("exc_value:",exc_value)
        print("exc_traceback:",exc_traceback)
```



### [4. 断言](#) 

Python assert（断言）用于判断一个表达式，在表达式条件为 false 的时候触发异常。断言可以在条件不满足程序运行的情况下直接返回错误，而不必等待程序运行后出现崩溃的情况。

```
assert expression [, arguments]
```

等价于：

```python
if not expression:
    raise AssertionError(arguments)
```

**使用：**

```python
import sys
val = 17

def func():
    return False

assert val >= 18, "未成年不符合规定"

assert func(), "未返回True, 执行错误"

assert ('linux' in sys.platform), "该代码只能在 Linux 下执行"
```



#### [4.1 unittest](#)

**Unittest是Python内部自带的一个单元测试的模块**，它设计的灵感来源于Junit，具有和Junit类似的结构，有过Junit经验的朋友可以很快上手。**unittest 是基于功能测试的单元测试。**

* 批量执行用例 
* 提供丰富的断言知识 
* 可以生成报告

核心要素:

* TestCase（测试用例） 
* TestSuite(测试套件)
* TestRunner(测试执行，执行TestUite测试套件的)
* TestLoader(批量执行测试用例-搜索指定文件夹内指定字母开头的模块)
* Fixture(固定装置(两个固定的函数，一个初始化时使用，一个结束时使用))

### 

-----

`时间`: `[]` 