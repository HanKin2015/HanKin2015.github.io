---
layout: '[default_layout]'   
title: 那些大佬的刷题模板           
date: 2018-01-02 22:47:41  
toc: true                  
tags:                        
- C++

categories:                  
- others

---
```C++
remote:  __________________________________________________
remote: |                    _                             |
remote: | /|,/ _   _ _      / ` /_  _ .  _ _/_ _ _   _    _|
remote: |/  / /_' / / /_/  /_, / / / / _\  /  / / / /_| _\ |
remote: |             _/                                   |
remote: |               ~~** Hankin2017 **~~               |
remote: |__________________________________________________|
remote:
remote:
remote:                       ___
remote:                    /`   `'.
remote:                   /   _..---;
remote:                   |  /__..._/  .--.-.
remote:                   |.'  e e | ___\_|/____
remote:                  (_)'--.o.--|    | |    |
remote:                 .-( `-' = `-|____| |____|
remote:                /  (         |____   ____|
remote:                |   (        |_   | |  __|
remote:                |    '-.--';/'/__ | | (  `|
remote:                |      '.   \    )"";--`\ /
remote:                \        ;   |--'    `;.-'
remote:                |`-.__ ..-'--'`;..--'`
remote:
remote: :*~*:._.:*~*:._.:*~*:._.:*~*:._.:*~*:._.:*~*:._.:*~*
remote:
```
<!--more-->
```C++
#include<bits/stdc++.h>

#define rep(i, l, r) for(int i=l; i<=r; i++)
#define dow(i, l, r) for(int i=l; i>=r; i--)
#define clr(x, c) memset(x, c, sizeof(x))
#define travel(x) for(edge *p=fir[x]; p; p=p->n)
#define all(x) (x).begin,(x).end
#define pb push_back
#define fi first
#define se second
#define l(x) Left[x]
#define r(x) Right[x]
#define lowbit(x) (x&-x)

using namespace std;

typedef long long ll;
typedef pair<int,int> Pii;
typedef long double ld;
typedef unsigned long long ull;

inline int read()
{
    int x=0; bool f=0; char ch=getchar();
    while (ch<'0' || '9'<ch) f|=ch=='-', ch=getchar();
    while ('0'<=ch && ch<='9') x=x*10+ch-'0', ch=getchar();
    return f?-x:x;
}

#define maxn 109

#include<algorithm>
#include <iostream>
#include <stdlib.h>
#include <string.h>
#include  <stdio.h>
#include   <math.h>
#include   <time.h>
#include   <vector>
#include   <bitset>
#include    <queue>
#include      <set>
#include      <map>
using namespace std;

const int N=105;
```
```C++
#include <bits/stdc++.h>
#define db double
#define uint unsigned int
#define ll long long
#define ull unsigned long long
#define fir first
#define sec second
#define mkp make_pair
#define pb push_back
#define pii pair <int, int>
#define rep(i, a, b) for (int i = (a), __end = (b); i <= __end; ++i)
#define repdown(i, a, b) for (int i = (a), __end = (b); i >= __end; --i)
#define RG register
#define clr(a) memset(a, 0, sizeof(a))
using namespace std;

const int mod = 998244353;
```

```C++
#include<bits/stdc++.h>
using namespace std;
#define X first
#define Y second
#define mp make_pair
#define pb push_back
#define rep(i,a,n) for(int i=(a);i<=(n);++i)
#define dep(i,a,n) for(int i=(a);i>=(n);--i)
#define eps 1e-8
#define pi 3.1415926535897
#define sqr(x) ((x)*(x))
#define MAX(a,b) a=max(a,b)
#define MIN(a,b) a=min(a,b)
#define SZ(x) ((int)(x).size())
#define CPY(a,b) memcpy(a,b,sizeof(a))
#define CLR(a) memset(a,0,sizeof(a))
#define POSIN(x,y) (1<=(x)&&(x)<=n&&1<=(y)&&(y)<=m)
#define all(x) (x).begin(),(x).end()
#define COUT(S,x) cout<<fixed<<setprecision(x)<<S<<endl
#define buli(x) (__builtin_popcountll(x))
#define bur0(x) (__builtin_ctzll(x))
#define bul2(x) (63-__builtin_clzll(x))
#define pw(x) ((ll(1))<<(x))
#define upmo(a,b) (((a)=((a)+(b))%mo)<0?(a)+=mo:(a))
#define mmo(a,b) (((a)=1ll*(a)*(b)%mo)<0?(a)+=mo:(a))
#define y0 y0z
#define y1 y1z
#define yn ynz
#define j0 j0z
#define j1 j1z
#define jn jnz
#define tm tmz
#ifdef LOCAL
#define debug(...) fprintf(stderr, __VA_ARGS__)
#else
#define debug(...) 
#endif
typedef long long ll;
typedef double lf;
typedef pair<int,int> pii;
typedef pair<ll,ll> pll;
typedef pair<lf,lf> pff;
typedef complex<double> CD;
const int inf=0x3f3f3f3f;
const int mo=1000000007;
inline void gn(long long&x){
    int sg=1;char c;while(((c=getchar())<'0'||c>'9')&&c!='-');c=='-'?(sg=-1,x=0):(x=c-'0');
    while((c=getchar())>='0'&&c<='9')x=x*10+c-'0';x*=sg;
}
inline void gn(int&x){long long t;gn(t);x=t;}
inline void gn(unsigned long long&x){long long t;gn(t);x=t;}
inline void gn(double&x){double t;scanf("%lf",&t);x=t;}
inline void gn(long double&x){double t;scanf("%lf",&t);x=t;}
template<class T1,class T2>inline void gn(T1&r,T2&s){gn(r),gn(s);}
template<class T1,class T2,class T3>inline void gn(T1&r,T2&s,T3&t){gn(r),gn(s),gn(t);}
template<class T1,class T2,class T3,class T4>inline void gn(T1&r,T2&s,T3&t,T4&u){gn(r),gn(s),gn(t),gn(u);}
inline void gs(char *s){scanf("%s",s);}
inline void gc(char &c){while((c=getchar())>126 || c<33);}
inline void pc(char c){putchar(c);}
const int DX[]={1,0,-1,0},DY[]={0,1,0,-1};
ll powmod(ll a,ll b) {ll res=1;a%=mo;for(;b;b>>=1){if(b&1)res=res*a%mo;a=a*a%mo;}return res;}
ll powmod(ll a,ll b,ll mo) {ll res=1;a%=mo;for(;b;b>>=1){if(b&1)res=res*a%mo;a=a*a%mo;}return res;}
ll gcd(ll a,ll b) { return b?gcd(b,a%b):a;}
//*******************************************

const int N=111,M=111111;
int l,m,n,t,C;
int a[N][N],vis[N][N];
char ch;
queue<pii>Q;
int main(){
#ifdef LOCAL
    freopen("F.in","r",stdin);freopen("F.out","w",stdout);
#endif
```
