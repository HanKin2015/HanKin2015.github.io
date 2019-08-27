---
layout: '[default_layout]'   
title: 数据分析之数据可视化
date: 2018-09-29 13:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- ML
- Python

categories:                  
- ML

---
# 1、数据集的来源
- [numpy之random库简单的随机数据生成](https://blog.csdn.net/brucewong0516/article/details/79011562)
- [教你在Python中用Scikit生成测试数据集](https://blog.csdn.net/tmb8z9vdm66wh68vx1/article/details/79212888)
<!--more-->
- 1、np.random.rand(d0, d1, …, dn)
np.random.rand(3,2) #生成3行2列的随机数组
np.random.rand(3,2,2) #生产3维的随机数组
- 2、randn(d0, d1, …, dn)返回一个样本，具有标准正态分布。
- 3、randint(low[, high, size])
	- 返回随机整数，范围区间为\[low,high），包含low，不包含high
	- 参数：low为最小值，high为最大值，size为数组维度大小，dtype为数据类型，默认的数据类型是np.int
	- high没有填写时，默认生成随机数的范围是\[0，low)
- 4、np.random.random([size])生成\[0,1)之间的浮点数,与np.random.rand()功能类似
- 5、numpy.random.choice(a[, size, replace, p])生成一个随机样本，从一个给定的一维数组a中随机选取
- 6、numpy.random.seed()生成随机数的种子，使得每次生成随机数相同

**注意**
```
np.random.seed(2) # 种子和随机函数放在一起运行才能使随机数不变
np.random.rand(3)
```

# 2、画散点图看分布

# 3、资料满满
[python seaborn画图](https://blog.csdn.net/suzyu12345/article/details/69029106)
[Python数据可视化-seaborn](https://www.cnblogs.com/gczr/p/6767175.html)

[Python data visualizations on the Iris dataset](https://www.kaggle.com/benhamner/python-data-visualizations/notebook)