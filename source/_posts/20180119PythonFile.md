---
layout: '[default_layout]'   
title: Python文件处理           
date: 2018-01-19 10:47:41  
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- Python

categories:                  
- others

---
# 第1章 文件简介
## 1-1 课程简介和基本概念...(05:47)
linux文件：一切设备都可以看成文件。P
文件属性：用户、读、写、执行权限。
文件：python中文件是对象。
<!--more-->
#第2章 Python文件基础操作
## 2-1 python文件操作之文件打开...(13:00)
ls -l:
-rw-rw-r--:第一个‘-’是文件，如果是目录应该是‘d’；第一组‘rw-’:表示当前用户有读写没有执行；第二组‘rw-’:表示当前用户组有读写没有执行；第三组‘r--’表示其他用户只有读权限
chmod +x hello.py：添加执行权限

chmod增加权限说明
如果给所有人添加可执行权限：chmod a+x 文件名；
如果给文件所有者添加可执行权限：chmod u+x 文件名；
如果给所在组添加可执行权限：chmod g+x 文件名；
如果给所在组以外的人添加可执行权限：chmod o+x 文件名；

Python 文件打开方式

name: 文件路径
mode: 打开方式
buf:  缓冲buffering大小

Python 读取方式

文件读取方式
read([size]): 读取文件，默认读取全部
readline([size]): 读取一行
readlines([size]): 读取完文件，返回每一行所组成的列表

文件写入方式
write(str): 将字符串写入文件
writelines(sequence): 写多行到文件

文件打开方式
r:  只读方式打开[文件必须存在]
w:  只写方式打开[文件不存在则创建文件 文件存在则清空文件内容]
a:  追加方式打开[文件不存在则创建文件]
r+: 读写方式打开
a+: 追加读写方式打开
rb: 二进制方式打开

## 2-2 python文件操作之文件读取...(11:35)
iter_f = iter(f)   使用iter（）方法，将文件转换成迭代器iter_f      不消耗内存
用来读取字节大小和缓冲大小接近的内容的行（内容大小不一定恰好是那么多），那个参数size的作用，是用来指定缓冲buff大小的，不设置的话默认是8192。

参数在1~DEFAULT_BUFFER_SIZE（2^13=8192）返回的结果是一样的，都是返回一个DEFAULT_BUFFER_SIZE左右大小；

但是8193就不一样了，他在DEFAULT_BUFFER_SIZE~2*DEFAULT_BUFFER_SIZE之间，返回2个DEFAULT_BUFFER_SIZE左右大小；
结论，size只有在设置成DEFAULT_BUFFER_SIZE的整数倍的时候，返回结果才会不一样！！

## 2-3 python文件操作之文件写入...(08:56)
主动调用close（）或flush方法，写缓存同步到磁盘；
写入数据量大于或等于写缓存，写缓存同步到磁盘

## 2-4 python文件操作之文件关闭...(06:07)
file.fileno() ：已打开文件个数，每打开一个文件，fileno数字累加，直到1024，就打不开了
因此良好的习惯：
打开一个文件，后面就要跟着close（）
更好的方法是用with closing（）函数，这样就不用担心打开文件后忘记关闭文件了
妙极妙极！

ps  查看进程
cat /proc/20384/limits
    进程/进程ID
查看打开文件的最大限制

## 2-5 python文件操作之文件指针...(08:52)
Python文件指针定位方式：
os.SEEK_SET ： 相对文件起始位置 = 0
os.SEEK_CUR ： 相对文件当前位置 = 1
os_SEEK_END ：相对文件结尾位置 = 2
seek(offset[, whence]) : 移动文件指针；
                      offset : 偏移量，可以为负数
                      whence ： 偏移相对位置

f.tell()  查指针
f.seek(5,os.SEEK.SEEK_CUR)

# 第3章 文件属性及OS模块使用
## 3-1 python文件属性编码格式...(15:24)
python2中
1 unicode转换utf-8：a = unicode.encode(u'慕课','utf-8')
2 创建utf-8编码文件：import codecs 
   f = codecs.open('test.txt','w','utf-8')
特别注意：python3默认是unicode编码，不需要转码到utf-8，‘慕课‘前面也不用加u

file.flieno()文件描述符
file.mode 文件打开权限
file.encoding 文件编码格式(如果没有返回值，就表示是一个ANSI码的文件)
file.closed 文件是否关闭
文件标准输入 sys.stdin
文件标准输出 sys.stdout
文件标准错误 sys.stderr

sys.argv

## 3-3 OS模块对文件和目录操作...(12:12)
os.open(filename, flag [,mode]):打开文件
os.O_CREAT:创建文件
os.O_RDONLY:只读方式打开
os.O_WRONLY:只写方式打开
os.O_RDWR:读写方式打开

os.read(fd, buffersize):读取文件
os.write(fd, string):写入文件
os.lseek(fd, pos, how): 文件指针操作
os.close(fd):关闭文件


os.access(path, mode)： F_OK, R_OK ,W_OK, X_OK
os.listdir(path)： 返回当path路径下所有文件名组成的列表
os.remove(path)：删除文件
os.rename(old, new)：修改文件或者目录名
os.mkdir(path[, mode])：创建目录
os.makedirs(path[, mode])：创建多级目录
os.removedirs(path)：删除多级目录
os.rmdir(path)：删除目录(目录必须空目录)

os.path方法
os.path.exists(path)：当前路径是否存在   |  也可以判断是否有该文件
os.path.isdir(s)：是否是一个目录
os.path.isfile(path)：是否是一个文件
os.path.getsize(filename)：返回文件大小  | 返回目录文件大小
os.path.dirname(p)：返回路径的目录
os.path.basename(p)：返回路径的文件名

# 第五章：练习
使用Python管理init文件：实现查询、添加、删除和保存。
import ConfigParser导入模块

cfg.set('section','name','value') 可以插入，修改section下的条目('name','value')
cfg.remove_option('section','name')删除section下的条目('name','value')，返回TRUE（删除成功）或FALSE

cfg.items(seif,section,raw=False,var=None)返回（name，value）元组tuple组成的列表,
利用for循环可以返回section下的所有值

cfg.read(self,filename) 读入一个文件  返回文件名列表
cfg.sections(self) 返回所有的section name 组成的一个列表

ConfigParser模块
利用ConfigParser模块的ConfigParser类来创建ConfigParser模块的对象cfg