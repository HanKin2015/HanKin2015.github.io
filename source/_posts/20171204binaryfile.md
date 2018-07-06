---
layout: '[default_layout]'   
title: 二进制文件的读取和存储           
date: 2017-12-25 10:47:41  
toc: true                  
tags:                        
- 二进制

categories:                  
- others

---
不敢去玩，不敢偷懒，不敢生病，每天抬头是黑夜，低头是白天，天天造出晚归，蓬头垢面，变丑变胖。

严重性 代码  说明  项目  文件  行   禁止显示状态
错误  C4996   'fopen': This function or variable may be unsafe. Consider using fopen_s instead. To disable deprecation, use _CRT_SECURE_NO_WARNINGS. See online help for details. Acm f:\vs\acm\acm\生成数据集.cpp 35  


在函数中，先将1左移7位，就可以得到二进制值10000000，再将此值与一个字符“按位与”，然后判断其值是否为0。不为0就输出1，否则就输出0。类似的操作做8次，就可以输出一个字节的8位二进制码了。
<!--more-->
[C++读写二进制文件](http://blog.csdn.net/lightlater/article/details/6364931)
[用C++程序理解汉字的机内码表示](http://blog.csdn.net/sxhelijian/article/details/24498045)
唱歌不好听的人怎么学好唱歌？

```
//dataset.txt
i厉害
love
you
这里随便写。
```

```C++
#include "stdafx.h"
#include <cstdio>
#include <stdio.h>
#include <string.h>
#define NSIZE  8

/***********文本文件转二进制**********/
void Text2Bin(const char* sIn, const char* sOut) {
    char a[255];
    int count = 0;
    int ch;
    for (int i = 0; i < 255; i++) a[i] = '\0';  //初始化，将文本文件存储
    FILE* fin = fopen(sIn, "r");
    FILE* fout = fopen(sOut, "w");
    for (int i = 0; i < 255; i++) fscanf(fin, "%c", &a[i]);
    for (int k = 0; k < 255 && a[k] != '\0'; k++)
    {
        ch = a[k];
        for (int a = 7; a >= 0; a--) fprintf(fout, "%d", ch >> a & 1);
    }
    fclose(fin);
    fclose(fout);
    return;
}

/***********二进制文件转文本文件**********/
void Bin2Text(const char* sIn, const char* sOut) {
    FILE* fin = fopen(sIn, "r");
    FILE* fout = fopen(sOut, "w");
    char str[255 * 8];
    for (int i = 0; i < 255; i++) str[i] = '\0';
    int i = 0, j = 0, iTemp = 0, flag = 0;
    int  ibina[NSIZE];
    char cRead[NSIZE];
    char cChar;
    for (int a = 0; a < 255; a++) fscanf(fin, "%c", &str[a]);
    while (str[flag] != '\0') {
        for (int b = flag; b >= flag && b < flag + NSIZE; b++) {
            //printf("%d",b%8);
            cRead[b % 8] = str[b];
            //printf("%c",cRead[b%8]);
        }
        for (i = 0; i < NSIZE; i++) {
            ibina[i] = (cRead[i] - '0');
        }
        iTemp = 1;
        cChar = 0;
        for (j = 7; j >= 0; j--)
        {
            //printf("%c",ibina[j]);
            //printf("%d\n",cChar);
            cChar += ibina[j] * iTemp;
            iTemp *= 2;
        }
        printf("%c", cChar);
        fprintf(fout, "%c", cChar);
        flag = flag + 8;
    }
    fclose(fin);
    fclose(fout);
    return;
}

int main() {
    Text2Bin("dataset.txt", "da1.txt");
    Bin2Text("da1.txt", "da2.txt");
    printf("\nSuccessfully converted file!\n");
    return 0;
}
```