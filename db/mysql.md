# mysql
零. 概述  
1. MySQL数据库命令不区分大小写。但在MAC的终端，如果你想使用tab自动补全命令，那么你就必须使用大写

一. 安装配置
1. 版本说明：
    msi是安装版，zip是免安装版，后者比前者大而且配置好可能要花一番功夫
2. 在mac下dmg安装后会有两个mysql的目录：/usr/local/mysql, 这是一个link，指向/usr/local/mysql-xxxxx...(即实际的mysql目录)。

二。使用
1. use [数据库名字]进入数据库时出现信息：
>Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

原因是mysql进入数据库会预读数据库信息，数据库太大会导致进入时很慢，所以提示说的是在登录数据库的时候加上参数 -A(我试了下，在启动的时候加有用，在use [dbname]后加没用)

三.问题
1. 我的mac上安装的mysql没有类似my.default的配置文件，网上说的要自己在etc目录下新建一个my.cnf
2. mysql的自动补全需要在配置文件中设置一下，由于我的mac中没找到配置文件，暂时不折腾

四.经验
1. 今天在命令行里创建表，字段名和表名我都没加``，结果一直最后一行报错，然后我加上它就好了。以前好像不用加的，难道我记错了？