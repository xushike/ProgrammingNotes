# unix

# unix

#  一 概述
## 3 常识
### 3.1 unix 思想
1. 一个工具只做好一件事情

### 3.2 usr目录的全称
Unix System Resource,一般放程序软件,注意不是user

# 六 问题
## 1 已解决
### 1.1 Linux下/usr/bin与/usr/local/bin/区别
通常/usr/bin下面的都是系统预装的可执行程序，会随着系统升级而改变;/usr/local/bin目录是给用户放置自己的可执行程序的地方，推荐放在这里，不会被系统升级而覆盖同名文件

执行顺序:如果两个目录下有相同的可执行程序，谁优先执行受到PATH环境变量的影响,写在前面的优先执行

### 1.2 关于/usr/libexec目录
参考FHS标准的section4.7：https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html#usrlibexec

大概就是该目录的二进制文件，主要不是给用户或者脚本直接使用的。实际使用时，因为版本差异，可以看作和/usr/lib一样。

比如mac查看的java安装位置的命令是`/usr/libexec/java_home`

## 2 未解决