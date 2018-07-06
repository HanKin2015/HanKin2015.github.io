---
layout: '[default_layout]'   
title: 那些年玩的英雄联盟LOL           
date: 2017-06-23 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- Sublime

categories:                  
- others

---
大一的时候安装了英雄联盟，但是没有怎么玩，打人机都打不赢，我还记得当时玩德玛出了6个多兰盾。大一暑假的时候，和一哥呆在一个宿舍，开始了我的英雄联盟之路，一直打到了大四，研究生的时候就没有怎么玩了，现在装了Linux系统就更不能玩了。再说，我现在迷上了王者荣耀，准备今天20180419上一波王者，目前星耀2两颗星，加油！！！
<!--more-->
英雄联盟
|大区   	|大号  |      小号|
|:----------:|:-------:|:------:|
|比尔吉沃特|  1655  | 245  |
|巨龙之巢| 480| 0|
|德玛西亚| 0  | 276 |
|男爵领域| 71 | 0  |
|无畏先锋|  15 | 121 |
|扭曲丛林| 0 |  *  |
|战争学院|  39  |   0  |
|艾欧尼亚|  0 | 113|
|黑色玫瑰|  67 | 0 |
|恕瑞玛|  1 |  116 |
|水晶之痕| 0 | * |
|弗雷尔卓德| * | 0 |
|德克萨斯| * | 14 |
|总共区数 | 11  | 10 |
|总共场数| 3213| 3213|

16岁，她向我表白，我拒绝了，毕业后各奔东西。我们经历了不同的爱情。26岁时，人群中，我向她求婚。她问我，当初你为什么不答应。我说，我想成为你的归宿而不是初恋。现在我们才懂得什么是爱情。

长到这么大，我说不出来我最爱的一部电影，说不出来我最爱的一首歌，说不出来我最爱的一个人。时常觉得人生其实没那么有趣，偶尔也会质疑活着的意义，所有来自于书上和别人口中的意义都不曾说服过我。但今天突然觉得，大概人生最大的意义就是用余生去找到那些最爱吧。

1.2还有一个停用词语料库，所谓停用词就是指高频词汇，如the,a,and等等。有时候在进一步处理之前需要将他们过滤出去。

>>>from nltk.corpus import stopwords
>>>stopwords=stopwords.words('english')
['i', 'me', 'my', 'myself', 'we', 'our', 'ours', 'ourselves', 'you', 'your', 'yours', 'yourself', 'yourselves', 'he', 'him', 'his', 'himself', 'she', 'her', 'hers', 'herself', 'it', 'its', 'itself', 'they', 'them', 'their', 'theirs', 'themselves', 'what', 'which', 'who', 'whom', 'this', 'that', 'these', 'those', 'am', 'is', 'are', 'was', 'were', 'be', 'been', 'being', 'have', 'has', 'had', 'having', 'do', 'does', 'did', 'doing', 'a', 'an', 'the', 'and', 'but', 'if', 'or', 'because', 'as', 'until', 'while', 'of', 'at', 'by', 'for', 'with', 'about', 'against', 'between', 'into', 'through', 'during', 'before', 'after', 'above', 'below', 'to', 'from', 'up', 'down', 'in', 'out', 'on', 'off', 'over', 'under', 'again', 'further', 'then', 'once', 'here', 'there', 'when', 'where', 'why', 'how', 'all', 'any', 'both', 'each', 'few', 'more', 'most', 'other', 'some', 'such', 'no', 'nor', 'not', 'only', 'own', 'same', 'so', 'than', 'too', 'very', 's', 't', 'can', 'will', 'just', 'don', 'should', 'now', 'd', 'll', 'm', 'o', 're', 've', 'y', 'ain', 'aren', 'couldn', 'didn', 'doesn', 'hadn', 'hasn', 'haven', 'isn', 'ma', 'mightn', 'mustn', 'needn', 'shan', 'shouldn', 'wasn', 'weren', 'won', 'wouldn']
