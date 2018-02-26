# redis
[TOC]
## 一 概述
### 1 简介
#### 主要应用场景
1. 提供缓存服务，存储访问频率高的热数据防止穿透到数据库
2. 在分布式系统中可以作为实现分布式锁的一种实现方案

### 3 常识
#### NoSQL（not only sql）简介
要想弄懂redis,先来了解下NoSQL
1. c语言开发
2. 主要的应用场景：
    - 缓存
    - 消息队列
    - 网站统计、应用排行榜
    - 数据过期处理

##### 为什么需要NoSQL？
1. 用以解决传统关系型数据库难以解决的几个问题
    1. high performance：高并发读写
    2. huge storage：海量数据的高效存储和访问
    3. high scalability && high availability:高扩展性和高可用性
2. 优点：
    1. 易扩展
    2. 灵活的数据结构
    3. 大数据量，高性能
    4. 高可用
##### NoSQL的主要产品
- couchdb
- redis
- neo4j
- mongodb
- membase
- riak

##### NoSQL的四大分类
1. key-value(优势：快速查询，劣势 ：缺少结构化)
2. 列存储（功能局限）
3. 文档数据库（典型的如mongodb）
4. 图形数据库

### 4 文档
### 5 网址
1. 首选官网,上面还有在线联系:[redis官网](https://redis.io/)

## 二 安装配置
### 1 win
### 2 linux
#### 2.1 ubuntu
1. 安装
    安装之后redis.conf文件在`/etc/redis`
2. 启动服务端:`redis-server [可选的redis.conf绝对路径]`
3. 启动客户端:`redis-cli`


### 3 mac
## 三 基础
## 六 问题
reids-server

redis-cli

redis-benchmark

redis-conf
