---
layout: '[default_layout]'   
title: 马士兵的机器学习           
date: 2017-08-15 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- ML
- 马士兵

categories:                  
- ML

---
# 1、你应该了解这些
- 概率
- 编程的基础知识(java c++ c python)
- 一定的数学基础
- 得数据者得天下

# 内容
- 基本概念
    - MachineLearning DeepLearning
    - 训练集、测试集、特征值、分类、聚类、回归

<!-- more -->

- 常用算法
    - 监督学习
        - 分类
            - 决策树(Decision Tree)
            - KNN(k个nearest neigbors)
            - SVM(Support Vector Machine)
            - 神经网络(neural network)
            - 朴素贝叶斯(naive bayes)
        - 回归
            - 线性回归(Linear Regression)
            - 非线性回归(Non-Linear Regression)
    - 非监督学习
        - K-Means聚类等

# ML（machine learning）
## 交叉学科
- 计算机（软件、硬件、概率论、统计学、线代、高数、逼近论、凸分析、机械
- 机器不再是通过规则行动，而是通过归纳、统计来进行结果改进
- 机器不在需要外部明确的指示，而是通过经验和数据自动进行结果改进
- AI的核心
- 学习经验，针对任务，执行结果，经验越多，结果越好，则计算机有学习能力

## 应用
- 语音识别
    - 实时语音翻译
- 自然语言处理
    - Google翻译
- 自动驾驶
- 计算机视觉
    - 人脸识别
- 推荐系统GTR布加迪
- 无人机
- 垃圾邮件识别spam
- 机器人
- ...

# 深度学习
- 伴随大数据和计算能力的提高而产生的新的算法
- NN模拟人类神经元的构造
imagenet竞赛 --- 深度学习算法遥遥领先
DeepMind AlphaGo --- 规则 vs 学习

# 算法评估标准
- 准确率
- 速度
- 规模
- ...

# 2、神经网络入门教程
## 机器学习基本步骤
- 获取数据：获取、清洗、存储（hdfs）
- 数据拆分训练集和测试集
- 用特征向量训练算法
- 算法迭代与改进
- 实际应用
- 获取更多数据
- ...

## 多层前向神经网络
输入层（特征向量值）
隐藏层（可以有多层）
输出层（标记分类）
权重
偏置
激励函数activation function
隐藏层足够多，训练集足够大，可以模拟任何问题

## NN算法（BP=Back Propragation后向传播算法）
1. 特征向量标准化normalize(转化为0-1之间的值)
2. 随机初始化权重和偏置（-1 --- 1）
3. 传入样例
4. 计算神经元的值
    1. 对上层输入加权求和 $ S_j = \sum_{i=0}^m w_{ij} + b_j $
    2. 加上偏置值 
    3. 用激励函数产生最后结果（sigmoid function）逻辑函数？？
        1. $ x_j = f(S_j) $
        2. $ f(x) = \frac{1}{1+e^{-x}} $
---
1. 根据误差反向传送(更新，减小误差)
http://blog.csdn.net/acdreamers/article/details/44657439
2. 误差计算
    1. 输出层 Err = （结果）（1-结果）（预期值-结果）
    2. 隐藏层 Err = （结果）（1-结果）（后一层Err加权求和--Err*w）
    3. 权重更新
        1. $ \Delta w_{ij} = (leaningrate)Err_jO_i $
        2. $ w_{ij} = w{ij} + \Delta w_{ij} $
    4. 偏置更新
        1. $ \Delta b_j = (leaningrate)Err_j $
        2. $ b_j = b_j + \Delta b_j $
        3. 
## 训练终止
1. 一定次数（epoch）
2. 既定错误率
3. 权重更新低于某个Threshold（阈值）

# 激励函数
- 双曲函数
- 逻辑函数
- 阶跃函数
- ...

## Learning Rate
- 步长

## 训练NN
- 不断通过样例调整权重和偏向的过程
- 训练好的神经网络可以用于预测新的样例

## Tensorflow
- google开源的神经网络库
- 支持python/java/c

# 卷积神经网络入门
CNN: convolutional neural network
- TensorFlow是谷歌2015年开源的一个人工智能学习系统。主要目的是方便研究人员开展机器学习和深度神经网络方面的研究，目前这个系统更具有通用性，也可广泛用于其他计算领域。
- Tensorflow 支持多种前端语言，包括Python（Python也是tensorflow支持最好的前端语言），因此一般大家利用python实现对tensorflow的调用。

## 安装tensorflow
conda install tensorflow

## tensorflow基本使用
理解TensorFlow:
• 使用图(graph)来表示计算任务；
• 在被称之为会话(Session)的上下文(context)中执行图；
• 使用tensor（张量）表示数据；
• 通过变量(Variable)维护状态；
• 使用feed和fetch可以为任意的操作(arbitrary operation)赋值或者从其中获取数据。

TensorFlow是一个编程系统，使用图来表示计算任务。图中的节点被称作op（Operation），op可以获得0个或多个tensor，产生0个或多个tensor。每个tensor是一个类型化的多维数组。例如：可以将一组图像集表示成一个四维的浮点数组，四个维度分别是[batch，height，weight，channels]。
图（graph）描述了计算的过程。为了进行计算，图必须在会话中启动，会话负责将图中的op分发到CPU或GPU上进行计算，然后将产生的tensor返回。在Python中，tensor就是numpy.ndarray对象。

- TensorFlow程序通常被组织成两个阶段：构建阶段和执行阶段。
- 构建阶段:op的执行顺序被描述成一个图；
- 执行阶段:使用会话执行图中的op。
- 例如：通常在构建阶段创建一个图来表示神经网络，在执行阶段反复执行图中的op训练神经网络。













