---
layout: '[default_layout]'   
title: MathJax使用Latex语法编写数学公式            
date: 2017-11-01 15:45:41  
toc: true                  
tags:                        
- Latex
- MathJax

categories:                  
- 

---
# 介绍
MathJax允许你在你的网页中包含公式，无论是使用LaTeX、MathML或者AsciiMath符号，这些公式都会被javascript处理为HTML、SVG或者MathML符号。MathJax是一款相当强悍的在网页显示数学公式的插件。MathJax常使用LaTeX语法编写数学公式。

# 文档
[MathJax使用LaTeX语法编写数学公式教程](http://www.360doc.com/content/14/0930/23/9482_413578190.shtml)
[MathJax中文文档](http://mathjax-chinese-doc.readthedocs.io/en/latest/start.html)
[在线Latex公式编辑器](http://www.codecogs.com/latex/eqneditor.php)
[Latex公式编辑器](http://zh.numberempire.com/texequationeditor/equationeditor.php)

# 如何插入公式
LaTeX的数学公式有两种：行中(间)公式和独立(行内)公式。行中公式放在文中与其它文字混编，独立公式单独成行。

温馨提示：因为Markdown中\是转义字符，所以在Markdown中输入行内公式使用`\\(公式\\)`

    行中公式可以用如下两种方法表示：

    \(数学公式\)　或　$数学公式$（注意是美元符号）

    独立公式可以用如下两种方法表示：

    \[数学公式\]　或　$$数学公式$$

例子：`\\[J_\alpha(x) = \sum_{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha}\\]`

显示：\\[J_\alpha(x) = \sum_{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha}\\]

# 特别是文字之间的公式, 有时需要将公式的下标放在正下方。

1. 如果是数学符号，那么直接用\limits命令放在正下方，如Max函数下面的取值范围，需要放在Max的正下方。可以如下实现：
`$\max \limits_{a<x<b}\{f(x)\}$`
$\max \limits_{a<x<b}\{f(x)\}$

2. 若是普通符号，那么要用\mathop先转成数学符号再用\limits，如
`$ \mathop{a}\limits_{i=1}$` 
$ \mathop{a}\limits_{i=1}$

3. 对于双美元符之间的公式，Latex默认下标是放在正下方。所以就不需要加\limits。[栗子](http://jingyan.baidu.com/article/cb5d610502a2f8005d2fe062.html)

^表示上标, _表示下标。如果上下标的内容多于一个字符，要用{}把这些内容括起来当成一个整体。上下标是可以嵌套的，也可以同时使用。

另外，如果要在左右两边都有上下标，可以用\sideset命令。
例子：\sideset{^1_2}{^3_4}\bigotimes

显示：$\sideset{^1_2}{^3_4}\bigotimes$

# [Markdown中插入数学公式的方法](http://blog.csdn.net/xiahouzuoxin/article/details/26478179)
Markdown自由书写的特性很好，唯独遇到数学公式时就要煞费苦心——每次都是先使用Latex书写(在线的Latex编辑器)，然后保存为图片，使用img标签进行引用，当公式很多的时候稍显复杂。

本文的方法使用html的语法，调用公式生成API，在线生成Latex数学公式，免去将公式保存为图片的麻烦。当然，弊端也是有的，公式太多，可能会造成刷新比一般的网页慢一些。

## 方法一：使用Google Chart的服务器
    <img src="http://chart.googleapis.com/chart?cht=tx&chl= 在此插入Latex公式" style="border:none;">

## 方法二：使用forkosh服务器
    img src="http://www.forkosh.com/mathtex.cgi? 在此处插入Latex公式">

## 方法三：使用MathJax引擎
大家都看过Stackoverflow上的公式吧，漂亮，其生成的不是图片。这就要用到MathJax引擎，在Markdown中添加MathJax引擎也很简单.

    <script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

$$\phi$$

$$\in$$

[制作个人简历](http://blog.csdn.net/eclipsexys/article/details/45268829)












