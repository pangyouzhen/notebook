# 概述

- 核心：分布式存储（HDFS）和分布式处理（Mapreduce）
- 和云计算的关系：Iaas  (infrastructure) , Paas (platform) , Saas (software), 云计算的关键技术, 虚拟化，分布式存储，分布式计算， 多租户

# Hadoop

- hadoop 的节点主要有
  - namenode，负责协调集群中数据存储，（这些数据存储到哪些地方了，去哪地方找，所以是协调）
  - datanode，存储被切分的数据块，（存储具体的数据）
  - jobtracker，协调数据计算任务
  - tasktracker，负责执行jobtracker指派的任务
  - secondarynamenode，帮助namenode收集文件系统运行的状态信息
- hadoop 企业安装
  - 企业安装因为服务器比较多，所以一般使用自动化部署工具，现在比较流行的是docker

# HDFS

## hdfs

- 块。每一个块为64M
- namenode 存储元数据，将原数据保存在内存中，保存文件，block，datanode之间的映射关系
- datanode 存储文件内容，文件内容保存在磁盘，维护了block id 到datanode本地文件的映射关系

### 名称节点和数据节点

在HDFS中，名称节点（Namenode）负责管理命名空间（namespace）保存了两个核心的数据结构
- FsImage: 维护文件系统树和文件树中的所有文件和文件夹的metadata
- EditLog:记录了所有针对文件的创建删除重命名等操作

hadoop启动时将fsimage和editlog进行合并，因为fsimage比较小，所以把fsimage独立出来
secondaryNamenode ，并解决editlog不断增大的问题

## HDFS存储原理

- 增强容错性和可用性，解决方案：多副本保存，数据冗余来解决，一般默认为3个副本
- 数据存储：
  - 1副本：上传文件的数据节点
  - 2副本：与1副本不同机架的节点上
  - 3副本：与1副本相同机架的不同节点

## HDFS常用命令

- 常用命令是hadoop  fs
# Hbase

## 概述

### habse与传统数据库的对比

- 数据类型。关系型数据库 关系模型，hbase   未经解释的字符串，没有数据类型
- 数据操作：hbase 只提供了插入，删除，查询的操作
- 列存储和行存储。
- 索引，关系型数据库多个索引，habse  只有一个索引 行键
- 数据维护
- 可伸缩性

## 访问接口

## 数据模型

### 数据模型概述

- hbase需要根据行键，列族，列限定符，时间戳来确定一个单元格

概念视图和物理视图

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

### 不同类型数据库的比较

## CAP

- C 一致性
- A可用性
- P分析容忍性
- MYSQL等关系型数据CA，NOSQL一般强调CP

## mongodb的使用

- 创建：不用创建表
- 插入：db.coll.insert({'a':1})

# 云数据库

# Mapreduce

# Hive

## 概述

数据仓库：用于支持管理和决策
数据集市：
pig，hive，hbase：pig实现数据的ETL，hive常用来批处理，hbase时时数据分析

## hive

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

  - SUM()函数
  - AVG()函数
  - MAX()函数
  - MIN()函数
  - COUNT(*)函数
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

- spark是将结果放在内存中,hadoop使用磁盘
- spark基于DAG进行迭代计算，RDD形成的任务成DAG
- spark四大组件：spark streaming，spark SQL，spark Mllib，spark graphx。

## spark 运行流程

### 基本概念

- RDD: resillient distributed dataset(弹性分布式数据集)。是分布式内存的一个抽象概念，提供了一种高度受限的共享内存模型
- Executor：是运行在工作节点（workernode）的一个进程，负责运行task
- task：运行在Executor上的工作单元
- Job：一个Job 包含多个RDD及作用于相应RDD上的各种操作。
- Stage：是Job的基本调度单位，一个Job分组为多组的Task，每组Task被称为stage，没有Shuffle关系
- 一个Application 由一个Driver和若干个Job组成，一个Job由多个Stage组成，一个Stage由多个没有Shuffle关系的Task组成

### RDD运行原理



## Spark SQL



# 流计算

# 图计算





