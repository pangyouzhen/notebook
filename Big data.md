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

# 云数据库

# Mapreduce

# Hive

# Spark

# 流计算

# 图计算





