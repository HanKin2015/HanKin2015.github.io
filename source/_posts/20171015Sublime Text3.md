---
layout: '[default_layout]'   
title: Sublime Text3           
date: 2017-10-15 10:47:41  
toc: true                  
tags:                        
- Sublime Text

categories:                  
- others

---
# 注册
百度一下：sublime text3 注册码 3143(版本号)
希望大家支持正版!!!
参考的注册码:

    —– BEGIN LICENSE —–  
    TwitterInc  
    200 User License  
    EA7E-890007  
    1D77F72E 390CDD93 4DCBA022 FAF60790  
    61AA12C0 A37081C5 D0316412 4584D136  
    94D7F7D4 95BC8C1C 527DA828 560BB037  
    D1EDDD8C AE7B379F 50C9D69D B35179EF  
    2FE898C4 8E4277A8 555CE714 E1FB0E43  
    D5D52613 C3D12E98 BC49967F 7652EED2  
    9D2D2E61 67610860 6D338B72 5CF95C69  
    E36B85CC 84991F19 7575D828 470A92AB  
    —— END LICENSE ——  
<!--more-->
# 开启左侧的目录树
刚安装的时候默认不展示sideBar的 如果要展示sideBar，需要进入view -> side Bar-->Show Side Bar 这样设置就会有左侧文件夹了。

project -> add folders to project

# 微软输入法ctrl+shift+B

# 主题(Material Theme)
You can install this awesome theme through the Package Control.

Press Ctrl + Shift + P to open the command palette.
Type Package Control: Install Package and press enter. Then search for Material Theme.

[9个最佳的SublimeText主题](http://www.techug.com/post/9-best-sublime-text-themes.html)
[2017 年最佳 Sublime Text 3 主题](https://juejin.im/entry/599a1bed6fb9a0248070d4b1)

# [更多操作](http://www.css88.com/archives/5858?utm_source=tuicool&utm_medium=referral)

# 使用sublime的snippets(片段)功能
在 Sublime 中，可以通过 Sublime-snippet 来快速补全代码。
我的存储路径：C:\Users\Administrator\AppData\Roaming\Sublime Text 3\Packages\User\Snippets

## 创建
1. 打开sublime,选择tools->Developer然后选择new snippet
2. <content><![CDATA[ 这里放模板内容 ]]></content>
   <tabTrigger>这里放需要在编辑器输入的内容</tabTrigger>
3. 然后保存在Packages/User下,最好是新建一个snippnets的目录,专门来放这些片段代码,因为User下面可能还会放别的东西,那样就比较杂乱啦.保存的文件后缀必须是"sublime-snippet".

## 说明
- <content><![CDATA[ ]]></content> 定义了补全的内容
    - ${1:elem name} 中： 1是输入点的序号，1表示的是第一个输入点，elem name表示的是输入点的默认值。
    - ${2:content} 中：2表示第二个输入点。
- <tabTrigger> ： 定义了触发补全的字符串
- <description> ：对snippet描述
打开任意一个文件，通过输入触发补全的字符串，然后按Tab键，就可以补全内容。再按Tab进入下一个输入点。

上面的是snippet在任意类型的文件中都能触发。如果要限定文件类型，可以用
<scope>source.文件类型</scope>。

    <snippet>
        <content><![CDATA[ 你需要插入的代码片段${1:name} ]]></content>
        <!-- 可选：快捷键，利用Tab自动补全代码的功能 -->
        <tabTrigger>xyzzy</tabTrigger>
        <!-- 可选：使用范围，不填写代表对所有文件有效。附：source.css和test.html分别对应不同文件。 -->
        <scope>source.python</scope>
        <!-- 可选：在snippet菜单中的显示说明（支持中文）。如果不定义，菜单则显示当前文件的文件名。 -->
        <description>My Fancy Snippet</description>
    </snippet>
    ${1:name}表示代码插入后，光标所停留的位置，可同时插入多个。其中:name为自定义参数（可选）。
    ${2}表示代码插入后，按Tab键，光标会根据顺序跳转到相应位置（以此类推）。

windows也可以为软件设置快捷键。

# Sublime Text 3常用用户自定义配置推荐

    {
    "auto_complete_selector": "source,text", //用到snippet的话加此行,否则请无视我
    "font_size": 16, //不用多说,字体大小,同样可以按住CTRL+'+'或者'-'或者'鼠标滚轮'调整
    "font_face": "Comic Sans MS",
    "ignored_packages":
    [
    "Vintage"
    ], //忽视此包...
    "word_separators": "./\\()\"':,.;<>~!@#$%^&*|+=[]{}`~?", //这些字符会在鼠标双击时隔断,可自行删除不必要的,例如这个被我修改过删除了'-'符号,详情可参考我之前写的<<sublime text快速选择带有横线(连接符)的类名或ID名等>>,上一篇就是了
    "word_wrap": true, //一行内容太长了,自动换行(如果你够'自信'的话,又喜欢拖动X轴滚动条请无视我)
    "highlight_line": true, //高亮显示当前编辑的行,有时自动折行看不清,这个就把一整块显示出来,清晰一些
    "show_encoding": true, //编辑器底部显示编码信息,用GBK编码的偶尔出现乱码,看看这个能查一下,虽然作用不大,放在下面也不占地方,无所谓了
    "save_on_focus_lost": true, //当焦点从当前编辑文档中丢失,会自动保存,看个人喜好咯
    "highlight_modified_tabs": true, //高亮TAB显示被修改过的文档,如果上一条为关闭,修改过的文件看起来更清晰
    "draw_minimap_border": true, //在编辑器右侧小代码地图上为当前区加个边框,视力不好可以加上,比如我
    "always_show_minimap_viewport": true, //总是显示这个迷你地图窗口,还是视力不好
    "show_tab_close_buttons": false //不显示TAB标签上的关闭图标(个人认为没用,文件多了不小心切换的时候关了更麻烦,真的需要关闭某个标签的时候,可以在左侧栏已打开的文件中点叉叉,当然个人更加推荐使用快捷键CTRL+W)
    //注释 BY WHIDY 2014年5月15日...
    }

# 设置了word_wrap还是不能自动换行
解决: View -> Word Wrap Column -> Automatic

