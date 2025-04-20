### [Python 复合数据类型 标准库](#)
`在Python的标准库中定义了一些非常有用的数据类型，例如时间类型、随机数等等`

-----
- [x] [`1. 时间类型`](#1-时间类型)
- [x] [`2. `](#2-)
- [x] [`3. `](#3-)
- [x] [`4. `](#4-)
- [x] [`5. `](#5-)
-----

### [1. 时间类型 ](#)
Python内置两个关于时间处理的包，**time** 和 **datetime**。偶尔还会用到一个 **calendar** 模块! 从命名上讲，
`time`包提供处理时间相关的函数，`datetime`包提供处理时间日期相关的函数。

#### [1.1 Time](#)
**time.sleep(second)** ,它接收一个参数，用于以单位秒指定睡眠时间,单位为 秒 second，任何调用该方法的线程都会阻塞至计时完成。
**time.time()** ,它返回一个秒级别的时间戳（本质上是从1970至今经过的秒数，float类型，小数点后范围不定）。

**这两个函数是time包中使用最频繁的函数！**

```python
time.sleep(2) #sleep 2 second

print("时间戳:{0}".format(time.time()))
#时间戳:1667824771.89697
```

同时它有两个变量 **timezone、tzname**

`time.timezone` `是当地时区（未启动夏令时）距离格林威治的偏移秒数（>0，美洲;<=0大部分欧洲，亚洲，非洲）。`  
`time.tzname` `属性time.tzname包含一对根据情况的不同而不同的字符串，分别是带夏令时的本地时区名称，和不带的。`

```python
print(time.timezone)  #-28800
print(time.tzname)    #('中国标准时间', '中国夏令时')
```

##### [1.1.1 格式化时间 localtime(sec)](#)
**time** `模块提供了` `localtime` `函数，将一个本地浮点数的时间戳转换为一个时间元组！` **本质上是一个 class 类型名为 struct_time**

```python
#官方定义
def localtime(secs: float | None = ...) -> struct_time:...
```

```python
import time

localtime = time.localtime(time.time())
print ("本地时间为 :", localtime)

#本地时间为 : time.struct_time(tm_year=2016, tm_mon=4, tm_mday=7, 
#            tm_hour=10, tm_min=28, tm_sec=49, tm_wday=3, tm_yday=98, tm_isdst=0)
```

|`属性`|`说明`|
|:---|:---|
|`tm_year`|`四位数表示 年`|
|`tm_mon`|`1 到 12`|
|`tm_mday`|`1 到 31`|
|`tm_hour`|`0 到 23`|
|`tm_min`|`0 到 59`|
|`tm_sec`|`0 到 61 (60或61 是闰秒)`|
|`tm_wday`|`0 到 6 (0是周一)`|
|`tm_yday`|`一年中的第几天，1 到 366`|
|`tm_isdst`|`是否为夏令时，值有：1(夏令时)、0(不是夏令时)、-1(未知)，默认 -1`|

```python
import time
localtime = time.localtime(time.time())

print ("year :", localtime.tm_year) # year : 2022
print ("month :", localtime.tm_mon) # month : 11
print ("day :", localtime.tm_mday)  # day : 7
print ("hour :", localtime.tm_hour) # hour : 20
```

##### [1.1.2 strftime](#)
`我们可以使用` **time** `模块的` **strftime** `方法来格式化日期。`
```python
time.strftime(format[, t])
```
`展示当前时间:`
```python
print (time.strftime("%Y/%m/%d %H:%M:%S", time.localtime()))
#2022-11-09 10:00:38
```

**格式化时间 - 格式化符号**

* `%y 两位数的年份表示（00-99）`
* `%Y 四位数的年份表示（000-9999）`
* `%m 月份（01-12）`
* `%d 月内中的一天（0-31）`
* `%H 24小时制小时数（0-23）`
* `%I 12小时制小时数（01-12）`
* `%M 分钟数（00-59）`
* `%S 秒（00-59）`
* `%a 本地简化星期名称`
* `%A 本地完整星期名称`
* `%b 本地简化的月份名称`
* `%B 本地完整的月份名称`
* `%c 本地相应的日期表示和时间表示`
* `%j 年内的一天（001-366）`
* `%p 本地A.M.或P.M.的等价符`
* `%U 一年中的星期数（00-53）星期天为星期的开始`
* `%w 星期（0-6），星期天为星期的开始`
* `%W 一年中的星期数（00-53）星期一为星期的开始`
* `%x 本地相应的日期表示`
* `%X 本地相应的时间表示`
* `%Z 当前时区的名称`
* `%% %号本身`

##### [1.1.3 strptime](#)
`会返回一个` **struct_time** `对象！`

```python 
# 将格式字符串转换为时间戳
time_str = "2022-11-09 10:00:38"
tm = time.strptime(time_str, "%Y-%m-%d %H:%M:%S")

print(tm)
```

##### [1.1.4 mktime](#)
`接受时间元组并返回时间戳` （ **1970** `纪元后经过的` **浮点秒数**）。 

```python
time.mktime(tm)
print(time.mktime(tm))
#1667959238.0

t = (2022, 2, 17, 17, 3, 38, 1, 48, 0)
secs = time.mktime( t )
#1667959238.0
```

##### [1.1.5 运行时间](#)
**time** 提供了 **perf_counter()** 返回系统运行时间，**process_time()** 返回进程的运行时间 
```python
print(time.perf_counter())   # 返回系统运行时间 48072.7521242
print(time.process_time())   # 返回进程运行时间 0.046875 
```

##### [1.1.6 asctime](#)
**time.asctime([tupletime])**：`接受时间元组并返回一个可读的形式为"Thu Nov  8 09:31:15 2018"的24字符的字符串；`

```python
t = (2022, 2, 17, 17, 3, 38, 1, 48, 0)
secs = time.mktime( t ) #转换为浮点时

#浮点数 转 字符串元祖
sre_tm = time.asctime(time.localtime(secs))

print(sre_tm)
#Thu Feb 17 17:03:38 2022
```

##### [1.1.7 ctime](#)
作用相当于asctime(localtime(secs))。可以直接 **time.ctime(secs)**
```python
t = (2022, 2, 17, 17, 3, 38, 1, 48, 0)
secs = time.mktime( t ) #转换为浮点时

#浮点数 直接转 字符串元祖
sre_tm = time.ctime(secs)

print(sre_tm)
#Thu Feb 17 17:03:38 2022
```

##### [1.1.8 gmtime](#)
接收时间戳（1970纪元后经过的浮点秒数）并返回格林威治天文时间下的时间元组t。 **注：t.tm_isdst始终为0**

```python
sec = time.time()

tm = time.localtime(sec) #当前本地时间
tmg = time.gmtime(sec) #格林时间

print (time.strftime("%Y/%m/%d %H:%M:%S", tm))
#2022/11/09 10:43:45  东八区时间
print (time.strftime("%Y/%m/%d %H:%M:%S", tmg))
#2022/11/09 02:43:45  格林威治天文时间
```

#### [1.2 Calendar](#)
此模块的函数都是日历相关的，例如打印某月的字符月历。

### [2.](#) 

### [3.](#) 

### [4.](#) 

### [5.](#) 

-----
`时间`: `[]` 