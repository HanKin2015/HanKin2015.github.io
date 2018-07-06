---
layout: '[default_layout]'   
title: 类中的虚函数、纯虚函数和普通函数           
date: 2018-03-24 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- C/C++

categories:                  
- C/C++

---
参考：[C++虚函数与纯虚函数的区别](https://www.cnblogs.com/fzhe/archive/2013/01/02/2842513.html)
[C++ 在继承中虚函数、纯虚函数、普通函数，三者的区别](https://www.cnblogs.com/xudong-bupt/p/3570304.html)

# 1、什么是虚函数？

C++的虚函数主要作用是“运行时多态”，父类中提供虚函数的实现，为子类提供默认的函数实现。子类可以重写父类的虚函数实现子类的特殊化。

那些被virtual关键字修饰的成员函数，就是虚函数。虚函数的作用，用专业术语来解释就是实现多态性（Polymorphism），多态性是将接口与实现进行分离；用形象的语言来解释就是实现以共同的方法，但因个体差异而采用不同的策略。
<!--more-->
虚函数声明如下：virtual ReturnType FunctionName(Parameter)；

虚函数必须实现，如果不实现，连接器器将报错，错误提示为：

>error LNK****: unresolved external symbol "public: virtual void __thiscall
ClassName::virtualFunctionName(void)"

# 2、为什么要用纯虚函数？

在很多情况下，基类本身生成对象是不合情理的。例如，动物作为一个基类可以派生出老虎、孔雀等子类，但动物本身生成对象明显不合常理。为了解决这个问题，方便使用类的多态性，引入了纯虚函数的概念，将函数定义为纯虚函数（方法：virtual ReturnType Function()= 0;），则编译器要求在派生类中必须予以重写以实现多态性。同时含有纯虚拟函数的类称为抽象类，它不能生成对象。

C++中包含纯虚函数的类，被称为是“抽象类”。抽象类不能使用new出对象，只有实现了这个纯虚函数的子类才能new出对象。
>报错error: invalid new-expression of abstract class type 'A'|

C++中的纯虚函数更像是“只提供申明，没有实现”，是对子类的约束，是“接口继承”。
C++中的纯虚函数也是一种“运行时多态”。

```
//纯虚函数在虚函数后面加了=0。
#include <iostream>
using namespace std;

class A
{
public:
    virtual void out1() = 0;  //由子类实现
    virtual ~A(){};
    virtual void out2() { //默认实现
        cout<<"A(out2)"<<endl;
    }
    void out3() {   //强制实现
        cout<<"A(out3)"<<endl;
    }
};

class B: public A
{
public:
    virtual ~B() {};
    void out1() {
        cout<<"B(out1)"<<endl;
    }
    void out2() {
        cout<<"B(out2)"<<endl;
    }
    void out3() {
        cout<<"B(out3)"<<endl;
    }
};

int main()
{
    A* a = new A;  //这样会new失败

    A *ab=new B;
    ab->out1();
    ab->out2();
    ab->out3();
    cout<<"************************"<<endl;
    B *bb=new B;
    bb->out1();
    bb->out2();
    bb->out3();

    delete ab;
    delete bb;
    return 0;
}
```

# 3、语法规范
- 在类成员方法的声明（不是定义）语句前面加个单词：virtual，她就会摇身一变成为虚函数。

- 在虚函数的声明语句末尾中加个 =0 ，她就会摇身一变成为纯虚函数。

- 子类可以重新定义基类的虚函数，我们把这个行为称之为复写（override）。

- 不管是虚函数还是纯虚函数，基类都可以为提供他们的实现（implementation），如果有的话子类可以调用基类的这些实现。

- 子类可自主选择是否要提供一份属于自己的个性化虚函数实现。

- 子类必须提供一份属于自己的个性化纯虚函数实现。

[超级详细的虚函数和纯虚函数以及经典多态场景](https://mp.weixin.qq.com/s?__biz=MzAxNzYzMTU0Ng==&amp;mid=2651289202&amp;idx=1&amp;sn=431ffd1fae4823366a50b68aed2838d4&amp;chksm=80114627b766cf31f72018ef5f1fe29591e9f6f4bd72018e7aea849342ca6f0a271fb38465ae#rd)
类如果不提供虚函数的实现，那就会自动调用基类的缺省方案。而子类如果不提供纯虚函数的实现，则编译将会失败。




