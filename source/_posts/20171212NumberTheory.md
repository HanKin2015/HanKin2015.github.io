---
layout: '[default_layout]'   
title: 数论及数论四大定理         
date: 2017-12-12 14:47:41  
toc: true                  
tags:                        
- Math

categories:                  
- Math

---
# 数论 （数学分支）
&emsp;&emsp;数论是纯粹数学的分支之一，主要研究整数的性质。整数可以是方程式的解（丢番图方程）。有些解析函数（像黎曼ζ函数）中包括了一些整数、质数的性质，透过这些函数也可以了解一些数论的问题。透过数论也可以建立实数和有理数之间的关系，并且用有理数来逼近实数（丢番图逼近）。
按研究方法来看，数论大致可分为初等数论和高等数论。初等数论是用初等方法研究的数论，它的研究方法本质上说，就是利用整数环的整除性质，主要包括整除理论、同余理论、连分数理论。高等数论则包括了更为深刻的数学研究工具。它大致包括代数数论、解析数论、计算数论等等。
<!--more-->

# 费马大定理(费马定理) （数学史上著名的定理）
费马大定理，又被称为“费马最后的定理”，由17世纪法国数学家皮耶·德·费玛提出。
它断言当整数n >2时，关于x, y, z的方程 x^n + y^n = z^n 没有正整数解。
德国佛尔夫斯克曾宣布以10万马克作为奖金奖给在他逝世后一百年内，第一个证明该定理的人，吸引了不少人尝试并递交他们的“证明”。
被提出后，经历多人猜想辩证，历经三百多年的历史，最终在1995年被英国数学家安德鲁·怀尔斯彻底证明。

# 同余定理(同余)
数论中的重要概念。给定一个正整数m，如果两个整数a和b满足a-b能够被m整除，即(a-b)/m得到一个整数，那么就称整数a与b对模m同余，记作a≡b(mod m)。对模m同余是整数的一个等价关系。

# 伪素数 
费马小定理: 假如p是质数，若p不能整除a，则 a^(p-1) ≡1 (mod p)，若p能整除a，则a^(p-1) ≡0 (mod p)。
伪素数，又叫做伪质数：它满足费马小定理，但其本身却不是素数。最小的伪素数是341。有人已经证明了伪素数的个数是无穷的。事实上，费马小定理给出的是关于素数判定的必要非充分条件。若n能整除2^(n-1)-1，并n是非偶数的合数，那么n就是伪素数。第一个伪素数341 是萨鲁斯（Sarrus)在1819年发现的。

费马小定理也就是说如果一个数p满足gcd(a, p) = 1 并且a^(p-1) ≡0 (mod p), 则p是质数。但存在其特例，也就是说费马小定理有BUG，但也不能这么说。费马小定理只能正推，不能反推。所以说是p满足费马小定理，但p不是质数，而是另外一个称呼伪素数 (一定是奇数)。

```C++
//求伪素数
#include <iostream>
#include <cmath>
using namespace std;

bool IsPrime(int n)
{
    for(int i = 2; i <= sqrt(n); i++) {
        if(n % i == 0) return false;
    }
    return true;
}

int QuickPow(int a, int b, int mod)
{
    int ret = 1;
    a = a % mod;
    while(b) {
        if(b & 1) ret =( ret * a )% mod;
        a =( a * a )% mod;
        b >>= 1;
    }
    return ret;
}

int main()
{
    for(int i = 2; i < 800000; i++) {
        if(QuickPow(2, i - 1, i) == 1) {
            if(!IsPrime(i)) {
                cout << i << endl;
            }
        }
    }
    return 0;
}
```

# 指数循环节
其实就是欧拉定理的一种推广。
 ![](http://img.blog.csdn.net/20140613151829390)
 （其中Φ 为欧拉函数）

# 质数和素数
质数（prime number）又称素数，有无限个。质数定义为在大于1的自然数中，除了1和它本身以外不再有其他因数。

# 数论四大定理 
威尔逊定理、欧拉定理、孙子定理、费马小定理并称数论四大定理。

## 1、威尔逊定理
若p为质数，则p可整除(p-1)!+1。
如：7为质数，则7可整除(7 - 1)! + 1 = 721，即721 % 7 == 0。

## 2、欧拉定理
在数论中，欧拉定理（Euler Theorem，也称费马-欧拉定理或欧拉函数定理）是一个关于同余的性质。欧拉定理得名于瑞士数学家莱昂哈德·欧拉，该定理被认为是数学世界中最美妙的定理之一。欧拉定理实际上是费马小定理的推广。此外还有平面几何中的欧拉定理、多面体欧拉定理(在一凸多面体中，顶点数-棱边数+面数=2)。西方经济学中欧拉定理又称为产量分配净尽定理，指在完全竞争的条件下，假设长期中规模收益不变，则全部产品正好足够分配给各个要素。另有欧拉公式。

欧拉定理，也称费马-欧拉定理或欧拉函数定理。欧拉定理实际上是费马小定理的推广。
若n,a为正整数，且n,a互素，即gcd(a,n) = 1，则a^φ(n) ≡ 1 (mod n), 其中φ(n)为欧拉函数。
如：n = 5, a = 7. 因为与5互质的有1、2、3、4，即φ(5) = 4，则(7 ^ 4)  % 5 = 2401 % 5 = 1。

### 欧拉函数
在数论，对正整数n，欧拉函数是小于n的正整数中与n互质的数的数目（φ(1)=1）。此函数以其首名研究者欧拉命名(Euler'so totient function)，它又称为Euler's totient function、φ函数、欧拉商数等。 例如φ(8)=4，因为1,3,5,7均和8互质。 从欧拉函数引伸出来在环论方面的事实和拉格朗日定理构成了欧拉定理的证明。

#### 通式
![](https://gss0.bdstatic.com/-4o3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D146/sign=972114bf49a98226bcc12f23bc80b97a/f3d3572c11dfa9ecf6f6c0dd68d0f703908fc124.jpg)
φ(x) = x * (1 - 1/p1) * ... * (1 - 1/pn)

其中p1, p2……pn为x的所有质因数，x是不为0的整数。
φ(1)=1（唯一和1互质的数(小于等于1)就是1本身）。
注意：每种质因数只一个。 比如12=2*2*3那么φ（12）=12*（1-1/2）*(1-1/3)=4

#### 特例
- 若n是质数p的k次幂，![](https://gss2.bdstatic.com/9fo3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D211/sign=8a21a419ac18972ba73a07cbd7cd7b9d/f9198618367adab410da834e8cd4b31c8701e4b1.jpg) ，因为除了p的倍数外，其他数都跟n互质。
- 设n为正整数，以 φ(n)表示不超过n且与n互素的正整数的个数，称为n的欧拉函数值
φ：N→N，n→φ(n)称为欧拉函数。
- 欧拉函数是积性函数——若m,n互质， ![](https://gss3.bdstatic.com/-Po3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D140/sign=daa516337cec54e745ec1e1a89399bfd/bd3eb13533fa828b5d8406eefa1f4134970a5a1c.jpg)
- 特殊性质：当n为奇数时，![](https://gss0.bdstatic.com/-4o3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D96/sign=52a5c55ef1246b607f0ebe72eaf8e29d/8cb1cb134954092331f8f8739558d109b3de492e.jpg)  , 证明与上述类似。
- 若n为质数，则 φ(n) = n  - 1 ，如11，1、2、3、4、5、6、7、8、9、10都是与11互质的数。

```C++
//质数的快速求法
[利用辛达拉姆筛进行素数判定](http://blog.csdn.net/han_kin/article/details/47685799)
```

```C++
//因数数的快速求法，时间复杂度根号n。
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int n;
    while(cin >> n) {
        int temp = sqrt(n);
        for(int i = 1; i < temp; i++) {
            if(n % i == 0) {
                cout << i << ' ' << n / i << ' ';
            }
        }
        if(temp * temp == n) cout << temp;
        cout << endl;
    }
    return 0;
}
```

```C++
//质因数的快速求法
#include <iostream>
#include <cmath>
using namespace std;

int main()
{
    int n;
    while(cin >> n) {
        //Pollard Rho因数分解，时间复杂度是n^0.25？不是n
        for(int i = 2; i <= n; i++) {
            if(n % i == 0) cout << i << ' ';
            while(n % i == 0) n /= i;
        }
        cout << endl;
    }
    return 0;
}
```

```C++
//欧拉函数
#include <iostream>
#include <cmath>
using namespace std;

int gcd(int a, int b)
{
    return b ? gcd(b, a % b) : a;
}

int eular(int n)
{
    int ret=1,i;
    for(i=2;i*i<=n;i++)
    {
        if(n%i==0)
        {
            n/=i,ret*=i-1;
            while(n%i==0) n/=i,ret*=i;
        }
    }
    if(n>1) ret*=n-1;
    return ret;
}

/*线性筛O(n)时间复杂度内筛出maxn内欧拉函数值*/
int m[maxn],phi[maxn],p[maxn],pt;//m[i]是i的最小素因数，p是素数，pt是素数个数

int make()
{
    phi[1]=1;
    int N=maxn;
    int k;
    for(int i=2;i<N;i++)
    {
        if(!m[i])//i是素数
            p[pt++]=m[i]=i,phi[i]=i-1;
        for(int j=0;j<pt&&(k=p[j]*i)<N;j++)
        {
            m[k]=p[j];
            if(m[i]==p[j])//为了保证以后的数不被再筛，要break
            {
                phi[k]=phi[i]*p[j];
/*这里的phi[k]与phi[i]后面的∏(p[i]-1)/p[i]都一样（m[i]==p[j]）只差一个p[j]，就可以保证∏(p[i]-1)/p[i]前面也一样了*/
                break;
            }
            else
                phi[k]=phi[i]*(p[j]-1);//积性函数性质，f(i*k)=f(i)*f(k)
        }
    }
}

int main()
{
    int n;
    while(cin >> n) {
        //小于n的正整数中与n互质的数的数目
        int cnt = 0;
        for(int i = 1; i < n; i++) {
            if(gcd(i, n) == 1) cnt++;
        }
        cout << cnt << endl;

        //根据通式计算
        int ans = n;
        for(int i = 2; i <= n; i++) {
            if(n % i == 0) {
                ans = (ans / i) * (i - 1);
            }
            while(n % i == 0) n /= i;
        }
        cout << ans << endl;
    }
    return 0;
}
```

# 3、孙子定理
孙子定理，又称中国剩余定理。
孙子定理是中国古代求解一次同余式组（见同余）的方法。是数论中一个重要定理。又称中国余数定理。一元线性同余方程组问题最早可见于中国南北朝时期（公元5世纪）的数学著作《孙子算经》卷下第二十六题，叫做“物不知数”问题，原文如下：
有物不知其数，三三数之剩二，五五数之剩三，七七数之剩二。问物几何？即，一个整数除以三余二，除以五余三，除以七余二，求这个整数。《孙子算经》中首次提到了同余方程组问题，以及以上具体问题的解法，因此在中文数学文献中也会将中国剩余定理称为孙子定理。
公元前后的《孙子算经》中有“物不知数”问题：“今有物不知其数，三三数之余二 ，五五数之余三 ，七七数之余二，问物几何？”答为“23”。
明朝程大位用歌谣给出了该题的解法：“三人同行七十稀，五树梅花廿一枝，七子团圆月正半，除百零五便得知。”
以现代的说法，是找出三个关键数70，21，15。解法的意思就是用70乘3除所得的余数，21乘5除所得的馀数，15乘7除所得的余数，然後总加起来，除以105的余数就是答案。


# 4、费马小定理
假如p是质数，若p不能整除a，则 a^(p-1) ≡1（mod p），若p能整除a，则a^(p-1) ≡0（mod p）。
若p是质数，且a,p互质，那么 a的(p-1)次方除以p的余数恒等于1。
证明：
因为p是质数，且（a，p)=1，所以φ(p)=p-1。由欧拉定理可得a^(p-1) ≡1（mod p）。证毕。对于该式又有a^p ≡a（mod p），所以，费马小定理的另一种表述为：假如p是质数，且gcd(a,p)=1，那么a^p ≡a（mod p）。
欧拉定理，也称费马-欧拉定理或欧拉函数定理。欧拉定理实际上是费马小定理的推广。



