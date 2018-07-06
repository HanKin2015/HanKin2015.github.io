---
layout: '[default_layout]'   
title: STL list "list iterator not incrementable" [转载]          
date: 2018-02-02 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- list
- c++

categories:                  
- others

---
这几天在vc.net下写一个小东西,涉及到list的使用.程序运行到使用erase删除list中某个元素的时候,会弹出异常对话框,提示的异常为:”list iterator not incrementable”.调试检查半天无果,就特意写了一个小程序测试:
<!--more-->
```
#include<stdio.h>      
#include <iostream>  
#include <list>  
using namespace std;    
int main()    
{    
    list<int> listInt;    
    listInt.push_back(1);    
    listInt.push_back(2);    
    listInt.push_back(3);    
    for (list<int>::iterator iter = listInt.begin(); iter != listInt.end(); ++iter)    
    {    
        if( *iter == 2)    
            listInt.erase(iter);   
    }    
    return 0;    
}  
```
上面貌似简单的程序会抛出同样的异常.为此特意去看一书,看到erase源码,终于明白问题所在.erase中会将迭代器销毁掉.这样在erase之后,iter的指向已经乱了,debug可以看到开始是从1开始的,过后就是负多少了.所以会报错list iterator not incrementable.简单的解决方法是在erase之后直接break出来,就可以了.如果删除操作不至一次,那可以如下:
iter = listInt.erase(iter) ;
iter–;
erase会返回下迭代器,但在for中又会加1,所以,为了遍历的完整性,需要做减1的操作.