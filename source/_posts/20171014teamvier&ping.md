---
layout: '[default_layout]'   
title: 远程桌面连接           
date: 2017-10-14 21:36:41  
toc: true                  
tags:                        
- teamviewer
- ping

categories:                  
- Social Network

---
Everything should be made as simple as possible, but no simpler.
# 远程桌面mstsc
windows系统自带的远程桌面软件，但只能在同一个局域网里远程。
- win+R调出运行窗口输入mstsc
- 输入对方的ip地址
- 然后输入对方的开机密码

# 远程协助msra
Windows系统自带的软件，似乎只是远程演示，不能控制，没有过多的尝试。
- 邀请信任的人帮助你
- 帮助邀请人

<!--more-->

# 虚拟机virtualBox
参考：[ 为什么有时ping不通www.baidu.com但可以访问www.baidu.com网页？](http://blog.csdn.net/stpeace/article/details/45116425)
&emsp;&emsp;了解网络的人， 基本上都用过ping命令， 这个优秀的小工具通常能非常靠谱地检测网络的连通性。 但是， 某次， 在某个特殊环境中， 我发现ping不通www.baidu.com但可以访问www.baicom.com网页. 刚开始一看， 这不是矛盾了么？ 后来仔细想想， 觉得没什么不合理的。

&emsp;&emsp;ping www.baidu.com会利用到dns协议和icmp协议， 在上述特殊环境中， ping www.baidu.com后， 发现只有www.baidu.com对应的ip, 也就是说， dns解析是成功， 但没有ping过程的回显。

&emsp;&emsp;然后， 能登录www.baidu.com啊。 我们知道， 登录www.baidu.com首先会用到dns协议， 然后会利用http协议， 而http是基于tcp的， 所以三次握手是成功的。 那为什么ping不通呢？ 原来是网络环境屏蔽了ping用到的icmp报文， 而能上网， 表明网络连接肯定是好的， 且没有屏蔽掉三次握手报文， 也没有屏蔽掉端口。

&emsp;&emsp;另外， 在该环境下， 可以执行telnet www.baidu.com 80试试， 可以看到， 能连通， 再次说明三次握手ok的， 且没有屏蔽对应的端口。

总之:
- 在多数情况下， ping基本可以反映网络的连通与否； 
- 在少数情况下， ping不通的时候网络也可能是连通好的。

# [远程控制链接](http://www.bianceng.cn/OS/skills/201510/49156.htm)
曾经我的windows10电脑可以与虚拟机中所有linux系统ping通，然而今天出现问题了。windows能ping进去，centos系统ping不通。更奇怪的是master和其他三台服务器ping不通，被隔离了。

# anydesk远程桌面
因文件加密，请在下载前，暂时关闭360等类似软件，以免下载失败。

# teamviewer VS 向日葵
曾经是向日葵的用户，直到用了teamviewer才觉相见恨晚！teamviewer相对向日葵可以使用到的功能更加多样也更加专业与细致，对于收费而言teamviewer个人免费许可基本完胜向日葵，诸如文件传输等功能向日葵也有，不过不好意思要收费，不过相对最大问题在于移动客户端体验太差。清晰度上也不输于向日葵（基于局域网，不知teamviewer是否基于局域网优化过）不过向日葵有一点那就是硬件优势，向日葵更容易整合国内相对容易的硬件创新与制造环境，定制相应的产品。总结：软件优化与体验我倾向与teamviewer，与硬件相结合是向日葵的专长

# AnyDesk VS teamviewer
同样的连接，AD卡得要死，TV快得要命，看来天下是没有免费的午餐，不要钱的肯定不行。
AD不如TV流畅，穿透力不强。

最后，推荐使用teamviewer，感觉还不错，目前在使用中。













