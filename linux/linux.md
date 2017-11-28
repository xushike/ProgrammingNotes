# linux
[TOC]
## 一. 概述
1. linux版本：分为内核版本和发型版本，后者相当于在前者的基础上加了一些个性化的东西，核心可以是一样的。
慕课网上说：服务器领域用得最多的是redhat，也可以选择一些收费的服务；ubuntu有好看的图形界面；centOS和redhat内核是一样的，但是完全免费，现在用的人越来越多了；
fedora是redhat公司的个人版，其实相当于集成了最新功能的版本，而且界面也不错(不过稳定性就很难保证)；
2. linux和windows的不同：  
linux严格区分大小写  
linux中所有内容以文件形式保存，包括硬件(一切皆文件)
linux不靠扩展名区分文件类型(但是有约定俗成的一些规则：比如二进制软件包.rpm、简本文件.sh、配置文件.conf等，是linux为了照顾系统管理员，也可以不写)
2. 开源软件：apache、nginx、mysql、php、mongoDB、python、ruby、sphinx、samba
3. www.netcraft.com：对网站和服务器分析的网站
### 1. 一些常识
#### 1.1 一些快捷键
1. 复制粘贴快捷键(windows中cmd似乎不生效)：
```
ctrl+insert:复制
shift+insert:粘贴
```
2. 终端清屏快捷键：`ctrl+L`，在终端有任务进行的时候不会生效
3. 同一应用有多个窗口时，可以通过`alt+~`切换，mac也一样，win不行
#### 1.2 关于gcc
>网友的回答：gcc 最开始的时候是 GNU C Compiler, 如你所知，就是一个c编译器。但是后来因为这个项目里边集成了更多其他不同语言的编译器，GCC就代表 the GNU Compiler Collection，所以表示一堆编译器的合集。 g++则是GCC的c++编译器。
现在你在编译代码时调用的gcc，已经不是当初那个c语言编译器了，更确切的说他是一个驱动程序，根据代码的后缀名来判断调用c编译器还是c++编译器 (g++)。比如你的代码后缀是*.c，他会调用c编译器还有linker去链接c的library。如果你的代码后缀是cpp, 他会调用g++编译器，当然library call也是c++版本的。
当然我说了这么多你可能感到有些混乱，没关系，你就把gcc当成c语言编译器，g++当成c++语言编译器用就是了。
#### 1.3 学习linux的一些网站
1. 查询linux命令：[http://man.linuxde.net/](http://man.linuxde.net/)
2. debian官方：[https://www.debian.org/doc/manuals/debian-faq/](https://www.debian.org/doc/manuals/debian-faq/)
3. 鸟哥的linux私房菜(推荐)：[http://linux.vbird.org/linux_basic/0320bash.php#bash](http://linux.vbird.org/linux_basic/0320bash.php#bash)
#### 1.4 网友推荐的linux书籍(按学习顺序排列)
1. 《鸟哥的Linux私房菜：基础学习篇》
2. 《Linux Shell 脚本攻略》
3. 《UNIX环境高级编程》
4. 《Linux系统编程》
5. 《Linux内核设计的艺术》
6. 《Linux内核设计与实现》
#### 1.5 动态链接和静态链接
1. 动态链接和静态链接的区别是，前者前者不会把依赖编译进程序里，而后者会；所以前者编译的程序占用更小，在程序有相同依赖时更节约空间，而后者
2. 动态链接库和静态链接库一般是编译集成一系列的接口（函数），在linux中前者一般后缀为`.so`，后者为`.a`
#### 1.6 关于linux的`./`和`.`等
1. `.`一般表示当前目录，可以不写；如果放在文件名前则表示隐藏文件
2. `/`一般表示根目录，也是目录分隔符，`/etc/`表示根目录下的etc目录，`/etc`则会检测etc是目录还是文件，虽然一般etc都是目录
3. `./`：（待补充）
    1. 本人的理解是：`./`其实也是表示当前目录，和`.`一样，但是在执行程序时，linux的默认搜索目录里没有当前目录，如果只是加上`.`系统又会把`.`和程序连在一起当成一个命令，而`/`是目录分隔符，如果再加上`/`，系统就不会误会了，所以如果你在当前目录中执行程序就要加上路径`./`，用全路径代替也是可以的(全路径执行的话是`/xx/xx/xx`，可加`.`可不加)。（所以把`.`加到PATH中就不需要这命令了？）
    2. linux似乎默认是优先查找PATH环境变量下的路径，最后才搜索当前目录，这点和win相反
#### 1.7 关于`.bashrc`文件
1. 在linux用户目录`$HOME`（/home/xxx）下`ls -al`可以看到4个隐藏文件：
    ```bash
    .profile（待补充）
    .bash_history       记录之前输入的命令
    .bash_logout        当你退出时执行的命令
    .bash_profile       当你登入shell时执行
    .bashrc             当你登入shell时执行
    ```
    1. 后两个的区别：`.bash_profile`只在会话开始时被读取一次，而`.bashrc`则每次打开新的终端时，都要被读取
    2. 这些文件是每一位用户对终端功能和属性设置，修改.bashrc可以改变环境变量PATH、别名alias和提示符
    3. 除了可以修改用户目录下的.bashrc文件外，还可以修改如`/etc/profile`文件、`/etc/bashrc`文件及目录`/etc /profile.d`下的文件。但是修改/etc路径下的配置文件会应用到整个系统，属于系统级的配置，而修改用户目录下的.bashrc则只是限制在用户应用上，属于用户级设置。建议修改用户目录下的`.bashrc`，即无需root权限，也不会影响其他用户。
    4. rc的意思是run commands，参见[https://en.wikipedia.org/wiki/Run_commands](https://en.wikipedia.org/wiki/Run_commands)

2. PATH环境变量修改
    1. **PATH变量决定了shell将到哪些目录中寻找命令或程序**,作为惯例，所有环境变量名都是大写
    2. 设置变量时直接用名称，但使用时加上$(?):
        ```bash
        #设置，比如在原基础上新增变量
        PATH=$PATH:/usr/local/arm/3.4.1/bin
        #使用，比如输出
        echo $PATH
        ```
        这样设置的新PATH其实是局部变量，在新终端中不会生效（和win似乎是反着的），加上export才是全局，而且加上后只对当前和以后的终端生效
    3. 为了让修改永久添加到`$PATH`，只要将`export`的那行添加到`.bashrc`或`/etc/bashrc`文件中，然后用`source ~/.bashrc`使其立即生效。（一般会在`.bash_profile`文件中显式调用`.bashrc`，登陆linux启动bash时首先会去读取`~/.bash_profile`文件，这样`~/.bashrc`也就得到执行了，你的个性化设置也就生效了）
3. alias别名
    1. 一般在.bashrc或/etc/bashrc文件里有几句话
        ```bash
        alias rm='rm -i'
        alias cp='cp -i'
        alias mv='mv -i'
        ```
        可以在该配置文件中添加自己风格的别名，如“alias ll='ls -l'”，只需要在终端中输入“ll”就实现了“ls -l”的功能
4. 提示符(意义不大)
#### 1.8 关于文件扩展名
1. 关于判断文件类型：与win不同的是，linux不是根据文件的扩展名来判断文件是否能执行，而是查看文件内的头部信息来判断，另外，gcc是根据文件扩展名来判断
2. 关于是否加上文件名：虽然linux不通过扩展名判断，但还是推荐加上，为了使用时方便
#### 1.9 关于distribution
distribution一般是指发行版的意思，Linux真正意义上说只是一个内核，我们通常使用的都是基于Linux内核的发行版了。如常见的Linux发行版有：Ubuntu、Fedora、Suse、ArchLinux等
## 二. 安装配置
## 三. 基础（命令）
### 1 查看相关命令
1. 查看文件
    1. ls 
        1. `--full-time`：一般情况下似乎看不到年份信息，此命令可以显示全部日期信息
2. 查看命令历史：`history`
### 2 文件操作相关
#### 2.1 压缩相关
1. 首先明确linux中打包和压缩是不同的，打包是把多个文件变成一个总的文件；因为linux中很多压缩程序只能对一个文件压缩，所以一般是先打包再压缩
2. tar
    >关于tar这个命令名字的来历：Initially, tar archives were used to store files conveniently on magnetic tape. The name "Tar" comes from this use（最初，tar档案被用来方便地在磁带上存储文件。 “焦油”这个名字来自这个用途。）
    1. `-z`或`--gzip`或`--ungzip`：通过gzip指令处理备份文件
    2. `-v`：显示操作过程
    3. `-f [压缩或备份的文件]`或`--file=[压缩或备份的文件]`：指定备份文件
    4. `-c`或`--create`：建立新的备份文件
    5. `-x`或`--extract`或`--get`：从备份文件中还原文件
    6. `-t`或`--list`：列出备份文件的内容
    6. `-C [目录]`：在指定目录解压缩。
    ```bash
    # 最常用的例子如下
    # 压缩：
    tar -zcv -f filename.tar.gz 要被压缩的文件或目录名称 
    # 查询：
    tar -ztv -f filename.tar.gz 
    # 解压缩：
    tar -zxv -f filename.tar.gz -C 欲解压缩的目录
    ```
#### 2.2 文件移动复制
1. 

## 四. 使用
1. 
## 五. 问题
1. 学会使用linux联机帮助
2. 在命令行执行命令的时候输入命令会怎么样
3. linux的鼠标中键表示什么？
4. 移动到终端正在输入的命令前后面快捷键
5. linux的计算器？
6. sbin
7. 删除包和依赖呢？
```bash
dpkg -P package #删除包（包括配置文件）
dpkg -L package #列出与该包关联的文件
```
8. linux按时间顺序排列
9. man 3 xxx
10. dpkg所有参数在哪儿看
11. 为什么`./`是运行，可以加在最后?
12. 知道 Linux 下最大的坑是什么么？就是动态链接库。
为什么 Linux 大部分软件都要求编译安装，就是因为动态链接库。
13. linux和mac上各种格式包的安装和区别
14. 内容太多终端显示不完怎么办，终端中如何翻页等

