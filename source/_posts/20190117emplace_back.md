---
layout: '[default_layout]'   
title: 新技能GET--emplace_back函数
date: 2019-01-17 13:48:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- C++
- 容器
- Vector
- Emplace_back
- Map

categories:                  
- C/C++

---
[C++11容器中新增加的emplace相关函数的使用](https://blog.csdn.net/fengbingchun/article/details/78670376)
C++11中，针对顺序容器(如vector、deque、list)，新标准引入了三个新成员：emplace_front、emplace和emplace_back，这些操作构造而不是拷贝元素。这些操作分别对应push_front、insert和push_back，允许我们将元素放置在容器头部、一个指定位置之前或容器尾部。
当调用push或insert成员函数时，我们将元素类型的对象传递给它们，这些对象被拷贝到容器中。而当我们调用一个emplace成员函数时，则是将参数传递给元素类型的构造函数。emplace成员使用这些参数在容器管理的内存空间中直接构造元素。
emplace函数的参数根据元素类型而变化，参数必须与元素类型的构造函数相匹配。emplace函数在容器中直接构造元素。传递给emplace函数的参数必须与元素类型的构造函数相匹配。
其它容器中，std::forward_list中的emplace_after、emplace_front函数，std::map/std::multimap中的emplace、emplace_hint函数，std::set/std::multiset中的emplace、emplace_hint，std::stack中的emplace函数，等emplace相似函数操作也均是构造而不是拷贝元素。
emplace相关函数可以减少内存拷贝和移动。当插入rvalue，它节约了一次move构造，当插入lvalue，它节约了一次copy构造。
<!--more-->

# map的遍历

不断的发现以前的自己是个傻逼，这就是人生。
人这一生，其实都在不断找借口好让自己心安理得地活下去。
我出门代步用A8，旅游一般开jeep，但是我最喜欢的还是开玩笑

# map按key排序
在下面的代码里实现。

# map按value排序
```
#include <bits/stdc++.h>
#include <hash_map>
using namespace std;
/*
由于hash_map定义在__gnu_cxx命名空间中，故你必须在使用时限定名字空间__gnu_cxx::hash_map，
或者使用using关键字加一个  using namespace __gnu_cxx;
*/
using namespace __gnu_cxx;

template<typename T>  // auto不能修饰参数
void DISPLAY(T m)
{
    for (auto i : m) {
        cout << i.second << endl;
    }
    for (auto it = m.begin(); it != m.end(); it++) {
        cout << it->first << it->second << endl;
    }
    return;
}

// hash_*系列例如hash_map,hash_set 等已经被废弃了，C++11用unordered_map，unordered_set等来替代
void HASH_MAP()
{
    hash_map<int, string> m;
    m[23] = "helu";
    m[520] = "chengqiqi";
    m[12] = "hejian";
    DISPLAY(m);   // 可以看出默认按照key排序输出
    return;
}

void SORT_KEY()
{
    map<int, string, greater<int> > m;  // 默认是less
    m[23] = "helu";
    m[520] = "chengqiqi";
    m[12] = "hejian";
    DISPLAY(m);
    return;
}

/*
基本思路就是：想直接用sort排序是做不到的，sort只支持数组、vetctor等的排序，所以我们可以先把map装
进pair里，然后再放入vector，自定义sort实现排序。
*/

int main()
{
    HASH_MAP();
    SORT_KEY();
    return 0;
}
```
锤子定律非常简单，可以概括为一句话：当你的脑子里有一个锤子的时候，你会满世界找钉子。
# C++保留两位小数
```c++
#include <iomanip>  //不要忘了头文件
using namespace std;

int main()
{
	//第一种写法
	cout<<setiosflags(ios::fixed)<<setprecision(2);

	//第二种写法
	cout.setf(ios::fixed);
	cout<<setprecision(2);

	//第三种写法
	cout<<fixed<<setprecision(2);
	return 0;
}
```


