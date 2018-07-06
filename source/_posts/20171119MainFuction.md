---
layout: '[default_layout]'   
title: main函数           
date: 2017-11-19 10:47:41  
toc: true                  
tags:                        
- main

categories:                  
- C++

---
# 1、main函数
main函数,又称主函数,是程序执行的起点，main是相对来说的,如同音学理论之主调于泛音,泛音即程序中的除main之外的其他函数，迎合人们的思考方式而生成的而非必定的模式.有主有次，执行起来条清缕析，既可将程序模块化又实现了一个闭合的整体。

main()称之为主函数，是所有程序运行的入口。其余函数分为有参或无参两种，均由main()函数或其它一般函数调用，若调用的是有参函数，则参数在调用时传递。
<!--more-->

# 2、一般形式
    int　main(int argc,char *argv[])//整数类型主函数(整数类型统计参数个数,字符类型*数组指针至字符[])
    {
    //百度百科示例代码......
    }

    int main(void)//整数类型主函数(无类型)
    {
    ...
   do something
    ...
    }
其中char **argv可以写成char *argv[]，两者等价。

# 3、DOS编译运行之GCC和G++
graphics.h是DOS程序的库的头文件，VS2012是不支持的。而且现在几乎没有编译器支持这个了，而且就算支持，编译出来的程序也可能运行不了。

[gcc和g++到底啥关系？](https://www.zhihu.com/question/20940822)

gcc 最开始的时候是 GNU C Compiler, 如你所知，就是一个c编译器。但是后来因为这个项目里边集成了更多其他不同语言的编译器，GCC就代表 the GNU Compiler Collection，所以表示一堆编译器的合集。 g++则是GCC的c++编译器。现在你在编译代码时调用的gcc，已经不是当初那个c语言编译器了，更确切的说他是一个驱动程序，根据代码的后缀名来判断调用c编译器还是c++编译器 (g++)。比如你的代码后缀是*.c，他会调用c编译器还有linker去链接c的library。如果你的代码后缀是cpp, 他会调用g++编译器，当然library call也是c++版本的。

## 编译
- 安装TMD-GCC软件，并配置环境变量。
- 键盘win + r   （ 这里的r是run的意思）
- 输入cmd,回车，你就看到了命令行
- 输入gcc -v       --查看电脑中gcc版本，但我的电脑需要用gcc.exe -v或g++.exe -v。
- g++.exe test.cpp 编译c++文件，使用gcc.exe编译失败。最好使用gcc编译c程序，g++编译c++程序。这样默认生成的程序为a.exe。
- g++exe test.cpp -o test.exe  可以指定生成的执行文件名
- test   直接可以看到运行的结果了，后面也可以增加参数。

>>编译阶段，g++会调用gcc，对于c++代码，两者是等价的，但是因为gcc命令不能自动和C＋＋程序使用的库联接，所以通常用g++来完成链接，为了统一起见，干脆编译/链接统统用g++了，这就给人一种错觉，好像cpp程序只能用g++似的。

## 运行
    //test.c or test.cpp
    #include <string.h>
    #include <stdio.h>
    #include <cstdlib>
    #define pi 3.1415926
    int main(int argc, char **argv)
    {
        if(argc < 2) {
            printf("参数数量不够！需要输入密码！\n");
            printf("USAGE: ./MainFunction [password] [others]\n");
            return 0;
        }
        if(strcmp(argv[1],"pass")!=0)//设置口令的比较
        {
            printf("password error!\n");
            exit(0);
        }
        printf("success\n");
        printf("参数数量为%d\n", argc);
        return 0;
    }

使用DOS命令行运行程序，加入其他参数，如密码、赋值。
- gcc.exe test.cpp -o test.exe
- test pass ok yes

## 问题
当你输入gcc时，之所以你看到了（说明你没有安装编译器或没有配置path路径）：
>>不是内部或外部命令，也不是可运行的程序或批处理文件。

当你输入gcc时，之所以你看到了（你需要使用gcc.exe）：
>>系统找不到指定路径

error: ‘exit’ was not declared in this scope
>>添加#include <cstdlib>

# 4、此外，下面有cd命令的其他用法：

    D:              进入D盘
    C:              进入C盘
    cd myc      --可以进入到名字为myc的目录（必须C盘存在这个文件夹）
    cd..         可以返回上一层目录
    cd\         返回到根目录
    cd d:\myc   进入D盘的名字为myc的目录
    cd /?        查看cd命令的具体用法。

# 5、main函数常用的调试技巧
## 1、ifdef和ifndef
    #define DEBUG
    #ifdef DEBUG
    //do something
    #endif //DEBUG

## 2、计时器
[【C/C++】计时函数比较](https://www.cnblogs.com/dwdxdy/p/3214905.html)
对于方法6-RDTSC指令，FREQUENCY指CPU的频率，查看电脑的信息，你会发现你电脑的处理器CPU。我的是3.6GHz，所以FREQUENCY的值为3.6*10^9。

## 万能头文件
>>#include<bits/stdc++.h>

但也有以下两个缺点：
1、因其包含的头文件的过多，导致程序编译慢.
2、其不属于标准库里面的头文件，只是gcc的内部实现，可移植性不好.

## π取值
>>#define pi arctan(1)*4
