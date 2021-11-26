---
title: python大杂烩
date: 2021-10-13 22:48:55
tags: Python
---


#### 记录遇到的各种python知识点（重要的与较为复杂的单独记录）


#### pyQt5 用户交互图形设计界面

#### Lambda函数

#### Eval函数
对字符串才行？  eval的输入是一个字符串


#### os工具库



#### 全局变量，配合函数能否修改问题
def change(a,b):
    a = 10
    b+=a
a = 4
b = 5
change(a,b)
print(a)
print(b)


#### 可迭代对象

#### ‘复制字符串，列表’类型问题，变与不变？内存，指针问题
s = 'hello'
item = [s]
s = 'world'
print(item)





python保留字是啥, import keyword

私有变量，共有变量

#### 单例模式
单例模式实现方法：
装饰器  对√
元类    对√
基类   错×
模块导入   对√



字符串没有sort函数

sorted('字符串'，reverse=True) 会将字符串变成列表


#### copy函数讲解

#### args和kwargs参数
单星号和双星号问题，生成元组和字典


#### pip install命令(help,show,list,name?)

#### python中创建一个类，并用这个类创建实例后，实例会自带一些属性和方法：
__dir__
__hash__
__init__
__new__



#### 异常处理












