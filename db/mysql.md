# mysql
[TOC]
## 一. 概述
### 3 常识
1. mysql是开源的关系型数据库管理系统，最早由MySQL AB公司开发，目前属于oracle公司
1. MySQL数据库命令不区分大小写。但在MAC的终端，如果你想使用tab自动补全命令，那么你就必须使用大写

#### 3.1 mysql用什么语言写的
mysql是c语言写的，红帽系统中默认有mysql

## 二. 安装配置
### 1. 版本和安装包说明：

### 2. windows下的安装
1. msi是安装版，zip是免安装版，后者比前者大而且配置好可能要花一番功夫

### 3. mac下的安装
2. 在mac下dmg安装后会有两个mysql的目录：/usr/local/mysql, 这是一个link，指向/usr/local/mysql-xxxxx...(即实际的mysql目录)。

### 4. linux下的安装
### 5. mysql图形界面工具
1. MySQL GUI Tools
由mysql官方提供的早期的图形界面工具，现在下载界面可以看到“Please note that development of MySQL GUI Tools has been discontinued. ”，而是推荐使用MySQL Workbench
2. MySQL Workbench
是下一代的可视化数据库设计、管理的工具，它同时有开源和商业化的两个版本，支持多系统。前身是FabForce公司的DBDesigner4。
3. navicat
用得应该是最多的
4. sequel pro
支持mac平台，是由Cocoa和面对对象的C（Mac OSX）编写的，看到有些大牛在用
4. SQLyog
5. mysqlcc

## 三. 基础
1. use [数据库名字]进入数据库时出现信息：
>Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

原因是mysql进入数据库会预读数据库信息，数据库太大会导致进入时很慢，所以提示说的是在登录数据库的时候加上参数 -A(我试了下，在启动的时候加有用，在use [dbname]后加没用)

## 五 经验
1. 今天在命令行里创建表，字段名和表名我都没加``，结果一直最后一行报错，然后我加上它就好了。以前好像不用加的，难道我记错了？
2. workbench左下角显示[not connection]()，原因在于没有启动数据库服务

## 六 问题
1. 我的mac上安装的mysql没有类似my.default的配置文件，网上说的要自己在etc目录下新建一个my.cnf
2. mysql的自动补全需要在配置文件中设置一下，由于我的mac中没找到配置文件，暂时不折腾
3. mysql连接数的极限是多少：300到700(300是机械硬盘的理想情况，实际可能200就gg)
