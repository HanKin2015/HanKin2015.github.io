---
layout: '[default_layout]'   
title: typedef和define、强类型和弱类型的区别      
date: 2017-11-20 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- C/C++
- typedef
- define

categories:                  
- C/C++

---
# 1、ios::sync_with_stdio(false);

<!--more-->

# 2、define x 3宏定义，相当于是常数变量-const
1) #define是预处理指令，在编译预处理时进行简单的替换，不作正确性检查，不关含义是否正确照样带入，只有在编译已被展开的源程序时才会发现可能的错误并报错。例如： 
#define PI 3.1415926 
程序中的：area=PI*r*r 会替换为3.1415926*r*r 
如果你把#define语句中的数字9 写成字母g 预处理也照样带入。 

2）typedef是在编译时处理的。它在自己的作用域内给一个已经存在的类型一个别名，但是You cannot use the typedef specifier inside a function definition。 

3）typedef int * int_ptr; 
与 
#define int_ptr int * 
作用都是用int_ptr代表 int * ,但是二者不同，正如前面所说 ，#define在预处理 时进行简单的替换，而typedef不是简单替换 ，而是采用如同定义变量的方法那样来声明一种类型。也就是说; 

//refer to (xzgyb(老达摩)) 
#define int_ptr int * 
int_ptr a, b; //相当于int * a, b; 只是简单的宏替换 

typedef int* int_ptr; 
int_ptr a, b; //a, b 都为指向int的指针,typedef为int* 引入了一个新的助记符 


这也说明了为什么下面观点成立 
//QunKangLi(维护成本与程序员的创造力的平方成正比) 
typedef int * pint ; 
#define PINT int * 

那么： 
const pint p ;//p不可更改，但p指向的内容可更改 
const PINT p ;//p可更改，但是p指向的内容不可更改。 

pint是一种指针类型 const pint p 就是把指针给锁住了 p不可更改 
而const PINT p 是const int * p 锁的是指针p所指的对象。 

3）也许您已经注意到#define 不是语句 不要在行末加分号，否则 会连分号一块置换。

# 3、总结
#define 没有参加编译，在预处理的时候就被替换掉了。
typedef参加编译和链接。
typedef是重命名，可以为枚举结构体等等重新命名，提高代码整洁。

别用typedef了，c++11提供了新的关键字，using AAA = int  ，define也尽量少用

# 5、强类型和弱类型
强类型指的是程序中表达的任何对象所从属的类型都必须能在编译时刻确定。常见的强类型语言有C++、Java、Apex和Python等。强类型语言在大规模信息系统开发中具有巨大优势。

弱类型语言也称为弱类型定义语言。与强类型定义相反。像vb，php等就属于弱类型语言·

# 6、宏定义 #define 和常量 const 的区别
## 类型和安全检查不同

宏定义是字符替换，没有数据类型的区别，同时这种替换没有类型安全检查，可能产生边际效应等错误；

const常量是常量的声明，有类型区别，需要在编译阶段进行类型检查

## 编译器处理不同

宏定义是一个"编译时"概念，在预处理阶段展开，不能对宏定义进行调试，生命周期结束与编译时期；

const常量是一个"运行时"概念，在程序运行使用，类似于一个只读行数据

## 存储方式不同

宏定义是直接替换，不会分配内存，存储与程序的代码段中；

const常量需要进行内存分配，存储与程序的数据段中

## 定义域不同
```
void f1 ()
{
    #define N 12
    const int n 12;
}
void f2 ()
{
    cout<<N <<endl; //正确，N已经定义过，不受定义域限制
    cout<<n <<endl; //错误，n定义域只在f1函数中
}
```
## 定义后能否取消

宏定义可以通过#undef来使之前的宏定义失效

const常量定义后将在定义域内永久有效
```
void f1()
{
  #define N 12
  const int n = 12;

  #undef N //取消宏定义后，即使在f1函数中，N也无效了
  #define N 21//取消后可以重新定义
}
```
## 是否可以做函数参数

宏定义不能作为参数传递给函数

const常量可以在函数的参数列表中出现

```
1.const 定义常量之后，是不能够改变的

2.宏定义是可以取消的

定义： #define    N    21
取消： #undef    N    12

const限定符定以后是不可以改变的，所以在定义时必须赋初始值，要不然是错误的，除非这个变量是用extern修饰的外部变量。 例如：

const int A=10;       //正确。
const int A;          //错误，没有赋初始值。
extern const int A;   //正确，使用extern的外部变量。
```





