### [Python IO、文件系统](#)

` 一门语言的基本操作了，文件操作有文件的内容输入输出，还有文件系统的各种操作，创建文件，查看目录，压缩解压缩，解密加密....`

-----

- [x] [1. 文件系统概述](#1-文件系统概述)
- [x] [2.](#2-)
- [x] [3. ](#3-)
- [x] [4. ](#4-)
- [x] [5. ](#5-)

-----

### [1. 文件系统](#)
文件系统管理是**Linux内核主要负责的四种功能之一**，软件由程序+数据+文档组成，而文件则用于存储软件的数据，重要性不言而喻。对于程序设计而言，我们首先要明白文件系统有哪些学习的内容：首先我们要明白在计算机中文件分为两大类： **文本文件** 和**二进制文件**，前者的例子如：源代码文件、txt文档... ，而图片文件、音频视频、数据库数据文件都属于二进制文件。

**文本文件**：每个文本文件都需要确定自己的编码格式 `ascii` `unicode`、`GBK`、`utf-8`，不然就无法正确解析文本内容！ 所以了解文件的**编码格式**是需要的、同时对文件的读写是需要**缓存区**的，对于超大型文件，是无法一下子全部读入内存的，采用缓存区一部分一部分读写是必然的选择。

要知道文件不只是存储文本或者二进制数据，还有一类特殊的文件，我们称之为 **目录文件**，这也是我们需要掌握的内容。学会如何创删目录，文件路径操作也是我们的必修课。同时对**文件的基本信息**例如，创建日期，大小，文件后缀等等

**由于文件操作是Linux内核的功能，显然文件操作本质上是调用操作系统的功能！而不是需要深入细节了解每个字节的移动存储。**

#### [1.1 文件编码格式](#)
**ASCII**：七位就可以表达式一个字符，总共表示128位字符。一个字节的容量就足以表示！可以满足英文书写的基本需求，但是对于中文、日文、俄文等文字无法表示。

**ISO-8859-1**:  八位表示一个字符，能表示256个字符，兼容ASCII。ISO-8859-1收录的字符除ASCII收录的字符外，还包括西欧语言、希腊语、泰语、阿拉伯语、希伯来语对应的文字符号。同样无法表示地球上所有的文字。

**GB码**: GB 即"国标"的汉语拼音缩写，为中华人民共和国国家标准的意思．国标编码就是中华人民共和国信息交换汉字编码标准（GB2312－80），**目前主要有GB2312、GBK、GB18030三种。**  

* GB18030采用单字节、双字节、四字节分段编码。
* GB2312编码方案于1980年发布，收录汉字6763个，采用双字节编码。
* GBK编码方案于1995年发布，收录汉字21003个，采用双字节编码。

**Unicode**: 又叫 `万国码、统一码`，大小能表示地球上所有的文字信息。 现在有三种版本，**UTF-8、UTF-16、UTF-32**

**UTF-32**，用四个字节表示一个符号，也就是可以表示`2^32`个字符。因为UTF-32对每个字符都使用4字节，就空间而言，是非常没有效率的。

**UTF-16**：Unicode字符的码位，需要1个或者2个16位长的码元来表示，因此这是一个变长表示。

>  `UTF`是 `UCS` `Transformation Format` 的缩写，可以翻译成统一码字符集转换格式。



##### [1.1.1 UTF-8 ](#)
是针对Unicode的一种可变长度字符编码。它可以用来表示Unicode标准中的任何字符，而且其编码中的第一个字节仍与ASCII相容，使得原来处理ASCII字符的软件无须或只进行少部分修改后，便可继续使用。**应用最广泛的编码格式！** 不同的文字使用不同的字节长度存储！这种表示方式，英文编码只需要一个字节，中文编码，一个字符需要三个字节，依靠每个字节的前几位来判断多少个字节表示一个字符。

* 如果字节以0开始，则表示一个字节就是一个字符。
* 如果字节以110开始，则表示这个字节加上后面一个字节表示一个字符。

<table log-set-param="table_view" data-sort="sortDisabled">
<caption>UTF-8编码格式</caption>
<tbody>
<tr>
<th width="180" height="30"><div class="para" label-module="para">字节</div></th>
<th width="360" height="30"><div class="para" label-module="para">格式</div></th>
<th width="180" height="30"><div class="para" label-module="para">实际编码位</div></th>
<th width="180" height="30"><div class="para" label-module="para">码点范围</div></th>
</tr>
<tr>
<td width="180" height="30"><div class="para" label-module="para">1字节</div></td>
<td width="360" height="30"><div class="para" label-module="para">0xxxxxxx</div></td>
<td width="180" height="30"><div class="para" label-module="para">7</div></td>
<td width="180" height="30"><div class="para" label-module="para">0 ~ 127</div></td>
</tr>
<tr>
<td width="180" height="30"><div class="para" label-module="para">2字节</div></td>
<td width="360" height="30"><div class="para" label-module="para">110xxxxx 10xxxxxx</div></td>
<td width="180" height="30"><div class="para" label-module="para">11</div></td>
<td width="180" height="30"><div class="para" label-module="para">128 ~ 2047</div></td></tr>
<tr>
<td width="180" height="30"><div class="para" label-module="para">3字节</div></td>
<td width="360" height="30"><div class="para" label-module="para">1110xxxx 10xxxxxx 10xxxxxx</div></td>
<td width="180" height="30"><div class="para" label-module="para">16</div></td>
<td width="180" height="30"><div class="para" label-module="para">2048 ~ 65535</div></td></tr>
<tr>
<td width="180" height="47"><div class="para" label-module="para">4字节</div></td>
<td width="360" height="47"><div class="para" label-module="para">11110xxx 10xxxxxx 10xxxxxx 10xxxxxx</div></td>
<td width="180" height="47"><div class="para" label-module="para">21</div></td>
<td width="180" height="47"><div class="para" label-module="para">65536 ~ 2097151</div></td>
</tr>
</tbody>
</table>



#### [1.2 IO](#)
IO，可以理解为输入输出，将**数据(字节流)**从其他底层流向程序这叫输入，将**程序中的数据(字节流)**存储向文件、屏幕、其他位置这叫输出。

* Python 提供了**os** 模块，它提供了非常丰富的方法用来处理文件和目录。包括文件权限，重命名、目录操作。

* **os.path** 模块提供路径操作

* **tempfile**    该模块用于创建临时文件和目录，它可以跨平台使用。

  

### [2.  简单文件操作](#) 
我们将介绍如何对一个文件(非目录文件)进行读写。 Python **open()** 方法用于打开一个文件，并返回**文件对象**。在对文件进行处理过程都需要使用到这个函数，如果该文件无法被打开，会抛出 **OSError**。

```python
def open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None):
    pass
```

- `file`: 必需，文件路径（相对或者绝对路径）。
- `mode`: 可选，文件打开模式
- `buffering`: 设置缓冲
- `encoding`: 一般使用`utf8`
- `errors`: 报错级别
- `newline`: 区分换行符
- `closefd`: 传入的file参数类型
- `opener`: 设置自定义开启器，开启器的返回值必须是一个打开的文件描述符。

根据其创建方式的不同，文件对象可以处理对真实磁盘文件，对其他类型存储，或是对通讯设备的访问（例如标准输入/输出、内存缓冲区、套接字、管道等等）。文件对象也被称为 *文件类对象* 或 *流*。

实际上共有三种类别的文件对象: `原始二进制文件,` `缓冲二进制文件` 以及 `文本文件`。

#### [2.1 open函数参数解释](#)

##### 2.1.1 mode 参数
**mode** 参数表示打开文件的模式。

| `字符` | ` 意义`                                                      |
| ------ | ------------------------------------------------------------ |
| `r`    | `	以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。` |
| `w`    | `文本写入，并先清空文件（慎用），文件不存在则创建。`         |
| `x`    | `文本写，排它性创建，如果文件已存在则失败`                   |
| `a`    | `文本写，如果文件存在则在末尾追加，不存在则创建。` **文件指针将会放在文件的结尾** |
| `b`    | `二进制模式，例如：'rb'表示二进制读`                         |
| `t`    | `文本模式（默认）`                                           |
| `+`    | `可读可写`                                                   |
| `ab`   | `以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。` |
| `a+`   | ` 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。` |
| `ab+`  | `以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。` |
| `wb`   | `二进制打开一个文件只用于打开`                               |
| `wb+`  | `组合模式`                                                   |



##### 2.1.2 buffering 参数
**buffering** 是一个可选的整数，用于设置缓冲策略。

* **0**：传入 0 来关闭缓冲（只允许在二进制模式下）。
* **1**：传入 1 来选择行缓冲（只在文本模式下可用）。
* **x>0**： 传入一个整数 > 1 来表示固定大小的块缓冲区的字节大小。


##### 2.1.3 encoding
这只能在文本模式下使用。默认编码依赖于平台。 [编码参数请查看此处](./Encoding.md)


##### 2.1.4 errors

*errors* 是一个可选的字符串参数，用于指定如何处理编码和解码错误 ,  **这不能在二进制模式下使用**。

- `'strict'` :如果存在编码错误，`'strict'` 会引发 [`ValueError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ValueError) 异常。 默认值 `None` 具有相同的效果。
- `'ignore'`: 忽略错误。请注意，忽略编码错误可能会导致数据丢失。
- `'replace'`: 会将替换标记（例如 `'?'` ）插入有错误数据的地方。
- `'surrogateescape'` 将把任何不正确的字节表示为 U+DC80 至 U+DCFF 范围内的下方替代码位。
- `'backslashreplace'`: 用Python的反向转义序列替换格式错误的数据。
- `'namereplace'` （也只在编写时支持）用 `\N{...}` 转义序列替换不支持的字符。

##### 2.1.5 *newline* 

换行符确定如何从流中解析换行符。它可以是None、""、"\n"、"\r"和"\r\n"。

##### 2.1.6 closefd

如果 *closefd* 为 `False` 且给出的不是文件名而是文件描述符，那么当文件关闭时，底层文件描述符将保持打开状态。如果给出的是文件名，则 *closefd* 必须为 `True` （默认值），否则将触发错误。

##### 2.1.7 opener

可以通过传递可调用的 opener 来使用自定义开启器。然后通过使用参数（ file，flags ）调用 opener 获得文件对象的基础文件描述符。 opener 必须返回一个打开的文件描述符（使用 os.open as opener 时与传递 None 的效果相同）。


#### [2.2 file 对象](#)

file 对象使用 open 函数来创建，下表列出了 file 对象常用的函数：

| 序号 | 方法及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | `file.close()`关闭文件。关闭后文件不能再进行读写操作。       |
| 2    | `file.flush()`刷新文件内部缓冲，直接把内部缓冲区的数据立刻写入文件, 而不是被动的等待输出缓冲区写入。 |
| 3    | `file.fileno()`返回一个整型的文件描述符(file descriptor FD 整型), 可以用在如os模块的read方法等一些底层操作上。 |
| 4    | `file.isatty()`如果文件连接到一个终端设备返回 True，否则返回 False。 |
| 6    | `file.read(size)`从文件读取指定的字节数，如果未给定或为负则读取所有。 |
| 7    | `file.readline(size)`读取整行，包括 "\n" 字符。              |
| 8    | file.readlines([sizeint\])](https://www.runoob.com/python3/python3-file-readlines.html)读取所有行并返回列表，若给定sizeint>0，返回总和大约为sizeint字节的行, 实际读取值可能比 sizeint 较大, 因为需要填充缓冲区。 |
| 9    | file.seek(offset[, whence\])](https://www.runoob.com/python3/python3-file-seek.html)移动文件读取指针到指定位置 |
| 10   | `file.tell()`返回文件当前位置。                              |
| 11   | file.truncate([size\])](https://www.runoob.com/python3/python3-file-truncate.html)从文件的首行首字符开始截断，截断文件为 size 个字符，无 size 表示从当前位置截断；截断之后后面的所有字符被删除，其中 windows 系统下的换行代表2个字符大小。 |
| 12   | [file.write(str)](https://www.runoob.com/python3/python3-file-write.html)将字符串写入文件，返回的是写入的字符长度。 |
| 13   | [file.writelines(sequence)](https://www.runoob.com/python3/python3-file-writelines.html)向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。 |



#### [2.3 读取一个文本文件的所有行](#)

```python
idxFile = open("./index.py",mode="rt",encoding="utf-8")

lines = idxFile.readlines()
for line in lines:
    print(line, end="")

idxFile.close()
```





### [3.](#) 





### [4.](#) 





### [5.](#) 





-----

`时间`: `[]` 