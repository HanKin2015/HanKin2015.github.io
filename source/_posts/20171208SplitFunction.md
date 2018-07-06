---
layout: '[default_layout]'   
title: split函数        
date: 2017-12-08 10:47:41  
toc: true                  
tags:                        
- C++
- Split

categories:                  
- C++

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
[C++常见问题: 字符串分割函数 split](https://www.cnblogs.com/dfcao/p/cpp-FAQ-split.html)
```C++
void SplitString(const string& s, vector<string>& v, const string& c)
{
    string::size_type pos1, pos2;
    pos2 = s.find(c);
    pos1 = 0;
    while (string::npos != pos2)
    {
        v.push_back(s.substr(pos1, pos2 - pos1));

        pos1 = pos2 + c.size();
        pos2 = s.find(c, pos1);
    }
    if (pos1 != s.length())
        v.push_back(s.substr(pos1));
}
```

#
size_type:
 
由string类类型和vector类类型定义的类型，用以保存任意string对象或vector对象的长度，标准库类型将size_type定义为unsigned类型
　　string抽象意义是字符串， size（）的抽象意义是字符串的尺寸， string::size_type抽象意义是尺寸单位类型
　　string::size_type它在不同的机器上，长度是可以不同的，并非固定的长度。但只要你使用了这个类型，就使得你的程序适合这个机器。与实际机器匹配。
　　eg:
　　string::size_type从本质上来说，是一个整型数。关键是由于机器的环境，它的长度有可能不同。 例如：我们在使用 string::find的函数的时候，它返回的类型就是 string::size_type类型。而当find找不到所要找的字符的时候，它返回的是 npos的值，这个值是与size_type相关的。假如，你是用 string s; int rc = s.find(.....); 然后判断，if ( rc == string::npos ) 这样在不同的机器平台上表现就不一样了。如果，你的平台的string::size_type的长度正好和int相匹配，那么这个判断会侥幸正确。但换成另外的平台，有可能 string::size_type的类型是64位长度的，那么判断就完全不正确了。 所以，正确的应该是： string::size_type rc = s.find(.....); 这个时候使用 if ( rc == string::npos )就回正确了。
　　st.size()表示st中的字符数量，字符数量的统计是由 1 开始累计计算的，所以字符数量正好比字符串的下标索引数（由 0 开始累计计算）大 1 ，这里的index != st.size();的效果等同于index < st.size();
 
 
size_t
 
size_t不是容器概念。
size_type是容器概念，没有容器不能使用。
见例程：
[cpp] view plain copy
#include<iostream>  
#include<vector>  
using namespace std;  
int main()  
{  
 cout<<" typeid(size_t).name() = "<<typeid(size_t).name()<<endl;  
 cout<<" typeid(vector<int>::size_type).name() = "<<typeid(vector<int>::size_type).name()<<endl;  
  
 return 0;  
}   
 
from:http://blog.sina.com.cn/s/blog_5ff6e6ed0100da4j.html
 
先是看到了在看标准库string时size_type，后来在学习标准库bitset的时候有碰到了size_t，晕啊
先说说是在什么样的机缘巧合下与size_type相遇的吧，O(∩_∩)O
标准库string里面有个函数size，用来返回字符串中的字符个数，具体用法如下：
string st("The expense of spirit/n");
cout << "The size of "<<st<<"is"<<st.size()
     << "characters, including the newline"<<endl;
那么size()这个函数返回的类型到底是什么呢？一定要记住，绝对不是整形，而是size_type类型的，所以千万不要把size的返回值赋给一个int变量。
那么size_type到底是一种什么样的类型呢？
string类类型和许多其他库类型都定义了一些配套类型（companion type）。通过这些配套类型，库类型的使用就能与机器无关。size_type就是这些配套类型中的一种。
size_type被定义为与unsigned型（unsigned int, unsigned long）具有相同的含义，而且可以保证足够大能够存储任意string对象的长度。为而来使用由string类型定义的size_type类型。程序员必须加上作用于操作符来说明所使用的size_type类型是由string类定义的。
我们为什么不适用int变量来保存string的size呢？
使用int变量的问题是：有些机器上的int变量的表示范围太小，甚至无法存储实际并不长的string对象。如在有16位int型的机器上，int类型变量最大只能表示32767个字符的string对象。而能容纳一个文件内容的string对象轻易就能超过这个数字，因此，为了避免溢出，保存一个string对象的size的最安全的方法就是使用标准库类型string：：size_type().
一点注意：虽然是在学习标准库string的时候巧遇了size_type类型，但是，其实vector库也可以定义size_type类型，在vector库中还有一个difference_type类型，该类型用来存储任何两个迭代器对象间的距离，所以是signed类型的。
什么是size_t类型呢？其实本质上和size_type没有多大区别
其实size_t和size_type类似，size_t 类型定义在cstddef头文件中,该文件是C标准库的头文件stddef.h的C++版本.它是一个与机器相关的unsigned类型,其大小足以保证存储内存中对象的大小。用法如下：
bitset<32> bitvec;
size_t sz=bitvec.size();
 另外sizeof操作符的返回值的类型也为size_t哦


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