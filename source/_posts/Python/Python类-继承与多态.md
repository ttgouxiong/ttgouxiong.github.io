---
title: Python类 继承与多态
date: 2021-11-03 22:43:48
tags: Python
---

#### Python继承与多态
关于Python的封装，继承、多态、重写 - 陆柒的文章 - 知乎
https://zhuanlan.zhihu.com/p/109841156

- 静态代码优先执行，且只执行一遍：
例：
print('A')
class Person(object):
    print('B')
    def __init__(self,name):
        print('C')
        self.name = name
    print('D')
print(E)

p1 = Person('name1')
p2 = Person('name2')


输出结果：ABDECC


- 例题 
super()是一个特殊函数，他会把父类和子类关联起来（对√）
子类除了拥有继承父类而来的属性和方法外，还可以定义子类自己的属性和方法（对√）
定义子类的实例时，可以通过子类的init(方法)，给父类的所有属性赋值（对√）
对于继承而来的父类方法，如果它不符合子类所期望的行为，那么就必须建立新的类（错×）

- 例题