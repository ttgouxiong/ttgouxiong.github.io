---
title: Pyqt5学习
date: 2021-12-04 20:35:36
tags: Python
---

跟着B站大佬学习PyQt5
https://www.bilibili.com/video/BV154411n79k?p=2&spm_id_from=pageDriver


环境配置
https://blog.csdn.net/Thanlon/article/details/103916371?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163861796816780357230997%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=163861796816780357230997&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-103916371.pc_search_es_clickV2&utm_term=pyqt5&spm=1018.2226.3001.4187


https://blog.csdn.net/qq_32892383/article/details/108867482?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163861796816780357230997%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=163861796816780357230997&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-3-108867482.pc_search_es_clickV2&utm_term=pyqt5&spm=1018.2226.3001.4187



### 第一课时 PyQt5基础知识
- 什么是QT：C++，图形交互
- 学习内容

### 第二课时 搭建PyQt5开发环境
1. Python
通过Anaconda安装
2. PyQt5
3. PyCharm

### 第三课时 开发第一个基于PyQt5的桌面应用
必须使用两个类：QApplication（应用程序）和Qwidge(窗口)，都在PyQt5.QtWidgets

### 第四课时 安装配置QtDesigner

### 第五课时 QtDesigner快速入门

### 第六课时 将.ui文件转换成.py文件
（上面几个课时的内容都在最前面的链接里面有）

方法一：python代码
python -m PyQt5 .uix.pyuic demo.ui -o demo.py(文件名)

方法二：
pyuic5 demo.ui -o demo.py

### 第七课时 在QtDesigner中使用水平布局
四种布局，本节介绍垂直布局，代码文件为MainWinHorizontalLayout.py
这里详细介绍了，生成的UI文件转换成的py文件里面的函数，是如何被Run函数运行的！

### 第八课时 在QtDesigner中使用垂直布局

### 第九课时 在QtDesigner中同时使用垂直和水平布局

### 第十课时 在QtDesigner中使用栅格布局
