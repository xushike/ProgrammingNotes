# pl/sql
# 一 概述
## 1 简介
1. PL/SQL的一般语法是基于ADA和Pascal编程语言
1. pl/sql的优点
    1. 提供了大量的数据类型
    2. 支持面向对象的编程,以及异常处理，封装，数据隐藏
    3. 支持静态和动态SQL
    4. 允许一次发送语句的整块到数据库。这降低了网络流量，并提供高性能的应用程序

## 3 常识
### 3.1 oracle中的错误
都是形如`ORA-[num]`的形式

### 3.2 rowid,rownum和row_number()
#### rowid
每一行数据都有一个唯一的标识符，或者称为rowid

#### rownum
表示查询结果行的编号,第一行分配的是1，第二行是2，依此类推.rownum不能以任何表的名称作为前缀.

它是个伪字段:因为rownum都是从1开始，但是1以上的自然数在rownum做等于判断是时认为都是false条件，所以无法查到rownum = n（n>1的自然数）.比如`select rownum,id,name from student where rownum =2;  --无记录`

使用场景:一般用于限制返回的行数,比如分页,比如取结果中的前多少行等.

注意:默认情况下,rownum是系统按照记录插入时的顺序给记录排的号,所以一般都是结合子查询来使用.

例子1:`select rownum ,id,name from student order by name`的结果如下,

```
    ROWNUM ID     NAME
---------- ------ ---------------------------------------------------
         3 200003 李三
         2 200002 王二
         1 200001 张一
         4 200004 赵四
```

使用子查询`select rownum linenum,id,name from (select * from student order by name)`后是,

```
    ROWNUM ID     NAME
---------- ------ ---------------------------------------------------
         1 200003 李三
         2 200002 王二
         3 200001 张一
         4 200004 赵四
```

例子2:项目中常用到的分页查询:

```sql
select *
from (select RID
        from (select R.RID, ROWNUM LINENUM
                from (select t.rowid RID from xxx t) R
                where ROWNUM <= @page_index * @page_size)
        where LINENUM > @page_size * (@page_index - 1)) TAB1
inner join xxx m on m.rowid = TAB1.RID
```

#### row_number()
一般使用形如`select ROW_NUMBER() over(partition by xxx  order by xxx) as linenum from xxx where xxxx`,就是给结果的每行分配一个编号(从1开始),其中开窗函数over里头的分组及排序的执行晚于后面"where，group by，order by"的执行

例子1:

```sql
select   
ROW_NUMBER() over(partition by customerID  order by insDT) as rows,  
customerID,totalPrice, DID  
from OP_Order where insDT>'2011-07-22' 
```

#### row_number()与rownum的区别
使用rownum进行排序的时候是先对结果集加入伪列rownum然后再进行排序，而row_number()在包含排序从句后是先排序再计算行号。

### 3.3 partition by和group by
前者是分析形函数,后者是聚合函数(待补充)

# 三 基础
## 1 语法和子句
### 1.1 增
### 1.2 删
delete from xxx 
### 1.3 改
update xxx set xxx = xxx,xxx= xxx
### 1.4 查
`select * from  xxx`

### 1.5 模糊查询like
`%`表示一个或多个字符,`_`表示一个字符,对于特殊符号可以使用ESCAPE标识符来查找,如`select * from emp where ename like '%*_%' escape '*'`,escape表示*后面的那个符号不当成特殊字符处理，就是查找普通的_符号(待补充)

### 1.5 group by分组
在`group by`子句的字段可以不在`select`后面,但是对于在`select`后面的非组函数字段,则必须在`group by`子句中
1. 按日期分组:`group by char(t.xxx,'yyyy-mm-dd')`

    上面是按日分组.如果是按周分组是`group by char(t.xxx,'yyyy-IW')`,按月分组则是`group by char(t.xxx,'yyyy-mm')`,按季度是`group by char(t.xxx,'yyyy-Q`,按年是`group by char(t.xxx,'yyyy')`

2. 按时间段分组:``
### 1.6 having过滤分组后的结果
放在group by后面
1. 和where的异同

    where子句中不能使用组函数,但是having可以;其他情况可以通用,从sql优化角度看,尽量使用where,因为having是先分组再过滤,而where是先过滤再分组
    
### 1.7 order by排序
有个快捷写法:用select后面字段的序号代替字段,比如`select deptno,avg(sal) from emp group by deptno order by 2`,那么里面的2就代表了avg(sal)

## 2 函数
### 2.1 分组函数(组函数)
常用的有六个:avg,sum,min,max,count,wm_concat(行转列);注意这几个函数都不会计算空值,比如`count(*)`是14,但`count(comm)`可能是10,最佳实践是使用`nvl`函数,如`count(nvl(comm,0))`
1. 组函数的嵌套:可以直接嵌套,比如
```sql
--求部门平均工资的最大值
select max(avg(sal))
from emp
group by deptno
```
其实按我个人不知道的情况下的理解应该是用max函数将整个求平均工资的语句包起来,事实上却不是我想的这样,需要多理解理解这个group by

#### avg
当字段的值为空时不会参与计算

#### wm_concat
行转列,中间用逗号拼接

### 2.2 nvl滤空函数

### 2.3 日期函数
#### ADD_MONTHS(date,number_months):增减月份

### 2.4 字符串相关函数
#### lengthb()和length()
- lengthb():计算string所占的字节长度
- length():计算string所占的字符长度

对于单字节字符,上面两个的结果是一样的;一个汉字在Oracle数据库里占多少字节跟数据库的字符集有关，UTF8时，长度为三;可以用`length(‘string’)=lengthb(‘string’)`判断字符串是否含有中文.
#### Upper(),Lower(),Initcap(),Concat(),Substr(),Replace(),Instr(),Lpad(),Rpad(),Trim()
Lpad():左侧填充

Rpad():右侧填充

Trim():去除首尾空格

### 2.1 decode
流程控制,效果类似于`if else`
1. 可用于`order by`的指定排序,如`order by decode(m.status,10,20,30,90,0,99)`

### 2.2 sum
一般用法:`sum(t.xxx)`

### 2.3 to_char(),to_number(),to_date()
1. number转date:`to_date(20180203,'yyyy-mm-dd')`,后面这个`yyyy-mm-dd`格式不管怎么写,最终转换出来都是类似这样的`2018/2/3`
2. date转char:`to_char(sysdate,'yyyy-mm-dd')`,会被转换成`2018-03-06`

### 2.4 like,instr和substr

`substr(<string>, <start_position> [,length])`:截取字符,注意plsql中所有字符串的第一个位置的index是从1开始,而不是从0开始

`like`用于模糊查询,`instr`用于判断是否包含某字符串,`substr`用于截取字符串;因为like的效率比较低,所以能用后面的情况下尽量用后面的

### 2.5 distinct去重
如果后面跟多个字段就是对多个字段去重,所以想对多个字段中的单个字段去重的话还是用`group by`

## 3 命令行命令
### 3.1 show user:查看当前用户
### 3.2 desc [表名]:查看表结构
### 3.3 host cls:清屏
### 3.4 /:执行上一条语句
### 3.5 a(--append) [xxx]:增加命令,一定要和[xxx]空两个空格以上

## 4 注释
1. 单行注释:`-- xxx`
2. 多行注释:`/* xxx */`

## 5 变量
### 5.1 
#### rownum
(未整理)只用于排序和分页?

# 四 高级

# 五 经验
## 1 总结
1. 在oracle中,很多的问题都是通过子查询解决的

# 六 问题
## 1 已解决
### 1.1 invalid SQL statement
### 1.2 date format picture ends before converting entire input string
`to_date()`格式化日期必须必须必须保证传入的字符串和要转换的格式精确匹配.前面若含有时分秒格式化的时候也必须含有。比如`to_date(‘2015-12-12 12:12:12’,'yyyy/mm/dd hh24:mi:ss')`

### 1.3 invalid user.table.column, table.column, or column specification
一般是列名不对

### 1.4 identifier is too long
标识符太长,超过了oracle限制的30个字符

### 1.5 column not allowed here
传入的值不符合要求,比如值的名字写错了,值的类型不对等.

## 2 未解决
1. 易百教程:[http://www.yiibai.com/plsql/](http://www.yiibai.com/plsql/)
2. Oracle调优经验
3. 变量的声明
4. job是啥
5. 子查询是啥

6. lengthb(),substrb()

7. 项目中不支持卡号模糊查询,是因为索引的问题?
8. plsql中的冒号表示什么

9. 分析形函数,聚合函数,开窗函数