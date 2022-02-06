---
title: Python装饰器
date: 2022-2-06 22:34:04
tags: Python
---
### 一段代码样例：

首先写一个判断数字是否是质数的函数，之后再写一个函数将2到10000的所有质数打印出来

![](/images/Python/装饰器1.jpg)

接下来我们想看下过程用了多少时间

![](/images/Python/装饰器2.jpg)

这样发现prime_num函数不好，因为不光有判断质数的代码，还有计算时间的代码，如果此时还有很多函数想要计算完成时间，那每个函数都要写进去计算时间的代码，我们想把这部分算时间的代码单独抽出来，于是就有了装饰器。

![](/images/Python/装饰器3.jpg)

那如果我们运行的函数有输入参数呢，相应的装饰器那里也要添加上对应的参数

![](/images/Python/装饰器4.jpg)

### 学习资料
- Youtube大佬讲解
https://www.youtube.com/watch?v=QqRvteWBSWg