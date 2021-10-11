---
title: （十）Spark
date: 2020-12-29 16:26:56
tags: 大数据技术原理与应用
---

### 一. Spark概述
#### 1. Spark简介

Hadoop是基于磁盘，Spark是基于内存，所以延迟低，实时效果好
- Spark最初由美国加州伯克利大学（UCBerkeley）的AMP实验室于2009年开发，是基于内存计算的大数据并行计算框架，可用于构建大型的、低延迟的数据分析应用程序
- 2013年Spark加入Apache孵化器项目后发展迅猛，如今已成为Apache软件基金会最重要的三大分布式计算系统开源项目之一（Hadoop、Spark、Storm）
- Spark在2014年打破了Hadoop保持的基准排序纪录：Spark/206个节点/23分钟/100TB数据，Hadoop/2000个节点/72分钟/100TB数据。Spark用十分之一的计算资源，获得了比Hadoop快3倍的速度

Spark的特点：
- 运行速度快：使用DAG执行引擎以支持循环数据流与内存计算
- 容易使用：支持使用Scala、Java、Python和R语言进行编程，可以通过Spark Shell进行**交互式编程**，可以实时查看，及时修改，提高效率
- 通用性：Spark提供了完整而强大的技术栈，包括SQL查询、流式计算、机器学习和图算法组件
- 运行模式多样：可运行于独立的集群模式中，可运行于Hadoop中，也可运行于Amazon EC2等云环境中，并且可以访问HDFS、Cassandra、HBase、Hive等多种数据源

#### 2. Scala简介
Scala是一门现代的多范式编程语言，运行于Java平台（JVM，Java 虚拟机），并兼容现有的Java程序

Scala的特性：
- Scala具备强大的并发性，支持函数式编程，可以更好地支持分布式系统
- Scala语法简洁，能提供优雅的API

Scala兼容Java，运行速度快，且能融合到Hadoop生态圈中
Scala是Spark的主要编程语言，但Spark还支持Java、Python、R作为编程语言
Scala的优势是提供了REPL（Read-Eval-Print Loop，交互式解释器），提高程序开发效率

#### 3. Spark与Hadoop的对比

Hadoop存在如下一些缺点：
- 表达能力有限，有的操作不能仅用简单的Map和Reduce表达
- 磁盘IO开销大
- 延迟高：任务之间的衔接涉及IO开销（先进磁盘，MapReduce再取走）；在前一个任务执行完成之前，其他任务就无法开始，难以胜任复杂、多阶段的计算任务

Spark在借鉴Hadoop MapReduce优点的同时，很好地解决了MapReduce所面临的问题。相比于Hadoop MapReduce，Spark主要具有如下优点：
- Spark的计算模式也属于MapReduce，但不局限于Map和Reduce操作，还提供了多种数据集操作类型，编程模型比Hadoop MapReduce更灵活
- Spark提供了内存计算，可将中间结果放到内存中，对于迭代运算效率更高

Spark基于DAG的任务调度执行机制，要优于Hadoop MapReduce的迭代执行机制
- 使用Hadoop进行迭代计算非常耗资源
- Spark将数据载入内存后，之后的迭代计算都可以直接使用内存中的中间结果作运算，避免了从磁盘中频繁读取数据

### 二. Spark生态系统（多个部分组成）

在实际应用中，大数据处理主要包括以下三个类型：
- 复杂的批量数据处理：通常时间跨度在数十分钟到数小时之间（MapReduce）
- 基于历史数据的交互式查询：通常时间跨度在数十秒到数分钟之间（Impala）
- 基于实时数据流的数据处理：通常时间跨度在数百毫秒到数秒之间（Storm）

这样做难免会带来一些问题：
- 不同场景之间输入输出数据无法做到无缝共享，通常需要进行数据格式的转换
- 不同的软件需要不同的开发和维护团队，带来了较高的使用成本
- 比较难以对同一个集群中的各个系统进行统一的资源协调和分配

Spark的设计遵循“一个软件栈满足不同应用场景”的理念，逐渐形成了一套完整的生态系统。既能够提供内存计算框架，也可以支持SQL即时查询、实时流式计算、机器学习和图计算等。Spark可以部署在资源管理器YARN之上，提供一站式的大数据解决方案。因此，Spark所提供的生态系统足以应对上述三种场景，即同时支持批处理、交互式查询和流数据处理

Spark生态系统组件的应用场景

|应用场景|时间跨度|其他框架|Spark生态系统中的组件|
|:----|:----|:----|:----|
|复杂的批量数据处理 | 小时级| MapReduce，Hive|Spark|
|基于历史数据的交互式查询|分钟级，秒级|Impala，Dremel,Drill|Spark SQL|
|基于实时数据流的数据处理|毫秒，秒级|Storm，S4|Spark Streaming|
|基于历史数据的数据挖掘|-|Mahout|MLlib|
|图结构数据的处理|-|Pregel，Hama|GraphX|

### 三. Spark运行架构

#### 1. 基本概念

- **RDD**：是Resillient Distributed Dataset（弹性分布式数据集）的简称，是分布式内存的一个抽象概念，提供了一种高度受限的共享内存模型
- DAG：是Directed Acyclic Graph（有向无环图）的简称，反映RDD之间的依赖关系
- Executor：是运行在工作节点（WorkerNode）的一个进程，负责运行Task
- Application：用户编写的Spark应用程序
- Task：运行在Executor上的工作单元
- Job：一个Job包含多个RDD及作用于相应RDD上的各种操作
- Stage：是Job的基本调度单位，一个Job会分为多组Task，每组Task被称为Stage，或者也被称为TaskSet，代表了一组关联的、相互之间没有Shuffle依赖关系的任务组成的任务集

#### 2. 架构设计
![](/images/大数据概述/spark架构.jpg)

与Hadoop MapReduce计算框架相比，Spark所采用的Executor有两个优点：
- 一是利用多线程来执行具体的任务，减少任务的启动开销
- 二是Executor中有一个BlockManager存储模块，会将内存和磁盘共同作为存储设备，有效减少IO开销

一个Application由一个Driver和若干个Job构成，一个Job由多个Stage构成，一个Stage由多个没有Shuffle关系的Task组成

当执行一个Application时，Driver会向集群管理器申请资源，启动Executor，并向Executor发送应用程序代码和文件，然后在Executor上执行Task，运行结束后，执行结果会返回给Driver，或者写到HDFS或者其他数据库中

#### 3. Spark运行基本流程
（1）首先为应用构建起基本的运行环境，即由Driver创建一个SparkContext，进行资源的申请、任务的分配和监控
（2）资源管理器为Executor分配资源，并启动Executor进程
（3）SparkContext根据RDD的依赖关系构建DAG图，DAG图提交给DAGScheduler解析成Stage，然后把一个个TaskSet提交给底层调度器TaskScheduler处理；Executor向SparkContext申请Task，Task Scheduler将Task发放给Executor运行，并提供应用程序代码
（4）Task在Executor上运行，把执行结果反馈给TaskScheduler，然后反馈给DAGScheduler，运行完毕后写入数据并释放所有资源

总体而言，Spark运行架构具有以下特点：
（1）每个Application都有自己专属的Executor进程，并且该进程在Application运行期间一直驻留。Executor进程以多线程的方式运行Task
（2）Spark运行过程与资源管理器无关，只要能够获取Executor进程并保持通信即可
（3）Task采用了数据本地性和推测执行等优化机制

### 四. RDD运行原理（这部分知识很重要是核心 之后补上）

#### 1.设计背景

#### 2. RDD概念

#### 3. RDD特性

#### 4. RDD之间的依赖关系

#### 5. Stage的划分

#### 6. RDD运行过程



### 五. Spark SQL

#### 1. 从Shark说起

#### 2. Spark SQL设计


### 六. Spark的部署和应用方式

#### 1. Spark三种部署方式

#### 2. 从Hadoop+Storm架构转向Spark架构

#### 3. Hadoop和Spark的统一部署