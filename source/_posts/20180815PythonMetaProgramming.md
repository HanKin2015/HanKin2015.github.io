---
layout: '[default_layout]'   
title: Python中的元编程      
date: 2018-08-15 22:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- Python
- 元编程

categories:                  
- PYTHON

---

# 1、简介
元数据是有关数据的数据，元编程就是编写用于操纵程序的某些程序。人们普遍认为，元程序就是生成其他程序的某些程序，但范式更加广泛。所有旨在自我读取、分析、转换或修改的程序都是元编程的范例。例如：
- 领域特定语言 (DSL)
- 解析器
- 解释器
- 编译器
- 定理证明器
- 术语重写器
<!--more-->
原文：[Python 中的元编程](https://mp.weixin.qq.com/s?__biz=MzUxMTc1NzE2Mw==&mid=2247483995&idx=1&sn=247d1fe63635f0d4f23a97d2eff7216c&chksm=f96f9c5fce181549f03436e4306522f1254a66c19bd0c82918319480692c7e44769fabd5d800&mpshare=1&scene=1&srcid=0815FjNdT1DLl6Qx2BFuozV3&pass_ticket=ONEOJB91HSDDPwB1YPiDZ4t%2F5pfRTKGKbpY%2FuEqM%2FLRB421gt9G%2BgmqvKQwlgt0e#rd)
# 2、元数据
元数据（Metadata），又称中介数据、中继数据，为描述数据的数据（data about data），主要是描述数据属性（property）的信息，用来支持如指示存储位置、历史数据、资源查找、文件记录等功能。元数据算是一种电子式目录，为了达到编制目录的目的，必须在描述并收藏数据的内容或特色，进而达成协助数据检索的目的。都柏林核心集（Dublin Core Metadata Initiative，DCMI）是元数据的一种应用，是1995年2月由国际图书馆电脑中心（OCLC）和美国国家超级计算应用中心（National Center for Supercomputing Applications，NCSA）所联合赞助的研讨会，在邀请52位来自图书馆员、电脑专家，共同制定规格，创建一套描述网络上电子文件之特征。
元数据是关于数据的组织、数据域及其关系的信息，简言之，元数据就是关于数据的数据。

# 3、思考
一切都是对象，而类创建了这些对象。但是，如果一切都是对象（类也是对象），那么谁来创建这些类呢？
```
class SomeClass:
    pass

object = SomeClass()
type(object)

>>>__main__.SomeClass


import inspect
inspect.isclass(SomeClass)
>>>True


inspect.isclass(object)
>>>False


inspect.isclass(type(object))
>>>True


type(SomeClass)
>>>type


inspect.isclass(type(SomeClass))
>>>true


type(type(SomeClass))
>>>type 'type'
type(type(type(SomeClass)))
>>>type 'type'
inspect.isclass(type(type(type(SomeClass))))
>>>True
```

除 type 之外，Python 中的一切都是对象，它们要么是类的实例，要么是元类的实例。


实例是实例化的类，而类是元类的实例。



