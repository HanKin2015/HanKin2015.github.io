---
layout: '[default_layout]'   
title: 2019“锐捷网络杯”华中区高校研究生程序设计大赛
date: 2019-06-03 16:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true
mathjax: true        
tags:                        
- C
- C++

categories:                  
- C/C++

---
毕业前最后的一次比赛，”锐捷网络杯“参加了三次，前两次均是三等奖。2018年因为自己没有理解到题意，错失了二等奖，得了三等奖中的第一名。这次比赛最终获得了第六名，还是不错吧（800，800，1500）。
一开始大家都在做第一道A题，题意很简单，但却是较最难的一道题，我最终在3个小时的时候才开始AC第一道题，还是12点钟临时加的（整体难度较大，添加2道简单的）。据说本次获奖的还能去福州公司参观，现场发证书和奖金，最快的一次。

<!--more-->
赛后题目链接：
[2017年第六届湖北省研究生程序设计竞赛](http://acm.whu.edu.cn/olive/arena/6#/)
[Eming Cup 2018](https://acm.whu.edu.cn:8080/oj/woj/contest/23da2mgxnjyds2yi)
[2019研究生大赛](https://acm.whu.edu.cn:8080/oj/woj/contest/23db4nbywcuaasfy)
website:  http://hbppc.contest.codeforces.com
login:  hbppcteam063
password:   jRDh8p0g

# K. A good game
```
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int T, n, m;
    cin >> T;
    for (int cnt = 1; cnt <= T; cnt++) {
        cin >> n >> m;
        int arr[100005];
        long long sum[100005];
        memset(sum, 0, sizeof(sum));
        for (int i = 1; i <= n; i++) {
            //cin >> arr[i];
            scanf("%d", &arr[i]);
            sum[i] += arr[i] + sum[i - 1];
        }
        long long ans = 0;
        int tmp[100005];
        for (long long i = 0; i < m; i++) {
            int a, b;
            //cin >> a >> b;
            scanf("%d%d", &a, &b);
            tmp[i] = sum[b] - sum[a - 1];
        }
        sort(tmp, tmp + m);
        for (long long i = 1; i <= m; i++) {
            ans = ans + tmp[i - 1] * i;
        }
        cout << ans << endl;
    }
    return 0;
}
```

# F. Sequence
```
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int T, n, m;
    cin >> T;
    for (int cnt = 1; cnt <= T; cnt++) {
        cout << "Case #" << cnt << ':' << endl;
        cin >> n >> m;
        int arr[100005];
        for (int i = 1; i <= n; i++) cin >> arr[i];
        for (int i = 0; i < m; i++) {
            int x, y , z;
            cin >> x >> y >> z;
            if (x == 0) {
                arr[y] = z;
            }
            else {
                int ans = 0;
                int tmp = z - y + 1;
                if (tmp & 1) {
                    int hj = 1;
                    for (int j = y; j <= z; j++) {
                        if (hj & 1) ans = ans ^ arr[j];
                        hj++;
                    }
                }
                cout << ans << endl;
            }
        }
    }

    return 0;
}
```

# J. Prefix
```
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n, m;
    cin >> n >> m;
    int d[26];
    for (int i = 0; i < 26; i++) cin  >> d[i];
    int maxn = 200005;
    long long q[maxn];
    map<string, int> COUNT, VALUE;
    string s[100005];
    for (int i = 0; i < n; i++) {
        cin >> s[i];
        int len = s[i].size();
        long long tmp = 1;
        string str = "";
        for (int j = 0; j < len; j++) {
            str += s[i][j];
            tmp = (tmp * d[s[i][j] - 'a']) % m;
            COUNT[str]++;
            VALUE[str] = tmp;
        }
        q[i] = tmp;
    }
    for (int i = 0; i < n; i++) {
        int ans = 0;
        int len = s[i].size();
        string str = "";
        for (int j = 0; j < len - 1; j++) {
            str += s[i][j];
            if (VALUE[str] > q[i]) ans += COUNT[str];
        }
        cout << ans << ' ';
    }
    cout << endl;
    return 0;
}
```

# G. Winer
这道题也算是比较简单的一道题，然鹅一开始一直没有发现坑点，后来知道了，发现也没有时间了，建立DAG（有向五环图），然后进行搜索遍历。下面的代码是超时的。
```
#include <bits/stdc++.h>
using namespace std;

struct node{
    int number, value;
};

bool cmp(node x, node y)
{
    return x.value > y.value;
}

int main()
{
    int N, Q, tmp;
    cin >> N >> Q;
    set<int> lose[100005];
    for (int i = 0; i < 3; i++) {
        node P[100005];
        for (int j = 0; j < N; j++) {
            cin >> tmp;
            P[j].number = j + 1;
            P[j].value = tmp;
        }
        sort(P, P + N, cmp);
        for (int j = 0; j < N; j++) {
            for (int k = j + 1; k < N; k++) {
                if (P[j].value != P[k].value) {
                    lose[P[j].number].insert(P[k].number);
                    for (set<int>::iterator hj = lose[P[k].number].begin(); hj != lose[P[k].number].end(); hj++) {
                        lose[P[j].number].insert(*hj);
                    }
                }
            }
        }
    }
    for (int i = 0; i < Q; i++) {
        cin >> tmp;
        //cout << lose[tmp].size() << endl;
        if (lose[tmp].size() >= N - 1) cout << "YES" << endl;
        else cout << "NO" << endl;
    }
    return 0;
}
/*
3 3
1 4 3
2 1 5
2 2 9
1
2
3

YES
YES
YES
*/
```

# A. A Easy Math Problem
https://acm.whu.edu.cn:8080/oj/woj/contest/23db4nbywcuaasfy/problem/A