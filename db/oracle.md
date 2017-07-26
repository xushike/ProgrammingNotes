# oracle
## 一. 概述
1. PL/SQL中的PL是Procedure Language,表示过程处理语句（如分支、循环等），是面向过程的语言,sql是对数据的操纵，而过程语言是对数据的处理，两者结合才能更强
2. 为什么要学PL/SQL呢？比如我要让某类人的工资增加10%，这个时候用sql来处理就很方便高效了
1. 提供的程序包，在联机帮助文档的books->PL->
## 二. 基础
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
