# 概述

## 什么是大数据

4V:  volume （量大）；Velocity（速度，比如storm）；variety （多样性，比如hbase中的非结构化数据）；value（高价值，数据是用来做决策的）

## 大数据的应用场景

- 核心：分布式存储（HDFS）和分布式处理（Mapreduce）
- 和云计算的关系：Iaas  (infrastructure) , Paas (platform) , Saas (software),

# Hadoop

## hadoop 集群节点

- namenode，负责协调集群中数据存储，（这些数据存储到哪些地方了，去哪地方找，所以是协调,包含两个核心部分)
  - FsImage: 维护文件系统树和文件树中的所有文件和文件夹的metadata
  - EditLog:记录了所有针对文件的创建删除重命名等操作
- datanode，存储被切分的数据块，（存储具体的数据）
- jobtracker，协调数据计算任务
- tasktracker，负责执行jobtracker指派的任务
- secondarynamenode，帮助namenode收集文件系统运行的状态信息

## hadoop 企业安装

- 企业安装因为服务器比较多，所以一般使用自动化部署工具，现在比较流行的是docker

## hadoop的核心：

- HDFS：
- mapreduce：
  - map：接收一个键值对（key-value）,产生中间一组键值对，根据key的值将value传到reduce函数
  - reduce：根据key的值将value组合成更小的值

在mapreduce中将map的结果分发到reduce中的过程就是shuffle，[spark中的shuffle和mapreduce的shuffle区别](http://blog.csdn.net/johnny_lee/article/details/22619585)

使用python实现wordcount的mapreduce过程[http://www.cnblogs.com/kaituorensheng/p/3826114.html]

# Hbase

## habse与传统数据库的对比

- 数据操作：hbase 只提供了插入，删除，查询的操作

## hbase的特点

- hbase的四维：行键，列族，列限定符，时间戳来确定一个单元格，其中行键（row key）是hbase的索引，hbase只支持一级索引，二级索引借助其他工具，hbase是存储未经解释的字符串，没有数据类型

# Nosql

## NoSQL的四大类型

### 键值存储：redis

- 应用场景：频繁读写,拥有简单模型,内容缓存，一般作为缓冲层

### 文档数据库： Mongodb

- 存储对象类型：json，xml，lxml

### 图数据库：Neo4j

- 典型应用：社交网络，模式识别，依赖分析，推荐系统

### 列族数据库：Hbase

- 优点：查找速度快，可扩展性强，容易进行分布式扩展，复杂度低

## mongodb的使用

- 创建：不用创建表
- 插入：db.coll.insert({'a':1})

# Hive

## 概述

pig，hive，hbase：pig实现数据的ETL，hive常用来批处理，一般喜欢做离线分析，hbase时时数据分析

## hive

hive本质是hadoop的数据仓库，所有的数据存在hdfs上，底层可以用mysql，db2等数据库进行存储，hive的查询操作转化成mapreduce作业。hive后期增加了对非结构化数据的支持，比如json格式的数据，但是实际应用中一般不会用hive存储非结构化数据

数据仓库更关注于OLAP，常用来做数据的决策，所以更关注查询的效率，而数据库更偏向业务，比如银行业务的数据用的数据库，但是你要进行用户的画像分析，就要用到数据仓库了

hive是不建立索引的，查询时是暴力扫描所有的数据

## hive 常见命令

- 更新数据：update 表名 set 列名=更新值 where 更新条件
- 删除

  - 删除数据：delete [from] 表名 [where 删除条件]
  - 删除表数据但是保留表的定义：truncate table 表名;
  - 删除表数据和表：drop table 表名;
- 查询：

  - 普通查询：select * from 表名 where 查询条件 order by 排序名
  - 限制行数：select top 5 * from student where sex='男';
  - 按百分数返回行: select top 20 percent sname,saddress from students
  - 查询某一列内容为空的记录：select sname as name from stu where address is null
- 模糊查询：

  - like:  select * from stu where sname like "张%"
  - between: select * from stu where grade between 60 and 80
  - in: select * from stu where address in ("GZ","SH")
  - 通配符：-  匹配一个字符，%匹配任意长度的字符，[] 括号里指定范围的一个字符，[^] 匹配不在括号里一个字符
- 聚合函数：

  - SUM()； AVG()；MAX()；MIN()；COUNT(*)
- 时间日期：
  - select from_unixtime(1323308,'')????
  - year，month， day
  - month_between(date1,date2): 返回date1和date2 之间相差的月份
  - datediff：使用datediff函数返回两个日期之间的天数
- 分组查询
  - 分组查询语句：select * from 表名 where .. group by ...having
  - SELECT *,Row_Number() OVER (partition by deptid ORDER BY salary desc) rank from employee; 对于每部分进行分区
- 连接查询
  - inner join ... on ...: 两个表中都要满足
  - full join: 把左右两个表中的数据都取出来，不管是否匹配
- 查询数据高级函数
  - cast： 数据类型的转换. select cast('12' as int ) from stu; 
  - with ties:  select top 10 with ties price from stu;  这样可能不止取第10行，因为若是11行，12行都与10的值相同的话也会取得到
  - with cube：这个参数会自动对group by 所列的分组列做加和计算？？
  - with roolup：只会根据group by子列所列的第一列做加总计算？？
  - union 合并多个查询结果。将多个查询结果做上下垂直合并，所以列数不会增加
- 字符串函数
  - length：字符串长度函数
  - reverse：字符串反转函数
  - concat：字符串连接函数
  - concat_ws: 带分隔符的字符串连接函数
  - substr：截取字符串
- 条件函数
  - case a when b then c when d then e else f end;  当a=b 时，返回c，否则返回f
- 子查询
- 数学函数
  - round函数：返回四舍五入的值
  - floor：向下取整。ceil： 向上取整

# Spark

## 简介

- hadoop的缺点：磁盘开销大; 其他的任务运行完之后才能运行其他的任务
- spark的优点：内存计算； 基于DAG调度而成
- spark四大组件：spark streaming，spark SQL，spark Mllib，spark graphx。

## spark 运行架构

### 基本概念

- RDD: resillient distributed dataset(弹性分布式数据集)。是分布式内存的一个抽象概念，提供了一种高度受限的共享内存模型，RDD简单讲就是一种数据结构，这种数据结构类似于数组，与普通数组的区别是RDD中的数据是分区进行存储的，RDD支持两种操作transformation：（常见的transformation有哪些）从现有的数据集中创建一个新的数据集和action（常见的action操作有哪些），在数据集上计算后产生一个值返回到驱动程序
- DAG：有向无环图，反映了RDD之间的依赖关系
- Executor：是运行在工作节点（workernode）的一个进程，负责运行task
- Application：用户编写的Spark应用程序
- Task：运行在Executor上的工作单元
- Job：一个Job 包含多个RDD及作用于相应RDD上的各种操作。
- Stage：是Job的基本调度单位，一个Job分组为多组的Task，每组Task被称为stage，没有Shuffle关系
- 一个Application 由一个Driver和若干个Job组成，一个Job由多个Stage组成，一个Stage由多个没有Shuffle关系的Task组成

### 架构设计

- Spark的运行架构包括集群资源管理器（Cluster Manager）、运行作业任务的工作节点（Worker Node）、每个应用的任务控制节点（Driver）和每个工作节点上负责具体任务的执行进程
- 资源管理器可以自带或Mesos或者Yarn

与hadoop mapreduce计算框架相比，spark所采用的Executor有两个优点：

- 一是利用多线程来执行具体的任务，减少任务的启动开销
- 而是Executor中有一个BlockManager存储模块，会将内存和磁盘共同作为存储设备，有效减少IO开销

### spark运行基本流程

spark运行中参与对象有Cluster manager，sparkcontext，executor

1. sparkcontext 首先向Clustermanager注册并申请资源
2. Clustermanager 向executor分配资源
3. executor向sparkcontext获取task
   1. 先初始化sparkcontext创建DAG Scheduler，task Scheduler
   2. 根据action生成job，并在job内部构建DAG
   3. DAG 根据DAG构建成stage
   4. stage转化为task
4. task在executor执行，执行进行注销



### RDD运行原理

- 窄依赖：是一个父节点对应一个子节点或者多个父节点对应一个子节点
- 宽依赖：是一个父节点对应多个子节点或者多个父节点对应一个子节点
