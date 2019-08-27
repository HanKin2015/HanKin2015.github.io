---
layout: '[default_layout]'   
title: C/C++的读取文件内容和python启动另一个py文件
date: 2019-02-23 21:48:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true
mathjax: true

tags:                        
- DBLP
- 数据集

categories:                  
- 园园工作室

---
# C语言的文件操作
模式	|描述
:------|:-------
r|	打开一个已有的文本文件，允许读取文件。
w|	打开一个文本文件，允许写入文件。如果文件不存在，则会创建一个新文件。在这里，您的程序会从文件的开头写入内容。如果文件存在，则该会被截断为零长度，重新写入。
a|	打开一个文本文件，以追加模式写入文件。如果文件不存在，则会创建一个新文件。在这里，您的程序会在已有的文件内容中追加内容。
r+|	打开一个文本文件，允许读写文件。
w+|	打开一个文本文件，允许读写文件。如果文件已存在，则文件会被截断为零长度，如果文件不存在，则会创建一个新文件。
a+|	打开一个文本文件，允许读写文件。如果文件不存在，则会创建一个新文件。读取会从文件的开头开始，写入则只能是追加模式。
如果处理的是二进制文件，则需使用下面的访问模式来取代上面的访问模式：
>"rb", "wb", "ab", "rb+", "r+b", "wb+", "w+b", "ab+", "a+b"


# C++的文件操作
参考地址：https://www.cnblogs.com/yongpan/p/8026489.html

格式	| 用途
:--|:--
ios::in|	以输入方式打开文件
ios::out|	以输出方式打开文件，如果文件不存在则新建，如果文件存在就将其原有内容全部清空
ios::app|	输出的数据追加到文件末尾
ios::ate|	打开一个文件，并将指针定位到文件末尾
ios::trunc|	打开一个文件，如果文件不存在则新建，如果存在，则清空原有文件中的内容
ios::binary|	以二进制方式打开文件，如果不指定则默认采用文本方式打开文件
ios::in | ios::out|	以输出和输入方式打开文件
ios::in | ios::binary|	以输入方式打开一个二进制文件
ios::out| ios::binary|	以输出方式打开一个二进制文件






# python启动另一个py文件
最简单的方法：

import os
os.system("python filename")
filename最好是全路径+文件名；

其他方法：

execfile('xx.py')，括号内为py文件路径；

如果需要传参数，就用os.system()那种方法；

如果还想获得这个文件的输出，那就得用os.popen（）；

```
import os

#os.system('python testB.py')
#os.system('python testC.py')
#execfile('./testB.py')  python3中淘汰
exec(open('./testB.py', encoding = 'utf-8').read())
exec(open('./testC.py', encoding = 'utf-8').read())
```
https://tianchi.aliyun.com/notebook-ai/?spm=5176.12281988.0.0.30674dd1bSompw
https://tianchi.aliyun.com/forum/postDetail?spm=5176.12281988.0.0.30674dd1bSompw&postId=3192
https://blog.csdn.net/ArrowYL/article/details/81094837
gcc, g++编译时消除特定警告的方法](https://blog.csdn.net/li_wen01/article/details/71171413)


