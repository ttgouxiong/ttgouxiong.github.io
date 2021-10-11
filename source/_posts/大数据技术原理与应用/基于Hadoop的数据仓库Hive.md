---
title: （八）基于Hadoop的数据仓库Hive
date: 2020-12-28 17:48:04
tags: 大数据技术原理与应用
---

### 一. 概述

#### 1. 数据仓库概念
数据仓库（Data Warehouse）是一个面向主题的（Subject Oriented）、集成的（Integrated）、相对稳定的（Non-Volatile）、反映历史变化（Time Variant）的数据集合，用于支持企业内部管理决策，商业分析。内部存有大量历史数据，便于企业构建经营管理系统。
![](/images/大数据概述/数据仓库.jpg)

#### 2. 传统数据仓库面临的挑战
- 无法满足快速增长的海量数据存储需求
- 无法有效处理不同类型的数据，无法存储非结构化的数据，比如日志
- 计算和处理能力不足，纵向扩展能力有限，水平扩展能力几乎没有

#### 3. Hive简介
Hive是构建在Hadoop之上的数据仓库工具，它支持大规模数据存储，分析，具有良好的可扩展性。Hive本身不存储和处理数据，某种程度上可以看作是用户编程接口。它依赖分布式文件系统HDFS存储数据，依赖分布式计算模型MapReduce处理数据。定义了简单的类似SQL的查询语言——HiveQL,用户可以通过编写的HiveQL语句运行MapReduce任务。可以很容易把原来构建在关系数据库上的数据仓库应用程序移植到Hadoop平台上。综上，Hive是一个可以提供有效、合理、直观组织和使用数据的分析工具

Hive具有的特点非常适用于数据仓库
- 采用批处理方式处理海量数据
Hive需要把HiveQL语句转换成MapReduce任务进行运行
数据仓库存储的是静态数据，对静态数据的分析适合采用批处理方式，不需要快速响应给出结果，而且数据本身也不会频繁变化
- 提供适合数据仓库操作的工具
Hive本身提供了一系列对数据进行提取、转换、加载（ETL）的工具，可以存储、查询和分析存储在Hadoop中的大规模数据
这些工具能够很好地满足数据仓库各种应用场景

#### 4.Hive与Hadoop生态系统中其他组件的关系
![](/images/大数据概述/生态.jpg)
- Hive依赖与HDFS存储数据
- Hive依赖MapReduce处理数据
- Pig是面向流向处理→主要用于数据仓库ETL过程，之后由Hive批处理数据。某些场景下Pig可以作为Hive的替代工具。
- HBase提供数据的实时访问，与HDFS互补来弥补HDFS实时性差的问题

#### 5. Hive与传统数据库的对比分析
Hive在很多方面和传统的关系数据库类似，但是它的底层依赖的是HDFS和MapReduce，所以在很多方面又有别于传统数据库

|对比项目|Hive|传统数据库|
|:-----:|:-----:|:-----:|
|数据插入|支持批量导入|支持单条和批量导入|
|数据更新|不支持|支持|
|索引|支持|支持|
|分区|支持|支持|
|执行延迟|高|低|
|扩展性|好|有限|

#### 6. Hive在企业中的部署和应用
- Hive在企业大数据分析平台中的应用
![](/images/大数据概述/企业.jpg)

- Hive在Facebook公司中的应用
基于Oracle的数据仓库系统已经无法满足激增的业务需求
Facebook公司开发了数据仓库工具Hive，并在企业内部进行了大量部署

### 二. Hive系统架构
- 用户接口模块包括CLI、HWI、JDBC、ODBC、Thrift Server
- 驱动模块（Driver）包括编译器、优化器、执行器等，负责把HiveSQL语句转换成一系列MapReduce作业
- 元数据存储模块（Metastore）是一个独立的关系型数据库（自带derby数据库，或MySQL数据库）

### 三. Hive工作原理（核心！）
Hive本身不做具体的数据处理和存储，Hive吧SQL语句转换成相关的MapReduce作业

#### 1. SQL语句转换成MapReduce作业的基本原理
- 连接（join）实现原理：
编写一个Map处理逻辑 → Map处理逻辑输入关系数据库的表 → 通过Map对他进行转换
![](/images/大数据概述/join.jpg)

- group by的实现原理：
存在一个分组（Group By）操作，其功能是把表Score的不同片段按照rank和level的组合值进行合并，计算不同rank和level的组合值分别有几条记录：
select rank, level ,count(*) as value from score group by rank, level
![](/images/大数据概述/group_by.jpg)

#### 2. Hive中SQL查询转换成MapReduce作业的过程
当用户向Hive输入一段命令或查询时，Hive需要与Hadoop交互工作来完成该操作：
- 驱动模块接收该命令或查询编译器
- 对该命令或查询进行解析编译
- 由优化器对该命令或查询进行优化计算
- 该命令或查询通过执行器进行执行

![](/images/大数据概述/SQL.jpg)

几点说明：
- 当启动MapReduce程序时，Hive本身是不会生成MapReduce算法程序的
- 需要通过一个表示“Job执行计划”的XML文件驱动执行内置的、原生的Mapper和Reducer模块
- Hive通过和JobTracker通信来初始化MapReduce任务，不必直接部署在JobTracker所在的管理节点上执行
- 通常在大型集群上，会有专门的网关机来部署Hive工具。网关机的作用主要是远程操作和管理节点上的JobTracker通信来执行任务
- 数据文件通常存储在HDFS上，HDFS由名称节点管理

### 四. Hive HA基本原理
问题：在实际应用中，Hive也暴露出不稳定的问题
解决方案：Hive HA（High Availability）
- 由多个Hive实例进行管理的，这些Hive实例被纳入到一个资源池中，并由HAProxy提供一个统一的对外接口
- 对于程序开发人员来说，可以把它认为是一台超强“Hive"

### 五. Impala
#### 1. Impala简介
Hive是建立在Hadoop之上的，有时间响应长的缺点（分钟级响应）
- Impala是由Cloudera公司开发的新型查询系统，它提供SQL语义，能查询存储在Hadoop的HDFS和HBase上的PB级大数据，在性能上比Hive高出3~30倍
- Impala的运行需要依赖于Hive的元数据
- Impala是参照 Dremel系统进行设计的
- Impala采用了与商用并行关系数据库类似的分布式查询引擎，可以直接与HDFS和HBase进行交互查询，不需要像Hive一样将语句转换成MapReduce，增强了实时性
- Impala和Hive采用相同的SQL语法、ODBC驱动程序和用户接口

|ODBC Driver||
|:-----:|:-----:|
|Impala|Metastore(Hive)|
|HDFS|HBase|

#### 2. Impala系统架构
Impala和Hive、HDFS、HBase等工具是统一部署在一个Hadoop平台上的，Impala主要由Impalad，State Store和CLI三部分组成
- Impalad：驻留在不同节点的进程
负责协调客户端提交的查询的执行
包含Query Planner、Query Coordinator和Query Exec Engine三个模块
与HDFS的数据节点（HDFS DN）运行在同一节点上
给其他Impalad分配任务以及收集其他Impalad的执行结果进行汇总
Impalad也会执行其他Impalad给其分配的任务，主要就是对本地HDFS和HBase里的部分数据进行操作

- State Store
会创建一个statestored进程
负责收集分布在集群中各个Impalad进程的资源信息，用于查询调度

- CLI
给用户提供查询使用的命令行工具
还提供了Hue、JDBC及ODBC的使用接口

说明：Impala中的元数据直接存储在Hive中。Impala采用与Hive相同的元数据、SQL语法、ODBC驱动程序和用户接口，从而使得在一个Hadoop平台上，可以统一部署Hive和Impala等分析工具，同时支持批处理和实时查询

#### 3. Impala查询执行过程
- 注册订阅
- 提交查询
- 获取元数据与数据地址
- 分发查询任务
- 汇聚结果
- 返回结果

#### 4. Impala与Hive的比较
![](/images/大数据概述/hive比较.jpg)

Hive与Impala的相同点总结如下：
- Hive与Impala使用相同的存储数据池，都支持把数据存储于HDFS和HBase中
- Hive与Impala使用相同的元数据
- Hive与Impala中对SQL的解释处理比较相似，都是通过词法分析生成执行计划

总结：
- Impala的目的不在于替换现有的MapReduce工具
- 把Hive与Impala配合使用效果最佳
- 可以先使用Hive进行数据转换处理，之后再使用Impala在Hive处理后的结果数据集上进行快速的数据分析

### 六. Hive编程实践（之后详细学 补上）

#### 1. Hive的安装与配置
#### 2. Hive的数据类型
#### 3. Hive基本操作
#### 4. Hive应用实例：WordCount
#### 5. Hive编程的优势