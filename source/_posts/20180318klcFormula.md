---
layout: '[default_layout]'   
title: 基姆拉尔森计算公式           
date: 2018-03-18 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- 数论

categories:                  
- others

---
通过日期判断是星期几可以通过基姆拉尔森计算公式算出。
基姆拉尔森计算公式外文名是Kim larsson calculation formula。

>W= (d+2*m+3*(m+1)/5+y+y/4-y/100+y/400+1) mod 7

在公式中d表示日期中的日数，m表示月份数，y表示年数。
注意：在公式中有个与其他公式不同的地方：
把一月和二月看成是上一年的十三月和十四月，例：如果是2004-1-10则换算成：2003-13-10来代入公式计算。
摘自百度百科：http://baike.baidu.com/view/739374.htm
<!--more-->
[基姆拉尔森计算公式 推导](https://www.cnblogs.com/SeekHit/p/7498408.html)