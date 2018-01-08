# oracle
## 一. 概述
1. PL/SQL中的PL是Procedure Language,表示过程处理语句（如分支、循环等），是面向过程的语言,sql是对数据的操纵，而过程语言是对数据的处理，两者结合才能更强
2. 为什么要学PL/SQL呢？比如我要让某类人的工资增加10%，这个时候用sql来处理就很方便高效了，而且PL/SQL是对oracle最高效的语言
1. 提供的程序包，在联机帮助文档的books->PL->
4. oracle默认开启事务，级别是read committed，所以对数据库修改之后最好加上commit
5. PL/SQL对大小写不敏感
### 1 简介
## 二. 安装配置
## 三. 基础
1. PL/SQL程序的基本结构
    1. `set serveroutput on`打开输出开关
    2. `declare`，作为程序的开始，后面是说明部分
    3. `begin`，后面是程序体
    3. `exception`，例外处理语句
    4. `end;`
    5. `/`，结束
2. 部分方法、关键字和特殊值
    1. desc,查看表的视图或者程序包的结构
    2. sysdate系统时间
    3. dbms_output.put_line('')，输出语句
    4. `||`是连接符
    5. accept接受一个输入，prompt提示
    ```PL/SQL
    accept num prompt '请输入一个字符';
    ```
    这里的num是一个地址值，含义是在改地址上保存了输入值，后面要用的话应该用
    ```PL/SQL
    pnum number := &num;
    ```
    6. show user显示当前用户
    7. show parameter [字符]：查询包含该字符的关键字

3. 变量的定义，变量名在前面，类型写后面，要赋值的话则加上`:=`
    1. 引用型变量，比如把emp表中name的类型定义给pname变量
    ```
    pname emp.name%type
    ```
    2. 记录型变量，代表表中一行的类型,比如把一行的类型定义给变量emp_rec
    ```
    emp_rec emp%rowtype
    ```    
4. 变量的赋值，除了上面的`：=`,还有`into`关键字
5. if语句，一共三种
    1. 
6. 循环语句，共三种
7. 光标，相当于结果集，一般的使用步骤是定义光标->定义变量->打开光标->使用->关闭光标
    1. 光标的4个属性：%found、%notfound、%isopen、%rowcount（影响的行数，相当于正在抓的是多少行，而不是总行数）
    2. oracle默认只能在同一个会话中打开300个光标
    3. 修改光标是
    ```
    alter system set open_cursors=400 scope=both;
    ```
    scope的取值有三个：memory（只更改当前的）、spfile（只更改数据库的，重启db后生效）、both都改
    4. 光标可以带参数
8. 例外，分两种，发生例外的时候可以用exception来捕获。当发生例外的时候，oracle会自动启动pmon（process monitor，经常监视器）来关闭异常的资源（比如未关闭的cursor）
    1. 系统例外
        1. No_data_found，一般是没找到记录的时候出现
        2. Too_many_rows，一般是把多条记录赋值给一个普通的变量
        3. Zero_Divide
        4. Value_error算术或转换错误
        5. Timeout_on_resource在等待资源时发生超时，经常出现在分布式数据库中
    2. 自定义例外，类型是exception，用raise抛出
## 四 pl/sql
## 五 经验
1. 一般对输出结果等不是直接打印出来，而是保存在某个表中，这样就不会因为程序关闭而丢失了