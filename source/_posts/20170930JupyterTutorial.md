---
layout: '[default_layout]'   
title: JUpyter Notebook学习                     
date: 2017-09-30 17:58:41  
toc: true                  
tags:                        
- JUpyter Notebook

categories:                  
- 

---
## 简介
&emsp;&emsp;jupyter,一个一体化的语言,IDE及通用分布式架构环境。比WEB更自然，jupyter用于通用软件开发的创新意义：使任何传统程序秒变WEB。Jupyter Notebook（此前被称为 IPython notebook）是一个交互式笔记本，支持运行 40 多种编程语言。

<!--more-->

&emsp;&emsp;目前用过的python ide有spyder, pycharm以及近年出的仿R studio的Rodeo，还是感觉jupyter notebook用的最得心应手。特别是在数据分析、机器学习等python编程的主力领域，我们的研究过程常常是探索性的，导入数据，查看数据的统计特征，试试这个模型，试试那个处理方法等，在这种情况下，notebook确实可以为我们提供一个高级“草稿本”，有了它，我们可以展示我们的探索过程，也可以在事后删去那些不相关的部分。应该说，jupyter notebook的流行是和特定领域的工作方式分不开的。比如，在python的网络开发领域，更流行的应该是pycharm，因为大家的工作并不一样。jupyter notebook的另外一个妙用是：提供了一种新的代码复用的方式。编程领域常见的代码复用方式编写一个新的外部库，然后提交到pypi或github,然后大家需要pip安装，整个流程还是比较复杂的。这种方式对于那些大型的库是很好的，但对于一些处理小问题的小脚本就有点大材小用了。比如，我只是想写一个绘制函数图像的脚本，其中预设一些绘图的格式，我就是只需要将相关功能实现在一个Notebook中，像这样：使用matplotlib绘制函数图像，当你把notebook下载起来，安装必要的库，然后就可以直接在notebook是使用相应的功能了。在notebook常用的领域中，像科学计算、数据分析与机器学习，这种代码复用的方式是非常方便的。至于notebook可能造成的滥用问题，我觉得这个可以通过使用者的代码规范来加以解决，适当设计整个book的结构，比如第一行写上这个Notebook的作者，联系方式，主要用途等信息，第二行导入所有必要的库，然后之下的每一行都是一个单独的功能模块，这样整个代码的结构就会清晰很多。这个方面，一些kaggle上面优秀的notebook很值得学习。

## 参考
[Python·Jupyter Notebook各种使用方法记录](http://blog.csdn.net/tina_ttl/article/details/51031113)

[27 个Jupyter Notebook的小提示与技巧](http://liuchengxu.org/pelican-blog/jupyter-notebook-tips.html)

[Python的functools.reduce用法](http://www.cnblogs.com/alan-babyblog/p/5194399.html)


我们需要使用其他类型的单元格，即 Header单元格和 Markdown单元格。

首先，我们在顶部添加一个 notebook 的标题。选中第一个单元格，然后点击Insert -> Insert单元格above（在上方插入单元格）。你会发现，文档的顶部马上就出现了一个新的单元格。点击在快捷键栏中的单元格类型，将其变成一个标题单元格（heading cell）

要想在 Jupyter notebook 中使用 matplotlib，需要告诉 Jupyter 获取 matplotlib 生成的所有图形，并将其嵌入 notebook 中。为此，需要计算：

%matplotlib inline

## 修改工作路径
网上很多教程，然而在我的windows10系统上毫无作用，有很多人跟我有[相同的情况](https://www.zhihu.com/question/31600197)。
根据方法一，在我的笔记本上成功，相同的环境，不懂。

### 方法一
1. cmd: jupyter notebook --generate-config
2. 找到 ~\.jupyter 中的文件 jupyter_notebook_config.py
3. 修改c.NotebookApp.notebook_dir = '你的目录'
4. 注意`\`这个是转义字符。

    ## The directory to use for notebooks and kernels.
    #c.NotebookApp.notebook_dir = u'C:\\Users\\Administrator\\Desktop\\JupyterNotebook'

### 方法二
windows下一种解决方案：在你要打开的目录里新建文本文档输入以下内容
    rem -- start_ipython_notebook_here.bat ---
    dir
    ipython notebook 
    pause
保存另存为.bat文件，使用时双击即可。

### 方法三
    ## The default URL to redirect to from `/`
    c.NotebookApp.default_url = '/tree/Desktop/JupyterNotebook'

### 方法四
第一步进入cmd，然后输入工作文件夹路径cd进入，最后运行jupyter-notebook命令即可。	
	
## [添加登录密码](https://www.jianshu.com/p/a9de7a089834)
	# Preparing a hashed password使用python运行为 Jupyter 创建密钥
    >>from notebook.auth import passwd
    >>passwd()
	Enter password: 
	Verify password: 
	'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
	
	# 修改配置文件
    c.NotebookApp.password = u'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'

## 运行BUG
### 1. IOPub data rate exceeded.

    The notebook server will temporarily stop sending output
    to the client in order to avoid crashing it.
    To change this limit, set the config variable
    `--NotebookApp.iopub_data_rate_limit`.

### 2. Python中matplotlib.pyplot.hist显示x must be 1D or 2D

只需要将倒数第二行的h=plot.hist(deg.values(),100)改为h=plot.hist(list(deg.values()),100)就可以了，python 3.x。

### 3. Python 'TypeError': 'Generator' object is not subscriptable

    def gcd1(a,b):
        """ the euclidean algorithm """
        while a:
                a, b = b%a, a
        return b
    for x in set1:
        print(gcd1(x, set2[x]))

A:This means that set2 is a generator, to get around this just turn it into a list.

    set2_list = list(set2)
    for x in set1:
        print(gcd1(x, set2_list[x]))

### 4. 消除警告提示语
    import warnings
    warnings.filterwarnings("ignore")

