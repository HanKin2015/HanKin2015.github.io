---
layout: '[default_layout]'   
title: 数据分析之模板
date: 2018-09-29 19:43:41  
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
[数据分析（业务向）技能总结](https://www.kesci.com/home/project/5b3b3ed771a61726e13833e3)
# 头文件
```
import numpy as np  # 数学
import pandas as pd
from sklearn import datasets  #用数据库去学习，或者把数据库放到tenserflow模块练习
from sklearn.model_selection import train_test_split # 数据集测试集分离
from sklearn.neighbors import KNeighborsClassifier   # 会选择邻近几个点作为他的邻居，综合临近几个点模拟出数据的预测值
from sklearn.model_selection import cross_val_score
import matplotlib.pyplot as plt
import warnings 
warnings.filterwarnings("ignore")
import seaborn as sns
import os
%matplotlib inline
```

<--!more-->
```python
# First, we'll import pandas, a data processing and CSV file I/O library
import pandas as pd

# We'll also import seaborn, a Python graphing library
import warnings # current version of seaborn generates a bunch of warnings that we'll ignore
warnings.filterwarnings("ignore")
import seaborn as sns
import matplotlib.pyplot as plt
sns.set(style="white", color_codes=True)

# Next, we'll load the Iris flower dataset, which is in the "../input/" directory
iris = pd.read_csv("../input/Iris.csv") # the iris dataset is now a Pandas DataFrame

# Let's see what's in the iris data - Jupyter notebooks print the result of the last thing you do
iris.head()

# Press shift+enter to execute this cell
```

[Python 打印语句](https://blog.csdn.net/chennai1101/article/details/59483438/)