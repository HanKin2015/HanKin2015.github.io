---
layout: '[default_layout]'   
title: SNAP Practice                  
date: 2017-10-14 21:36:41  
toc: true                  
tags:                        
- SNAP
- Stanford 
- Network

categories:                  
- Social Network

---
[官方教程](http://snap.stanford.edu/proj/snap-icwsm/SNAP-ICWSM14-part5.pdf)

# 安装
- [SNAP 4.0](http://snap.stanford.edu/releases/Snap-4.0.zip) (2017年7月27日)
- [Gnuplot](http://www.gnuplot.info/)，绘图和绘图包，用于绘制网络的结构属性（如度数分布）;
- [Graphviz](http://www.graphviz.org/)是绘图和可视化小图所需的绘图包;
- [NodeXL](http://nodexl.codeplex.com/)，一个将网络分析和SNAP集成到Microsoft Office和Excel中的图形前端。它允许没有编程技能的用户使用SNAP。

# 设置PATH环境变量
设置系统PATH变量，以便Gnuplot和Graphviz可用，或将可执行文件放在工作目录中。

<!--more-->

# SNAP程序编译
确保在系统上安装了带有C ++编译器的GCC包。

在主SNAP目录中运行“make all”。这将编译核心SNAP库和所有应用示例。

对于其他平台，请修改主SNAP目录中的Makefile.config。

# 'make'不是内部或外部命令，也不是可运行的程序或批处理文件，
如果用的是windows的mingw平台， 用 mingw32-make命令而不是书上讲的make命令, 构建可执行文件。然后从dos进入debug文件夹，直接输入可执行文件名（不包含后缀）

mingw32-make就是mingw提供的工具，实现linux下的make。
直接双击当然不行，你把用到的dll文件拷贝在.exe同一个文件夹里再试试

# 第一次尝试
Linux下有make命令，windows10安装了TDD-GCC编译器，直接使用mingw32-make命令编译失败。 
发现SNAP应该只能在Mac OS X，Linux直接编译，但在Windows上使用必须Cygwin虚拟机，即unix环境。
![](http://images.cnblogs.com/cnblogs_com/hankin2017/1078394/o_snap%20make%20err.png)

# 第二次尝试SNAP在Windows与Visual Studio
## Installation on Windows
- Install Visual Studio or Visual Studio Express
- Download and Unzip Snap package
- Go to subfolder examples
- Open project SnapExamples*.sln
    Visual Studio 2008 and 2010 projects are available

## VS:Creating New Project
1. Open Visual Studio and create a project Or start with examples/testgraph and modify it.
2. Include Snap.h in your main program #include “Snap.h”.
3. Include the path to directories “snap-core”, “glib-core” and “snap-adv” in your project.
右键单击项目   

> Properties(属性) -> Configuration Properties(配置属性) -> VC++ Directories(VC++目录) -> Include Directories(包含目录)

4. Character set must be configured to Multi-Byte: 
右键单击项目

> Properties(属性) -> Configuration Properties(配置属性) -> General(常规) -> Projects Defaults(项目默认值) ->  Character Set(字符集) -> Select “Use MultiByte Character Set”(选择“使用多字节字符集”)

配置Visual Studio与SNAP一起使用，需要将字符集设置为多字节，并指定SNAP包含目录的位置。

- 要将字符集设置为多字节，请右键单击项目，转到属性 - > 配置属性 - > 常规 - > 项目默认值 - > 字符集 - > 选择“使用多字节字符集“。

- 要指定SNAP包含目录的位置，请转到选项 - > 首选项 - > C ++目录 - > 包含目录，并将系统上的路径添加到SNAP文件夹glib-core，snap-core和snap-adv。

## 然而事情并没有那么简单！！！
### bug1:无法查找或打开pdb文件
运行程序后闪退！
在return 0前加一行代码，system("pause");重新编译运行即可。

### bug2:错误  C1083   无法打开包括文件: “Snap.h”: No such file or directory
解决方法：将SNAP文件夹glib-core，snap-core和snap-adv的路径添加到项目系统上。

### bug3:错误  LNK2019 无法解析的外部符号 
"int __cdecl gettimeofday(struct timeval *,struct timezone *)" (?gettimeofday@@YAHPAUtimeval@@PAUtimezone@@@Z)，该符号在函数 "double __cdecl `anonymous namespace'::WallClockTime(void)" (?WallClockTime@?A0x1244efcf@@YANXZ) 中被引用      

这个问题很严重，因为阿丁同学也遇到了这个问题。在查看了snap-4.0中的example程序，运行后毫无问题，完美运行。仔细查看，发现缺少了snap.cpp文件和snap.h文件。
右键单击项目->添加->现有项
其实这样就基本OK了，但我的程序又出现了其他的BUG。

### BUG4:错误  C4996   'fopen': This function or variable may be unsafe. 
Consider using fopen_s instead. To disable deprecation, use _CRT_SECURE_NO_WARNINGS. See online help for details. snap-4.0\glib-core\bd.cpp   56  

右键单击项目-属性-配置属性-C/C++-预处理器-预处理器定义-编辑-预处理器定义：
添加一句命令：_CRT_SECURE_NO_WARNINGS

### bug5:错误  C4996   'putenv': The POSIX name for this item is deprecated.
 Instead, use the ISO C and C++ conformant name: _putenv. See online help for details. TestSNAP2   c:\users\administrator\desktop\communitynetwork\snap-4.0\glib-core\env.cpp  289 

这个问题在VS 2012之前的版本中是不会当做错误的，只是提出一个警告。为了避免报错，可以使用以下两个宏定义来屏蔽掉这种错误。

    #define _CRT_SECURE_NO_DEPRECATE 1
    #define _CRT_NONSTDC_NO_DEPRECATE 1

也可以在预处理器定义中添加两句命令：
_CRT_SECURE_NO_DEPRECATE
_CRT_NONSTDC_NO_DEPRECATE

### BUG6：错误  C4700   使用了未初始化的局部变量“ct”  snap-4.0\snap-core\sim.cpp  209 
郁闷，官网自己写的程序也有这种错误。
修改 int ct = 0;
好奇怪，我查看了snap-4.0\testgraph\sim.cpp 209，它里面就已经初始化为0，不会报错。

