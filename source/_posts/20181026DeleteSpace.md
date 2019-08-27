---
layout: '[default_layout]'   
title: 删除字符串指针中空格和统计文章中的最频繁词
date: 2018-10-26 17:25:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- Char
- 指针
- C
- C++
- 优先队列

categories:                  
- 面试

---
# 指针函数和函数指针的区别
指针函数，简单的来说，就是一个返回指针的函数，其本质是一个函数，而该函数的返回值是一个指针。
函数指针，其本质是一个指针变量，该指针指向这个函数。总结来说，函数指针就是指向函数的指针。

[百度搜索特效：搜索黑洞，屏幕真的出现了黑洞一样的画面](https://baijiahao.baidu.com/s?id=1580218358235866033&wfr=spider&for=pc)

<!--more-->

# 删除字符串指针中空格
- 原始字符串不能是指针字符串，因不能对其本身进行修改
- 必须需要两个指针
- 末尾需置"\0"
```c++
#include <bits/stdc++.h>
using namespace std;

char* DeleteSpace(char* str)
{
    char* p = str, *q = str;
    int len = strlen(str);
    while (*q != '\0') {  // 指针字符串没有"\0"，但char数组有
        if (*q != ' ') {
            *p = *q;
            p++;
        }
        q++;
    }
    *p = '\0';
    return str;
}

int main()
{
    //char* str = "  he jian  ";   // 不能写成指针字符串，指针不能对其值进行修改
    char str[] = "  he jian  ";
    cout << DeleteSpace(str) << endl;
    return 0;
}
```

# assert进行样例调试
- 报错会出现Assertion failed: fun(5) == 6, file C:\Users\Administrator\Desktop\腾讯.cpp, line 41
- 不报错正常运行
```
#include <bits/stdc++.h>
using namespace std;

int fun(int n)
{
    return n;
}

int main()
{
    assert(fun(5) == 6);
    return 0;
}
```

# 统计文章中的最频繁K个词
- hash + 优先队列
- 堆
```
//出现次数最多的是个单词  
void top_k_words()  
{  
    timer t;  
    ifstream fin;  
    fin.open("modern c.txt");  
    if (!fin)  
    {  
        cout<<"can nont open file"<<endl;  
    }  
    string s;  
    hash_map<string,int> countwords;  
    while (true)  
    {  
        fin>>s;  
        if (fin.eof())  
        {  
            break;  
        }  
        countwords[s]++;  
    }  
    cout<<"单词总数 （重复的不计数）:"<<countwords.size()<<endl;  
    priority_queue<pair<int,string>,vector<pair<int,string>>,greater<pair<int,string>>> countmax;  
    for(hash_map<string,int>::const_iterator i=countwords.begin();  
        i!=countwords.end();i++)  
    {  
        countmax.push(make_pair(i->second,i->first));  
        if (countmax.size()>10)  
        {  
            countmax.pop();  
        }  
    }  
    while(!countmax.empty())  
    {  
        cout<<countmax.top().second<<" "<<countmax.top().first<<endl;  
        countmax.pop();  
    }  
    cout<<"time elapsed "<<t.elapsed()<<endl;  
}  
```

# 优先队列
- top
- size
- empty
- push
- pop
```
#include <bits/stdc++.h>
using namespace std;

#include <functional>
void PQueue()
{
    priority_queue<int, vector<int>, greater<int> > Q;   // 按照元素从小到大的顺序出队
    //priority_queue<pair<int,string>,vector<pair<int,string>>,greater<pair<int,string>>> countMax;

    int A[] = {7, 5, 2, 1, 3, 4, 6};
    for (int i = 0; i < 7; i++) {
        Q.push(A[i]);
        int tmp = Q.top();
        cout << tmp << endl;
    }
    return;
}

int main()
{
    PQueue();
    return 0;
}
```
