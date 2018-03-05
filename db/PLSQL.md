# pl/sql
## 一 概述
### 1 简介
1. PL/SQL的一般语法是基于ADA和Pascal编程语言
1. pl/sql的优点
    1. 提供了大量的数据类型
    2. 支持面向对象的编程,以及异常处理，封装，数据隐藏
    3. 支持静态和动态SQL
    4. 允许一次发送语句的整块到数据库。这降低了网络流量，并提供高性能的应用程序

## 三 基础
### 1 语法
#### 1.1 增
#### 1.5 分组group by
1. 按日期分组:`group by char(t.xxx,'yyyy-mm-dd')`

    上面是按日分组.如果是按周分组是`group by char(t.xxx,'yyyy-IW')`,按月分组则是`group by char(t.xxx,'yyyy-mm')`,按季度是`group by char(t.xxx,'yyyy-Q`,按年是`group by char(t.xxx,'yyyy')`

2. 按时间段分组:``

### 2 函数
##### 2.1 decode
流程控制,效果类似于`if else`
1. 可用于`order by`的指定排序,如`order by decode(m.status,10,20,30,90,0,99)`

##### 2.2 sum
一般用法:`sum(t.xxx)`

### 3 注释
1. 单行注释:`--`
2. 多行注释:`/**/`

## 六 问题
1. 易百教程:[http://www.yiibai.com/plsql/](http://www.yiibai.com/plsql/)
2. Oracle调优经验
