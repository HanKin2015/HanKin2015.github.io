---
layout: '[default_layout]'   
title: C语言的fgets() 与 gets()           
date: 2017-12-09 17:47:41  
toc: true                  
tags:                        
- C++

categories:                  
- C++

---
没有不喜欢哥哥的，只有不了解他的。
曾经看过一个评论：
张国荣先生，是一个100分的好人。和他的才华相比，他的容貌不值一提；和他的人品相比，他的才华不值一提。

君生我未生，我生君已老。恨不生同时，日日与君好。
与他的才华相比,他的容貌不值一提,与他的人品相比,他的才华不值一提。
<!--more-->

fscanf  是从文件中读取数据，使用之前要打开文件。 scanf 直接从屏幕上读取数据，使用之前不需要打开文件，直接从屏幕上输入数据，然后敲回车即可。

[gets和fgets函数的区别](https://www.cnblogs.com/aexin/p/3908003.html)
# gets
gets函数原型：char*gets(char*buffer);//读取字符到数组：gets(str);str为数组名。

gets函数功能：从键盘上输入字符，直至接受到换行符或EOF时停止，并将读取的结果存放在buffer指针所指向的字符数组中。读取的换行符被转换为null值，做为字符数组的最后一个字符，来结束字符串。

注意：gets函数由于没有指定输入字符大小，所以会无限读取，一旦输入的字符大于数组长度，就会发生内存越界，从而造成程序崩溃或其他数据的错误。

# fgets
fgets函数原型：char *fgets(char *s, int n, FILE *stream);//我们平时可以这么使用：fgets(str, sizeof(str), stdin);其中str为数组首地址，sizeof(str)为数组大小，stdin表示我们从键盘输入数据。

fgets函数功能：从文件指针stream中读取字符，存到以s为起始地址的空间里，知道读完N-1个字符，或者读完一行。

注意：调用fgets函数时，最多只能读入n-1个字符。读入结束后，系统将自动在最后加'\0'，并以str作为函数值返回。

[scanf,fscanf,sscanf的区别----整理](http://blog.csdn.net/liulina603/article/details/12081273)
read :以字节位计算长度,按照指定的长度和次数读取数据,遇到结尾或完成指定长度读取后停止.
fscanf :格式化读取,按照指定的格式串进行读取数据,并将数据初始化为指定的格式.所以在文本方式下才能有效的判断数据内容.
fgets :整行读取,遇到回车换行或结尾停止.在文本方式时使用.

其实文本和二进制的差别就在于读取的数据,文本方式会默认为是ASCII码,二进制方式则原样将数据读出.所以文本时候的格式控制如回车,制表符等,
二进制的时候是不能有效的自动判断的。 

scanf 从控制台输入 
fscanf 从文件输入 
sscanf 从指定字符串输入

# sscanf
1. 常见用法。
char str[512] = {0};
sscanf("123456 ", "%s", str);
printf("str=%s\n", str);

2. 取指定长度的字符串。如在下例中，取最大长度为4字节的字符串。
sscanf("123456 ", "%4s", str);
printf("str=%s\n", str);//str的值为1234

3. 取到指定字符为止的字符串。如在下例中，取遇到空格为止字符串。
sscanf("123456 abcdedf", "%[^ ]", str);//注意^后面有一空格
printf("str=%s\n", str);

4. 取仅包含指定字符集的字符串。如在下例中，取仅包含1到9和小写字母的字符串。
sscanf("123456abcdedfBCDEF", "%[1-9a-z]", str);
printf("str=%s\n", str);

5. 取到指定字符集为止的字符串。如在下例中，取遇到大写字母为止的字符串。
sscanf("123456abcdedfBCDEF", "%[^A-Z]", str);
printf("str=%s\n", str);

