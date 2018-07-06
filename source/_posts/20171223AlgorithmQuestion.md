---
layout: '[default_layout]'   
title: 算法题：最大间距          
date: 2017-12-23 19:47:41  
toc: true                  
tags:                        
- C++

categories:                  
- ACM

---
# 描述
给定一个未经排序的数组，写一个函数找出其排序表中连续两个要素的最大间距。如果数组中的要素少于 2 个，请返回 0。

注意事项：
1、可以假定数组中的所有要素都是非负整数，且最大不超过 32 位整数。
2、用排序的方法解决这个问题是比较简单的方法，但是排序的时间复杂度是O(nlogn), 能否使用线性的时间和空间复杂度的方法解决这个问题。
<!--more-->
格式：

输入行输入一个未经排序的数组num，最后输出排序表中两个要素的最大间距。

# 样例输入
>num =  [ 1，9，2，5 ]

# 样例输出
>4

# 思路
最普通的求法：
```
#include <iostream>
#include <cmath>
#include <algorithm>
using namespace std;

int main()
{
    int n, num[1005];
    while(cin >> n) {
        for(int i = 0; i < n; i++) cin >> num[i];
        if(n < 2) {
            cout << 0 << endl;
            continue;
        }
        sort(num, num + n);
        int ans = num[1] - num[0];
        for(int i = 2; i < n; i++) {
            if(num[i] - num[i - 1] > ans) ans = num[i] - num[i - 1];
        }
        cout << ans << endl;
    }
    return 0;
}
```

设置数组a【65536】，遍历原无序数组b，令a【bi】=1，则数组a中值为一的项的下标为原数组b的有序排列，遍历数组a，记录当前最大距离。但题目要求32位整数。。。
```C++
#include <iostream>
#include <cmath>
#include <algorithm>
#include <cstring>
using namespace std;

int main()
{
    int n, num[1005];
    while(cin >> n) {
        int temp[65536];
        memset(temp, 0, sizeof(temp));
        for(int i = 0; i < n; i++) {
            cin >> num[i];
            temp[num[i]] = 1;
        }
        if(n < 2) {
            cout << 0 << endl;
            continue;
        }
        int per = -1, ans = -1;
        for(int i = 0; i < 65536; i++) {
            if(temp[i]) {
                if(per == -1) {
                    per = i;
                    continue;
                }
                if(i - per > ans) ans = i - per;
                per = i;
            }
        }
        cout << ans << endl;
    }
    return 0;
}
```

别人的主要思想：将所有数按bit分为分到32个数组中，然后依次利用桶排序（2个桶）将这32个数组中的数进行排序，最后合并求出最大间距。时间复杂度和空间复杂读都是O（N）。代码如下：
```C++
def maxInterVal(unsorted_array):
    # divide unsorted_array into n-bit numbers (1<=n<=32)
    bit_nums = [[] for i in range(32)]
    for n in unsorted_array:
        bit_nums[len(bin(n))-3].append(n)
    sorted_array = []
    # bucket sort in each n-bit number list
    for i in range(len(bit_nums)):
        for j in range(0, i+1):
            temp = [[], []] # two buckets here
            for n in bit_nums[i]:
                temp[(n>>j)%2].append(n)
            bit_nums[i] = temp[0] + temp[1]
        sorted_array += bit_nums[i]
    return max_interval(sorted_array)
```



