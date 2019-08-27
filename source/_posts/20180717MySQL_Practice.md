---
layout: '[default_layout]'   
title: MySQL实战           
date: 2018-07-27 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- MySQL
- Sql

categories:                  
- SQL

---
# 一、linux下查看mysql服务的两种方式：
方式一：
[root@localhost bin]ps -ef|grep mysql

方式二：
[root@localhost bin]netstat -nlp
<!--more-->
# 二、linux下启动mysql服务的两种方式：
命令行方式：
[root@localhost bin]cd /usr/bin
[root@localhost bin]./mysqld_safe &

服务方式：
[root@localhost ~]service mysql start

如果服务在启动状态，直接重启服务用以下命令：
[root@localhost ~]service mysql restart

# 三、linux下关闭mysql服务的两种方式：
命令行方式：
[root@localhost ~]mysqladmin -u root shutdown

服务方式：
[root@localhost ~]service mysql stop

# 1、登录MySQL
>mysql -u root(用户名) -p
输入密码

# 2、MySQL添加用户、删除用户与授权
https://www.cnblogs.com/wanghetao/p/3806888.html
https://www.cnblogs.com/xujishou/p/6306765.html

# 2、找到第N高的成绩
索引问题就是一个查找问题。。。
数据库索引，是数据库管理系统中一个排序的数据结构，以协助快速查询、更新数据库表中数据。索引的实现通常使用B树及其变种B+树。
[数据库索引使用的好处与坏处](https://blog.csdn.net/csy288/article/details/54586410)

https://www.jianshu.com/p/dc053deb94f2
https://blog.csdn.net/sanqima/article/details/42746419
https://baike.baidu.com/item/%E8%B4%9D%E5%8F%B6%E6%96%AF%E5%85%AC%E5%BC%8F/9683982?fr=aladdin
https://baijiahao.baidu.com/s?id=1596169784713150436&wfr=spider&for=pc

# Mark表
| ID  |  sex   | course   |  mark |
|:---:|:------:|:--------:|:-----:|
|A001 |男      |语文      |98     |
|A002 |男      |语文      |92     |
|A003 |男      |数学      |84     |
|A004 |女      |英语      |87     |
|A001 |男      |数学      |68     |
|A007 |女      |英语      |77     |

# Student表
| ID  |  name   |   class  |  birth |  native |
|:---:|:-------:|:--------:|:------:|:-------:|
|A001 |张三     |一班      |1998    |湖北武汉 |
|A002 |李四     |二班      |1992    |重庆万州 |
|A003 |王麻子   |一班      |1984    |重庆万州 |
|A004 |小美     |一班      |1987    |湖北武汉 |
|A005 |小米     |二班      |1968    |湖南长沙 |

# 建表语句
```


```
# 问题
1. 查找分数大于80的数据（ID、课程、分数）
2. 显示学生所有的信息，A001就显示第一条
3. 显示学生的年龄
4. 没有参加考试的学生姓名
5. 参加考试的学生姓名（不重复）
6. 课程平均分大于80的学生姓名
7. 显示地区分数的简单总和
8. 学生的课程平均分排名
9. 班级的课程平均分
10. 谈谈两张表在结构设计上的问题






