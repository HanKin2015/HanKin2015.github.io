---
layout: '[default_layout]'   
title: split函数        
date: 2017-12-08 10:47:41  
toc: true                  
tags:                        
- C++
- Split

categories:                  
- C/C++

---
# split函数
split函数是编程语言中使用的一种函数名称，它是指返回一个下标从零开始的一维数组，split函数包含指定数目的子字符串。
Java中的 split  函数是用于按指定字符（串）或正则去分割某个字符串，结果以字符串数组形式返回。
如：    
```C++
String str="1234@abc";  
String[] a = str.split("@");  
System.out.println("处理结果: "+a[0]+","+a[1]);   //输出的是: 处理结果: 1234,abc  
```
但是C++标准库里面没有字符分割函数split。
<!--more-->

# 自己实现split函数
参考：[C++常见问题: 字符串分割函数 split](https://www.cnblogs.com/dfcao/p/cpp-FAQ-split.html)
```C++
void SplitString(const string& s, vector<string>& v, const string& c)
{
    string::size_type pos1, pos2;
    pos2 = s.find(c);
    pos1 = 0;
    while (string::npos != pos2) {
        v.push_back(s.substr(pos1, pos2 - pos1));
        pos1 = pos2 + c.size();
        pos2 = s.find(c, pos1);
    }
    if (pos1 != s.length()) v.push_back(s.substr(pos1));
}
```

# 用C语言中的strtok 函数来进行分割

原型:  char *strtok(char *str, const char *delim);

strtok函数包含在头文件<string.h>中，对于字符数组可以采用这种方法处理。当然也可以将字符数组转换成字符串之后再使用法一。测试代码如下

```C++
#include <string.h>
#include <stdio.h>

int main(){
  char s[] = "a,b*c,d";
  const char *sep = ",*"; //可按多个字符来分割
  char *p;
  p = strtok(s, sep);
  while(p){
    printf("%s ", p);
    p = strtok(NULL, sep);
  }
  printf("\n");
  return 0;
}
//输出: a b c d
```