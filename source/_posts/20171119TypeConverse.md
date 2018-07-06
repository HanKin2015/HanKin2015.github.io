---
layout: '[default_layout]'   
title: C++中常见的类型转换           
date: 2017-11-15 10:47:41  
toc: true                  
tags:                        
- C++
- String
- Int
- Char

categories:                  
- C++

---
# 1、C语言类型强制转换 
强制类型转换是通过类型转换运算来实现的。其一般形式为： （类型说明符） (表达式) 其功能是把表达式的运算结果强制转换成类型说明符所表示的类型。
 如果一个运算符两边的运算数类型不同，先要将其转换为相同的类型，即较低类型转换为较高类型，然后再参加运算，转换规则如下图所示。

<!--more-->

```C++
double ←── float 高
↑
long
↑
unsigned
↑
int ←── char,short 低
```
<!--more-->

# 2、string转char[], char转string
```C++
#include <sstream>
char c;
string str;
stringstream stream;
stream << c;
str = stream.str();
```
我觉得也可以直接str[0] = c或者str += c。

# 3、string和char*的转换
## string转char*
主要有三种方法可以将str转换为char*类型，分别是：data(); c_str(); copy();
1.data()方法，如：

    1 string str = "hello";
    2 const char* p = str.data();//加const  或者用char * p=(char*)str.data();的形式

同时有一点需要说明，这里在devc++中编译需要添加const，否则会报错invalid conversion from const char*  to char *，这里可以再前面加上const或者在等号后面给强制转化成char*的类型。

下面解释下该问题，const char*是不能直接赋值到char*的,这样编译都不能通过,理由:假如可以的话,那么通过char*就可以修改const char指向的内容了,这是不允许的。所以char*要另外开辟新的空间，即上面的形式。

2.c_str()方法，如：

    1 string str=“world”;
    2 const char *p = str.c_str();//同上，要加const或者等号右边用char*

3.copy()方法，如：

    1 string str="hmmm";
    2 char p[50];
    3 str.copy(p, 5, 0);//这里5代表复制几个字符，0代表复制的位置，
    4 *(p+5)=‘\0’;//注意手动加结束符！！！

## char * 转string。
可以直接赋值，相当于char*为char[]。

    1 string s;
    2 char *p = "hello";//直接赋值
    3 s = p;

# 4、int和string的转换
[C++ int与string的转化](https://www.cnblogs.com/nzbbody/p/3504199.html)

## ftoa：浮点数强制成字符串。
这个不是C标准库中的函数，而是Windows平台下扩展的，标准库中有sprintf，功能比这个更强，用法跟printf类似。
```C++
// crt_sprintf.c
// compile with: /W3
// This program uses sprintf to format various
 
//data and place them in the string named buffer.
// 程序使用sprintf 将各种数据格式化后置于字符数组buffer中
#include <stdio.h>
int main( void )
 
{
   char  buffer[200], s[] = "computer", c = 'l';
   int   i = 35, j;
   float fp = 1.7320534f;
   // 格式化并打印各种数据到buffer
   j  = sprintf( buffer,    "   String:    %s\n", s ); // C4996
   j += sprintf( buffer + j, "   Character: %c\n", c ); // C4996
   j += sprintf( buffer + j, "   Integer:   %d\n", i ); // C4996
   j += sprintf( buffer + j, "   Real:      %f\n", fp );// C4996
    
   printf( "Output:\n%s\ncharacter count = %d\n", buffer, j );
}
```

## atof 
atof()，是C 语言标准库中的一个字符串处理函数，功能是把字符串转换成浮点数，所使用的头文件为<stdlib.h>。该函数名是 “ascii to floating point numbers” 的缩写。语法格式为：double atof(const char *nptr)。
```C++
#include<stdlib.h>
int main()
{
char*a="-100.23";
char*b="200e-2";
doublec;
c=atof(a)+atof(b);
printf(“c=%.2lf\n”,c);
return 0;
}
```

## atoi
atoi (表示 ascii to integer)是把字符串转换成整型数的一个函数，应用在计算机程序和办公软件中。atoi( ) 函数会扫描参数 nptr字符串，跳过前面的空白字符（例如空格，tab缩进）等。
可以通过isspace( )函数来检测），直到遇上数字或正负符号才开始做转换，而在遇到非数字或字符串结束时('\0')才结束转换，并将结果返回。如果 nptr不能转换成 int 或者 nptr为空字符串，那么将返回 0 。
```C++
//vs2013里调用printf函数请使用预处理命令#define _CRT_SECURE_NO_WARNINGS
#include <stdlib.h>
#include <stdio.h>
 
int main(void)
{
    int n;
    char *str = "12345.67";
    n = atoi(str);
    printf("n=%d\n",n);
    return 0;
}
```

## itoa 
itoa是广泛应用的非标准C语言和C++语言扩展函数。由于它不是标准C/C++语言函数，所以不能在所有的编译器中使用。但是，大多数的编译器（如Windows上的）通常在<stdlib.h>/<cstdlib>头文件中包含这个函数。
```C++
#include <stdlib.h>
#include <stdio.h>
int main(void)
{
    int number=12345;
    char string[25];
    itoa(number, string, 10);//按十进制转换
    printf("integer = %dstring = %s\n", number, string);
    itoa(number, string, 16);//按16进制转换
    printf("integer = %dstring = %s\n", number, string);
    return 0;
}
```


