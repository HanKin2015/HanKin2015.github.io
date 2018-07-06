---
layout: '[default_layout]'   
title: C++新特性---支持foreach循环语句       
date: 2017-11-15 10:47:41  
toc: true                  
tags:                        
- Sublime

categories:                  
- others

---
# 新特性：支持for(int i : arr)语句
这种有冒号的for循环叫做foreach循环，foreach语句是java5的新特征之一，在遍历数组、集合方面，foreach为开发人员提供了极大的方便。
foreach语句是for语句的特殊简化版本，但是foreach语句并不能完全取代for语句，然而，任何的foreach语句都可以改写为for语句版本。
foreach并不是一个关键字，习惯上将这种特殊的for语句格式称之为“foreach”语句。从英文字面意思理解foreach也就是“for 每一个”的意思。实际上也就是这个意思。
数组和容器都能这样使用。
<!--more-->

```C++
#include <iostream>
#include <bits/stdc++.h>
#define NSIZE 8
using namespace std;

int main()
{
    int arr[] = {11, 12, 13, 14, 15};
    for(int i : arr) {
        cout << i << " " << arr[i - 1] << endl;
    }
    return 0;
}
```

# 新特性遍历和迭代器遍历速度比较
新特性遍历速度明显提高，修改值需要用到地址符号&。
```C++
#include "stdafx.h"
#include <stdio.h>
#include <time.h>
#include <vector>
#include <map>
#include <list>
#include <string>
#include <cstdio>
#include <stdio.h>
#include <string.h>
#include <iostream>
#include <set>
#define DEBUG
using namespace std;

void KO()
{
    clock_t t = clock();
    vector<int> v;
    for (int i = 0; i < 10000000; i++) {
        v.push_back(i);
    }
    printf("TIME: %d ms\n", clock() - t);
    t = clock();
    for (int i : v) {
        if (i > 8888888) {
            cout << i << endl;
            break;
        }
    }
    printf("TIME: %d ms\n", clock() - t);
    t = clock();
    vector<int>::iterator it = v.begin();
    for (; it != v.end(); it++) {
        if (*it > 8888888) {
            cout << *it << endl;
            break;
        }
    }
    printf("TIME: %d ms\n", clock() - t);
    return;
}

#ifdef DEBUG
int main(void)
{
    clock_t t = clock();
    KO();
    printf("\nTIME: %d ms\n", clock() - t);
    return 0;
}
#endif // DEBUG
```
