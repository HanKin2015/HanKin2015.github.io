---
layout: '[default_layout]'   
title: 精通Linux/Unix平台上的C/C++编程        
date: 2018-03-15 21:06:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- 网络编程
- Linux
- C/C++

categories:                  
- C++研发工程师

---
# 1、Linux中的基础知识
## 编辑器
emacs----编辑器之神
vim----神的编辑器
vim 是vi的升级版本，它不仅兼容vi的所有指令，而且还有一些新的特性在里面。

### shell （计算机壳层）
在计算机科学中，Shell俗称壳（用来区别于核），是指“提供使用者使用界面”的软件（命令解析器）。它类似于DOS下的command.com和后来的cmd.exe。它接收用户命令，然后调用相应的应用程序。

## 安装软件
>sudo apt-get update  更新安装包资源的下载地址（建议安装软件前更新一下）
### sudo
sudo是linux系统管理指令，是允许系统管理员让普通用户执行一些或者全部的root命令的一个工具，如halt，reboot，su等等。这样不仅减少了root用户的登录 和管理时间，同样也提高了安全性。sudo不是对shell的一个代替，它是面向每个命令的。
<!--more-->

## cc （cc 编译器）
linux下cc和gcc是同一个东西. cc 是 unix 上 C 编译器 传统 名字。linux 仿 unix，你可以用 名字 cc . linux 上 C 编译器 就是 GNU C 编译器 gcc。 unix 上 可以另装 gcc， 但 unix 自带的 cc 编译器 不是 gcc。cc是以前在unix上的编译器，gcc是GNU组织开发的编译器，功能和cc相同，甚至更强大。

## vim命令
/*使用touch命令可以创建一个空文本文件*/
ndd 删除当前及以下n行
a 光标后插入  shift + a 末尾插入
i 光标前插入   shift + i 首部插入
o 光标下行插入  shift + o 光标上行插入
:set nu 显示行号
:sp 文件名      vim支持多个文件窗口编写
ctrl + w + 下箭头 切换文件窗口
ndd  可以删除n行，会把文件内容放到剪切版，再按p就可以粘贴回来
:wqa  保存退出全部文件

## include中<>会在标准库中查找，“”会在当前目录下查找（引号中可以写.c文件名）

## 头文件产生的原因
```
项目比较大的时候，提前把一些不常改动的源代码编译成.o文件，变成静态库，这样可以节省后来编译的时间。
把函数预先编译成静态库文件（编译而不执行），在其它函数中调用速度更快
gcc -c 文件名 -o 文件名  //编译为静态库文件，扩展名一般为 .o
gcc -c xx.c -o xx.o(将xx先编成机器语言静态库文件不可执行)
gcc xx.c -o xx.out(直接翻译成机器语言可执行xx.out)
./xx.out(执行本地可执行文件)
cat xx.xx(直接显示文件内容)
gcc -c min.c -o min.o
参数：
-c 编译文件，产生obj文件
-o 制定编译后的文件名
```

# 2、关于C/C++
## 完整的main函数，可以和系统交互的
```
#include <stdio.h>

int main(int argv, char* argc[])
{
    printf("hello world \n");
    return 0;
}
```
argv是传入参数的数量，默认是文件名，所以是1。
argc[]里面存储的传入参数的详细。
98标准里面不能再for循环里初始化变量。

## gcc语句直接执行
>gcc main.c -o main.out && ./main.out

## 检查是否成功执行
>echo $?    成功返回0，失败返回1
其中为啥返回0呢？？因为return 0。注意 命令1 && 命令2，只有命令1返回0才执行命令2，所以main函数返回0是有它的道理。

[echo命令详解](http://www.runoob.com/linux/linux-shell-echo.html)

# 3、标准输入流、输出流、错误流
stdio.h提供
stdin标准输入流
stdout标准输出流
stderr标准错误
scanf(...)实际是fscanf(stdin,...);
printf(...)实际是fprintf(stdout,...);
输出错误实际是fprintf(stderr,...);

标准输入是程序可以读取其输入的位置。缺省情况下，进程从键盘读取 stdin 。
标准输出是程序写入其输出的位置。缺省情况下，进程将 stdout 写到终端屏幕上。
标准错误是程序写入其错误消息的位置。缺省情况下，进程将 stderr 写到终端屏幕上。
fscanf(stdin(或文件名),"%d",&a);//从文件读取数据
fprintf(stdout(或文件名),"%d",a);//将数据写入文件

# 4、重定向
`>>` 输出流重定向符号，把显示在屏幕上的内容重定向到文件中，内容会添加到文件的末尾，即不会覆盖。
如：ls /etc >> etc.txt  会把etc文件夹下的内容保存到文件中
`>`也是输出流重定向，不过会覆盖原文件内容，每次都是最新的。
`1>>` 和 `>>`是等价的。前面也可以写2，或许是多个重定向id。

`<`输入流重定向符号。

错误流规定返回的值不能为0。

# 6、管道原理
>ls /etc/ | grep ab 
|是管道符号，grep是搜索命令，显示包含ab的内容

>ps  -e 显示进程命令
ps -e | grep ssh  显示包含ssh的进程

管道把多个小工具拼接起来形成另外一个工具。
>./input.o  |  ./avg.o
input.o程序是输入多个数，输出和和数量，即sum，n。
avg.o程序是输入两个数，计算商，输出商值。
利用管道就可以把两个程序进行合并。

# 7、C语言判断相等的语句把数字放在前面，例如if（1==len）的作用是什么？？
防止由于书写错误而引起的错误，比如1=len，书写的时候少写了一个等号，则len=1就认为是赋值操作，没有问题，但是1=len就会报错了。

赋值语句成功返回的值为1。




