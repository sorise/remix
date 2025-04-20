### [Python 面向对象](#)
`Python从设计之初就已经是一门面向对象的语言, Class是用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法，对象是类的实例。`

-----

- [ ] [`1. 面向对象技术`](#1-面向对象技术)
- [ ] [`2. 类的成员`](#2-类的成员)
- [ ] [`3.继承`](#3-继承)
- [ ] [`4. 魔法方法`](#4-魔法方法)
- [ ] [`5. 抽象类`](#5-抽象类)
- [ ] [`6. 对象创建过程`](#6-对象创建过程)
- [ ] [`7. 深拷贝和浅拷贝`](#7-深拷贝和浅拷贝)

-----

### [1. 面向对象技术](#)
常见的编程范式有如下几种，**结构化编程**  **面向对象编程**  **函数式编程** 面向对象的设计方法是对结构化编程的优化、升级，而不是完全取代! 
类把数据与功能绑定在一起。创建新类就是创建新的对象 类型，从而创建该类型的新 实例 。类实例支持维持自身状态的属性，还支持（由类定义的）修改自身状态的方法。

* **结构化编程** `: 自顶向下，逐步细化；清晰第一，效率第二；书写规范，缩进格式；基本结构，组合而成。`
* **面向对象编程** :`特点` ：`封装性、`  `继承性、` `多态性、` `抽象` `核心概念是类和对象`
* **函数式编程**: `把函数作为参数传递给另一个函数，也就是所谓的高阶函数， 函数可以返回一个函数！ 函数式编程没有副作用`

**Python 定义类的语法** **实例化一个类**

```python
class ClassName:
    "类的说明注释"
    pass #类的成员

#实例化一个类
obj = ClassName(""" 参数 """)
```

**Python的面向对象既有 C++ 的多继承，还具有和C++一样的没有接口的特点。同时又兼顾JavaScript的特性，比如静态属性可以通过类去访问！对象里面有一个类指针，类似于 JS里面的\_\_proto\_\_ 指向类的公共部分(类属性-静态方法，类方法)！**

#### [1.1 Python 面向对象技术概念](#)

`Python`中的类提供了面向对象编程的所有基本功能：类的继承机制允许多个基类，派生类可以覆盖基类中的任何方法，方法中可以调用基类中的同名方法。
**Python 虽然有多继承，但是千万别用！**  **python没有接口**，但是在python中由抽象类和抽象方法去实现接口功能，接口是不能被实例化的，只能被别的类继承去实现相应的功能。

* `类(Class)`:` 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。`
* `方法`：`类中定义的函数。`
* `类变量`：`类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。`
* `数据成员`：`类变量或者实例变量用于处理类及其实例对象的相关的数据。`
* `方法重写`：`如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。`
* `局部变量`：`定义在方法中的变量，只作用于当前实例的类。`
* `实例变量`：`在类的声明中，属性是用变量来表示的，这种变量就称为实例变量，实例变量就是一个用 self 修饰的变量。`
* `继承`：`即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。`
* `实例化`：`创建一个类的实例，类的具体对象。`
* `对象`：`通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。`


#### [1.2 OOP的四大特点](#)
需要常记的是 抽象和多态，要区分多态和重载！ 四大特点是 `封装` `继承` `抽象` `多态` 

**封装 -- 将数据和对数据操作进行整合** `就是将要访问的数据保护起来，不让外界直接访问类的属性和字段，而是对外提供有限的访问接口，授权外部仅能通过类提供的接口进行访问！`  
**继承 -- 实现代码的复用** `继承在编程语言里最直接的体现就是父子类的关系，继承最大的好处就是能够实现代码的复用！`  
**抽象 -- 抽象更多的是能够让程序的设计和实现分离。** `抽象主要指的是隐藏方法的具体实现，让方法的调用者无需关心方法的具体实现，只需要关心类提供了哪些功能即可!` `例如 Java的接口和抽象类`  
**多态 -- 多态指的是子类可以替换父类!** `对同一个完全相同的消息，所表现出来的动作是各不相同的！`  
**重载** `函数名相同，但是函数的参数不同，调用时根据参数的不同决定调用哪一个函数。`


#### [1.3 创建类](#)
使用 `class` 语句来创建一个新类，`class` 之后为类的名称并以冒号结尾 `:` 

**创建一个用户类**
```python
class User:
    '类的帮助信息'   #类文档字符串
    #public
    name:string = '';
    age: int = 0;
    #private 被保护起来的数据
    __id = 0
    
    #外部接口
    def getID(self):
        return  self.__id;
    
    def __init__(self, userName, userAge, id) -> None:
        self.name = userName
        self.age = userAge
        self.__id = id
    def toString(self) -> string:
        return f"UID:{self.__id} Name: {self.name} Age:{self.age}";
#end class User

me = User("jxkicker",24, 2016110418)

print(me.getID())
```

**创建一个电子游戏类**
```python
import datetime as dt
import string

class computerGame:
    """
    表示一款 电子游戏
    """
    #private 静态属性
    __names: dict
    __type: string
    __price: float
    #public 静态属性
    publisher: string
    createDateTime: dt.datetime
    country: string
    cumulativeSales = "3.85 亿"
    #构造函数
    def __init__(self, * ,names:dict, type: string, price: float):
        self.__names = names
        self.__type = type
        self.__price = price
        self.country = list(names.values())[0]

    def setPublisher(self, prName, create):
        self.publisher = prName
        self.createDateTime = create

    def getName(self):
        return self.__names[self.country]

    def setCountry(self, country):
        self.country = country
    def __repr__(self):
        return f"""
        游戏名称: {self.getName()}\n
        游戏类型:{self.__type}\n
        游戏价格:{self.__price}\n
        发行商:{self.publisher}\n
        发行日期:{self.createDateTime}\n
        累计销量:{self.cumulativeSales}
        """

dnames = {
    "eng":"Grand Theft Auto V",
    "zh":"侠盗飞车罪恶都市"
}

# 实例化类 调用构造函数
GTA5 = computerGame(names=dnames, type="开放式动作冒险游戏", price=69.99)
GTA5.setCountry("eng")
GTA5.setPublisher("Rockstar Games", dt.datetime(2016,5,15))

print(GTA5)
"""
游戏名称: Grand Theft Auto V
游戏类型:开放式动作冒险游戏
游戏价格:69.99
发行商:Rockstar Games
发行日期:2016-05-15 00:00:00
累计销量:3.85 亿
"""
```

### [2. 类的成员](#) 
Python 支持的类成员有构造函数，私有属性，公开属性，私有方法，公开方法，运算符重载！ **Python类的对象使用 点 . 调用或访问自身的成员**



**Python 有三种不同的方法！ 他们的区别如下：**

1. **类方法：不能获取构造函数定义的变量，可以获取类的属性，通过装饰器@calssmethod进行修饰。** 
2. **静态方法：不能获取构造函数定义的变量，也不可以获取类的属性，通过装饰器@staticmethod进行修饰。**
3. **实例方法：既可以获取构造函数定义的变量，也可以获取类的属性值。**



#### [2.1 构造函数](#)
**Python** 有一个名为 `__init__()` 的特殊方法（构造方法），该方法在类实例化时会自动调用! 也就是`C#，C++, JAVA` 里面常说的构造函数！
函数的第一个参数必然为 **self** **代表的是类的实例，代表当前对象的地址，而** `self.__class__` **则指向类。**
在类的内部，使用 **def** 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 **self**, 且为第一个参数，**self** 代表的是类的实例

> `Python 会自动绑定类方法的第一个参数指向调用该方法的对象。如此，Python解释器就能知道到底要操作哪个对象的方法了。因此，程序在调用实例方法和构造方法时，不需要手动为第一个参数传值`

**构造函数语法:**
```python
def __init__(self,""" 参数列表 """):
    #代码块
    pass
```

```python
import datetime as dt
import string

class Kitty:
    type: string  #类属性 Java 静态成员
    name: string  #类属性 Java 静态成员
    age: int      #类属性 Java 静态成员
    def __init__(self,name, type, age, /) -> None:
        print("调用构造函数")  #调用构造函数
        print(self.__class__) #<class '__main__.Kitty'>
        self.name = name  #对象属性
        self.type = type  #对象属性
        self.age = age	  #对象属性

remix = Kitty("remix","银渐层", 1)
print(remix.name) #remix
```

#### [2.2 属性](#)
属性可以在类的内部添加，还可以支持JavaScript类似的语法，即在内外添加。属性还支持私有属性！ **总的来说有两种属性**

1、内置类属性：Python类中存在各种内置属性。例如_dict_、_doc_、_name _ 等。
2、用户定义的属性：属性是在类定义中创建的。可以为类的现有实例动态创建新属性。属性也可以绑定到类名。

**按照属性所在可以分为：对象属性 和 静态属性(类属性)**

1、对象属性： 通过 **\_\_init\_**\_ 方法定义在 self 上面的属性。或者给对象添加额外的属性！

2、静态属性(类属性):  定义在内中，使用类名进行访问


##### [2.2.1 常见内置属性](#)
`当python创建一个类之后，系统就自带了一些属性，叫内置类属性。这些属性名用双下划线包括并与普通属性名区分。` **注意：有的属性是只有类有，有的属性是类和对象都有！**

**以此类为例：**

```python
class Person:
    """A class name Person"""
    def __init__(self, name, age):
        self.name = name  #对象属性
        self.age = age	  #静态属性
 
p1 = Person('Aaron', 20)
```

|`属性`|`含义`|
|:----|:----|
|`__name__`|`当前定义的【类】的名字  ` **只有类有，属于静态属性**  |
|`__module__`|`【类或对象】所属的模块名` **类和对象都有**  |
|`__dict__`|`【类或对象】的属性（包含一个字典，由类的数据属性组成）` **类和对象都有** |
|`__doc__`|`【类或对象】的文档字符串 - 一般写在class 类下面`  **类和对象都有** |
|`__base__`|`当前【类】的父类`  **只有类有，属于静态属性** |
|`__bases__`|`当前【类】所有父类构成的元组`  **只有类有，属于静态属性** |
|`__class__`|**对象属性** `返回当前对象所属类型`   `<class '__main__.Mammal'>` |

```python
print(Person.__name__)  # 输出：Person

print(Person.__module__) # 输出：__main__
print(p1.__module__) # 输出：__main__

print(Person.__dict__) 
# 输出
"""
{
    '__module__': '__main__', 
    '__doc__': 'A class name Person', 
    '__init__': <function Person.__init__ at 0x7f46262ff700>, 
    '__dict__': <attribute '__dict__' of 'Person' objects>, 
    '__weakref__': <attribute '__weakref__' of 'Person' objects>
}
""" 
print(p1.__dict__) 
# 输出
"""
{
    'name': 'Aaron', 
    'age': 20
}
"""
print(Person.__base__) # 输出：<class 'object'>
print(Person.__bases__) # 输出：(<class 'object'>,)
```

##### [2.2.2 动态绑定属性](#)
`可以直接给对象添加额外的属性` **当然属性只属于被绑定的对象！**

```python
class Phone:
    #用于 print的方法
    def __str__(self) -> str:
        return str(self.__dict__) 
        
xiaomi = Phone()
xiaomi.name = "xiaomi 12 pro 天玑版"
xiaomi.price = "3199"
xiaomi.memory = 12
xiaomi.hardDish = 256

print(xiaomi)
#{'name': 'xiaomi 12 pro 天玑版', 'price': '3199', 'memory': 12, 'hardDish': 256}
```

##### [2.2.3 私有属性](#)
`__private_attrs`：两个下划线开头，声明该属性为私有，不能在类的外部被使用或直接访问。在类内部的方法中使用时 `self.__private_attrs`。

```python
class Phone:
    def __init__(self,* , name, price, memory, hardDisk) -> None:
        self.__name = name
        self.__price = price
        self.__memory = memory
        self.__hardDisk = hardDisk
    #用于 print的方法
    def __str__(self) -> str:
        return str(self.__dict__) 

    def getName(self):
        return self.__name
        
xiaomi = Phone(name="xiaomi 12 pro 天玑版", price=3199.00,  memory=12, hardDisk=256)

print(xiaomi.getName()) #xiaomi 12 pro 天玑版
print(xiaomi)
```



#### [2.3 类属性/静态属性](#)

只需要将属性定义在类中即可，**使用类名称访问！ 当然也可以使用对象访问到类属性！** **类似于 C# Java的静态！**

```python
class User:
    '表示一个用户类'   #类文档字符串
    userCount: int = 0  #静态属性
    userDataBaseName = "testDB" #静态属性
    #外部接口
    def getID(self):
        return  self.__id;
    
    def __init__(self, userName, userAge, uid, upwd) -> None:
        self.name = userName  #对象属性
        self.age = userAge
        self.uid = uid
        self.__password = upwd 
        User.userCount += 1

    def toString(self) -> str:
        return f"UID:{self.__id} Name: {self.name} Age:{self.age}";

lzm = User("lizhiming", 18, "2016110418", "123456")
jx = User("jiangxing", 18, "2016110417", "123457")

print(User.userDataBaseName) #testDb
print(User.userCount) #2
print(jx.userCount) #2 也可以通过对象访问
```



#### [2.4 属性封装](#)

使用 **@property** 可以实现 `C#` 的属性封装效果!

在绑定属性时，我们直接把属性暴露出去，没办法检查参数，导致可以把属性会被随便更改。我们可以使用setter和getter方法，在setter方法里面限制参数。**这种方法，使用起来不太舒服！ 我们可以使用装饰器！**

```python
class Student(object):
    def get_score(self):
        return self._score

    def set_score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0~100!')
        self._score = value


s = Student()
s.set_score(100)
print("score:", s.get_score())
```

**使用 @property 可以实现封装属性效果：**

```python
import types

class User:
    def __init__(self, name: str, age: int, score: int):
        self.name = name
        self.age = age
        self.__score = score

    @property
    def score(self):
        return self.__score

    @score.setter
    def score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0~100!')
        self.__score = value

umix = User(name='remix', age=28, score=80)

print(umix.score) #80
umix.score = 75
print(umix.score) #75
```



#### [2.5 实例方法](#)

在类的内部，使用 **def** 关键字来定义一个方法，与一般函数定义不同，类方法必须包含参数 **self**, 且为第一个参数，**self 代表的是类的实例**。
`__private_method`：两个下划线开头，声明该方法为私有方法，只能在类的内部调用 ，不能在类的外部调用。`self.__private_methods`。

```python
class Site:
    def __init__(self, name, url):
        self.name = name       # public
        self.__url = url   # private
 
    def who(self):
        print('name  : ', self.name)
        print('url : ', self.__url)
    
     # 私有方法
    def __foo(self):         
        print('这是私有方法')

    # 公共方法
    def foo(self):            
        print('这是公共方法')
        self.__foo()
```



#### [2.5.1 动态绑定实例方法](#)

**动态绑定方法，需要借助 types.MethodType()**   实际上**python**所有类都是**type**类的实例对象，动态添加了 **Person**的实例方法！

```python
import types

class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age


me = User("remix",24)
def toString(self) -> str:
    return f"{{ Name: {self.name}, Age: {self.age} }}"

me.toString = types.MethodType(toString, me)

print(me.toString())
```



#### [2.6 类方法](#)

**类方法：不能获取构造函数定义的变量，可以获取类的属性，通过装饰器@calssmethod进行修饰。** 

**有一个参数 cls 表示当前类,可以通过 cls 访问类属性！ **

```PYTHON
class TestDB:
    count: int = 0

    @classmethod
    def addCount(cls, val: int):
        cls.count += val

TestDB.addCount(20);

print(TestDB.count)  #20
```



##### [2.6.1 动态绑定类方法](#)

`需要MethodType 绑定！`

```python
import types

class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

User.count = 0

@classmethod
def AddCount(cls, value):
    cls.count += value
    return cls.count

User.Increse = types.MethodType(AddCount, User)

print(User.Increse(30))  #30
print(User.Increse(40))  #70
```



#### [2.7 静态方法](#)

**静态方法：不能获取构造函数定义的变量，也不可以获取类的属性，通过装饰器@staticmethod进行修饰。**

**没有参数，无法直接访问类属性**

```PYTHON
class TestDB:
    count: int = 0

    @classmethod
    def addCount(cls, val: int):
        cls.count += val

    @staticmethod
    def CNM(a, b):
        return a + b

TestDB.addCount(20);

print(TestDB.count)  #20
print(TestDB.CNM(20, 30))
```



##### 2.7.1 动态添加静态方法

`动态添加静态方法需要一些处理！` `它不需要，MethodType 辅助 `

```python
import types

class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

User.count = 0

@staticmethod
def AddCount(value):
    return value

User.Increse = AddCount

print(User.Increse(30))  #30
print(User.Increse(40))  #40

```



####  [2.8 通过类名调用实例方法](#)

利用 **self** 参数我们可以通过类名访问属性方法：

```python
import types

class User:
    def __init__(self, name: str, age: int, score: int):
        self.name = name
        self.age = age
        self.__score = score

    def eat(self, food):
        print("the %s has been eaten by %s" % (food,self.name))

umix = User(name='remix', age=28, score=80)

User.eat(umix, "Apple")  #访问实例方法
```



#### [2.9 类对象](#)

在Python 中，类具有一些类属性，还有类方法，静态方法，这些不定义在对象上面，而定义在类上面的公共部分存在哪里？Python对每一个类都创建了一个 **类对象**！ 存放这些公共属性！ 而这个类的实例内置一个属性，指向这个类对象，获得公共部分的属性或者执行调用！





### [3. 继承](#) 

Python 同样支持类的继承，如果一种语言不支持继承，类就没有什么意义。继承允许我们定义继承另一个类的所有方法和属性的类。

**父类**是继承的类，也称为基类。 **Python 有一个终极父类 Object类，默认所有的类都继承至Object类**

**子类**是从另一个类继承的类，也称为派生类。

**Python 支持多继承，也就是说 会有 继承菱形问题**

继承语法如下所示:

```python
class ClassName(FatherClass1,FatherClass2,FatherClass3...):
    pass
```

在继承中基类的构造方法（\_\_init\_\_()方法）不会被自动调用，它需要在其派生类的构造方法中亲自专门调用。

#### [3.1 super() 函数](#)

Python 还有一个 **super()** 函数，它会使子类从其父继承所有方法和属性。**super()**方法的存在就是为了解决多重继承的问题，在一个父类中使用**super()**方法用于调用下一个父类的方法。super()的2种表达：

* super().方法(参数列表)

* super(子类名，self).方法(参数列表)



```python
import types

#python3 所有类都可以继承于 object 基类
class Animal(object): 
    def __init__(self, name:str,age:int) -> None:
        self.name = name
        self.age = age

    def eat(self) -> None:
        print("eat food")

    
class Cat(Animal):
    def __init__(self, name: str, age: int, sex) -> None:
        super().__init__(name, age)  
        #super(Cat, self).__init__(name, age)  也可以这样写
        self.sex = sex
    
    #复写父类方法
    def eat(self) -> None:
        super().eat()
        print("the food is mouse!")

A= Animal("lizhiming", 24)
C = Cat("Remi", 2, False);

print('"A" IS Animal?', isinstance(A, Animal)) #True
print('"A" IS Cat?', isinstance(A, Cat)) #False
print('"C" IS Animal?', isinstance(C, Animal)) #True
print('"C" IS Cat?', isinstance(C, Cat)) #True

A.eat()
C.eat()
"""
eat food
eat food
the food is mouse!
"""
```



#### [3.2 继承语法](#)

学生类继承自用户类，并且重写父类的方法！ 重写父类的方法很简单，只需要在子类中写一个和父类方法同名的方法就ok了！

```python
import types

#父类
class User:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def eat(self, food):
        print("the %s has been eaten by %s" % (food,self.name))

#子类
class Student(User):
    def __init__(self, name: str, age: int, score: float):
        super().__init__(name, age)
        self. __score = score
    
    def eat(self, food):
        print("the %s has been eaten by the student %s" % (food,self.name))

    @property
    def score(self):
        return self.__score

    @score.setter
    def score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0~100!')
        self.__score = value



umix = Student("remix", 19, 98.5)

umix.eat("pineapple")
#the pineapple has been eaten by the student remix
```



#### [3.3 子类中调用父类的方法](#)

`需要用到 super函数`

```python
class Cat(Animal):
    def __init__(self, name: str, age: int, sex) -> None:
        super(Cat, self).__init__(name, age)
        self.sex = sex
    
    def eat(self) -> None:
        super().eat(self)  #调用父类方法
        print("the food is mouse!")
```



#### [3.4 多继承](#)

**我们来实现一个多继承！ 一个菱形继承就出来！**  **我的建议是，千万别用多继承！**

```python
#父类  哺乳动物
class Mammal(Object):
	pass

#子类 牛
class Cattle(Mammal): 
    pass
#子类 人类
class Human(Mammal):
    pass
    
#孙子 牛头人
class NiuTouRen(Cattle,Human):
```

在python中是可以**多继承**的，继承的先后顺序是有区别的，当我们调用方法的时候，如果第一个继承的找不到，才会去第二个中找，但是只要在第一个类中找到调用的那个方法，即使参数个数不匹配也不会调用第二个父类中的，此时会报错。

**如果一个类继承多个父类的时候，优先继承的是第一个类的属性和方法，也即若想优先继承哪个类，就把哪个类放在最前面即可。**



#### [3.5 多继承的构造函数参数问题](#)

由于`Cattle`类和`Human` 第三个参数的类型不一样，导致了多继承无法实现！ **要完成多继承，参数最好使用字典传参**

```python
import types


class Mammal:
    __type:str = "mammal"  #哺乳动物
 
    def __init__(self, name:str,age:int) -> None:
        self.name = name
        self.age = age
    
    def eat(food) -> None:
        print("eat food: {0}" % food)

class Cattle(Mammal): 
    __type:str = "牛头人"
    def __init__(self, * ,name:str,age:int, color: str) -> None:
        super(Cattle, self).__init__(name, age)       
        self.color = color

    def call():
        print("哞哞哞哞")

class Human(Mammal):
    __type:str = "智人"

    def __init__(self, * ,name:str, age:int, sex: bool, wisdom: int) -> None:
        super(Human, self).__init__(name, age)       
        self.sex = sex
        self.wisdom  = wisdom

    def __str__(self) -> str:
        sexName: str = "男"
        match(self.sex):
            case True:
                sexName = "男"
            case _:
                sexName = "女"
        return f"我是{self.__type}, 我的名字是{self.name}，年龄为{self.age}岁！我的性别是{sexName}"

    
class NiuTouRen(Cattle, Human):
    __type:str = "牛头人"
    
    def __init__(self, name: str, age: int, color: str, sex: bool, wisdom: int) -> None:
        super().__init__(name, age, color, sex, wisdom)

ntr = NiuTouRen("米勒加斯", 56, "黄色", True, 250)
```

**多继承需要关注，构造函数问题，你无法分别给不同的父类构造函数传递不同的参数，你只能通过super() 调用父类构造函数！但是你只能调用一次。并且参数会用于每一个父类的构造函数！**



#### [3.6 多继承方法调用问题](#)

NTR一般的设计！



#### [3.7 最好别用多继承](#)

**多继承是反人类的，千万别用！**



### [4. 魔法方法](#) 

**魔法方法(magic methods)**：`python`中的魔法方法是指方法名以 `两个下划线开头并以两个下划线结尾的方法`，因此也叫`Dunder Methods (Double Underscores)`。**常用于运算符重载**。魔法方法会在对类的某个操作时后端自动调用，而不需要自己直接调用。魔法方法也用在继承、类型转换、内置方法调用、迭代器、线程协程、继承、拷贝、属性、描述符...！



#### [4.1 字符串转换](#)

用于将类转换为格式化或者非格式化的字符串！

| `方法`        | `返回值` | `参数个数`           | `说明`                                                   |
| :------------ | :------- | :------------------- | :------------------------------------------------------- |
| ` __str__`    | `str`    | ` (self)`            | ` print(obj)` `用于打印输出`                             |
| ` __repr__`   | ` str`   | ` (self)`            | `用于交互式命令 直接输出！`                              |
| ` __format__` | ` str`   | `(self, formatstr) ` | ` 被内置方法string.fromat()调用, 返回一个新格式的字符串` |
| `__unicode__` | `str`    | `(self)`             | `被内置方法unicode()调用, 返回一个unicode的字符串`       |
| `__hash__`    |          | `(self)`             | `被内置方法hash()调用, 返回一个整型数`                   |

`以下载命令行中实现`

```shell
>>> class Phone:
...     def __str__(self) -> str:
...         return "This is a Phone"
...     def __repr__(self) -> str:
...         return "Show Phone"
... 
>>> myPhone = Phone()
>>> print(myPhone)
This is a Phone
>>> myPhone
Show Phone
>>> 
```



##### [4.1.1  \_\_hash\_\_](#)

`__hash__`  `函数对类的实例做了哈希，使每个对象都有一个唯一值对应!`  `在Python中自定义的对象默认是可 hash 的`，**并且默认hash 值是通过id 获得，这个id 指的是存储的地址**，`但从地址得到的hash 值一般不符合我们的要求，我们更希望是通过对具体数据进行hash ，然后得到hash 值。`

`以下是一个实体类：`

```python
class Phone:
    def __init__(self, brand: str, name: str,price):
        self.brand = brand
        self.name = name
        self.price = price
    
    def __eq__(self, other):
        if isinstance(other, Phone):
            return hash(self) == hash(other)
        return False

    def __hash__(self):
        return hash((self.brand, self.name, self.price))


xiaomi = Phone("xiaomi", "小米 12 Pro 天玑版", 3499)
xp = Phone("xiaomi", "小米 12 Pro 天玑版", 3499)

if xp == xiaomi:
    print("一样内容！")  #一样内容！
    
xhash = hash(xiaomi)
print(xhash)  #-3233097180176029452  每次运行值都不一样
```

`代码里不仅实现了` **\_\_hash\_\_**`，还实现了`  **_\_eq\_\_**。先暂且记住两个是需要同时实现的。`

#### [4.2 一元运算符重载](#)

也就是参数个数0，运算符重载而已！

| `方法`    | `返回值`   | `参数个数` | `说明`                                      |
| :-------- | ---------- | ---------- | ------------------------------------------- |
| `__pos__` | `用户定义` | `(self)`   | `会被取正操作符调用,例如 +a`                |
| `__neg__` | `用户定义` | `(self)`   | `会被取反操作符调用,例如 -a`                |
| `__abs__` | `用户定义` | `(self)`   | `在调用内置函数abs()的时候被调用, 取绝对值` |



**取反操作**

```python
class valArray:
    def __init__(self, *vals) -> None:
        for v in vals:
            if not isinstance(v, int) and not isinstance(v, float):
                raise TypeError("传递的参数必须是 int 或者 float")
        self.__values = list(vals)
    
    def __neg__(self):
        values = []
        for t in self.__values:
            values.append(0 - t)
        return valArray(*values)

    def __str__(self) -> str:
        return str(self.__values)

scores = valArray(56, -78, 45,-95.5, 69, 52, 78, 94, -75)

print(-scores)
```



#### [4.3 二元运算符重载](#)

也就是参数个数1，运算符重载而已！

| `方法`    | `返回值`   | `参数个数`      | `说明`                                  |
| :-------- | ---------- | --------------- | --------------------------------------- |
| `__add__` | `用户定义` | `(self, other)` | `当使用+执行加法运算的时候被调用 a + b` |
| `__mul__` | `用户定义` | `(self, other)` | `当使用*执行乘法运算的时候被调用 a * b` |
| `__sub__` | `用户定义` | `(self, other)` | `当使用-执行减法运算的时候被调用 a - b` |
| `__div__` | `用户定义` | `(self, other)` | `当使用-执行减法运算的时候被调用 a / b` |
| `__eq__`  | `布尔值`   | `(self, other)` | `当使用==运算符进行比较时被调用`        |
| `__mod__` | `用户定义` | `(self, other)` | `当使用%执行取余运算的时候被调用`       |

`加法 a + b 为例：`

```python
class Vector:
   def __init__(self, a, b):
      self.a = a
      self.b = b
 
   def __str__(self):
      return 'Vector (%d, %d)' % (self.a, self.b)
   
   def __add__(self,other):
      return Vector(self.a + other.a, self.b + other.b)
 
v1 = Vector(2,10)
v2 = Vector(5,-2)

print (v1 + v2)  #Vector(7,8)
```



#### [4.4 拷贝](#)

浅拷贝和硬拷贝

| `方法`         | `返回值`   | `参数个数`         | `说明`                                                       |
| -------------- | ---------- | ------------------ | ------------------------------------------------------------ |
| `__copy__`     | `用户定义` | `(self)`           | `被copy.copy()调用,返回一个对象的浅拷贝, 一个新实例包含的数据是引用` |
| `__deepcopy__` | `用户定义` | `(self, memodict)` | `被copy.deepcopy()调用, 返回一个对象的深拷贝, 对象数据全部拷贝一份` |







#### [4.5 重点方法](#)

浅拷贝和硬拷贝

| `方法`     | `返回值`   | `参数个数`             | `说明`                                                       |
| ---------- | ---------- | ---------------------- | ------------------------------------------------------------ |
| `__new__`  | `用户定义` | (cls, *args, **kwargs) | `在实例化一个对象的时候被调用` `__new__至少有一个参数cls,代表当前类`, `必须要有返回值,返回创建的对象` |
| `__init__` | `用户定义` | `(self, 构造函数参数)` | `构造函数` `用于初始化对象，被__new__方法调用`, `__init__必须有一个参数 self` |
| `__del__`  | `无`       | `(self)`               | `对象的析构方法`                                             |



```python
class Mammal(object):
    __type:str = "mammal"  #哺乳动物
    #初始化操作
    def __init__(self, name:str,age:int) -> None:
        print("call __init__")
        self.name = name
        self.age = age
	#创建对象
    def __new__(cls, *args, **kwargs) -> object:
        print("call __new__")
        print(args) #('Human', 25000)
        print(kwargs) #{}
        return super(Mammal, cls).__new__(cls) 
        #这个返回值 作为 self 参数 传递给 __init__  

    def printDict(self):
        print(self.__dict__)

    def __del__(self):
        print("delete over")

human = Mammal("Human", 25000)
human.printDict()
# call __new__
# call __init__
# {'name': 'Human', 'age': 25000}
print(human.__class__)
# <class '__main__.Mammal'>
# delete over
```





### [5. 抽象类](#) 

**用抽象类代替接口，是python多继承存在的唯一理由！** 在python中根本就没有一个叫做interface的关键字，如果非要去模仿接口的概念   **Python 里面有一个 模块，专门用来设计模块类！**  

**抽象类是一个特殊的类，它的特殊之处在于只能被继承，不能被实例化**



`python也有抽象类的概念但是同样需要借助模块实现`

```python
from abc import ABCMeta
from abc import abstractmethod

#吃方法的一个抽象类
class IEat(metaclass=ABCMeta):
	#修饰后就是抽象方法
    @abstractmethod
    def eat(self, food) -> None:
        pass
```



#### [5.1  实现抽象类](#)

`实现抽象类 eat方法`

```python
class Mammal(IEat):
    __type:str = "mammal"  #哺乳动物
    
    def __init__(self, name:str,age:int) -> None:
        self.name = name
        self.age = age

    def eat(self, food):
        print(f"we eat {food}")
```



#### [5.2 孙子类重写抽象方法](#)

`懂得都懂！`

```python
class Human(Mammal):
    __type:str = "智人"

    def __init__(self, name:str, age:int, sex: bool, wisdom: int) -> None:
        super().__init__(name, age)       
        self.sex = sex
        self.wisdom  = wisdom

    def __str__(self) -> str:
        sexName: str = "男"
        match(self.sex):
            case True:
                sexName = "男"
            case _:
                sexName = "女"
        return f"我是{self.__type}, 我的名字是{self.name}，年龄为{self.age}岁！我的性别是{sexName}。"

    def eat(self, food):
        print("we are human, we eat {0}".format(food) )


me = Human("jx", 25, True, 125)
me.eat("apple")
#we are human, we eat apple
print(me)
#我是智人, 我的名字是jx，年龄为25岁！我的性别是男。
```



### [6. 对象创建过程](#)

如下所示！`__new__` 在前，先创建对象，`__init__` 在后，初始化对象

```python
#以此为例
me = Human("jx", 25, True, 125)
#先调用 Human 的 obj = __new__(Human, 25, True, 125)
#将返回值 obj 传递给 __init__(obj, , 25, True, 125)
#等到 __init__ 运行完毕以后 
#再将 obj 传递给 me
```



####  [6.1 继承视角下对象的创建过程](#)

`遵循 先从祖先 new --> 当前new 方法 调用完，在从祖先 init ---> 当前类 init方法 调用完！`

```python
class A:
    __classname__ : str = "object -> A"

    def __new__(cls: type[object],*args, **kwargs) -> object:
        obj = super(A, cls).__new__(cls)
        print("call the A __new__") 
        return obj

    def __init__(self, name) -> None:
        print("call the A __init__")
        self.name = name

class B(A):
    __classname__ : str = "object -> A -> B"

    def __new__(cls: type[object], *args, **kwargs) -> object:
        obj = super(B, cls).__new__(cls)
        print("call the B __new__") 
        return obj

    def __init__(self, name, age) -> None:
        super(B, self).__init__(name)
        print("call the B __init__") 
        self.age = age

son = B("remix", 25)
print(son.__classname__)

"""
call the A __new__
call the B __new__
call the A __init__
call the B __init__
object -> A -> B
"""
```



### [7.  浅拷贝和深拷贝](#)

如果理解C++，就很好懂他们的区别！浅拷贝，可以理解为，就复制了引用！深拷贝就不一样了，是重新按照原来的对象，构造了一个新的对象，将这个新的对象的引入返回。对于简单的 object，用 浅拷贝和深拷贝没什么区别！

在python 中：

- **直接赋值：**其实就是对象的引用（别名）。
- **浅拷贝(copy)：**拷贝父对象，不会拷贝对象的内部的子对象。
- **深拷贝(deepcopy)：** copy 模块的 deepcopy 方法，完全拷贝了父对象及其子对象。



**内置对象： dict 字典类型实现的就是深拷贝！**

```python
grades = {
    "liming": 89.56,
    "jiakun": 98.5,
    "jx": 95.2,
    "huyu":96.3
}

#浅拷贝
cpyGds = grades.copy()
cpyGds["jx"] = 96

print(grades["jx"])  #95.2
print(id(cpyGds), id(grades))
#2061455656512 2061455656256
```

**浅拷贝的问题在于，对于内部对象不进行深拷贝, 导致内部引用原来的对象**

```python
grades = {
    "liming": [89.56, 85.5],
    "jiakun": [98.5, 98.3],
    "jx": [95.2, 89.2],
    "huyu":[96.3, 98.5]
}

#浅拷贝的问题
cpyGds = grades.copy()
cpyGds["jx"][1] = 99 

print(grades["jx"])  #[95.2, 99]
print(id(cpyGds), id(grades))
#1705554150976 1705554150720
```



`Python`提供了名为`copy`的模块，其中包含`copy()`和`deepcopy()`函数。

第一个函数`copy.copy()` ，可以用来复制列表或字典这样的可变值，而不是只复制引用。

两者的区别是`copy.copy()`是这复制了列表或字典的值，但是引用还是同一个。而`copy.deepcopy()`是产生一个新的引用使新的变量和被复制变量引用不同。

```python
import copy
grades = {
    "liming": [89.56, 85.5],
    "jiakun": [98.5, 98.3],
    "jx": [95.2, 89.2],
    "huyu":[96.3, 98.5]
}

#深拷贝
dpcpy_grades = copy.deepcopy(grades)

dpcpy_grades["jx"][1] = 100

print(grades["jx"])
#[95.2, 89.2]
```



#### [7.1 类拷贝](#)

浅拷贝和硬拷贝, 每个对象有两个魔法方法， 用于进行深拷贝和浅拷贝, 如果你定义，那么 `copy()`和`deepcopy()`函数就会调用如下函数进行拷贝！而不是运用系统默认提供的拷贝函数！

| `方法`         | `返回值`   | `参数个数`         | `说明`                                                       |
| -------------- | ---------- | ------------------ | ------------------------------------------------------------ |
| `__copy__`     | `用户定义` | `(self)`           | `被copy.copy()调用,返回一个对象的浅拷贝, 一个新实例包含的数据是引用` |
| `__deepcopy__` | `用户定义` | `(self, memodict)` | `被copy.deepcopy()调用, 返回一个对象的深拷贝, 对象数据全部拷贝一份` |



```python
import copy

class A:
    "一个新的类"
    def __str__(self) -> str:
        return f"Name:{self.name},Scores:{self.scores}"

    def __init__(self, name, scores: list) -> None:
        self.name = name
        self.scores = scores

    def __deepcopy__(self, memodict):
        print("call deep copy func")
        return A(self.name, self.scores)


a = A("remix", [78,98,75,85])
a2 = copy.deepcopy(a)
print(a)
```







-----
`时间`: `[]` 