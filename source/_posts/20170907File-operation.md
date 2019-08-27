---
layout: '[default_layout]'   
title: python文件操作
date: 2017-09-07 19:12:41
updated: 
permalink: 
render_drafts: true
copyright: true
password: 
comments: true
toc: true                  
tags:                        
- Python
- Rar
- Zip
- 解压
- 文件加密

categories:                  
- Python

---
## 1、读写文件
### 文件读写示例
	#!/usr/bin/python
	# -*- coding: UTF-8 -*-

	try:
	    f = open("testfile", "w")
	    f.write("这是一个测试文件，用于测试异常!!")
	except IOError:
	    print("Error: 没有找到文件或读取文件失败")
	else:
	    print("内容写入文件成功")
	finally:
		f.close()

<!-- more -->

### 文件的打开方式
	f = open(‘文件','mode')
	‘r'：只读（缺省。如果文件不存在，则抛出错误）
	‘w'：只写（如果文件不存在，则自动创建文件），此时无法调用f.read()方法，且当调用f.write()时，将清空文件原有内容
	‘a'：附加到文件末尾
	‘r+'：读写
	如果需要以二进制方式打开文件，需要在mode后面加上字符”b”，比如”rb”，”wb”等

### 文件的属性：
	f.closed #标记文件是否已经关闭，由close()改写
	f.encoding #文件编码
	f.mode #打开模式
	f.name #文件名
	f.newlines #文件中用到的换行模式，是一个tuple
	f.softspace #boolean型，一般为0，据说用于print

### 文件的读写方法
	f.read([size]) #size为读取的长度，以byte为单位
	f.readline([size]) #读一行，如果定义了size，有可能返回的只是一行的一部分
	f.readlines([size]) #把文件每一行作为一个list的一个成员，并返回这个list。其实它的内部是通过循环调用readline()来实现的。如果提供size参数，size是表示读取内容的总长，也就是说可能只读到文件的一部分
	f.write(str) #把str写到文件中，write()并不会在str后加上一个换行符
	f.writelines(seq) #把seq的内容全部写到文件中。这个函数也只是忠实地写入，不会在每行后面加上任何东西
	f.close() #关闭文件
	f.flush() #把缓冲区的内容写入硬盘
	f.fileno() #返回一个长整型的”文件标签“
	f.isatty() #文件是否是一个终端设备文件（unix系统中的）
	f.tell() #返回文件操作标记的当前位置，以文件的开头为原点
	f.next() #返回下一行，并将文件操作标记位移到下一行。把一个file用于for … in file这样的语句时，就是调用next()函数来实现遍历的
	f.seek(offset[,from]) #将文件打操作标记移到offset的位置。这个offset一般是相对于文件的开头来计算的，一般为正数。但如果提供了from参数就不一定了，from可以为0表示从头开始计算，1表示以当前位置为原点计算。2表示以文件末尾为原点进行计算。需要注意，如果文件以a或a+的模式打开，每次进行写操作时，文件操作标记会自动返回到文件末尾。
	f.truncate([size]) #把文件裁成规定的大小，默认的是裁到当前文件操作标记的位置。
	Python在读取一个文件时，会记住其在文件中的位置，如果第二次仍需要从头读取，则需要调用f.seek(0)重新从头开始读取。

## 2、压缩和解压缩文件1(zip/unzip)
1. 单个文件压缩成zip文件
	zFile = zipfile.ZipFile("./dict.zip", "w", zipfile.ZIP_DEFLATED)
	zFile.write("dict.txt")
	zFile.close()
	#ZIP_DEFLATED是压缩标志，如果使用它需要编译了zlib模块，如果仅仅是打包而不压缩的话，可以改为zipfile.ZIP_STORED

2. 把zip文件解压缩  
	zFile = zipfile.ZipFile("dict.zip","r")
	num = len(zFile.namelist())
	print(num)

	for filename in zFile.namelist():
	    data = zFile.read(filename)
	    file = open(filename, "w+b")
	    file.write(data)
	    file.close()

3. 压缩文件夹
	import os
	f = zipfile.ZipFile('dir.zip','w',zipfile.ZIP_DEFLATED)
	startdir = "./data"
	for dirpath, dirnames, filenames in os.walk(startdir):
	  for filename in filenames:
	    f.write(os.path.join(dirpath,filename))
	f.close()

## 3、Python os.walk() 方法
1. 概述
os.walk() 方法用于通过在目录树种游走输出在目录中的文件名，向上或者向下。
在Unix，Windows中有效。

2. 语法
walk()方法语法格式如下：
	os.walk(top[, topdown=True[, onerror=None[, followlinks=False]]])

3. 参数
	top -- 根目录下的每一个文件夹(包含它自己), 产生3-元组 (dirpath, dirnames, filenames)【文件夹路径, 文件夹名字, 文件名】。
	topdown --可选，为True或者没有指定, 一个目录的的3-元组将比它的任何子文件夹的3-元组先产生 (目录自上而下)。如果topdown为 False, 一个目录的3-元组将比它的任何子文件夹的3-元组后产生 (目录自下而上)。
	onerror -- 可选，是一个函数; 它调用时有一个参数, 一个OSError实例。报告这错误后，继续walk,或者抛出exception终止walk。
	followlinks -- 设置为 true，则通过软链接访问目录。

4. 返回值
该方法没有返回值。

## 4、markdown中的空格显示
	半角空格&ensp;或&#8194;
	全角空格&emsp;或&#8195;
	不换行空格&nbsp;或&#160; 

## 5、压缩和解压缩文件2(rar/unrar)
&emsp;&emsp;rarfile是模仿zipfile模块写的，所以接口几乎一样，只有rar和zip的字符差别。但是zip功能是python内置模块，rar不是，不是亲妈生的有些问题，还存在严重的跨平台问题。  
&emsp;&emsp;所以需要安装unrar包，我发现conda install unrar无法查询到包文件，改用了pip安装。

### conda和pip
&emsp;&emsp;Conda和pip服务于不同的目的，并且只在一小部分任务中直接竞争：即在孤立的环境中安装Python包。
pip代表Pip Installs Packages，是Python的官方认可的包管理器，最常用于安装在Python包索引（PyPI）上发布的包。   
&emsp;&emsp;pip和PyPI都由Python包装管理局（PyPA）管理和支持。   
&emsp;&emsp;简而言之，pip是Python包的通用管理器; conda是一个与语言无关的跨平台环境管理器。对于用户，最显着的区别可能是这样的：pip在任何环境中安装python包; conda安装在conda环境中的任何包装。如果你正在做的是在孤立的环境中安装Python包，conda和pip + virtualenv大多是可互换的，模数依赖处理和包可用性的一些差异。通过隔离环境(conda-env或virtualenv)，您可以在其中安装软件包，而无需修改您的系统Python安装。    
&emsp;&emsp;conda和pip服务不同的受众和不同的目的。 如果你想在现有的系统Python安装中管理Python包，conda不能帮助你：通过设计，它只能在conda环境中安装包。 如果你想说，使用依赖于外部依赖的许多Python包（NumPy，SciPy和Matplotlib是常见的例子），同时以一种有意义的方式跟踪这些依赖，pip不能帮助你：它 管理Python包和只有Python包。Conda和pip不是竞争对手，而是侧重于不同用户组和使用模式的工具。

安装后运行程序报错：“Couldn't find path to unrar library...”
参考：修改后始终报错，感觉Win10的环境变量生效有点慢，我在源文件中调试调试就自动能运行了。
http://blog.csdn.net/ysy950803/article/details/52939708
http://blog.csdn.net/big_talent/article/details/52367184

	#! rar文件的解压，和zip类似
	import os
	file_name = "dict.rar"
	if os.path.isfile(file_name):
	    pass
	else:
	    os.mkdir(file_name)
	    print('新建一个目录')
	rFile = rarfile.RarFile(file_name,mode='r',pwd=None)
	#os.chdir("dit.rar")
	print(type(rFile))
	print(rFile.filename)
	rFile.extractall()

&emsp;&emsp;弄了一半天，rar文件很蛋疼，好像不能进行压缩，只有解压方法。

### 其他压缩文件格式
- gz： 即gzip，通常只能压缩一个文件。与tar结合起来就可以实现先打包，再压缩。
- tar： linux系统下的打包工具，只打包，不压缩
- tgz：即tar.gz。先用tar打包，然后再用gz压缩得到的文件
- zip： 不同于gzip，虽然使用相似的算法，可以打包压缩多个文件，不过分别压缩文件，压缩率低于tar。
- rar：打包压缩文件，最初用于DOS，基于window操作系统。压缩率比zip高，但速度慢，随机访问的速度也慢。

#### gz
	import gzip  
	import os  
	def un_gz(file_name):  
	    """ungz zip file"""  
	    f_name = file_name.replace(".gz", "")  
	    #获取文件的名称，去掉  
	    g_file = gzip.GzipFile(file_name)  
	    #创建gzip对象  
	    open(f_name, "w+").write(g_file.read())  
	    #gzip对象用read()打开后，写入open()建立的文件中。  
	    g_file.close()  
	    #关闭gzip对象

#### tar
	import tarfile  
	def un_tar(file_name):  
	       untar zip file"""  
	    tar = tarfile.open(file_name)  
	    names = tar.getnames()  
	    if os.path.isdir(file_name + "_files"):  
	        pass  
	    else:  
	        os.mkdir(file_name + "_files")  
	    #由于解压后是许多文件，预先建立同名文件夹  
	    for name in names:  
	        tar.extract(name, file_name + "_files/")  
	    tar.close()  	 

```
import rarfile

rar = rarfile.RarFile('hello.rar')
# 返回所有文件夹和文件
print(rar.namelist())
# 原来文件大小
rar.getinfo('hello.txt').file_size
# 压缩后文件大小
rar.getinfo('hello.txt').compress_size

# 默认模式r,读
azip = zipfile.ZipFile('hello.rar', 'r')  # ['bb/', 'bb/aa.txt']
# 返回所有文件夹和文件
print(azip.namelist())
# 返回该zip的文件名
print(azip.filename)

# 压缩文件里bb文件夹下的aa.txt
azip_info = azip.getinfo('bb/aa.txt')
# 原来文件大小
print(azip_info.file_size)
# 压缩后大小
print(azip_info.compress_size)

# 这样可以求得压缩率，保留小数点后两位
print('压缩率为{:.2f}'.format(azip_info.file_size/azip_info.compress_size))
```

## 6、文件加密解密(base64/pycrypto)
### base64
DeprecationWarning: encodestring() is a deprecated alias since 3.1, use encodebytes()   
Base64编码，64指A-Z、a-z、0-9、+和/这64个字符，还有“=”号不属于编码字符，而是填充字符。为什么发明这么个编码呢，这个编码的原理很简单，“破解”也很容易，原因是电子邮件刚出来的时候，只传递英文字符，这没有问题，但是后来，中国人，日本人都要发email，这样问题就来了，因为这些字符有可能会被邮件服务器或者网关当成命令处理，故必须得有一种编码来对邮件进行加密，但是加密的目的是为了能够使得一些原始的服务器不出问题（现在服务器早已经能处理这些乱七八糟得情况了，不过因为已经形成了一套规范，所以邮件还是得经过Base64编码才能传递）。

优点：方法简单
缺点：不保险，别人拿到密文可以自己解密出明文

编码原理：将3个字节转换成4个字节((3 X 8)=24=(4X6))，先读入3个字节，每读一个字节，左移8位，再右移四次，每次6位，这样就有4个字节了。
解码原理：将4个字节转换成3个字节，先读入4个6位(用或运算)，每次左移6位，再右移3次，每次8位，这样就还原了。

	import base64
	str1 = base64.encodebytes(bytes("hello world","utf8"))
	#str2 = base64.encodestring(bytes("hello world","utf8"))
	str3 = base64.decodebytes(s1)
	print(str1)
	#print(str2)
	print(str3)

### pycrypto模块
高级加密标准（Advanced Encryption Standard，AES），是美国联邦政府采用的一种区块加密标准。这个标准用来替代原先的DES，已经被多方分析且广为全世界所使用。经过五年的甄选流程，高级加密标准由美国国家标准与技术研究院（NIST）于2001年11月26日发布于FIPS PUB 197，并在2002年5月26日成为有效的标准。2006年，高级加密标准已然成为对称密钥加密中最流行的算法之一。

AES只是个基本算法，实现AES有若干模式。其中的CBC模式因为其安全性而被TLS（就是https的加密标准）和IPSec（win采用的）作为技术标准。简单地说，CBC使用密码和salt（起扰乱作用）按固定算法（md5）产生key和iv。然后用key和iv（初始向量，加密第一块明文）加密（明文）和解密（密文）。

	#ValueError: AES key must be either 16, 24, or 32 bytes long
	#ValueError: IV must be 16 bytes long
	from Crypto.Cipher import AES
	obj = AES.new('This is a key123', AES.MODE_CBC, 'This is an IV456')
	message = "The answer is no"
	ciphertext = obj.encrypt(message)
	print(ciphertext)
	obj2 = AES.new('This is a key123', AES.MODE_CBC, 'This is an IV456')
	data = obj2.decrypt(ciphertext)
	print(data)

### zip暴力破解
说多了都是泪，python3默认使用bytes，python2默认使用string，导致以前的方法不能在python3中使用，花了我两天时间才明白这个道理，最后在linux中安装python2.7破解成功。
1. 进入虚拟机，下载并解压最新Python 2.7的源代码并解压安装
	wget https://www.python.org/ftp/python/2.7.10/Python-2.7.10.tar.xz 
	tar xf Python-2.7.10.tar.xz

2. 压缩文件：zip FileName.zip DirName
zip -re filename.zip filename 回车，输入2次密码  
zip -rP password filename.zip filename  password是要输入的密码  
unzip filename.zip 按提示输入密码 
unzip -P password filename.zip password是要解压的密码，这个不会有提示输入密码的操作 

3. 使用python命令直接编译python脚本文件
```
import zipfile 
try:
	with zipfile.ZipFile('Spyder.zip') as zFile:     #创建ZipFile对象
		#解压文件
		zFile.extractall(path='./',pwd='123')
		print('Extract the Zip file successfully!')
except:
	raise
	print('Extract the Zip file failed!')
```

4. python2.7版本密码字典破解zip
```
import zipfile

def get_pwd():
	#密码字典的路径
	pwdPath='pwd.txt'
	pwdFile=open(pwdPath,'r')
	for line in pwdFile.readlines():
		password=line.strip('\n')
		print 'Try the password %s' % password
		if pojie_zip('hejian.zip', password):
			break
	pwdFile.close()

def pojie_zip(path, password):
	if path[-4:]=='.zip':
		#path = dir+ '\\' +file
		#print path
		zFile = zipfile.ZipFile(path, "r",zipfile.zlib.DEFLATED)
		#print zip.namelist()
		try:
			#若解压成功，则返回True,和密码
			zFile.extractall(pwd=password)
			print ' ----success!,The password is %s' % password
			zFile.close()
			return True
		except:
			pass #如果发生异常，不报错
	print 'error'

if __name__ == "__main__":
	get_pwd()
```

http://www.jb51.net/article/86892.htm

参考：
http://www.jb51.net/article/88218.htm
http://blog.csdn.net/luoshengkim/article/details/46647423
http://blog.csdn.net/ice110956/article/details/26597179
[Python模块学习：zipfile zip文件操作](http://python.jobbole.com/81519/)