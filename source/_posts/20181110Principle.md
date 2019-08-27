---
layout: '[default_layout]'   
title: 容斥原理           
date: 2018-11-10 22:47:41  
toc: true                  
tags:                        
- 容斥原理    

categories:                  
- Algrithm

---
# 容斥原理
在计数时，必须注意没有重复，没有遗漏。为了使重叠部分不被重复计算，人们研究出一种新的计数方法，这种方法的基本思想是：先不考虑重叠的情况，把包含于某内容中的所有对象的数目先计算出来，然后再把计数时重复计算的数目排斥出去，使得计算的结果既无遗漏又无重复，这种计数的方法称为容斥原理。
[《程序设计中的组合数学》——容斥定理](https://www.cnblogs.com/rhythmic/p/5503272.html)
[容斥定理](http://blog.csdn.net/han_kin/article/details/47662801)
<!--more-->

韦恩图能够鲜明的解释这个原理。

# 描述
要计算几个集合并集的大小，我们要先将所有单个集合的大小计算出来，然后减去所有两个集合相交的部分，再加回所有三个集合相交的部分，再减去所有四个集合相交的部分，依此类推，一直计算到所有集合相交的部分。

# 代码实现
时间复杂度：2^n （n集合个数）
总共就2^n种组合（子串），然后判断每种可能中有多少集合来判断正负。
```
int solve (int n, int r)
{
    /*求质数*/
    vector<int> p;
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) {
            p.push_back (i);
            while (n % i == 0) n /= i;
        }
    }
    if (n > 1) p.push_back (n);

    int sum = 0;   // 非互质的个数
    for (int msk = 1; msk < (1 << (int)p.size()); msk++) {  // 子串有2^k种可能
        int mult = 1, bits = 0;
        /*每种可能用bit位表示，最多k位，然后看bit位上是否形成组合*/
        for (int i = 0; i < (int)p.size(); ++i) {
            if (msk & (1 << i)) {
                ++bits;
                mult *= p[i];
            }
        }
        int cur = r / mult;
        //cout << cur << endl;
        if (bits % 2 == 1) sum += cur;
        else sum -= cur;
    }
    return r - sum;
}
```

# 两个同一个问题
1. 给出整数n和r。求区间[1;r]中与n互素的数的个数。
2. 给定一个区间[A,B],找出在这个区间内与给定的n互质的整数的个数。

两个问题解决方案一样，去解决它的逆问题，求不与n互素的数的个数。
```
#include <bits/stdc++.h>
#define LL long long
using namespace std;

// 求n的质因数
void FindPrimeFactor(int n, int a[], int &cnt)
{
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            a[cnt++] = i;
            while (n % i == 0) n /= i;
        }
    }
    if (n > 1) a[cnt++] = n;
    return;
}

// 复杂度也是2^k
LL Solve2(LL n, int a[], int cnt)
{
    LL res = 0;
    int t = 1, que[1005] = { -1}; // 依据容斥原理，que[0]的值是-1
    for (int i = 0; i < cnt; i++) {  // 比如2 3 4，形成-1 2 3 -6 4 -8 -12 24
        int k = t;
        for (int j = 0; j < k; j++) {
            que[t++] = que[j] * a[i] * (-1);  // 难点
            /*乘以-1和-1^k是一样的效果
            重点在第一个for循环，新加进去的数和前面形成组合子串*/
        }
    }
    cout << "t = " << t << endl;
    for (int i = 1; i < t; i++) {
        cout << que[i] << endl;
        res += n / que[i];
    }
    return res;
}

int solve (int n, int r)
{
    /*求质数*/
    vector<int> p;
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) {
            p.push_back (i);
            while (n % i == 0) n /= i;
        }
    }
    if (n > 1) p.push_back (n);

    int sum = 0;   // 非互质的个数
    for (int msk = 1; msk < (1 << (int)p.size()); msk++) {  // 子串有2^k种可能
        int mult = 1, bits = 0;
        /*每种可能用bit位表示，最多k位，然后看bit位上是否形成组合*/
        for (int i = 0; i < (int)p.size(); ++i) {
            if (msk & (1 << i)) {
                ++bits;
                mult *= p[i];
            }
        }
        int cur = r / mult;
        //cout << cur << endl;
        if (bits % 2 == 1) sum += cur;
        else sum -= cur;
    }
    return r - sum;
}

/*
题目：给定一个区间[A,B],找出在这个区间内与给定的N互质的整数的个数。
T(0 < T <= 100)the number of test cases
each of the next T lines contains three integers A, B, N where (1 <= A <= B <= 10^15) and (1 <=N <= 10^9).

直接求互质复杂度高，可以用素数筛选法求非互质的数。
求[1,B]-[1,A-1]。
*/

// 直接算一定有错误，必须使用容斥原理
LL Solve(LL n, int a[], int cnt)
{
    LL res = 0;
    for (int i = 0; i < cnt; i++) {
        for (int j = 1; ; j++) {
            if (j * a[i] > n) {
                res += j - 1;
                break;
            }
        }
    }
    return res;
}
/*
N = 12 --- 2 3
18  2 4 6 8 10 12 14 16 18
    3 6 9 12 15 18
会返回结果为15.
正确答案是12.
*/

int main()
{
    const int maxn = 1005;
    int a[maxn] = {2, 3, 4}, cnt = 3;
    //FindPrimeFactor(12, a, cnt);
    //cout << Solve2(18, a, cnt) << endl;
    cout << solve(12, 18) << endl;

    __int64 i, T, x, y, n, sum;
    while(scanf("%I64d", &T) != EOF) {
        for(i = 1; i <= T; i++) {
            scanf("%I64d%I64d%I64d", &x, &y, &n);
            //sum = y - haha(y) - (x - 1 - haha(x - 1)); //由于区间是[x,y],求出[1,y]的互质个数，再减去[1,x-1]的互质个数
            printf("Case #%I64d: ", i);
            printf("%I64d\n", sum);
        }
    }
    return 0;
}
```

# 另外一个缠绕我很久的问题，居然是容斥原理
[NEUQ1027：谷学长的童年（概率问题）](https://hankin2015.github.io/2017/12/18/20171218NEUQ1021/)





