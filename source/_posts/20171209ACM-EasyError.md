---
layout: '[default_layout]'   
title: 刷题中的易错点           
date: 2017-12-09 21:47:41  
toc: true                  
tags:                        
- C++

categories:                  
- ACM

---
# 易错1：sqrt函数
```C++
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int tmp = sqrt(6);
    if(tmp * tmp == 6) cout << "6666666" << endl;       //这种方法可取
    //这种方式在本地可能编译成功，但在有些编译环境可能会永远成立，即把sqrt返回的值当作double类型
    if(sqrt(6) * sqrt(6) == 6) cout << "6666666" << endl;   
    return 0;
}
```
<!--more-->

# 易错点2：递归参数中的+1
```C++
#include <iostream>
using namespace std;

void Sum(int arr[], int tag, int &sum, int n) {
    if(tag > 3) return;
    if(n > 4) return;
    sum += arr[tag];
    //tag使用++，但值没有传递过去，一直都是0，所以输出是5；如果tag使用+1，输出则是10
    Sum(arr, tag++, sum, n + 1);
    return;
}

int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6}, sum = 0;
    Sum(arr, 0, sum, 0);
    cout << sum << endl;
    return 0;
}
```

# 易错点3：pow函数的使用
原型：在TC2.0中原型为extern float pow(float x, float y); ，而在VC6.0中原型为double pow( double x, double y );
头文件：math.h/cmath(C++中)
功能：计算x的y次幂。
返回值：x不能为负数且y为小数，或者x为0且y小于等于0，返回幂指数的结果。
返回类型：double型，int，float会给与警告！
```C++
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    for(int i = 2; i < 1000; i++) {
        int n = i, sum = 0;
        while(n) {
            //sum += pow(n % 10, 3);
            int tmp = n % 10;
            sum += tmp * tmp * tmp;
            n /= 10;
        }
        if(sum == i) cout << i << "  ";
    }
    cout << endl;
    int tmp = pow(5, 3);
    cout << tmp << endl;
    cout << pow(5, 3) << endl;
    double t = pow(5, 3);
    cout << t << endl;
    return 0;
}
```

# 易错点4：char数组
给char数组赋值时记得在末尾以'\0'字符，计算长度的时候不会计算在内。
```C++
#include <iostream>
#include <bits/stdc++.h>
#define NSIZE 8
using namespace std;

int main()
{
    char g[7] = {'h', 'e', 'j', 'i', 'a', 'n', '\0'};
    cout << strlen(g) << endl;
    cout << g << endl;

    //只要多给出一个字符空间，编译器会自动在末尾添加'\0'
    char gg[10] = {'h', 'e', 'j', 'i', 'a', 'n'};
    cout << strlen(gg) << endl;
    cout << gg << endl;

    char *s = "hejian";
    cout << strlen(s) << endl;
    cout << s << endl;

    char k[7];
    k[0] = 'h', k[1] = 'e', k[2] = 'j', k[3] = 'i', k[4] = 'a', k[5] = 'n', k[6] = '\0';
    cout << strlen(k) << endl;
    cout << k << endl;

    char f[6];
    cin >> f;   //这里会自动扩充空间
    cout << strlen(f) << endl;
    cout << f << endl;
    return 0;
}
```

# 易错点5：for循环中多个变量
```C++
#include <iostream>
using namespace std;

int main()
{
    //这样会输出6个hello，相当于中间是或运算，需要加与符号
    for(int i = 0, j = 0; i < 4, j < 6; i++, j++) {
        cout << "hello" << endl;
    }
    return 0;
}
```

# 易错点6：容器中使用叠加容器出现>>
第一种可能是流运算符，也就是cin>>+输入内容
第二种可能是位运算，即x>>n把数表示为二进制后每位都想右移N位

所以在容器中需要空格隔开，如list< int, list< int, int> >。
