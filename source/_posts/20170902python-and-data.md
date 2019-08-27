---
layout: '[default_layout]'
title: 利用python进行数据分析
date: 2017-09-02 12:58:41
toc: true
tags:
- Python
- Data
categories: 
- 机器学习
---

在进行多方尝试后，我最后的选择是Anaconda + Pycharm，用anaconda集成的ipython做工作台，做一些分析和小段程序调试的工作，用Pycharm写相应脚本和程序包的开发。这两个工具都是跨平台的，也都有免费版本。

[python操作总结](http://www.icourse163.org/course/BIT-1001872001)
# 利用python进行数据分析
## 20170810
### 第1章 准备工作
cython
python是解释型语言，Java和C++是编译型语言，python慢   
全局解释器锁GIL  
- NumPy（Numerical Python的简称）是python科学计算的基础包  
- pandas（panel data面板数据）提供大量数据结构和函数-----DataFrame  
- matplotlib 绘制数据图表  
- IPython是一个增强的python shell  
- SciPy是一组专门解决科学计算中各种标准问题域的包的集合   

<!-- more -->

在python3.0问世以前，所有的python代码都是向后兼容的   
---
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    from numpy import *
    数据规整munge/munging/wrangling
    伪码pseudocode
    语法糖syntactic sugar
---

### 第2章 引言
bit.ly 
usa.gov

JSON:JavaScript Object Notation,这是一种常用的Web数据格式。
u'New_York'     单引号前面的u表示Unicode（一种标准的字符串编码格式）
$\theta$
$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$
---
    1、\v可以作为转义字符，表示纵向制表符，这里你把后斜杠全部改为前斜杠试试。建议以后凡是路径名中的\，全部改为\\或者/，以避免转义字符的歧义。

    2、'C:\...'前面加r，r'C:\...'
---
python有许多内置或第三方模块可以将JSON字符串转换成Python字典对象。  
DATaFrame是pandas中用于将数据表示为一个表格。  
fillna函数可以替换缺失值（NA），而未知值（空字符串）可以通过布尔型数组索引加以替换。  






