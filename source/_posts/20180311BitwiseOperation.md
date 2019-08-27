---
layout: '[default_layout]'   
title: 位运算应用           
date: 2018-03-11 13:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- 位运算

categories:                  
- 数据结构算法

---
# 1、位与(and &)、位或(or |)、按位异或(xor ^)、按位同或()、按位取反(not ~)
`注意：`C语言的按位取反运算，对于符号位同样取反。
101(5)   1011(11)
5 & 11 = 1(1)
5 | 11 = 1111(15)
[按位取反是真的难以理解](http://blog.csdn.net/wangshu214/article/details/51955298)：
0000 0101 -> 1111 1010符号位为1，为负数需要-1 -> 1111 1001 -> 取反得到结果0000 0110(-6)。
~5 = (-6)
0000 1011 -> 1111 0100符号位为1，为负数需要-1 -> 1111 0011 -> 取反得到结果0000 1100(-12)。
~11 = (-12)
<!--more-->
5 ^ 11 = 1110(14)
计算机中的负数是以其补码形式存在的 补码 = 原码取反 + 1。
负数的补码求原码和负数的原码求补码的方法一样:除符号位外，每位求反，末位加一。
100   = 0110 0100（原码）= 0110 0100（补码）
-100 = 1110 0100（原码） = 1001 1100 （补码）
异或 = 1111 1000（补码） =  1000 0111（取反） + 1 = 1000 1000（原码） = -8

同或是一个词汇，“同或”可以是一个数学运算符，应用于逻辑运算。 其运算法则为a同或b=ab+a‘b’（a'为非a），也可以表示其它的含义。
C语言中不提供“同或”运算，似乎只有异或，异或得反就是同或。
5 同或 11 = (1)

# 2、注意跟逻辑与(&&)、逻辑或(||)、逻辑非(!)的区别
# 3、同或的实现
```
//网上同或的程序，有点不是很明白。
#include <iostream>
using namespace std;
int same_or(int perm1,int perm2)
{
    int tmp = perm1 > perm2 ? perm1 : perm2;
    int n=0, refer=~0, value;
    while(tmp>>n) n++;
    refer <<= n;
    tmp = perm1 & perm2;
    cout << tmp << endl;
    cout << perm1 << endl;
    cout << perm2 << endl;
    cout << refer << endl;
    perm1=~(perm1|refer);  //排除perm1高位上无效bit的干扰，如排除0001 1111的前面3个0
    perm2=~(perm2|refer);  //同上
    cout << perm1 << endl;
    cout << perm2 << endl;
    value=perm1&perm2;
    return value|tmp;
}

int main()
{
    int c=same_or(11,5);
    cout<<c<<endl;
    return 0;
}
```

# 4、shl运算<<、shr运算>>
a shl b就表示把a转为二进制后左移b位（在后面添b个0）。
和shl相似，a shr b表示二进制右移b位（去掉末b位），相当于a除以2的b次方（取整）。

# 5、应用一：两个数交换
```
#include <iostream>
using namespace std;

int main()
{
    int a, b;
    cin >> a >> b;
    a = a ^ b;
    b = a ^ b;
    a = a ^ b;
    cout << a << ' ' << b << endl;
    return 0;
}
```

# 6、[应用二：二进制中1的个数](http://blog.csdn.net/peiyao456/article/details/51724099)
假设x是一个32位整数。经过下面五次赋值后，x的值就是原数的二进制表示中数字1的个数。
```
int count_ones(int num)  
{  
    int m_2 = 0x55555555;  
    int m_4 = 0x33333333;  
    int m_8 = 0x0f0f0f0f;  
    int m_16 = 0x00ff00ff;  
    int b = (m_2&num) + ((num >> 1)&m_2);  
    int c = (m_4&b) + ((b >> 2)&m_4);  
    int d = (m_8&c) + ((c >> 4)&m_8);  
    int g = (m_16&d) + ((d >> 8)&m_16);  
    return g;  
}  
```
```
//n不能为负数
int NumberOf1(int n)
{
    int count = 0;
    while(n){
        if(n & 1){
            count++;
        }
        n = n >> 1;
    }
    return count;   
}
```
```
//可以为负数
int NumberOf1(int n)
{
    int count = 0;
    while(n){
        count++;  //只要n不为0则其至少有一个1
        n = n & (n - 1);
    }
    return count;
}
```

# 7、应用三：n皇后问题位运算版
# 8、应用四：快速判断一个数是否是2的幂次方
```
#include <iostream>
using namespace std;

int main()
{
    int num;
    while(cin >> num) {
        if(num & (num - 1)) cout << "no" << endl;
        else cout << "yes" << endl;
    }
    return 0;
}
```

# 9、应用五：计算 1^2^3^4.....^100
[从1异或到N](http://blog.csdn.net/a3630623/article/details/12371727)
综上所述：
f(1, n)  =  f(0, n)  =

   n      n % 4 == 0

   1      n % 4 == 1

   n +1   n % 4 == 2

   0      n % 4 == 3

# 10、利用异或运算去除数组中重复的数
异或运算：一种基于二进制的位运算，特点：同值取0，异值取1.
性质：
交换律： a^b = b^a;
结合律： (a^b)^c = a^(b^c)
对任意的a: a^a = 0; a^0=a; a^(-1) = ~a.

因此，如果有多个数异或，其中由重复的数，不论这些重复的数是否相邻，如果这些数重复了偶数次，则异或后会全部消去；如果重复出现了奇数次，则会保留一个。

这就是理论基础。

题目1：1-1000放在含有1001个元素的数组中，只有唯一的一个元素值重复，其它均只出现一次。每个数组元素只能访问一次，设计一个算法，将它找出来；不用辅助存储空间，能否设计一个算法实现？

题目2：一个数组中只有一个数字出现了一次，其他的全部出现了两次，求出这个数字。
