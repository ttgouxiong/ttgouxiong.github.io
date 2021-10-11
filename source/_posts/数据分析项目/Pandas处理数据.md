---
title: Pandas处理数据
date: 2021-01-17 08:27:37
tags: 数据分析项目
---

### 一. 数据探索
#### 1. Pandas库
- 什么是pandas库：一个专门用于数据分析的库
- pandas库的作用：提供高效处理大量复杂数据所需的工具
- 导入pandas库：import pandas as pd

#### 2. pandas库的主要数据结构
**Series对象**
- 什么是Series对象：一组数据＋索引
如何创建Series对象：pd.Series(data) —— 参数data —— ['老大','老二','老三','小四'] —— 需要传入的数据

**DataFrame对象**
- 什么是DataFrame对象：一组数据+行索引+列索引
如何创建DataFrame对象：pd.DataFrame(data) —— 参数data —— data={'年龄':[1,2,3,4],'排名':[1,2,3,4]} —— 需要传入的数据

**Series对象与DataFrame对象的区别于联系**
- 区别：索引不同
- 联系：DataFrame对象可以看成Series对象构成

#### 3. 读取数据
pd.read_csv(path,encoding)
- 参数path = './工作/clean_data.csv' —— 文件路径
- 参数encoding = 'utf-8' —— 编码格式

#### 4. 查看数据
- 查看头部数据：df.head(n) 查看头部n行数据
- 查看尾部数据: df.tail(n) 查看尾部n行数据
- 查看数据基本信息: df.info()
- 查看某一列数据: df['column'] column:想要查看的列名
- 查看某一列数据的频数分布：s.value_counts()


### 二. 数据分析
#### 1. 数据的类型
- 数值型数据 —— 表示大小或多少的数据，像年龄，年购买量
- 分类型数据 —— 可以用标记或名称来识别项目的类型的数据，像用户ID，性别，行业，岗位，购买原因

#### 2. 数值型数据分析方法
最小值：s.min()
最大值：s.max()
平均值：s.mean()
中位数：s.median()

#### 3. 分类型数据分析方法
频数分布：s.value_counts()/s.value_counts().sum()


### 三. 数据清洗
#### 1. 缺失值
- 缺失值概念：表格中缺失的数据
- 缺失值处理：查找缺失值 —— df.isna()  删除缺失值 —— df.dropna()

#### 2. 重复值
- 重复值概念：表格中出现的重复数据
- 重复值处理：查找重复行 —— df.duplicated()  查看重复数据 —— df[df.duplicated()]  删除重复值 —— df.drop_duplicates()

#### 3. 异常值
- 异常值概念：表格中存在异常小或异常大的数据
- 异常值处理：查看数据描述性统计信息 —— df.describe() 布尔索引：数据范围抽取 —— df = df[<范围>] 查看重复数据 —— df[df.duplicate()]

#### 4. 数据写入
df.to_csv(path,encoding,index):path——文件路径,encoding——编码方式，index = False——取消行索引


### 四. 数据分析（进阶）
#### 1. 处理时间数据
- 转化日期数据：pd.to_datetime(arg,format): 参数arg——要转化的数据，参数format——要转化成的日期格式
- 提取月份信息：s.dt.month
- 添加新列：df['colname'] = s —— 参数colname —— 要添加的新列的名字

#### 2. 分组聚合操作
df.groupby(key)['colname'].sum()
分组操作定义：根据某项规则将数据分入不同的组
分组操作代码：df.groupby(key) —— 参数key —— 要进行分组的列的列名
聚合操作定义：针对数据的某些列，去求得某些值（平均值，总和）的过程
聚合操作代码：['colname'].sum() —— 参数colname —— 要进行聚合操作的列名

#### 3. 折线图
- 折线图使用场景：一般针对数值型数据，一般用来分析数据的变化趋势
- 折线图绘制：s.plot(kind,figsize,label)

