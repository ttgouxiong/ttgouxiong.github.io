---
title: （二）大数据处理架构Hadoop
date: 2020-12-24 16:04:49
tags: 大数据技术原理与应用
---

### 一. 概述

#### 1. Hadoop简介
- Hadoop是Apache旗下一个开源分布式计算平台，基于Java语言开发，跨平台特性较好
- Hadoop是一个项目一个整体，核心是分布式文件系统HDFS（存储）和MapReduce（处理）
- 开源，免费，操作简单很多后台程序被隐藏，有点像傻瓜软件

#### 2. Hadoop发展历史
最早是Doug Cutting开发的文本搜索库，后来因为排序打破世界纪录火了，迅速成为大数据时代最具影响力的的开源分布式发布平台，并成为事实上的大数据处理标准。

#### 3. Hadoop的特性
Hadoop是一个能够对大量数据进行分布式处理的软件框架。
- 高可靠性
- 高效性
- 高可扩展性
- 高容错性
- 成本低（几个差一点的电脑也能构成集群）
- 运行在Linux系统
- 支持多种编程语言
![](/images/大数据概述/hadoop应用现状.jpg)

#### 4. Hadoop版本演变
第一代 Hadoop1.0
第二代 Hadoop2.0
![](/images/大数据概述/hadoop版本.jpg)

第二代增加了资源调度框架，也增加了名称节点热备份（增加了第二名称节点）

选择版本的时候要考虑：是否开源，是否稳定，是否有实践经验，是否有强大的社区支持。
目前流行的版本：
- Apache Hadoop 个人的话一般选这个，免费，但性能评分不高
- Cloudera(CDH:Cloudera Distribution Hadoop) 企业一般用，评价高
- 星河 企业用，国产，评分高
- Hortonworks
- MapR

### 二. Hadoop项目结构

2代之后的框架图如下
![](/images/大数据概述/hadoop项目结构.jpg)

组件 | 功能
:---- | :---- 
HDFS | 分布式文件系统
MapReduce | 分布式并行编程模型（对磁盘）
YARN | 资源管理和调度器
Tez | 运行在YARN之上的下一代Hadoop查询处理框架 （构建有向无环图）
Hive | Hadoop上的数据仓库：企业用来决策分析，对历史数据多维分析，OLAP分析。转化一系列SQL语句为MapReduce作业
Hbase | Hadoop上的非关系型的分布式数据库
Pig | 一个基于Hadoop的大规模数据分析平台，提供类似SQL的查询语言Pig Latin 轻量级分析 （）流数据处理
Sqoop | 用于在Hadoop与传统数据库之间进行数据传递
Oozie | Hadoop上的工作流管理系统
Zookeeper | 提供分布式协调一致性服务
Storm | 流计算框架
Flume | 一个高可用的，高可靠的，分布式的海量日志采集，聚合和传输的系统
Ambari | Hadoop快速部署工具，支持Apache Hadoop集群的供应，管理和监控
Kafka | 一种高吞吐量的分布式发布订阅消息系统，可以处理消费者规模的网站中方的所有动作流数据
Spark | 类似于Hadoop MapReduce的通用并行框架 针对内存计算，性能比MapReduce高一个数量级

### 三. Hadoop集群的部署与使用

#### 1. 集群节点类型
- NameNode: HDFS的节点，会被首先访问，里面记录着数据位置的信息在哪个DataNode上面，负责协调集群中的数据存储
- DataNode: HDFS的节点，存储被拆分的数据块
- JobTracker: MapReduce的节点，协调数据计算任务，管理作业，拆分分配
- TaskTracker: MapReduce的节点，负责执行有JobTracker指派的任务
- SecondaryNameNode: HDFS的节点，帮助NameNode手机文件系统运行的状态信息，在HDFS1.0当中是冷备份，不能第一时间顶上去需要时间
集群中大部分机器设备作为DataNode与TaskTracker工作的，有的机器可能既是DataNode又是TaskTracker

#### 2. 集群硬件配置
企业选择集群时应该注意：
DataNode/TaskTracker的硬件规格:
- 4个磁盘驱动器（单盘1-2T）
- 2个4核CPU，至少2-2.5GHz
- 16-24GB内存
- 千兆以太网
NameNode中很多元数据是直接存在内存，里面有很多命名空间管理，块管理的服务所以需要更多RAM：
- 8-12个磁盘驱动器（单盘1-2T）
- 2个4核、8核CPU
- 16-72GB内存
- 千兆/万兆以太网
SecondaryNameNode在小型集群可以与NameNode共用一台机器，较大的集群可以采用与NameNode相同的硬件

#### 3. 集群规模要多大
比如一个公司可能每周会增加1T数据，要复制2份备用加一起3T，文件日志记录大概30%约1T，一共4T，相当于每周增加一部机器

#### 4. 集群网络拓扑
- 普通HADOOP集群结构有一个两阶网络构成
- 每个几家（Rack）有30-40个服务器，配置一个1GB交换机，并且上传到一个核心交换机或者路由器（1GB或以上）
- 相同的几家中的节点健的带宽总和，要大于不同机架间的带宽总和

#### 5. 集群建立，安装，测试
- 可以手动安装，也有自动安装非常方便
- Hadoop自带一些基准测试程序，比如可用于内部排序测试MapReduce性能

#### 6. 云计算环境中使用Hadoop
公司通过网络购买服务，在对方的计算机集群中搭建自己的Hadoop项目
