---
layout: '[default_layout]'   
title: python画图之雪花
date: 2019-02-21 20:48:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- Python
- Turtle
- 科赫曲线

categories:                  
- 随记

---
# 科赫曲线 
科赫曲线是一种像雪花的几何曲线，所以又称为雪花曲线，它是de Rham曲线的特例。科赫曲线是出现在海里格·冯·科赫的论文中，是分形曲线中的一种。

正整数n代表科赫曲线的阶数，表示生成科赫曲线过程的操作次数。科赫曲线初始化阶数为0，表示一个长度为L的直线。对于直线L将其等分为3段，中间一段用边长为L/3的等边三角形的两个边替代，得到1阶科赫曲线，它包含4条线段。进一步对每条线段重复同样的操作后得到的2阶科赫曲线。重复操作N次可以得到N阶科赫曲线。
<--more-->
# turtle
turtle 是 python 内置的一个比较有趣味的模块，俗称 海龟绘图，它是基于 tkinter 模块打造，提供一些简单的绘图工具。
官方文档：https://docs.python.org/3/library/turtle.html

[骚操作：用Python来一场人工造雪](https://mp.weixin.qq.com/s/RqY6vL36HkI6OWOHVnpDWg)

```python
# -*- coding: utf-8 -*-
"""
Created on Thu Feb 21 21:08:54 2019

@author: HanKin
"""

import turtle
from turtle import *

def koch(size,n):  # 科赫曲线
    if n == 0:
        turtle.fd(size)
    else:
        for angle in [0, 60, -120, 60]:
            turtle.left(angle)
            koch(size/3, n-1)
def main():
    turtle.setup(600, 600)
    turtle.pen(speed = 0, pencolor = 'blue')
    turtle.penup()
    turtle.goto(-200, 100)
    turtle.pendown()
    turtle.pensize(1)
    level = 5   # 阶数
    
    koch(400, level)
    turtle.right(120)  # 向右旋转120°
    koch(400, level)
    turtle.right(120)
    koch(400, level)
    
    turtle.hideturtle()
    done()  # turtle.done()用来停止画笔绘制，但绘图窗体不关闭

main()
```
![enter description here](./images/1550805143573.png)
![enter description here](./images/20190222115629.jpg "20190222115629")
# 小猪佩奇
[Python20秒画完小猪佩奇“社会人”，程序猿的手法是你想不到的独特](https://mp.weixin.qq.com/s/xUte5wKpYrO8PpoXXITSdA)

```python# -*- coding: utf-8 -*-
"""
Created on Thu Feb 21 22:08:12 2019

@author: HanKin
"""

from turtle import*

def nose(x,y):#鼻子
   penup()#提起笔
   goto(x,y)#定位
   pendown()#落笔，开始画
   setheading(-30)#将乌龟的方向设置为to_angle/为数字（0-东、90-北、180-西、270-南）
   begin_fill()#准备开始填充图形
   a=0.4
   for i in range(120):
       if 0<=i<30 or 60<=i<90:
           a=a+0.08
           left(3) #向左转3度
           forward(a) #向前走a的步长
       else:
           a=a-0.08
           left(3)
           forward(a)
   end_fill()#填充完成

   penup()
   setheading(90)
   forward(25)
   setheading(0)
   forward(10)
   pendown()
   pencolor(255,155,192)#画笔颜色
   setheading(10)
   begin_fill()
   circle(5)
   color(160,82,45)#返回或设置pencolor和fillcolor
   end_fill()

   penup()
   setheading(0)
   forward(20)
   pendown()
   pencolor(255,155,192)
   setheading(10)
   begin_fill()
   circle(5)
   color(160,82,45)
   end_fill()

def head(x,y):#头
   color((255,155,192),"pink")
   penup()
   goto(x,y)
   setheading(0)
   pendown()
   begin_fill()
   setheading(180)
   circle(300,-30)
   circle(100,-60)
   circle(80,-100)
   circle(150,-20)
   circle(60,-95)
   setheading(161)
   circle(-300,15)
   penup()
   goto(-100,100)
   pendown()
   setheading(-30)
   a=0.4
   for i in range(60):
       if 0<=i<30 or 60<=i<90:
           a=a+0.08
           lt(3) #向左转3度
           fd(a) #向前走a的步长
       else:
           a=a-0.08
           lt(3)
           fd(a)
   end_fill()

def ears(x,y): #耳朵
   color((255,155,192),"pink")
   penup()
   goto(x,y)
   pendown()
   begin_fill()
   setheading(100)
   circle(-50,50)
   circle(-10,120)
   circle(-50,54)
   end_fill()

   penup()
   setheading(90)
   forward(-12)
   setheading(0)
   forward(30)
   pendown()
   begin_fill()
   setheading(100)
   circle(-50,50)
   circle(-10,120)
   circle(-50,56)
   end_fill()

def eyes(x,y):#眼睛
   color((255,155,192),"white")
   penup()
   setheading(90)
   forward(-20)
   setheading(0)
   forward(-95)
   pendown()
   begin_fill()
   circle(15)
   end_fill()

   color("black")
   penup()
   setheading(90)
   forward(12)
   setheading(0)
   forward(-3)
   pendown()
   begin_fill()
   circle(3)
   end_fill()

   color((255,155,192),"white")
   penup()
   seth(90)
   forward(-25)
   seth(0)
   forward(40)
   pendown()
   begin_fill()
   circle(15)
   end_fill()

   color("black")
   penup()
   setheading(90)
   forward(12)
   setheading(0)
   forward(-3)
   pendown()
   begin_fill()
   circle(3)
   end_fill()

def cheek(x,y):#腮
   color((255,155,192))
   penup()
   goto(x,y)
   pendown()
   setheading(0)
   begin_fill()
   circle(30)
   end_fill()

def mouth(x,y): #嘴
   color(239,69,19)
   penup()
   goto(x,y)
   pendown()
   setheading(-80)
   circle(30,40)
   circle(40,80)

def setting():          #参数设置
   pensize(4)
   hideturtle()        #使乌龟无形（隐藏）
   colormode(255)      #将其设置为1.0或255.随后 颜色三元组的r，g，b值必须在0 .. cmode范围内
   color((255,155,192),"pink")
   setup(840,500)
   speed(10)

def main():
   setting()           #画布、画笔设置
   nose(-100,100)      #鼻子
   head(-69,167)       #头
   ears(0,160)         #耳朵
   eyes(0,140)         #眼睛
   cheek(80,10)        #腮
   mouth(-20,30)       #嘴
   done()

if __name__ == '__main__':
    main()
```