---
layout: '[default_layout]'   
title: 多种语言实现求最大值(排序)           
date: 2018-07-28 20:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- C/C++

categories:                  
- ACM

---
在Codeforces上面有一个特别的比赛，每道题使用一种语言，一种语言不能在两道题上使用。
题目：输入一组数字，按从小到大输出。
输入： 6 8 2 11 6 4 5 123456789101112 2 6（直到输入结束）
输出： 2 2 4 5 6 6 6 8 11 123456789101112
<!--more-->

## 1、C语言版本
#include <stdio.h>
```
/*
*输入：6 8 2 11 6 4 5 123456789101112 2 6
*输出：2 2 4 5 6 6 6 8 11 123456789101112
*/
#include <stdio.h>
#include <stdlib.h>
int comp(const void *a, const void *b)
{
    return *(long long*)a > *(long long*)b;  //这种写法运行结果正确
    //return *(long long*)a - *(long long*)b;  //真的奇怪，comp为啥是这样写感觉写反了，这是从小到大？？
}

int main()
{
    long long n[1005], cnt = 0;
    //while(scanf("%lld", &n[cnt++]) != EOF) { //这样也会把最后的终止符号算进里面，所以需要-1
        //if(cnt == 10) break;
    //}
    while(scanf("%lld", &n[cnt]) != EOF) cnt++;  //终止符需要前面回车符，然后ctrl+z
    printf("%lld\n", cnt);
    //qsort函数必须要自己写comp函数
    qsort(n, cnt, sizeof(n[0]), comp);  //这样CB结果不正确，但在线编译器结果是正确的
    for(int i = 0; i < cnt; i++) printf("%I64d ", n[i]);
    return 0;
}

```

# 2、C++版本
```
/*
*输入：6 8 2 11 6 4 5 123456789101112 2 6
*输出：2 2 4 5 6 6 6 8 11 123456789101112
*/
#include <iostream>
#include <algorithm>
using namespace std;

int main()
{
    long long n[1005], cnt = 0;
    while(cin >> n[cnt]) cnt++;  //C语言终止符需要前面回车符，然后ctrl+z，然而C++不需要
    sort(n, n+ cnt);
    for(int i = 0; i < cnt; i++) cout << n[i] << ' ';
    return 0;
}
```

# 3、python2版本
```
```

# 参考[A+B Problem](https://vijos.org/p/1000)
## Free Pascal Code
```
var a, b:longint;
begin
    readln(a, b);
    writeln(a + b);
end.
```

## C Code
```
#include <stdio.h>

int main()
{
    int a, b;
    scanf("%d%d", &a, &b);
    printf("%d\n", a + b);
    return 0;
}
```

## C++ Code
```
#include <iostream>

using namespace std;

int main()
{
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
    return 0;
}
```

## C# Code
```
using System;
using System.Linq;

class Program {
    public static void Main(string[] args) {
        Console.WriteLine(Console.ReadLine().Split().Select(int.Parse).Sum());
    }
}
```

## Python Code
```
print sum(map(int, raw_input().split()))
```

## Python 3 Code
```
print(sum(map(int, input().split())))

或者
s = input().split()
print(int(s[0]) + int(s[1]))
```

## Java Code
```
import java.io.IOException;  // *包含所有的话会运行更慢
import java.util.Scanner;

public class Main {
    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        System.out.println(a + b);
    }
}
```

## PHP Code
```
<?php

fscanf(STDIN, "%d %d\n", $a, $b);
echo ($a + $b) . "\n";
Rust Code
use std::io;
 
fn main() {
    let mut line = String::new();
    io::stdin().read_line(&mut line).expect("stdin");
 
    let sum: i32 = line.split_whitespace()
                       .map(|x| x.parse::<i32>().expect("integer"))
                       .sum(); 
    println!("{}", sum);
}
```

## Haskell Code
```
main = print . sum . map read . words =<< getLine
Javascript Code
const [a, b] = readline().split(' ').map(n => parseInt(n, 10));
print((a + b).toString());
```

## Go Code
```
package main
import "fmt"
func main() {
    var a, b int
    fmt.Scanf("%d%d", &a, &b)
    fmt.Printf("%d\n", a + b)
}
```

## Ruby Code
```
a, b = gets.split.map(&:to_i)
puts(a + b)
```

## JavaScript （Node.js）
```
const fs = require('fs')
const data = fs.readFileSync('/dev/stdin')
const result = data.toString('ascii').trim().split(' ').map(x => parseInt(x)).reduce((a, b) => a + b, 0)
console.log(result)
process.exit() // 请注意必须在出口点处加入此行
```