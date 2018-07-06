---
layout: '[default_layout]'   
title: malloc 和 new分配空间           
date: 2018-01-26 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- Sublime

categories:                  
- others

---
# malloc函数
malloc的全称是memory allocation，中文叫动态内存分配，用于申请一块连续的指定大小的内存块区域以void*类型返回分配的内存区域地址，当无法知道内存具体位置的时候，想要绑定真正的内存空间，就需要用到动态的分配内存。
void* 类型表示未确定类型的指针。C,C++规定，void* 类型可以通过类型转换强制转换为任何其它类型的指针。
一般需和free函数配对使用。
<!--more-->
从本质上来说，malloc是libc里面实现的一个函数，如果在source code中没有直接或者间接include过stdlib.h，那么gcc就会报出error：‘malloc’ was not declared in this scope。如果生成了目标文件（假定动态链接malloc），如果运行平台上没有libc（Linux平台，手动指定LD_LIBRARY_PATH到一个空目录即可），或者libc中没有malloc函数，那么会在运行时（Run-time）出错。new则不然，是c++的关键字，它本身不是函数。new不依赖于头文件，c++编译器就可以把new编译成目标代码。

在使用上，malloc 和 new 至少有两个不同: new 返回指定类型的指针，并且可以自动计算所需要大小。


第一、malloc 函数返回的是 void * 类型。
第二、函数的实参为 sizeof(int) ，用于指明一个整型数据需要的大小。
```
int *p = (int*)malloc(sizeof(int) * 100);
//分配可以放得下100个整数的内存空间。
free(p);
p = NULL;/*请加上这句*/
int *parr;
parr = new int[100];
//返回类型为int *类型(整数型指针)，分配大小为sizeof(int) * 100;
```
