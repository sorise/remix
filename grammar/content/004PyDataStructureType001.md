### [Python 复合数据类型](#)
**介绍:**  Python 内置了List, Tuple, 字典，时间等复合数据类型。

-----
- [x] [1. List 列表](#1-list-列表)
- [x] [2. Tuple 元祖](#2-tuple-元祖)
- [x] [3. Set 集合](#3-set-集合)
- [x] [4. Dictionary 字典](#4-dictionary-字典)
- [x] [5. Str 字符串](#5-str-字符串)
- [x] [6. 类型转换](#6-类型转换)


-----

### [1. List 列表](#)
可将不同值组合在一起。最常用的列表，是用方括号标注，逗号分隔的一组值。 **列表可以包含不同类型的元素** ，但一般情况下，各个元素的类型相同。
**Python不内置数组**,使用列表嵌套列表的方式表示d多维数组！ **推荐**列表里面存放相同类型元素，**不同类型元素需要组合请使用元祖**

* 序列都可以进行的操作包括索引，切片，加，乘，检查成员。
* Python已经内置确定序列的长度以及确定最大和最小的元素的方法
* 与字符串的索引一样，列表索引从0开始。列表可以进行截取、组合等。

创建列表的方式非常简单：
```python
# -*- coding: UTF-8 -*-
mixList = ['Google', 'Runoob', 1997, 2000]
numbers = [65, 78, 97, 45 ,95 ,75 ,56, 12]
name = ["remix", "yoki", "time", "tom", "jake"]
matrix = [
    [4,5,6,10],
    [7,8,9,15],
    [1,2,3,19]
]

print(matrix[1][1]) #8
```
**索引访问：**
应该是非常基础的了！支持一维，二维坐标访问
```python
print("first name: {0}".format(name[0])); #remix
print(matrix[1][1]) #8
```
**类型转换**
**list(s)**：将序列 s 转换为一个列表

遍历整个列表
```python
cars = ['lanbo','benchi', 'fentian','changan']

for branch in cars:
    print('brach:',branch.title())
else:
    print("we have listed all branchs.".title())
```

#### [1.1 从列表取值](#)
这又分两种情况，列表中的元素是可变类型还是不可变类型！ 取值使用的是直接深拷贝还是浅拷贝！

```python
variable = list[idx];
```

**结论:** **对于不可变类型，每次获取值都是执行的深拷贝，创建一个新值。** 
**对于可变类型，每次获得的都是对一个对象的引用，执行的是引用的拷贝，也就是浅拷贝！并没有创建一个新的对象！**

##### [1.1.1 元素类型是不可变成员](#)
**从列表取值 - 成员是指类型**  如果列表成员类型是一个不可变(值类型)， 那么会实现一次拷贝，新创建一个值

先取值，在改取得的值， 列表元素不改变
```python
#列表取值
name = ["remix", "yoki", "time", "tom", "jake"]

me = name[2]
print(me)  #time
me = "yado"
print(me, name[2]) #yado time
#修改从列表取得的值，列表里面的值并没有改变！
```

先取值，在改列表的的值， 取的值仍然保持最初取到的值！
```python
#列表取值
name = ["remix", "yoki", "time", "tom", "jake"]
me = name[2]

name[2] = "cake"

print("me: {0}, name[2]:{1}".format(me, name[2]));
#me: time, name[2]:cake
```

##### [1.1.2 元素类型是可变成员](#)
如果数据是可变类型，那么取值返回的就是引用了！  我们先创建一个User类！

```python
class User:
    name:string = '';
    age: int = 0;
    #private
    __id = 0
    def __init__(self, userName, userAge, id) -> None:
        self.name = userName
        self.age = userAge
        self.__id = id
    def toString(self) -> string:
        return f"UID:{self.__id} Name: {self.name} Age:{self.age}";
#end class User
```

先获得列表成员，然后修改值。那么都会改变！
```python
users = [
    User("jxkicker",24, 2016110418),
    User("remix",22, 2016110417),
    User("cicer",23, 2016110416),
    User("mike",25, 2016110414)
]

yumi = users[0]
yumi.name = "yumike"

print(users[0].toString())
#UID:2016110418 Name: yumike Age:24
```

先获得列表成员，然后列表里面的成员的值。那么都会改变！
```python
users = [
    User("jxkicker",24, 2016110418),
    User("remix",22, 2016110417),
    User("cicer",23, 2016110416),
    User("mike",25, 2016110414)
]

yumi = users[0]
users[0].name = "yumike"

print(yumi.toString())
#UID:2016110418 Name: yumike Age:24
```

#### [1.2 列表切片](#)
python列表的切片，获得的是原来对象的引用,也就是浅拷贝。并不是深拷贝！

切片语法，它有三个参数，分别为开始位置，结束位置，跳步！
```python
list[start:end:step]
```
**倒数取法，需要注意的是取到最后一位，不写下标即可！**

不可变数据切片
```python
# -*- coding: UTF-8 -*-
#         0   1   2    3   4   5   6 
scores = [45, 87, 99, 78, 77, 75, 15]
#         -7  -6  -5  -4  -3  -2   -1 

s1 = scores[0: 3]    # [45, 87, 99]
s2 = scores[-3: -1]  # [77, 75]
s3 = scores[-3: ]  # [77, 75, 15]
```

可变数据切片
```python
#slice
sliceUsers = users[0:2];
sliceUsers[0].name = "cokni"

for usr in users:
    print(usr.toString());
"""
UID:2016110418 Name: cokni Age:24
UID:2016110417 Name: remix Age:22
UID:2016110416 Name: cicer Age:23
UID:2016110414 Name: mike Age:25
"""
```
##### [1.2.1 利用切片进行逆序](#)
一个比较特别的操作，得到一个逆序的新列表，记住执行的是浅拷贝！
```python
# -*- coding: UTF-8 -*-
#         0   1   2    3   4   5   6 
scores = [45, 87, 99, 78, 77, 75, 15]
#         -7  -6  -5  -4  -3  -2   -1 
sslice = scores[::-1];

print(sslice) #[15, 75, 77, 78, 99, 87, 45]
```


#### [1.3 内置列表函数](#)
Python包含以下函数, 用以获得最大值，最小值，长度，类型转换！

* len(list):列表元素个数
* max(list):返回列表元素最大值
* min(list): 返回列表元素最小值
* list(seq):将元组转换为列表

```python
# -*- coding: UTF-8 -*-
scores = [45, 87, 99, 78, 77, 75, 15]
jina = ("jina", 28, False)

#tuple -> list
ul = list(jina)

print(f"max score:{max(scores)} min score:{min(scores)}  count:{len(scores)}")
#max score:99 min score:15  count:7

print(ul) 
#['jina', 28, False]
```

#### [1.3 更新列表元素](#)
更新有，修改，插入，删除！

##### [1.3.1 删除列表元素](#)
使用 del 操作符！ 可以删除某个元素！ del list[idx]

```python
# -*- coding: UTF-8 -*-
scores = [45, 87, 99, 78, 77, 75, 15]

del scores[1]
print(scores) #[45, 99, 78, 77, 75, 15]
```

* list.clear()  清空整个列表
* list.remove(obj)  移除列表中某个值的第一个匹配项

```python
scores = [45, 87, 99, 78, 77, 75, 15]

scores.remove(77)
# [45, 87, 99, 78, 75, 15]
```

##### [1.3.2 追加新元素](#)
追加元素有两种方法，追加或者插入

* list.append(obj) 在列表末尾添加新的对象
* list.insert(index, obj) 将对象插入列表

```python
scores = [45, 87, 99, 78, 77, 75, 15]

scores.append(400)
scores.insert(1, 569)

print(scores)
# [45, 569, 87, 99, 78, 77, 75, 15, 400]

scores.clear()
print(scores)  
# []
```

#### [1.4 列表脚本操作符](#)
列表对 + 和 * 的操作符与字符串相似。+ 号用于组合列表，* 号用于重复列表。

|操作|结果|说明|
|:----|:----|:----|
|[1, 2, 3] + [4, 5, 6]|[1, 2, 3, 4, 5, 6]|组合|
|['Hi!'] * 4|['Hi!', 'Hi!', 'Hi!', 'Hi!']|重复|

```python
# -*- coding: UTF-8 -*-
scores1 = [15, 35, 25]
scores2 = [15, 35, 25]

scores = scores1 + scores2
print(scores)
#[15, 35, 25, 15, 35, 25]
```

#### [1.5 其他操作](#)
lsit还可以执行栈的操作！ 通过pop和append

* list.pop([index=-1]) 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
* list.index(x[, start[, end]]) 函数用于从列表中找出某个值第一个匹配项的索引位置
* list.count(obj) 统计某个元素在列表中出现的次数
* list.copy()  复制列表

##### [1.5.1 copy](#)
不论成员是不可变类型还是可变，都执行的是深拷贝，来创建一个列表副本

```python
cusers = users.copy()
cusers[1].name = "alter name"
del cusers[2]

for usr in cusers:
    print(usr.toString())
"""
UID:2016110418 Name: jxkicker Age:24
UID:2016110417 Name: alter name Age:22
UID:2016110414 Name: mike Age:25
"""

for usr in users:
    print(usr.toString())

"""
UID:2016110418 Name: jxkicker Age:24
UID:2016110417 Name: alter name Age:22
UID:2016110416 Name: cicer Age:23
UID:2016110414 Name: mike Age:25
"""
```

#### [1.6 排序逆序](#)
python 内置了两个方法用于调整序列或者排序

* list.reverse()  反向列表中元素
* list.sort( key=None, reverse=False)  对原列表进行排序
    * reverse -- 排序规则，reverse = True 降序， reverse = False 升序（默认）。
    * key -- 主要是用来进行比较的元素，只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序。

```python
users.sort(key=lambda user: user.age, reverse=False)
# 根据年龄进行降序排序
for usr in users:
    print(usr.toString())

"""
UID:2016110417 Name: remix Age:22
UID:2016110416 Name: cicer Age:23
UID:2016110418 Name: jxkicker Age:24
UID:2016110414 Name: mike Age:25
"""
```

### [2. Tuple 元祖](#) 
Python的元组与列表类似，不同之处在于 **元组的元素不能修改，元祖内部的元素既不能增加也不能减少。** 元组使用小括号 ( )，**还可以不用括号** ，列表使用方括号 [ ]。 元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可。

元祖也支持切片、下标访问，但是切片返回的是一个全新的元祖！

```python
profession = (User("mike",25, 2016110414), True, "UESTC")
tup3 = "a", "b", "c", "d"   #  不需要括号也可以
tup2 = (1, 2, 3, 4, 5 )

print(profession[0].toString()) #UID:2016110414 Name: mike Age:25
print(profession[2]) #UESTC
```

**元组中只包含一个元素时，需要在元素后面添加逗号** **,**  否则括号会被当作运算符使用

```python
myTuple = (25,)
notTuple = (25) # 非元祖

print(f"type:{type(myTuple)} ")  # type:<class 'tuple'> 
print(f"type:{type(notTuple)} ") # type:<class 'int'>  
```

**类型转换** **tuple(iterable)**:将可迭代系列转换为元组。

```python
list1= ['Google', 'Taobao', 'Runoob', 'Baidu']
tuple1=tuple(list1)
print(tuple1)
# ('Google', 'Taobao', 'Runoob', 'Baidu')
```

#### [2.1 元祖切片](#)
切片语法，它有三个参数，分别为开始位置，结束位置，跳步！
```python
tuple[start:end:step]
```

使用例子：
```python
product = ("fruit", "apple", "pear", "walnut","banana", "cherry")
sp1 = product[0:2]
sp2 = product[0::2] #间隔一个

print(sp1); #('fruit', 'apple')
print(sp2); #('fruit', 'pear', 'banana')
```
#### [2.2 元组运算符](#)
元组中的元素值是不允许增加或者删除, 不允许修改，但是元祖本身和元祖之间是具有一些操作！

* **len(tup)** : 返回元祖的长度
* 链接运算符: **+** : 将两个元祖整合为一个元祖  (1, 2, 3) + (4, 5, 6) = (1, 2, 3, 4, 5, 6)
* 复制运算符: ***** :将元祖 * n复制成一个元祖 ('Hi!',) * 4 = ('Hi!', 'Hi!', 'Hi!', 'Hi!')
* 成员运算符 **in** ： 判断一个元素是否在元祖中！ 3 in (1, 2, 3) = True
* **min(tuple)** :返回元组中元素最小值
* **max(tuple)** : 返回元组中元素最大值。

```python
# -*- coding: UTF-8 -*-
fruits = ["fruit", "apple", "pear", "walnut","banana", "cherry"]
product = tuple(fruits)

scores = (56, 75, 85, 94)

print(f"tuple len: {len(product)}")
print(f"has 75: {75 in scores}")
```
#### [2.3 关于元组是不可变的](#)
所谓元组的不可变指的是元组所指向的内存中的内容不可变。 并不是指元祖不可重新赋值

元祖本身是可以重新赋值的
```python
tup = ('r', 'u', 'n', 'o', 'o', 'b')
#tup[0] = 'g'     # 不支持修改元素
tup = (1,2,3)
```

##### [2.3.1 可变类型内容可变](#)
元祖的不可变只是指定索引的引用不能改变，对于可变类型其 **内容还是可变的** ！

```python
usersTuple = (
    User("jxkicker",24, 2016110418),
    User("remix",22, 2016110417),
    User("cicer",23, 2016110416)
)

usersTuple[0].age = 26

print(usersTuple[0].toString())
#UID:2016110418 Name: jxkicker Age:26

usersTuple[2] = User("mike",27, 2016110419) #不被允许
```

### [3. Set 集合](#) 
**集合（set）** 是一个 **无序** 的 **不重复** 元素序列。 可以使用大括号 { } 或者 set() 函数创建集合，**注意**：创建一个 **空集合** 必须用 set() 而不是 { }，因为 { } 是用来创建一个 **空字典**。

创建语法
```python
parame = {value01,value02,""" ... """}
#or
set(value)
```

* **类型转换** **set(iterable)**:将可迭代系列转换为元组。
* **len(set)** 返回集合的元素个数
```python
# -*- coding: UTF-8 -*-
uniqueScores = set([12, 25 ,35, 45, 45])
oth = {45, 45, 95, 95, 35, 25}

print(uniqueScores)
#{25, 35, 12, 45}
print(oth)
#{25, 35, 45, 95}
```

#### [3.1 集合的基本操作](#)
集合也支持 增删改查基本操作！

* s.add( x ) 将元素 x 添加到集合 s 中，如果元素已存在，则不进行任何操作。
* s.remove( x ) 将元素 x 从集合 s 中移除，如果元素不存在，则会发生错误。
* s.discard() 方法用于移除指定的集合元素。 该方法不同于 remove() 方法，因为 remove() 方法在移除一个不存在的元素时会发生错误，而 discard() 方法不会。
* s.clear() 清空集合 s。
* s.pop()	随机移除元素
* s.update(set) 可以添加新的元素或集合到当前集合中
* s.copy()	拷贝一个集合 [深拷贝]

```python
# -*- coding: UTF-8 -*-
oth = {15, 25, 30, 35 ,45, 45};

oth.add(90)          #添加
oth.discard(45)      #删除
oth.update({77, 79}) #添加set

print(oth)
#{35, 79, 25, 90, 77, 30, 15}

names = set()
names.update({"remix", "youmi", "ccer", "rita"})
names.remove("ccer");

print(names)
#{'remix', 'rita', 'youmi'}
```

#### [3.2 集合操作符](#)
我们都知道集合之间的操作有交并补！

* & 返回两个集合的交集 等同于 **x.intersection(y)**
* | 返回两个集合的并集 等同于 **x.union(y)**

```python
# -*- coding: UTF-8 -*-
tName = {"unim", "yunk", "ikun"}
rName = {"unim", "yunk", "cnm", "fuck"}

# 返回两个集合的交集
intersection_names = tName & rName
union_names = tName | rName

print(intersection_names)   # {'unim', 'yunk'} 
print(union_names)   # {'ikun', 'cnm', 'yunk', 'unim', 'fuck'}
```

#### [3.3 集合整体操作](#)
我们看看定义定义在集合对象上面的操作！

* x.difference(y): 返回一个集合，元素包含在集合 x ，但不在集合 y ：
* difference_update()	移除集合中的元素，该元素在指定的集合也存在。
* intersection()	返回集合的交集
* intersection_update() 方法用于获取两个或更多集合中都重叠的元素，即计算交集。 在原始的集合上移除不重叠的元素。
* symmetric_difference()	返回两个集合中不重复的元素集合，返回对称差！
* **union()**	返回两个集合的并集

```python
# -*- coding: UTF-8 -*-
tName = {"unim", "yunk", "ikun"}
rName = {"unim", "yunk", "cnm", "fuck"}

# 返回两个集合的交集
intersection_names = tName.intersection(rName)
union_names = tName.union(rName)

print(intersection_names)   # {'unim', 'yunk'} 
print(union_names)   # {'ikun', 'cnm', 'yunk', 'unim', 'fuck'}

#两个集合的对称差
print(tName.symmetric_difference(rName)) 
#{'ikun', 'cnm', 'fuck'}
```

* x.isdisjoint(y)	判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。
* x.issubset(y)	判断指定集合是否为该方法参数集合的子集。 **x是否是y的子集**
* x.issuperset(y)	判断集合 y 的所有元素是否都包含在集合 x 中： **y是否x的子集**

### [4. Dictionary 字典](#) 
使用大括号 { } 创建空字典，字典是另一种可变容器模型，且可存储任意类型对象。
字典的每个键值 key=>value 对用 **冒号:** 分割，每个对之间用逗号 **,** 分割，整个字典包括在花括号 {} 中。
**字典的关键字key必须为不可变类型！**

```python
# -*- coding: UTF-8 -*-
userDictionary = {
    "remix": 3,
    "kicker": 5,
    "mike": 7,
    "cicer": 2,
    "youmi":2
}

print(userDictionary)
#{'remix': 3, 'kicker': 5, 'mike': 7, 'cicer': 2, 'youmi': 2}
print(userDictionary["cicer"])  #2
```
使用key作为下标访问对应的值！

**创建空字典** 两种方式，构造函数或者大括号！
```python
empDic = dict()
empDic_ = {}
print(empDic, empDic_) #{} {}
```

**将元祖转换为字典的方式：** 元祖里面的元素得是长度为2的列表，第一个元素还需要是不可变类型
```python
tup_to_dic = (["remix", 3], ["kicker",5], ["youmi", 2])
dic = dict(tup_to_dic)

print(dic)
#{'remix': 3, 'kicker': 5, 'youmi': 2}
```


#### [4.1 字典内置函数&方法](#)
Python字典包含了以下内置函数：

* str(dict) 输出字典，可以打印的字符串表示。
* len(dict) 计算字典元素个数，即键的总数。
* type(variable) 返回输入的变量类型，如果变量是字典就返回字典类型。
* in: 判断某个键是否在字典里面 key in Dictionary

```python
#{'remix': 3, 'kicker': 5, 'youmi': 2}
print(len(dic)) #3
```

#### [4.2 字典的基本操作](#)
增删改查 基本操作

##### [4.2.1 访问字典元素](#)
使用如下方式访问字典的值 dictName[key]  **如果用字典里没有的键访问数据，会输出错误如下：**

```python
tinydict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
print ("tinydict['Name']: ", tinydict['Name'])
print ("tinydict['Age']: ", tinydict['Age'])
# tinydict['Name']:  Runoob
# tinydict['Age']:  7

# 防止报错 先检测键是否存在
userDictionary = {
    "remix": 3,
    "kicker": 5,
    "mike": 7,
    "cicer": 2,
    "youmi":2
}

key = "youmi"

if key in userDictionary:
    print(f"dic[{key}]: {userDictionary[key]}")
```
##### [4.2.2 修改元素](#)
直接访问修改即可！
```python
userDictionary = {
    "remix": 3,
    "kicker": 5,
    "mike": 7,
    "cicer": 2,
    "youmi":2
}

userDictionary["youmi"] = 78; 
```

##### [4.2.3 删除某个字典元素](#)
需要使用到 **del** 操作  它可以删除某个元素，也可以删除整个字典！

```python
tinydict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
 
del tinydict['Name'] # 删除键 'Name'
tinydict.clear()     # 清空字典
del tinydict         # 删除整个字典
```
* dict.clear():将字典变成空字典
* del dict:直接让字典不存在！

##### [4.2.4 新增元素](#)
直接添加可以，也可以使用 dict.setdefault(key, default=None) 方法

```python
# -*- coding: UTF-8 -*-
userDictionary = {
    "remix": 3,
    "kicker": 5
}

#新增一个元素
userDictionary["youmi"] = 8

print(userDictionary)
```

#### [4.3 字典对象支持的操作](#)

* dict.copy() 返回一个字典的浅复制
* dict.fromkeys(seq[, value]) 创建一个新字典，以序列 seq 中元素做字典的键，value 为字典所有键对应的初始值。
* dict.get(key, default=None) 返回指定键的值，如果键不在字典中返回 default 设置的默认值
* dict.items() 方法以列表返回视图对象，是一个可遍历的key/value 对。
* dict.keys()  返回一个视图对象, 可以转换为列表
* dict.values() 返回一个视图对象 可以转换为列表
* dict.setdefault(key, default=None) 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default
* dict.update(dict2) 把字典dict2的键/值对更新到dict里
* pop(key[,default]) 删除字典 key（键）所对应的值，返回被删除的值。
* popitem() 返回并删除字典中的最后一对键和值。

```python
userDictionary = {
    "remix": 3,
    "kicker": 5
}

#新增一个元素
userDictionary["youmi"] = 8

keys= list(userDictionary.keys())
print(keys)
#['remix', 'kicker', 'youmi']

tinydict = {'Google': 'www.google.com', 'Runoob': 'www.runoob.com', 'taobao': 'www.taobao.com'}
 
print("字典值 : %s" %  tinydict.items())
#[('Google', 'www.google.com'), ('taobao', 'www.taobao.com'), ('Runoob', 'www.runoob.com')]
```

#### [4.4 字典遍历操作](#)
python对于字典的遍历支持好多种方式！

遍历key值
```python
for key in a:
    print(key+':'+a[key])
```
遍历value
```python
for value in a.values():
    print(value)
```
遍历字典项
```python
for kv in a.items():
       print(kv)
 
# ('a', '1')
# ('b', '2')
# ('c', '3')
```
遍历字典健值
```python
for key,value in a.items():
    print(key+':'+value)
 
# a:1
# b:2
# c:3

for (key,value) in a.items():
    print(key+':'+value)
 
# a:1
# b:2
# c:3
```

### [5. Str 字符串](#) 
在 Python 中处理文本数据是使用 **str** 对象，也称为 字符串。 字符串是由 **Unicode码** 位构成的不可变 序列

**原始字符串：** 使用前缀 r或者R
```python
message = r"\n is Newline character"
print(message)
#\n is Newline character
```

**字符串类** **str** 构造函数 
* class str(object='') :默认是空字符串
* class str(object=b'', encoding='utf-8', errors='strict')  errors 的默认值为 'strict'，表示编码错误会引发 UnicodeError

#### [5.1 字符串编码的方法](#)
str.encode(encoding='utf-8', errors='strict')  返回原字符串编码为字节串对象的版本。 默认编码为 'utf-8'。 可以给出 errors 来设置不同的错误处理方案。 errors 的默认值为 'strict'，表示编码错误会引发 UnicodeError。 
其他可用的值为 'ignore', 'replace', 'xmlcharrefreplace', 'backslashreplace' 

str.isascii() 如果字符串为空或字符串中的所有字符都是 ASCII ，返回 True ，否则返回 False 。ASCII 字符的码点范围是 U+0000-U+007F 。

#### [5.2 判断方法](#)
请查询API吧！

* str.isnumeric() 如果字符串中至少有一个字符且所有字符均为数值字符则返回 True ，否则返回 False 。 数值字符包括数字字符，以及所有在 Unicode 中设置了数值特性属性的字符，例如 U+2155, VULGAR FRACTION ONE FIFTH。 正式的定义为：数值字符就是具有特征属性值 Numeric_Type=Digit, Numeric_Type=Decimal 或 Numeric_Type=Numeric 的字符。
* str.islower() 如果字符串中至少有一个区分大小写的字符 4 且此类字符均为小写则返回 True ，否则返回 False 。
* tr.isspace() 如果字符串中只有空白字符且至少有一个字符则返回 True ，否则返回 False 。
* str.isdigit() 如果字符串中的所有字符都是数字，并且至少有一个字符，返回 True ，否则返回 False 。 数字包括十进制字符和需要特殊处理的数字，如兼容性上标数字。这包括了不能用来组成 10 进制数的数字，如 Kharosthi 数。 严格地讲，数字是指属性值为 Numeric_Type=Digit 或 Numeric_Type=Decimal 的字符。
* str.isdecimal() 如果字符串中的所有字符都是十进制字符且该字符串至少有一个字符，则返回 True ， 否则返回 False 。十进制字符指那些可以用来组成10进制数字的字符，例如 U+0660 ，即阿拉伯字母数字0 。 严格地讲，十进制字符是 Unicode 通用类别 "Nd" 中的一个字符。
* str.isalnum() 如果字符串中的所有字符都是字母或数字且至少有一个字符，则返回 True ， 否则返回 False 。 如果 c.isalpha() ， c.isdecimal() ， c.isdigit() ，或 c.isnumeric() 之中有一个返回 True ，则字符c是字母或数字。
* str.isalpha() 如果字符串中的所有字符都是字母，并且至少有一个字符，返回 True ，否则返回 False 。字母字符是指那些在 Unicode 字符数据库中定义为 "Letter" 的字符，即那些具有 "Lm"、"Lt"、"Lu"、"Ll" 或 "Lo" 之一的通用类别属性的字符。 注意，这与 Unicode 标准中定义的"字母"属性不同。

#### [5.3 访问](#)
再Python中，字符串也支持`[]` 索引访问!

```python
letter = "message is important"

print(letter[2])  # s
```

####

### [6. 类型转换](#)
python 类型转换有两种，一种是隐式类型转换，另一种是显示类型转换!

```python
num_int = 123
num_flo = 1.23

num_new = num_int + num_flo
```

以下是显示类型转换需要用的函数
```python
int(x [,base ])         将x转换为一个整数  
long(x [,base ])        将x转换为一个长整数  
float(x )               将x转换到一个浮点数  
complex(real [,imag ])  创建一个复数  
str(x )                 将对象 x 转换为字符串  
repr(x )                将对象 x 转换为表达式字符串  
eval(str )              用来计算在字符串中的有效Python表达式,并返回一个对象  
tuple(s )               将序列 s 转换为一个元组  
list(s )                将序列 s 转换为一个列表  
chr(x )                 将一个整数转换为一个字符  
unichr(x )              将一个整数转换为Unicode字符  
ord(x )                 将一个字符转换为它的整数值  
hex(x )                 将一个整数转换为一个十六进制字符串  
oct(x )                 将一个整数转换为一个八进制字符串  
```

**强制类型转换失败会直接报错**
```python
# -*- coding: UTF-8 -*-
msg_str = str("constructor is used!")

str_to_int = int(msg_str)
print(str_to_int)
#\n is Newline character
```

**类型转换错误需要捕获**

```python
# -*- coding: UTF-8 -*-
import sys

msg_str = str("constructor is used!")
try:
    str_to_int = int(msg_str)
    print(str_to_int)
except ValueError:
    print('error in cast')
finally:
    print('error no match')
```

-----
时间: [] 