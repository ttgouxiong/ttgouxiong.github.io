---
title: Pyinstaller打包神器
date: 2021-11-13 11:41:59
tags: Python
---

事情经过是这样的，我最近尝试写了个批量处理Excel和XML文件的python小工具想要发给别人用一下，但是别人的电脑上面没有安装相应的库，或者说有人电脑根本没有安装Python，那该怎么办呢，可不可以将所有我用到的代码全部封装到一个大文件里面一起打包发给别人，就像平时下载一个软件一样，这就用到python打包神器——Pyinstaller。下面会介绍传统的打包方式和进阶版打包方式。

- pyinstaller库安装：
PyInstaller是一个十分有用的第三方库，它能够在Windows、Linux、 Mac OS X 等操作系统下将Python源文件打包，通过对源文件打包，Python程序可以在没有安装Python的环境中运行，也可以作为一个独立文件方便传递和管理。

先下载pyinstaller，我比较懒，就直接用pip install pyinstaller，等待自动安装


- 传统打包方式

在代码的路径下进行cmd，就直接跳转到该路径的cmd界面，切记路径中不要有中文







好文分享：
https://blog.csdn.net/BearStarX/article/details/81054134

如何将Python.py文件打包为.exe可执行程序——pyinstaller 库的使用 - yang元祐的文章 - 知乎
https://zhuanlan.zhihu.com/p/25513571

为何用pyinstaller打包的项目这么大？ - 呆呆的回答 - 知乎（虚拟环境搭建介绍，应该非常好用）
https://www.zhihu.com/question/314112690/answer/611317071

Python 打包工具对比，Nuitka vs Pyinstaller - 千锋Python学院的文章 - 知乎
https://zhuanlan.zhihu.com/p/136023273