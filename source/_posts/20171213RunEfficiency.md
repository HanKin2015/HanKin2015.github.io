---
layout: '[default_layout]'   
title: C/C++在不同系统和编译器上的运行效率           
date: 2017-12-13 15:47:41  
toc: true                  
tags:                        
- C++

categories:                  
- C++

---
```C++
#include <stdio.h>
#include <time.h>

int main(void)
{
    clock_t t = clock();
    int i = 1;
    double sum = 0;
    for( ; ; ) {
        sum += 1.0 / i;
        //printf("%ld\n",i++);
        i++;
        if(sum >=115.0 )    break;
    }
    printf("\n\n%d\n", clock() - t);
    return 0;
}
```
<!--more-->
# Windows10(4核8逻辑)
- CodeBlocks16.01上.cpp运行21500
- CodeBlocks16.01上.c运行21429
- MicroSoft Visual Studio 2015上.cpp运行39282

# Windows(8核32逻辑)
- MicroSoft Visual Studio 2013上.cpp运行42900

# Centos6.6(32逻辑)
- .cpp运行18170
- .c运行18020
