---
layout: '[default_layout]'   
title: 数据处理常用基础操作(清洗、可视化、特征工程)[置顶]       
date: 2222-11-10 21:47:41  
toc: true                  
tags:                        
- Python
- DataFrame
- Pandas

categories:                  
- 机器学习

---
![](https://github.com/HanKin2015/Storage/blob/master/img10.jpg?raw=true)
<!--more-->

# 一、数据挖掘之pandas.DataFrame  
[用python做数据分析4|pandas库介绍之DataFrame基本操作](http://www.jianshu.com/p/682c24aef525)
[官方文档](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)
[用Python做科学计算](http://old.sebug.net/paper/books/scipydoc/index.html#)

数据地址：github.com
源代码地址：github.com

## 1、jupyter notebook显示plot图像
>%matplotlib inline

## 2、处理excel数据
后缀为xls或者xlsx
>import pandas as pd
data.to_excel('data.xlsx', index=False)

## 3、处理csv数据
>import pandas as pd
df_data = pd.read_csv('./data.csv', sep='\t')  #按照相应的间隔符读取数据，默认空格或者tab符

## 'utf-8' codec can't decode byte 0xd1 in position 9: invalid continuation byte
意思是utf-8编码不行，需要其他类型编码格式，默认应该是utf-8或者None。
```
data = pd.read_csv('air_tianjin_2017.csv', engine='python', encoding='gbk')
```

## 有中文路径问题
```
path = '文件/data数据.csv'
path = unicode(path, 'utf8')

pd.read_csv( '文件/data数据.csv', 'rb')

file = open(path)
pd.read_csv(file)
```

## 字符串前面添加u,r,b的含义
u/U:表示unicode字符串 
不是仅仅是针对中文, 可以针对任何的字符串，代表是对字符串进行unicode编码。 
一般英文字符在使用各种编码下, 基本都可以正常解析, 所以一般不带u；但是中文, 必须表明所需编码, 否则一旦编码转换就会出现乱码。 
建议所有编码方式采用utf8

r/R:非转义的原始字符串 
与普通字符相比，其他相对特殊的字符，其中可能包含转义字符，即那些，反斜杠加上对应字母，表示对应的特殊含义的，比如最常见的”\n”表示换行，”\t”表示Tab等。而如果是以r开头，那么说明后面的字符，都是普通的字符了，即如果是“\n”那么表示一个反斜杠字符，一个字母n，而不是表示换行了。 
以r开头的字符，常用于正则表达式，对应着re模块。

b:bytes 
python3.x里默认的str是(py2.x里的)unicode, bytes是(py2.x)的str, b”“前缀代表的就是bytes 
python2.x里, b前缀没什么具体意义， 只是为了兼容python3.x的这种写法

## 4、处理txt数据
>import pandas as pd
df_data = pd.read_table('./data.txt')
data.to_csv('data.txt', sep='\t', index=False)

## 5、数据可视化
```python
import matplotlib.pyplot as plt
%matplotlib inline

#marker为形状、s为形状大小，线条没有，c为颜色，也可以写全称size、color
#scatter为散点图、plot为折线图

plt.scatter(x轴数据, y轴数据, marker = 'o', s=200, c='red', label=标签名) 
plt.plot(x轴数据, y轴数据, marker = 'x', c='black', label='Comprehensive')
plt.legend()  # 让图例生效

plt.xlabel(x轴名称)
plt.ylabel(y轴名称)

plt.show()
```
```
def scatter(X, Y):
    #产生测试数据  
    x = np.arange(1,10)  
    y = x  
    fig = plt.figure()  
    ax = fig.add_subplot(111)   # 设置子图
    #设置标题  
    ax.set_title('Scatter Plot')  
    #设置X轴标签  
    plt.xlabel('X')  
    #设置Y轴标签  
    plt.ylabel('Y')  
    #添加批注
    for i in range(4):    # xy表示批注点位置，xxtext表示批注文字位置，arrowprops加箭头
        ax.annotate(Y[i],xy=(X[i,0],X[i,1]), xytext=(X[i,0],X[i,1]), arrowprops=dict(facecolor='black', shrink=0.05))
    #画散点图  
    ax.scatter(X[:,0],X[:,1],s = 75,c = 'r',marker = 'o',alpha=.5)  
    #设置图标  
    plt.legend('X')  
    #显示所画的图  
    plt.show()
```

### 画函数曲线
```
import numpy as np

x = np.arange(0, 12)
y1 = 2 * x + 5   #直线函数
y2 = x ** 2 + 5  #曲线函数

plt.plot(x, y1, c='yellow')
plt.plot(x, y2, c='red')

plt.show()
```

## 6、dataframe增加一行数据或者一列数据
### 增加一行
```
df = pd.DataFrame(columns=['name','sex','age', 'other'])
# 方法1(必须加列名)  居然无效???
df.append({'name': 'hejian', 'sex': 'man', 'age': 24, 'other': 'handsome'}, ignore_index=True, verify_integrity=False)

#方法2
df.loc[2] = ['hejian',  'man',  24, 'handsome']
```

## 7、排序
```
sorted([5, 2, 3, 1, 4])
a = [5, 2, 3, 1, 4]
a.sort()

sorted(res, key = lambda x:x[0])
df.sort_values(by=)
```

## 8、输出格式
```
ans = [1, 2, 3, 4]
res = []
for elem in ans:
    res.append(str(elem))
print(' '.join(res))  #按照空格间隔输出
print('*'.join(res))  #按照星号间隔输出
```

## 9、基本操作
### 创建DataFrame对象
```
df = pd.DataFrame(np.random.randint(0,10,(4, 3)), columns=list('bde'), index=range(4))

df = pd.DataFrame([1, 2, 3, 4, 5], columns=['cols'], index=['a','b','c','d','e'])
df.index
df.columns
df = pd.DataFrame(np.random.randint(low=0, high=10, size=(5, 5)), columns=['a', 'b', 'c', 'd', 'e'])
df = pd.DataFrame(data=d, dtype=np.int8)
df = pd.DataFrame({'x':x, 'y':y}, columns=['x', 'y'])
```

### 根据索引查看数据
>df.loc['a']   # 索引为ａ这一行的数据
df.iloc[0]      #跟上面的操作等价，一个是根据索引名，一个是根据数字索引访问数据

### 对每个元素乘以２
>print df.apply(lambda x:x*2)

### 对每个元素求平方(支持ndarray一样的向量化操作)
>print df**2

### 默认合并之接受索引已经存在的值
通过指定参数 how，指定合并的方式：inner(交集)、outer(并集)
>print dfb.join(df_a,how='inner')   # 合并两个DataFrame对象的交集

### 对DataFrame对象进行列扩充
>df['col4'] = ['cnn','rnn']      #直接添加一列数据

### 字段类型转换
```
import numpy as np
arr = np.array([1, 2, 3])
print(type(arr))
print(arr.dtype)
brr = arr.astype(np.float64)
print(type(brr))
print(brr.dtype)
print(arr)
print(brr)
crr = arr.astype(str)
print(type(crr))
print(crr.dtype)
crr
```

## 10、连接合并多个dataframe
```
df = df1.append(df2, ignore_index=True)  # 需要重新index
df
````
## 11、增删改查
[基本操作]()




# 二、基础的特征工程
## 1、查看数据类型和一些值
>df.info()
df.describe()
## 2、查看是否有缺失值
```
isnull
isna
isin(values)
```

## 3、良/恶性乳腺癌肿瘤预测实例
[ipython notebook分析]()
```
# 创建特征列表。
column_names = ['Sample code number', 'Clump Thickness', 'Uniformity of Cell Size', 'Uniformity of Cell Shape', 'Marginal Adhesion', 'Single Epithelial Cell Size', 'Bare Nuclei', 'Bland Chromatin', 'Normal Nucleoli', 'Mitoses', 'Class']

# 使用pandas.read_csv函数从互联网读取指定数据。
data = pd.read_csv('https://archive.ics.uci.edu/ml/machine-learning-databases/breast-cancer-wisconsin/breast-cancer-wisconsin.data', names = column_names )

# 将?替换为标准缺失值表示。
data = data.replace(to_replace='?', value=np.nan)
# 丢弃带有缺失值的数据（只要有一个维度有缺失）。
data = data.dropna(how='any')

# 输出data的数据量和维度。
data.shape

# 使用sklearn.cross_valiation里的train_test_split模块用于分割数据。
from sklearn.cross_validation import train_test_split

# 随机采样25%的数据用于测试，剩下的75%用于构建训练集合。
X_train, X_test, y_train, y_test = train_test_split(data[column_names[1:10]], data[column_names[10]], test_size=0.25, random_state=33)

# 查验训练样本的数量和类别分布。
y_train.value_counts()

# 查验测试样本的数量和类别分布。
y_test.value_counts()

# 从sklearn.preprocessing里导入StandardScaler。
from sklearn.preprocessing import StandardScaler
# 从sklearn.linear_model里导入LogisticRegression与SGDClassifier。
from sklearn.linear_model import LogisticRegression
from sklearn.linear_model import SGDClassifier

# 标准化数据，保证每个维度的特征数据方差为1，均值为0。使得预测结果不会被某些维度过大的特征值而主导。
ss = StandardScaler()
X_train = ss.fit_transform(X_train)
X_test = ss.transform(X_test)

# 初始化LogisticRegression与SGDClassifier。
lr = LogisticRegression()
sgdc = SGDClassifier()

# 调用LogisticRegression中的fit函数/模块用来训练模型参数。
lr.fit(X_train, y_train)
# 使用训练好的模型lr对X_test进行预测，结果储存在变量lr_y_predict中。
lr_y_predict = lr.predict(X_test)

# 调用SGDClassifier中的fit函数/模块用来训练模型参数。
sgdc.fit(X_train, y_train)
# 使用训练好的模型sgdc对X_test进行预测，结果储存在变量sgdc_y_predict中。
sgdc_y_predict = sgdc.predict(X_test)

# 从sklearn.metrics里导入classification_report模块。
from sklearn.metrics import classification_report

# 使用逻辑斯蒂回归模型自带的评分函数score获得模型在测试集上的准确性结果。
print 'Accuracy of LR Classifier:', lr.score(X_test, y_test)
# 利用classification_report模块获得LogisticRegression其他三个指标的结果。
print classification_report(y_test, lr_y_predict, target_names=['Benign', 'Malignant'])

 # 使用随机梯度下降模型自带的评分函数score获得模型在测试集上的准确性结果。
print 'Accuarcy of SGD Classifier:', sgdc.score(X_test, y_test)
# 利用classification_report模块获得SGDClassifier其他三个指标的结果。
print classification_report(y_test, sgdc_y_predict, target_names=['Benign', 'Malignant'])
```

## 4、召回率、精确率和F1值
假设我们手上有60个正样本，40个负样本，我们要找出所有的正样本，系统查找出50个，其中只有40个是真正的正样本，计算上述各指标。

TP: 将正类预测为正类数  40
FN: 将正类预测为负类数  20
FP: 将负类预测为正类数  10
TN: 将负类预测为负类数  30

准确率(accuracy) = 预测对的/所有 = (TP+TN)/(TP+FN+FP+TN) = 70%
精确率(precision) = TP/(TP+FP) = 80%
召回率(recall) = TP/(TP+FN) = 2/3
F值  = 正确率 * 召回率 * 2 / (正确率 + 召回率) （F 值即为正确率和召回率的调和平均值）
白话：精确率就是在所有预测为正例中有多少是预测正确的，召回率就是在全部本身就是正样本中有多少预测正确。

## 5、sklearn.model_selection.train_test_split随机划分训练集和测试集
train_test_split是交叉验证中常用的函数，功能是从样本中随机的按比例选取train data和testdata，形式为：

>X_train,X_test, y_train, y_test =
cross_validation.train_test_split(train_data,train_target,test_size=0.4, random_state=0)

参数解释：
train_data：所要划分的样本特征集
train_target：所要划分的样本结果
test_size：样本占比，如果是整数的话就是样本的数量
random_state：是随机数的种子。

随机数种子：其实就是该组随机数的编号，在需要重复试验的时候，保证得到一组一样的随机数。比如你每次都填1，其他参数一样的情况下你得到的随机数组是一样的。但填0或不填，每次都会不一样。
随机数的产生取决于种子，随机数和种子之间的关系遵从以下两个规则：
种子不同，产生不同的随机数；种子相同，即使实例不同也产生相同的随机数。

# 三、实例篇
数据文件：data.csv   data.txt  data.xlsx
数据内容(高中成绩)：

Date  |  Chinese  |  Math  |  English  |  Comprehensive 
:-----:|:----------:|:-------:|:--------:|:-----------------:
7         |    111          |   130  |     127      |        269    
8           |                   |    159|     ok        |       191
9       |       137         |   119  |    99          |     250
10      |       97          |   149  |   89         |       235
11      |       120         |   135 |    116        |       282 

## 1、生成数据并保存读取
```
import pandas as pd

if __name__=='__main__':
    data = pd.DataFrame(columns=['Date','Chinese','Math', 'English', 'Comprehensive'])
    data.loc[0] = [7,  111, 130, 127, 269]
    data.loc[1] = [8,  '', 159, 'ok', 191]
    data.loc[2] = [9, 137, 119, 99, 250]
    data.loc[3] = [10, 97, 149, 89, 235]
    data.loc[4] = [11, 120, 135, 116, 282]

    data.to_csv('')
```

# 四、附录
## 去除警告
```
import warnings
warnings.filterwarnings("ignore")

def ignore_warn(*arg, *swarg):
    pass

warning.warn = ignore_warn
```

### 忽略命令行下警告错误的输出
```
python -W ignore yourscript.py
with open as [for   ]
```

## enumerate
```
如果对一个列表，既要遍历索引又要遍历元素时，首先可以这样写：
list1 = ["这", "是", "一个", "测试"]
for i in range (len(list1)):
    print i ,list1[i]

上述方法有些累赘，利用enumerate()会更加直接和优美：
list1 = ["这", "是", "一个", "测试"]
for index, item in enumerate(list1):
    print index, item
>>>
0 这
1 是
2 一个
3 测试

enumerate还可以接收第二个参数，用于指定索引起始值，如：
list1 = ["这", "是", "一个", "测试"]
for index, item in enumerate(list1, 1):
    print index, item
>>>
1 这
2 是
3 一个
4 测试
```

### 补充
如果要统计文件的行数，可以这样写：
>count = len(open(filepath, 'r').readlines())
这种方法简单，但是可能比较慢，当文件比较大时甚至不能工作。

可以利用enumerate()：
```
count = 0
for index, line in enumerate(open(filepath,'r'))： 
    count += 1
```

## python 字符串查找的4个方法
### 1 find()方法：查找子字符串，若找到返回从0开始的下标值，若找不到返回-1

info = 'abca'
print info.find('a')##从下标0开始，查找在字符串里第一个出现的子串，返回结果：0

info = 'abca'
print info.find('a',1)##从下标1开始，查找在字符串里第一个出现的子串：返回结果3

info = 'abca'
print info.find('333')##返回-1,查找不到返回-1
### 2 index()方法：

python 的index方法是在字符串里查找子串第一次出现的位置，类似字符串的find方法，不过比find方法更好的是，如果查找不到子串，会抛出异常，而不是返回-1

info = 'abca'
print info.index('a')
print info.index('33')

### 3 4 rfind和rindex方法用法和上面一样，只是从字符串的末尾开始查找。

如果查找全部，可以先找到第一个，然后从当前为起点继续查找。另外一种方法就是正则表达式。

