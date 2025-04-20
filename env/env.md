



### [Python 环境生态](#)

-----

#### 1. Python 软件源

包库或者叫软件源是 Python 第三方软件的库的集合，或者市场，可以发布、下载和管理软件包，其中 pypi (Python Package Index) [https://pypi.org/](https://link.zhihu.com/?target=https%3A//pypi.org/) 是官方指定的软件包库，基于其上的 pip 工具就是从这里查找、下载安装软件包的。为了提高下载速度，世界上有很多 Pypi 的镜像服务器，在国内也有多个软件源，例如阿里的软件源是：[http://mirrors.aliyun.com/pypi/simple/](https://link.zhihu.com/?target=http%3A//mirrors.aliyun.com/pypi/simple/)。除此之外，还有其他软件源，如正对科学计算的 anaconda 的软件源 [https://repo.anaconda.com/](https://link.zhihu.com/?target=https%3A//repo.anaconda.com/)



#### 2. Python 包管理器

软件包源中的软件包数量巨大，版本多样，所以需要借助于软件源管理工具，例如 pip、conda、Pipenv、Poetry 等

**pip**:  是最常用的包管理工具，通过 `pip install <packagename>` 命令格式来安装软件包，使用的是 pypi 软件包源

**conda**: 多用作科学计算领域的包管理工具，功能丰富且强大，使用的软件包源是 Anaconda repository 和 Anaconda Cloud，conda 不仅支持 Python 软件包，还可以安装 C、C++ 、R 以及其他语言的二定制软件包。除了软件包管理外，还能提供相互隔离的软件环境。

**Pipenv**:是 Kenneth Reitz 在2017年1月发布的Python依赖管理工具，现在由PyPA维护。Pipenv 会自动帮你管理虚拟环境和依赖文件，并且提供了一系列命令和选项来帮助你实现各种依赖和环境管理相关的操作。

**Poetry**:和 Pipenv 类似，是一个 Python 虚拟环境和依赖管理工具，另外它还提供了包管理功能，比如打包和发布。你可以把它看做是 Pipenv 和 Flit 这些工具的超集。它可以让你用 Poetry 来同时管理 Python 库和 Python 程序

很多包管理工具不仅提供了基本的包管理功能，还提供了虚拟环境构建，程序管理的等功能。



#### 3.  环境变量

操作系统的环境变量可以为程序提供信息和做信息交换介质，进程可以共享操作系统中的环境变量，也可以为进程指定环境变量，其中 PATH 是很重要的环境变量，用于为操作系统和程序提供可执行文件的访问路径，例如写一个程序 a.exe，存放在 D:\MyProgram 中，在命令行中执行 a.exe ，会得到提示“ 无法找到程序 a.exe”，为了让系统找到，可以将 D:\MyProgram 路径加入到 PATH 环境变量中，当输入 a.exe 时，操作系统就会从 PATH 所提供的路径中逐个查找，这时就可以找到了。Linux 和 MacOS 具有相似的特性，甚至比 Windows 的功能更丰富。

Python 虚拟环境就是利用这个特性构建的，在激活虚拟环境之时，激活脚本会将当前命令行程序的 PATH 修改为虚拟环境的，这样执行命令就会在被修改的 PATH 中查找，从而避免了原本 PATH 可以找到的命令，从而实现了 Python 环境的隔离。



为了让开发容易区分当前环境是否虚拟环境以及是那个虚拟环境，命令提示符前会加上特殊标记，