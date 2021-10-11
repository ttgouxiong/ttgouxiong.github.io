---
title: （七）MapReduce
date: 2020-12-28 08:26:43
tags: 大数据技术原理与应用
---

### 一. 概述
#### 1. 分布式并行编程
MapReduce是分布式并行编程框架。
摩尔定律：CPU性能大约每隔18个月翻一番，但是由于CPU制作工业有上限天花板，2005年之后摩尔定律逐渐失效。然而需要处理的数据每年增加达50%，两者产生矛盾，解决办法：
- 单核变双核，四核，八核
- 借助分布式并行编程来提高程序性能

分布式程序运行在大规模计算机集群上，可以并行执行大规模数据处理任务，从而获得海量的计算能力。分布式并行编程模型MapReduce最早由谷歌公司提出，Hadoop MapReduce是它的开源实现并且做了很多优化处理，使用门槛低很多。
问题：在MapReduce出现之前，已经有像MPI这样非常成熟的并行计算框架了，那么为什么Google还需要MapReduce？MapReduce相较于传统的并行计算框架有什么优势？


|| 传统并行计算框架 | MapReduce |
|:----|:----|:----|
|集群架构/容错性|共享式（共享内存，共享储存），容错性差|非共享式，容错性好|
|硬件/价格/扩展性|刀片服务器，高速网，SAN，价格贵，扩展性差不可横向扩展|普通PC机，便宜，扩展性好|
|编程/学习难度|what-how，难|what，简单|
|使用场景|实时，细粒度计算，计算型密集|批处理，非实时，数据型密集|

#### 2. MapReduce模型简介
- MapReduce屏蔽了整个分布式程序运行的相关底层细节，将复杂的、运行与大规模集群上的并行计算过程高度地抽象到了两个函数：**Map**和**Reduce**
- 编程容易，不需要掌握分布式并行编程细节，也可以很容易把自己的程序运行在分布式系统上，完成海量数据的计算
- MapReduce采用“分而治之”策略，一个存储在分布式文件系统中的大规模数据集，会被切分成许多独立的分片（split），这些分片可以被多个Map任务并行处理
- MapReduce设计的一个理念就是“计算向数据靠拢”，而不是“数据向计算靠拢”。比如一个数据块存在在机器A上，会优先寻找A最近的map处理，数据不用迁移，因此减少移动数据所需要的大量网络传输开销
- MapReduce框架采用了Master/Slave架构，包括一个Master和若干个Slave。Master上运行JobTracker，Slave上运行TaskTracker
- Hadoop框架是用Java实现的，但是，MapReduce应用程序则不一定要用Java来写

#### 3. Map和Reduce函数

|函数|输入|输出|说明|
|:----|:----|:----|:----|
|Map|<k1,v1>如：<行号，'a,b,c'>|List(<k2,v2>)如：<'a',1>,<'b',1>,<'c',1>|1.将小数据集进一步解析成一批<key,value>对，输入Map函数中进行处理。2.每一个输入的<k1,v1>会输出一批<k2,v2>。<k2,v2>是计算的中间结果|
|Reduce|<k2,List(v2)(值列表)>如：<'a',<1,1,1>>|<k3,v3>（汇总求和）如：<'a',3>|输入的中间结果<k2,List(v2)>中的List(v2)表示是一批属于同一个k2的value|

### 二. MapReduce的体系结构
MapReduce体系结构主要由四个部分组成，分别是：Client、JobTracker、TaskTracker以及Task
- Client：用户编写的MapReduce程序通过Client提交到JobTracker端，用户可通过Client提供的一些接口查看作业运行状态
- JobTracker：JobTracker负责资源监控和作业调度。JobTracker 监控所有TaskTracker与Job的健康状况，一旦发现失败，就将相应的任务转移到其他节点。JobTracker会跟踪任务的执行进度、资源使用量等信息，并将这些信息告诉任务调度器（TaskScheduler），而调度器会在资源出现空闲时，选择合适的任务去使用这些资源
- TaskTracker：TaskTracker会周期性地通过“心跳”将本节点上资源的使用情况和任务的运行进度汇报给JobTracker，同时接收JobTracker 发送过来的命令并执行相应的操作（如启动新任务、
杀死任务等）。TaskTracker 使用“slot”等量划分本节点上的资源量（CPU、内存等）。一个Task 获取到一个slot后才有机会运行，而Hadoop调度器的作用就是将各个TaskTracker上的空闲slot分
配给Task使用。slot分为Map slot和Reduce slot两种，分别供Map Task和Reduce Task使用
- Task：Task分为Map Task和Reduce Task两种，均由TaskTracker启动

### 三. MapReduce工作流程
#### 1. 工作流程简述
![](/images/大数据概述/工作流程.jpg)
- 不同的Map任务之间不会进行通信
- 不同的Reduce任务之间也不会发生任何信息交换
- 用户不能显式地从一台机器向另一台机器发送消息
- 所有的数据交换都是通过MapReduce框架自身去实现的

#### 2. MapReduce各个执行阶段
![](/images/大数据概述/MapReduce.jpg)
- InputFormat: 对输入格式验证，对大数据集进行切分（是逻辑切分，定义起点终点，长度等，不是真的物理切分）
- Split（分片）:HDFS 以固定大小的block 为基本单位存储数据，而对于MapReduce 而言，其处理单位是split。split 是一个逻辑概念，它只包含一些元数据信息，比如数据起始位置、数据长度、数据所在节点等。它的划分方法完全由用户自己决定。
- Map任务的数量：Hadoop为**每个**split创建一个Map任务，split 的多少决定了Map任务的数目。大多数情况下，理想的分片大小是一个HDFS块。
- Reduce任务的数量最优的Reduce任务个数取决于集群中可用的reduce任务槽(slot)的数目。通常设置比reduce任务槽数目稍微小一些的Reduce任务个数（这样可以预留一些系统资源处理可能发生的错误）

### 四. Shuffle过程详解
Shuffle是MapReduce的核心知识
#### 1. Shuffle过程简介
![](/images/大数据概述/shuffle.jpg)

#### 2. Map端的Shuffle过程
输入数据和执行Map任务 → 写入缓存 → 溢写（分区，排序，合并） → 文件归并
为每个Map任务分配一个缓存，MapReduce默认100MB缓存
设置溢写比例0.8，防止数据丢失；分区默认采用哈希函数；排序是默认的操作；排序后可以合并（Combine）；合并不能改变最终结果
在Map任务全部结束之前进行归并；归并得到一个大的文件，放在本地磁盘；文件归并时，如果溢写文件数量大于预定值（默认是3）则可以再次启动Combiner，少于3不需要JobTracker会一直监测Map任务的执行，并通知Reduce任务来领取数据
- 合并（Combine）和归并（Merge）的区别：
两个键值对<“a”,1>和<“a”,1>，如果合并，会得到<“a”,2>，如果归并，会得到<“a”,<1,1>>

#### 3. Reduce端的Shuffle过程
- Reduce任务通过RPC向JobTracker询问Map任务是否已经完成，若完成，则领取数据
- Reduce领取数据先放入缓存，来自不同Map机器，先归并，再合并，写入磁盘
- 多个溢写文件归并成一个或多个大文件，文件中的键值对是排序的
- 当数据很少时，不需要溢写到磁盘，直接在缓存中归并，然后输出给Reduce

### 五. MapReduce应用程序执行过程
![](/images/大数据概述/应用程序.jpg)

### 六. 实例分析：WordCount
这个实例解释的特别好对理解MapReduce非常重要！！！！！

#### 1. WordCount程序任务
- 输入：一个包含大量单词的文本文件
- 输出：文件中每个单词及其出现次数（频数），并按照单词字母顺序排序，每个单词和其频数占一行，单词和频数之间有间隔。

一个WorldCount的输出输入实例

| 输入 | 输出 |
|:----|:----|
|Hello World, Hello Hadoop, Hello MapReduce|Hadoop 1, Hello 3, MapRedece 1, World 1|

#### 2. WorldCount设计思路
- 检查WorldCount程序任务是否可以采用MapReduce来实现
- 确定MapReduce程序的设计思路
- 确定MapReduce程序的执行过程

#### 3. 一个WorldCount执行过程的实例
假设分成3个切片
提示：因为MapReduce只能接受（Key，value）→ 所以可以输入（行号，值）
![](/images/大数据概述/wordcount.jpg)

用户没有定义Combiner时的Reduce过程示意图：
![](/images/大数据概述/reduce1.jpg)
用户定义Combiner时的Reduce过程示意图：
![](/images/大数据概述/reduce2.jpg)

### 七. MapReduce的具体应用
MapReduce可以很好的应用于各种计算问题
- 关系代数计算（选择，投影，并，交，差，连接）
- 分组与聚合运算
- 矩阵-向量乘法
- 矩阵乘法

例子：用MapReduce实现关系的自然连接
（之后补上例子~）