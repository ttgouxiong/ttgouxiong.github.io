---
title: python列表操作
date: 2021-11-26 22:45:35
tags: Python
---


#### 场景一 列表元素去除+合并
有很多文件，我们创建了两个列表来记录这些文件的信息。一个列表记录了文件的名字，另一个列表存储了这些文件里面的字段，文件的名称可能会重复，我们想将两个列表里面的重复文件名和字段合并。

file_name = ['file1','file2','file3','file2','file1','file5',]
word_list = [[11,1],[22,2],[33,3],[44,4],[55,5],[66,6]]

我们想变成

file_name = ['file1','file2','file3','file5',]
word_list = [[11,1，55,5],[22,2，44,4],[33,3],[66,6]]

下面是代码的实现过程与解释

![](/images/Python/列表合并重复元素.jpg)

#### 场景二 比较两个列表，呈现相同的元素与不同的元素
当我们将需要比对的信息放进不同的列表时，需要判断两个列表是否一致，如果不一致，将不同的元素信息分别打印出来，可以一目了然的看出哪些信息返回的不正确。
- 方法一：细致一些，可以显示出具体异常数据元素哪个列表有哪个列表没有

![](/images/Python/列表找出重复元素与不同元素.jpg)


- 方法二：利用python集合直接显示出不同的元素

![](/images/Python/列表找出重复元素2.jpg)
列表找出重复元素2
