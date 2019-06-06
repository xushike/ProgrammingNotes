# db
# 一 概述
## 1 简介
该目录主要是数据库的笔记

## 3 常识
### 3.1 不同数据库对sql的扩展
1. oracle：PL/SQL
1. DB2：SQL/PL
1. SQLSever:Transac-SQL(T-SQL)

### 3.2 数据集、样本数据库
许多数据库系统都为自家的产品提供了样本数据库，比如MySQL的sakila数据集，PostgreSQL的sakila数据集

### 3.3 E-R模型（ER Model）
ER模型，全称为实体联系模型、实体关系模型或实体联系模式图（ERD）（英语：Entity-relationship model）由美籍华裔计算机科学家陈品山发明，是概念数据模型的高层描述所使用的数据模型或模式图。

# 三 基础
1. 事务的ACID

# 四 高级


# 五 经验
## 1 已整理
### 1.1 朋友说的
1. 宁愿在代码中把两张表的数据组合到一起也不要用`union`
2. 能用程序做就不要只想用sql

# 六 问题
1. 不同数据库单表的极限是多少  
    目前我见得最多的就是oracle的四千万条数据
2. 数据结构中的mergelist表示什么意思？
    1. 合并表(或归并表)
    2. 一般用于将两个顺序表或两个链表合成一个表.
3. sqlDeveloper和pl/sql Developer？
4. 表的M/O(Mandatory or Optional)： “Mandatory”表示此查询字段必填；“Optional”表示此查询字段可选。
5. 一个 split 会产生 2GB 的垃圾?

# 七 未整理
1. MongoDB 
2. 时序数据库,比如influxdb
3. 数据库读写分离,主从数据库,数据库索引
4. 读写分离、负载均衡、数据水平拆分
