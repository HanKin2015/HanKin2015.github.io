---
layout: '[default_layout]'   
title: STL容器之list、vector、map、set、stack、queue、deque                 
date: 2017-10-13 16:58:41  
toc: true                  
tags:                        
- map
- set
- vector

categories:                  
- STL

---
https://www.cnblogs.com/zhaodun/p/6510161.html
[c++中vector的用法详解](http://blog.csdn.net/hancunai0017/article/details/7032383)

## list和vector
- list封装了链表,vector封装了数组, list和vector得最主要的区别在于vector使用连续内存存储的，它支持[]运算符，而list是以链表形式实现的，不支持[]。

- vector对于随机访问的速度很快，但是对于插入尤其是在头部插入元素速度很慢，在尾部插入速度很快。list对于随机访问速度慢得多，因为可能要遍历整个链表才能做到，但是对于插入就快的多了，不需要拷贝和移动数据，只需要改变指针的指向就可以了。另外对于新添加的元素，vector有一套算法，而list可以任意加入。

## map和set
- map,set属于标准关联容器，使用了非常高效的平衡检索二叉树：红黑树，他的插入删除效率比其他序列容器高是因为不需要做内存拷贝和内存移动，而直接替换指向节点的指针即可。
- set和vector的区别在于set不包含重复的数据。set和map的区别在于Set只含有key，而map有一个key和key所对应的value两个元素。
- map和hash_map的区别是hash_map使用了hash算法来加快查找过程，但是需要更多的内存来存放这些hash桶元素，因此可以算得上是采用空间来换取时间策略。

## multiset和multimap
multiset允许里面有重复元素。
multimap所不同的是它允许重复键。这个属性使得 multimap 比预想的要更有用：比如在电话簿中相同的人可以有两个以上电话号码，文件系统中可以将多个符号链接映射到相同的物理文件，或DNS服务器可以将几个URLs映射到相同的IP地址。在这些场合，你可以象下面这样：
```
// 注:伪码
multimap <string, string> phonebook;
phonebook.insert("Harry","8225687"); // 家里电话
phonebook.insert("Harry","555123123"); // 单位电话
phonebook.insert("Harry"," 2532532532"); // 移动电话
```

# vector用法
1.push_back   在数组的最后添加一个数据
2.pop_back    去掉数组的最后一个数据 
3.at                得到编号位置的数据
4.begin           得到数组头的指针
5.end             得到数组的最后一个单元+1的指针
6．front        得到数组头的引用
7.back            得到数组的最后一个单元的引用
8.max_size     得到vector最大可以是多大
9.capacity       当前vector分配的大小
10.size           当前使用数据的大小
11.resize         改变当前使用数据的大小，如果它比当前使用的大，则填充默认值
12.reserve      改变当前vector所分配空间的大小
13.erase         删除指针指向的数据项
14.clear          清空当前的vector
15.rbegin        将vector反转后的开始指针返回(其实就是原来的end-1)
16.rend          将vector反转构的结束指针返回(其实就是原来的begin-1)
17.empty        判断vector是否为空
18.swap         与另一个vector交换数据

    c.push_back(elem);   在容器最后位置添加一个元素elem
    c.pop_back();            删除容器最后位置处的元素
    c.erase(pos)        删除pos位置的数据
    c.at(index);                返回指定index位置处的元素
    c.begin();                   返回指向容器最开始位置数据的指针
    c.end();                      返回指向容器最后一个数据单元的指针+1
    c.front();                     返回容器最开始单元数据的引用
    c.back();                     返回容器最后一个数据的引用
    c.max_size();              返回容器的最大容量
    c.size();                      返回当前容器中实际存放元素的个数
    c.capacity();               同c.size()
     c.resize();                   重新设置vector的容量
    c.reserve();                同c.resize()
    c.erase(p);               删除指针p指向位置的数据，返回下指向下一个数据位置的指针（迭代器）
    c.erase(begin,end)     删除begin,end区间的数据，返回指向下一个数据位置的指针（迭代器）
    c.clear();                    清除所有数据
    c.rbegin();                  将vector反转后的开始指针返回(其实就是原来的end-1)
    c.rend();                     将vector反转后的结束指针返回(其实就是原来的begin-1)
    c.empty();                   判断容器是否为空，若为空返回true，否则返回false
    c1.swap(c2);               交换两个容器中的数据
    c.insert(p,elem);          在指针p指向的位置插入数据elem,返回指向elem位置的指针       
    c.insert(p,n,elem);      在位置p插入n个elem数据，无返回值
    c.insert(p,begin,end) 在位置p插入在区间[begin,end)的数据，无返回值

[如何使用vector的reserve和resize方法](https://blog.csdn.net/linhao19841211_2/article/details/8154805)
reserve用来（预留空间，）改变capacity，不改变size，会去分配内存，但不会构造出对象；如果改变后的capacity比当前capacity大，则capacity会变大；反之，capacity不变。

esize用来改变vector的size，有可能也会改变capacity。如果改变后的size比当前capacity大，则capacity会变大，同时构造出多出来的对象；反之，capacity不变，同时析构一些不再需要的对象。

reserve和resize都不会使capacity变小，但都有可能使capacity变大，具体怎么变大，reserve和resize是不一样的，reserve能准确控制capacity；而resize不能，vc里是每次增大一半的当前capacity。

# deque 即双端队列。
（deque，全名double-ended queue）是一种具有队列和栈的性质的数据结构。双端队列中的元素可以从两端弹出，其限定插入和删除操作在表的两端进行。

