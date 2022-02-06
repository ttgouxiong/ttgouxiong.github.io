---
title: python正则表达式
date: 2022-02-05 20:18:52
tags: Python
---


### 二、什么是常量
常量在re的函数中都可以使用，是flags参数：例：re.match(patern, text, flags=0)
常量可以叠加使用

常量列表：
IGNORECASE  忽略大小写的匹配
ASCII 只匹配ASCII格式字符（a,b,c）
DOTALL .可以匹配换行字符，正常是匹配不了的
MULTILINE 可以匹配多行
VERBOSE 正则表达式可以加注释
LOCALE （不推荐使用）
UNICODE
DEBUG
TEMPLATE

### 三、re模块函数
#### 查找一个匹配项
返回对象要加.group()才能变成字符串
- search 查找任意位置的匹配项
- match 必须从字符串开头匹配
- fullmatch 整个字符串与正则完全匹配

#### 查找多个匹配项
- findall 字符串任意位置查找，返回一个列表
- finditer 字符串任意位置查找，返回一个迭代器

#### 分割
- re.split(pattern, string, maxsplit=0, flags=0)

#### 替换
- re.sub(pattern, repl, string, count=0, flags=0) 
re.subn(pattern, repl, string, count=0, flags=0) 函数与 re.sub函数 功能一致，只不过返回一个元组 (字符串, 替换次数)。

### 学习疑问记录
- groups与group的区别：
https://blog.csdn.net/chr1991/article/details/80945455?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-1.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-1.pc_relevant_default&utm_relevant_index=1

- python元字符
|名称   | 英文名称    | 符号|
|:-----:|:----------:|:---|
|反斜杠  |Backslash    |\|
|插入符号| Caret       |^|
|美元符号|Dollar sign  |$|
|点      |Dot          |.|
|竖线    |Pipe symbol  |||
|问号    |Question mark|?|
|星号    |Asterisk     |*|
|加号    |Plus sign    |+|
|圆括号  |Parenthesis  |( )|
|方括号  |Square bracket|[ ]|
|花括号  |Curly brace   |{ }|




### 学习资料
- 知乎大佬的讲解（比较全面，函数，常量以及报错注意事项等）
https://www.zhihu.com/search?type=content&q=python%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F
- 入门的视频
https://www.bilibili.com/video/BV1xs411x71b?from=search&seid=1635822755251701827&spm_id_from=333.337.0.0
- python元字符
https://www.zhihu.com/search?type=content&q=python%20%E5%85%83%E5%AD%97%E7%AC%A6