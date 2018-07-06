---
layout: '[default_layout]'   
title: QT学习                     
date: 2017-09-30 17:58:41  
toc: true                  
tags:                        
- QT
- C++

categories:                  
- C/C++

---

[Qt参考文档](http://www.kuqin.com/qtdocument/index.html)
[Qt开源社区](http://www.qter.org/)
[Qt快速入门教程](http://www.qter.org/portal.php?mod=view&aid=26)

## 关于Qt
&emsp;&emsp;Qt是一个多平台的C++图形用户界面应用程序框架。Qt是完全面向对象的很容易扩展，并且 允许真正地组件编程。Qt是Trolltech公司的一个产品。

Qt被按不同的版本发行：
<!--more-->

- Qt企业版和Qt专业版 提供给商业软件开发。它们提供传统商业软件发行版并且提供免费升级和技术支持服务。 如果要获得最新报价，请浏览Trolltech公司网站的价格和可行性页面，或者与sales@trolltech.com联系。 企业版比专业版多一些扩展模块。
- Qt自由版是Qt仅仅为了开发自由和开放源码软件 提供的Unix/X11版本。在Q公共许可证和GNU通用公共许可证 下，它是免费的。最新的版本可以在这里下载。
- Qt/嵌入式自由版是Qt为了开发自由软件提供的嵌入式版本。 在GNU通用公共许可证下，它是免费的。

## 第1篇 Qt开发环境的搭建和hello world
环境是：Windows 10 + Qt 5.8.0（包含QtCreator 4.2.1）
QtCreator作为Qt官方的开发环境，对Qt各方面支持都非常完善，而且使用起来体验也非常好，所以没有特殊情况，建议大家使用Qt Creator进行Qt开发（PS：小白疑惑：难道还能使用其他IDE进行Qt开发？答疑：当然了，比如用的比较多的VS，不仅如此，即便不用IDE，直接使用记事本也可以编写Qt程序！）。

QtCreator主界面分为了6个模式：欢迎模式、编辑模式、设计模式、Debug调试模式、项目模式和帮助模式，分别由左侧的6个图标进行切换，对应的快捷键是Ctrl + 数字1到6。

这里的基类可选的有QMainWindow、QWidget和QDialog三个，关于这三个类会在后面的篇章中详细介绍，这里只要知道QMainWindow是一般桌面程序的主窗口即可。

问题一：http://blog.csdn.net/lyc_daniel/article/details/12945449
问题二：http://jingyan.baidu.com/article/ad310e80c231f31849f49e0f.html
问题三：http://blog.csdn.net/shangguanyunlan/article/details/54143100

### 发布程序
#### 设置应用程序图标

想要发布的程序有个漂亮的图标，操作非常简单，把要设置的ico图标放到源码目录，例如myico.ico文件，然后打开项目文件helloworld.pro，在最下面添加一行代码：
    RC_ICONS = myico.ico

巨坑运行debug中的exe文件：找不到动态链库，没有把dll文件拷贝完全，Qt安装目录下bin目录中的libgcc_s_dw2-1.dll、libstdc++-6.dll、libwinpthread-1.dll、Qt5Core.dll、Qt5Gui.dll和Qt5Widgets.dll这6个文件+Qt5Cored.dll、Qt5Guid.dll和Qt5Widgetsd.dll这3个文件拷贝到debug中。

这里是Qt提供的几个工具软件。其中Assistant是Qt助手，它已经集成到了QtCreator中，就是帮助模式；Designer是Qt设计师，它也集成到了Qt Creator中，就是设计模式； Linguist是Qt语言家，用来对软件进行国际化翻译。

## 第2篇 Qt5基础（二）编写Qt多窗口程序
在代码中直接使用中文本不是一个好的习惯，建议在编写程序时使用英文，当程序完成后使用Qt语言家来翻译整个软件中要显示的字符串，这个在后面的教程中会讲到。本系列教程中为了简便，一般会直接在代码中使用中文，但是为了以后可以进行国际化翻译，在界面上显示的字符串一般使用tr()函数包含。

有的童鞋可能会问，如果多次按下按钮，那么每次都会生成一个对话框，是否会造成内存泄露或者内存耗尽？这里简单说明一下，Qt的对象树机制保证了不会造成内存泄露，而且不用写delete语句，因为指明了对话框的父部件，所以当主窗口MainWindow销毁时会自动销毁创建的对话框。当然，严谨的童鞋也可以在mainwindow.h文件中先定义一个对话框对象，并在构造函数中进行创建，然后再到这里使用。

信号和槽是Qt非常核心的内容，可以说如果不会灵活使用信号和槽，那么使用Qt也就失去了意义，但是大家也不用急于掌握它，后面我们会循序渐进地学习。

还可以使用ctrl + 空格键来强制代码补全，不过这个一般会和我们的输入法的快捷键冲突，大家可以更改输入法的快捷键，也可以在Qt Creator中的工具→选项→环境→键盘中来设置快捷键。

方法一：button->disconnect，把信号槽断掉方法二：button->blockSignal(true)，让该按钮不再发出信号。等做完了再button->blockSignal(false)就行另：如果你的槽和按钮在同一线程，那么什么都不用做。在你执行槽函数的这段时间内，线程本身就不会响应事件。如果你这个槽函数耗时长达秒级，那么你会看到界面卡住了

放进scrollarea的窗口当然不期望自适应大小了，要不然怎么出滚动条。
想要实现你的设计：重写resizeEvent，设置按钮最小大小，这样可以保证scrollarea有效果
我猜测还可以使用QGraphicsView，用QGraphicsLayout ，不过既要出滚动条又能自适应大小这挺扯的

# 添加界面跳转 
右键添加文件->QT设计师界面类
Dialog without Buttons
类名：LoginDialog
头文件：logindialog.h
源文件：logindialog.cpp

# 在头文件里添加全局变量
变量需要初始化，否则调用后无法运行。

# 新建的ui界面，不能用ui添加布局，需要使用this

# 改变布局大小和字体、添加标题
    this->resize(500,400);
    this->setWindowTitle("一起Happy");
    QFont font;
    font.setPointSize(25);
    font.setFamily(("simsun"));
    this->setFont(font);

# 常用头文件

    #include <QDialog>
    #include <QPushButton>
    #include <QLabel>
    #include <QGridLayout>
    #include <QLineEdit>
    #include <QTextEdit>

# 居中显示
    userName->setAlignment(Qt::AlignHCenter);

# 输入框中的提示语显示
    userName->setPlaceholderText("请输入用户名");

# BUG
QTableWidget始终无法显示出来：没有设置行数。

# Big BUG
Dialog does not a type
头文件相互包含，删除互相包含。

比如：
classA.h
    #include "classB.h"

classB.h
    #include "classA.h"

这样会出现上面的报错。

# Qt捕捉窗口关闭事件与信号的捕捉
(1)首先添加依赖库：
[cpp]#include <QCloseEvent> 

(2)接着声明和定义closeEvent函数:
    a).h文件
[cpp]
protected: 
     void closeEvent(QCloseEvent *event); 

    b).cpp文件
[cpp]
void MainWindow::closeEvent(QCloseEvent *event) 
{ 
    //TODO: 在退出窗口之前，实现希望做的操作 
} 

# 确定界面
    QMessageBox mb(QMessageBox::Warning, "","确定要注销当前用户？");
    mb.setStandardButtons(QMessageBox::Ok|QMessageBox::Cancel);
    mb.setButtonText (QMessageBox::Ok,QString("确 定"));
    mb.setButtonText (QMessageBox::Cancel,QString("取 消"));
    if(mb.exec() == QMessageBox::Ok)
    {
        LoginDialog *loginDlg = new LoginDialog;
        this->hide();
        loginDlg->show();
    }

# 带参数的信号传递按钮
        QSignalMapper *signalmapper1 = new QSignalMapper(this);
        connect(joinBtn, SIGNAL(clicked()), signalmapper1,SLOT(map()));
        signalmapper1->setMapping(joinBtn,ee.EventID);
        connect(signalmapper1,SIGNAL(mapped(int)),this,SLOT(JoinBtnClicked(int)));


# 
    retrievePwd->setStyleSheet("background-color:transparent;font-size: 20px;color: rgb(0, 0, 0);font-family:'./fonts/方正宋刻本秀楷简体.TTF';");

















