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
#### 2.1 decode
流程控制,效果类似于`if else`
1. 可用于`order by`的指定排序,如`order by decode(m.status,10,20,30,90,0,99)`

#### 2.2 sum
一般用法:`sum(t.xxx)`

#### 2.3 to_char(),to_number(),to_date()
1. number转date:`to_date(20180203,'yyyy-mm-dd')`,后面这个`yyyy-mm-dd`格式不管怎么写,最终转换出来都是类似这样的`2018/2/3`
2. date转char:`to_char(sysdate,'yyyy-mm-dd')`,会被转换成`2018-03-06`

#### 2.4 like,instr和substr
`like`用于模糊查询,`instr`用于判断是否包含某字符串,`substr`用于截取字符串;因为like的效率比较低,所以能用后面的情况下尽量用后面的

#### 2.5 distinct去重
如果后面跟多个字段就是对多个字段去重,所以想对多个字段中的单个字段去重的话还是用`group by`

### 3 注释
1. 单行注释:`--`
2. 多行注释:`/**/`

## 六 问题
1. 易百教程:[http://www.yiibai.com/plsql/](http://www.yiibai.com/plsql/)
2. Oracle调优经验
3. 变量的声明