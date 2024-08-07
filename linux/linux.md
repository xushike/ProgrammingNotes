# linux
[TOC]

# 一 概述
## 1 简介
### linux和linux发行版
linux(linux内核版本)只是一个操作系统内核，还需要搭配其他一系列软件，才能组成完整的操作系统，这个完整的操作系统称为linux发行版。

常见发行版：

1. redhat:服务器领域用得最多，也可以选择一些收费的服务
    1. centOS:和redhat内核是一样的，但是完全免费，现在用的人越来越多了
    2. fedora:是redhat公司的个人版，其实相当于集成了最新功能的版本，而且界面也不错(不过稳定性就很难保证)
2. Debian
3. ubuntu:基于Debian，有好看的图形界面
4. Android

### linux和windows的不同
1. linux严格区分大小写  
2. linux中所有内容以文件形式保存，包括硬件(一切皆文件),所以linux中文件和目录能同名
3. linux不靠扩展名区分文件类型(但是有约定俗成的一些规则：比如二进制软件包`.rpm`、脚本文件`.sh`、配置文件`.conf`等，是linux为了照顾系统管理员，也可以不写)
4. linux是多用户系统,而win是单用户

## 3 常识
### 3.1 快捷键
1. 复制粘贴快捷键(windows中cmd不生效)：复制`ctrl+insert`，粘贴`shift+insert`
2. 终端清屏快捷键：`ctrl+L`或`clear`，在终端有任务进行的时候不会生效
3. 同一应用有多个窗口时，可以通过`alt+~`切换，mac也一样(有细微差别)，win不行
4. 强制结束:`ctrl+c`(?)
5. 挂起:`ctrl+z`,相当于暂停?然后可以用fg和bg在前后台之间切换
6. 文件结束EOF:`ctrl+d`,该快捷键会发送结束字符`EOF`，**而不是发送信号**，EOF表示一个特殊的二进制值。它一般有如下两个作用:
    1. 文本输入的结束:比如`wc`统计命令,输入任意字符之后`ctrl+d`就表示输入结束
    2. 退出终端:在没有文本输入的时候，终端收到EOF会退出

### 3.2 Locale
linux系统的区域设置、本地化策略。其中几个设置的优先级是`LC_ALL > LC_* >LANG`，比如git（>2.19）就会去读取该参数，发现`LANG=zh_CN.UTF-8`，就会设置git为中文。

### 1.2 关于gcc
>网友的回答：gcc 最开始的时候是 GNU C Compiler, 如你所知，就是一个c编译器。但是后来因为这个项目里边集成了更多其他不同语言的编译器，GCC就代表 the GNU Compiler Collection，所以表示一堆编译器的合集。 g++则是GCC的c++编译器。
现在你在编译代码时调用的gcc，已经不是当初那个c语言编译器了，更确切的说他是一个驱动程序，根据代码的后缀名来判断调用c编译器还是c++编译器 (g++)。比如你的代码后缀是*.c，他会调用c编译器还有linker去链接c的library。如果你的代码后缀是cpp, 他会调用g++编译器，当然library call也是c++版本的。
当然我说了这么多你可能感到有些混乱，没关系，你就把gcc当成c语言编译器，g++当成c++语言编译器用就是了。

### 1.5 动态链接和静态链接
动态链接和静态链接的区别:前者不会把依赖编译进程序里，而后者会；所以前者编译的程序占用更小，在程序有相同依赖时更节约空间，而后者

动态链接库和静态链接库一般是编译集成一系列的接口（函数），在linux中前者一般后缀为`.so`，后者为`.a`

### 1.6 关于linux的`./`和`.`等
1. `.`一般表示当前目录，可以不写；如果放在文件名前则表示隐藏文件
2. `/`一般表示根目录，也是目录分隔符，`/etc/`表示根目录下的etc目录，`/etc`则会检测etc是目录还是文件，虽然一般etc都是目录
3. `./`：（待补充）
    1. 本人的理解是：`./`其实也是表示当前目录，和`.`一样，但是在执行程序时，linux的默认搜索目录里没有当前目录，如果只是加上`.`系统又会把`.`和程序连在一起当成一个命令，而`/`是目录分隔符，如果再加上`/`，系统就不会误会了，所以如果你在当前目录中执行程序就要加上路径`./`，用全路径代替也是可以的(全路径执行的话是`/xx/xx/xx`，可加`.`可不加)。（所以把`.`加到PATH中就不需要这命令了？）
    2. linux似乎默认是优先查找PATH环境变量下的路径，最后才搜索当前目录，这点和win相反
### 1.7 关于`.bashrc`文件
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
    2. 设置变量时直接用名称，但使用时需要加上`$`:
        ```bash
        #设置，比如在原基础上新增变量
        PATH=$PATH:/usr/local/arm/3.4.1/bin
        #使用，比如输出
        echo $PATH
        ```
    3. 使用`export`：上面那样设置的新PATH其实是局部变量，在新终端中不会生效（和win似乎是反着的），加上`export`才是全局，而且加上后只对当前和以后的终端生效
        
        ```bash 
        export PATH=$PATH:/usr/local/arm/3.4.1/bin
        ```
        
        资料说`export`可以设置、修改和查看环境变量，但是查看的时候，比如`export $PATH`会提示`export: not valid in this context: ...`（虽然后面会跟着环境变量的内容，但是前面的错误让人不爽），没搞懂，干脆用`echo $PATH`查看。
    4. 为了让修改永久添加到`$PATH`，只要将`export`的那行添加到`.bashrc`或`/etc/bashrc`文件中，然后用`source ~/.bashrc`使其立即生效。（一般会在`.bash_profile`文件中显式调用`.bashrc`，登陆linux启动bash时首先会去读取`~/.bash_profile`文件，这样`~/.bashrc`也就得到执行了，你的个性化设置也就生效了）
3. `alias`:设置别名，在shell的配置文件中添加自己风格的别名，如`alias ll='ls -l'`，只需要在终端中输入`ll`就实现了`ls -l`的功能

    ```bash
    # 如果是bash，配置文件一般是在 .bashrc 或 /etc/bashrc 里
    # 一般默认就带了下面三个
    alias rm='rm -i'
    alias cp='cp -i'
    alias mv='mv -i'
    
    # 自定义
    alias ssh_qa2='ssh qa2@www.example.com' # alias设置的别名不支持空格，所以这里不能设置为 ssh qa2，可以用下划线等替代
    alias psql_test='psql "postgresql://postgres:xxx@hostA:portA/dbNameA?sslmode=disable"'
    ```
        
4. 提示符(意义不大)

### 1.8 关于文件扩展名
1. 关于判断文件类型：与win不同的是，linux不是根据文件的扩展名来判断文件是否能执行，而是查看文件内的头部信息来判断，另外，gcc是根据文件扩展名来判断
2. 关于文件命名：
    1. 关于扩展名
        linux没有文件扩展名的概念,即linux不通过扩展名判断文件类型.但是还是推荐加上扩展名，这样使用时更方便,而且有些应用程序可能会用到文件扩展名
    2. 关于标点符号
        不要使用空格,支持`.`,`-`和`_`
        
### 1.9 关于distribution
distribution一般是指发行版的意思，Linux真正意义上说只是一个内核，我们通常使用的都是基于Linux内核的发行版了。如常见的Linux发行版有：Ubuntu、Fedora、Suse、ArchLinux等

### 1.10 关于标准输入输出
执行shell命令时会自动打开三个标准文件:
- `stdin`标准输入文件,程序从中得到输入,默认连接到键盘
- `stdout`标准输出文件,运行结果输出到此,默认连接到屏幕
- `stderr`标准错误输出文件,错误信息(状态信息)输出到此,默认连接到屏幕

进程将从标准输入文件中得到输入数据，将正常输出数据输出到标准输出文件，而将错误信息送到标准错误文件中。
>弄懂linux的标准输入输出,才能理解重定向和管道的区别,如果还是不能理解,看这个例子及后面的释义:
```bash
cat myFile.txt | pbcopy
pbcopy < myFile.txt
```

1. 文件描述符
     一个程序可以在几个编号的文件流中的任一个上产生输出。虽然我们已经将这些文件流的前 三个称作标准输入、输出和错误，shell 内部分别将其称为文件描述符0、1和2。
1. 标准输入/输出
    标准输入输出有几个问题:
    - 每次的输入只能用一次
    - 修改不方便
    - 只能看不能动

    于是linux引入了两种机制:输入/输出重定向和管道
2. 重定向(即I/O重定向)I/O重定向允许我们更改输出位置和输入来源
    1. 标准输入重定向:把标准输入重定向到指定的文件中,即可以不来自键盘
        1. 直接跟文件名,如`wc hello.txt`
        2. 输入重定向:`[命令] < [文件名]`
        3. here文档,允许命令在获取命令行输入数据时像是在读取文档一样,后面跟的字符代表开始和结束的分割符,如:
        ```bash
        wc << !?
        这段话开始了
        这段话结束了
        !?
        ```
    2. 标准输出重定向(常用):把标准输出重定向到指定文件中
        1. 输出重定向,如果后面的文件已存在,会被覆盖:`[命令] > [文件名]`,如`ls > hello.out`
            1. 该命令不会重定向标准错误输出,比如`ls /bin/usr > output.file`,因为`/bin/usr`目录不存在,屏幕上会打印出标准错误输出,同时因为使用的是`>`重定向符,重定向操作开始重写文件，然后由于错误而停止，导致文件内容删除,如果不存在该文件,则会创建一个新的空文件
            2. 利用重定向的重写技巧,我们可以这样删除一个文件内容或者创建一个新的空文件:`> xxx.file`
        2. 输出追加重定向:不会覆盖原来文件的内容，而是追加到文件的尾部`[命令] >> [文件名]`
    3. 标准错误输出重定向:可在屏幕上看到正常输出结果,同时把错误重定向到文件中.因为重定向标准错误缺乏专用的重定向操作符,为了重定向标准错误，我们必须参考其文件描述符
        1. 重定向:`2>`,如`ls 2> err.file`
        2. 追加重定向:`2>>`
    4. 将输出和错误一起重定向到文件中
        1. 老版本的写法,旧版本shell中也有效,如`ls /bin/usr > output.file 2>&1`,注意顺序很重要,标准错误的重定向必须总是出现在标准输出重定向之后，不然不起作用

            ```bash
            nohup npm start > demo.log 2>&1 &
            ```
        2. 新版本写法,更精简合理,如`ls &> output.file`
    5. 重定向到黑洞`/dev/null`
        `/dev/null`是一个特殊文件,叫位存储桶,位存储桶是个古老的Unix概念.
3. 管道：管道用于处理标准输出的数据。对于把**一个命令的输出作为另一个命令的输入**,管道比重定向更加好用,可以通过`|`一直连下去,最后显示最后一个的输出,如`ls ~ | wc -w`
    1. 说明
        1. 管道**仅能处理标准输出的数据**,对标准错误输出没有能力处理
        2. 管道后所接的命令必须能够接受标准输入才行,否则无效,比如`ls`,`mv`,`cp`这些管道就没用,但是这些命令可以用命令替换
    2. 例子
        
        ```bash
        # 比如很多工具的安装脚本写在网页上，可以借助curl和sh来实现安装
        curl https://getcroc.schollz.com | bash
        ```

4. 其他:命令替换
    命令替换和重定向有点类似,区别在于命令替换是把一个命令的输出作为另一个命令的参数,有两种用法,具体参考字符展开中的命令替换
5. 其他:连续命令
    和管道不同在于,连续命令(用`;`分隔)中各个命令不存在相关性,只是顺序执行

### 1.11 关于命令的选项
大多数命令使用短选项——一个中划线加一个字符,但是许多命令也支持长选项——两个中划线加一个单词,而且许多命令允许把多个多个短选项合在一起使用,比如`ls -lt`

### 1.12 关于命令行的参数
1. 参数可重复:当有三个圆点跟在一个命令的参数后面， 这意味着那个参数可以重复，如`mkdir directory...`,可以使用`mkdir dir1 dir2 dir3`等同时创建多个目录

### 1.13 关于linux的普通文件(regular file)

### 1.14 关于linux的元键
现在键盘上,一般alt代表元键,如果是在终端中,则`esc`也可当做`alt`来用

### 1.15 终端，Shell，“tty”和控制台（console）有什么区别
参考知乎网友的回答:[终端，Shell，“tty”和控制台（console）有什么区别？](https://www.zhihu.com/question/21711307)

### 3.16 login shell 和 non-login shell，.bash_profile和.bashrc
为什么会有login shell和non-login shell：会读取不同的配置文件。

login shell：取得shell时需要完整登录流程（比如需要输入账号密码）就称为login shell，比如图形界面登录，ssh登录，命令行登录。一般会依次去读取几个配置文件，顺序如下：
1. `/etc/profile`
2. `~/.bash_profile` 或 `~/.bash_login` 或 `~/.profile`:这三个从左到右只要存在一个，后面的就不会被读取。

non-login shell：取得shell的方法不需要重复登录流程的就是non-login shell。仅会读取`~/.bashrc`

注意：linux的shell读取的配置和mac不同。

### 3.18 关于文件的创建时间
需要内核提供`xstat()`才可以拿到创建时间（但是大部分linux系统似乎都么有），所以一般认为linux没有文件的创建时间，在ext4文件系统下可以试试`debugfs -R 'stat <58826> ' /dev/mapper/tiny--vg-root`命令(未测试)

## 4 文档资料等
1. 网友写的Linux工具快速教程，还不错：https://linuxtools-rst.readthedocs.io/zh_CN/latest/index.html
1. 查询linux命令：[http://man.linuxde.net/](http://man.linuxde.net/)
2. debian官方：[https://www.debian.org/doc/manuals/debian-faq/](https://www.debian.org/doc/manuals/debian-faq/)
3. 鸟哥的linux私房菜(推荐)：[http://linux.vbird.org/linux_basic/0320bash.php#bash](http://linux.vbird.org/linux_basic/0320bash.php#bash)
1. 某博客
    1. 《鸟哥的Linux私房菜：基础学习篇》
    2. 《Linux Shell 脚本攻略》
    3. 《UNIX环境高级编程》
    4. 《Linux系统编程》
    6. 《Linux内核设计与实现》
    5. 《Linux内核设计的艺术》
2. 知乎Han:
    1. 《The Linux Command Line》(豆瓣 9.3分)，中文名“快乐的linux命令行”,作为入门和手册,中文翻译github地址:[http://billie66.github.io/TLCL/book/](http://billie66.github.io/TLCL/book/)
    2. 《The Pragmatic Programmer》（豆瓣 8.9分），中文名“程序员修炼之道”


# 二 安装配置

# 三 基础（常用工具或命令）

## 0 构架
### 常见名词


## 1 查看相关命令
### 1.1 查看文件信息
`ls`:最基础并且使用的最广泛的命令行中工具之一。它是一个POSIX兼容工具，在GNU基本工具集以及BSD各种变体上都可以使用
1. 列出当前目录所有文件:`ls`或`echo *`,列出其他目录`ls [路径]`,列出多个目录的文件`ls [路径1] [路径2]`
2. 只列出当前目录下的目录:`ls /`或`echo */`
3. 参数`--full-time`：一般情况下似乎看不到年份信息，此命令可以显示全部日期信息
4. 参数`-a`:列出所有文件,包括隐藏文件和以.开头的文件（linux中`.`代表当前目录,`..`代表父目录）
1. 参数`-l`:以长格式(每个一行?)查看文件详细信息
2. 参数`-t`按文件修改时间的先后来排序
3. 参数`-h`(`--human-readable`),以人可读的格式来显示文件大小
4. 参数`-i`(`--inode`):打印文件的索引节点(inode)信息
5. 参数`-S`,命令输出结果按照文件大小来排序,优先级比`-t`高
6. 参数`-r`(`--reverse`),以相反顺序来显示结果
7.  参数`-A`,列出除`.`和`..`外所有文件,包括隐藏文件

`lsof`(list open files,列出打开的文件)：列出某个进程打开的所有文件信息。因为unix中一切皆文件，所以它可以查看的文件包括：普通的文件，目录，NFS文件，块文件，字符文件，共享库，常规管道，符号链接，Socket流，网络Socket，UNIX域Socket等等。

参考：
1. https://www.ibm.com/developerworks/cn/aix/library/au-lsof.html#listing2

参数：
1. `-c<进程名>`：列出指定进程所打开的文件，如

    ```ssh
    lsof -c ssh 
    ```
1. `-i`:列出符合条件的进程,比如`4、6、协议、:端口、 @ip`等

使用（待补充）：
1. 查看端口占用情况`lsof -i:8080`
1. 恢复被删除的文件
2. 查看连接


### 1.2 查看文件类型:`file [filename]`
会打印文件类型和内容的简单描述,比如文本文件是`ASCII text`，类型有：
|属性|	文件类型|
|-|:-|
|`-`|	一个普通文件|
|`d`|	一个目录|
|`l`|	一个符号链接。注意对于符号链接文件，剩余的文件属性总是"rwxrwxrwx"，而且都是 虚拟值。真正的文件属性是指符号链接所指向的文件的属性。|
|`c`|	一个字符设备文件。这种文件类型是指按照字节流来处理数据的设备。 比如说终端机或者调制解调器|
|`b`|	一个块设备文件。这种文件类型是指按照数据块来处理数据的设备，例如一个硬盘或者 CD-ROM 盘。|

### 1.3 查看文件内容 cat more less tail head
`cat`: 读取或拼接文件。读取文件到标准输出, `cat`用于读取一个或多个文件,然后复制他们到标准输出,没有分页,经常用来显示简短的文本文件

`cat`使用
1. 不带参数使用,则是读取标准输入到标准输出,此时可以`ctrl+d`给它一个EOF结束.
2. `cat > xxx.txt`实现世界上最低能的文字处理器

`more`：略

`less`: 可查看所有类型的文本文件(即ASCII类型的文件,包括txt、配置文件、脚本等),如果查看非文本文件,则是乱码.特点是**自带分页**,可以接受标准输入.`less`是早期unix程序`more`的改进版,意味着"less is more"。支持管道，因为有分页,所以可以用来方便的查看产生标准输出的命令运行结果,比如`ls | less`、`history | less`、`ps -ef | less`

`less`常用操作
1. 导航
    1. 上一行`k`,下一行`j`,上一页`b`,下一页`space`,页首`g`,页尾`G`
    2. 跳到指定的行：输入`[Num]g`跳转到指定的行数。

        ```bash
        less example.txt
        90g # 跳转到第90行
        ```
    2. 标记导航：使用`m`标记，比如`ma`就是用a标记文本的当前位置，然后使用`'`导致过去，比如`'a`就是导航到标记的a处。一般用于大文件。
2. 向上/下查找匹配的字符串`?xxx`和`/xxx`,查看上/下一个匹配`n`和`N`
3. 仅显示匹配模式的行，而不是整个文件`&pattern`
4. 查看帮助文档`h`,退出less`q`
5. 多个文件时的下一个文件`:n`,上一个文件`:p`

    ```bash
    less exampleA exampleB
    ```
6. 使用配置的编辑器编辑当前文件`v`

`less`参数：
1. `-m`：像`more`那样显示百分比
1. `-N`：显示行号
1. `-I`：在后续查找字符串的时候忽略大小写
2. `-S`(`--chop-long-lines`)：使用了该选项后，`less`不会把长行换行显示，而是在一行中显示，超出的部分用左右箭头查看
5. `-~`：隐藏波浪符（~）。在浏览完文件内容后，`less`在后续的行上显示一系列的波浪符（~），该选项来可以关闭这个功能

### 1.4 查看命令类型 type
命令类型一般有：
1. file为外部指令
2. alias为别名。如果本来的命令和别名重名，优先使用别名。
3. builtin为系统（shell？）內建指令

参数:
1. `-a`:显示命令的绝对路径
    ```bash
    # 比如在mac下 type -a git 可能显示两个路径
    git is /usr/local/bin/git # 第一个是brew安装的git的软链接路径
    git is /usr/bin/git # 第二个是mac自带的git的路径
    ```
    
### 1.6 查看內建命令的帮助文档`help`
该命令是bash的內建的帮助工具,用法是`help [命令名]`,实例如
```bash
[me@linuxbox ~]$ help cd
cd: cd [-L|-P] [dir]
Change ...
```
注意表示法：出现在命令语法说明中的方括号，表示可选的项目。一个竖杠字符 表示互斥选项。帮助文档很简洁准确，但它决不是教程。

许多可执行程序支持一个`--help`选项，用于显示命令所支持的语法和选项说明.不过有些不支持,但是任何情况该命令都值得一试


### 1.7 查看程序手册 man
许多希望被命令行使用的可执行程序，提供了一个正式的文档，叫做手册或手册页(man page)。一个特殊的叫做man的分页程序(大多数man使用的是less)，可用来浏览他们。用法`man [program]`手册文档的格式有点不同:一般包含一个标题、命令语法的纲要、命令用途的说明、 以及每个命令选项的列表和说明,也包括系统管理员命令、程序接口、文件格式等。但手册文档通常并不包含实例，它打算作为参考手册，而不是教程。
1. 参数`[num]`:跳到手册的指定章节,如果有的话.因为man的手册是分章节的

### 1.8 查看命令历史：history
 1. 反向递增搜索:`ctrl+r`,搜索之后回车是执行,`ctrl+j`是复制到shell
 2. 执行特定行的命令`![num]`

### 1.9 查看日期:`date`
 1. 直接使用显示类似:`2017年12月 9日 星期六 20时19分25秒 CST`
 2. 还可以用date的格式化输出功能,比如`date +%Y/%m/%d`,会显示`2017/12/09`.从这里也可以看出linux的命令选项前不仅可以用`-`,在特殊情况下还可以用`+`

### 1.10 查看日历:`cal`
 1. 查看某年的日历:如,`cal 2017`,查看某年某月的日历:`cal [mon] [year]`

### 1.11 查看程序的资源信息:top(待补充)
对于`top`,它的命令似乎是后面手动输入的
1. 字段说明

    | 字段  | 说明                                          |
    | ----- | --------------------------------------------- |
    | `vir` | 进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES |
2. 命令说明

### 1.12 查看网络接口
`ifconfig`:是用来配置网络接口的命令(linux & mac)
1. 参数
    1. `-a`:可以显示当前所有的接口。
2. 显示说明
    1. `lo0`(`loopback0`)：回环接口、纯软件层面的虚拟网络接口，表示主机的回坏地址。并非真实存在，并不真实地从外界接收和发送数据包，而是在系统内部接收和发送数据包，因此虚拟网络接口不需要驱动程序。一般lo回环ipv4地址为:`127.0.0.1`，子网掩码：`255.255.255.0`
        1. 特点
            1. 接口地址永远是UP
            2. 该接口可以配置地址，甚至配置全1的掩码，节省地址空间
            3. 不能封装任何链路层协议
        2. 场景
            1. 路由器使用loopback接口地址作为该路由器产生的所有IP包的源地址，这样使过滤通信量变得非常简单
            1. 比如测试一个网络程序，但又不想让局域网或外网的用户能够查看，只能在此台主机上运行和查看所用的网络接口。比如把 HTTPD服务器的指定到回坏地址，在浏览器输入 `127.0.0.1`就能看到你所架WEB网站了。但只是您能看得到，局域网的其它主机或用户无从知道。

    2. `eth0`(`ethernet0`):以太网接口。以太网接口与网卡对应，每个硬件网卡(一个MAC)对应一个以太网接口，其工作完全由网卡相应的驱动程序控制。如果物理网卡只有一个，而却有eth1，eth2等，则可能存在无线网卡或多个虚拟网卡，虚拟网卡由系统创建或通过应用层程序创建，作用与物理网卡类似。比如连接WIFI的时候`eth0`可能就是分配给WIFI用的。字段说明(行数可能变化)
        1. 第一行
            1. `Link encap`:连接类型，比如Ethernet（以太网）
            1. `HWaddr`表示网卡的物理地址
        2. 第二行
            1. `inet addr`用来表示网卡的IP地址，比如`192.168.199.238`
            2. `Bcast`广播地址，比如`192.168.120.255`
            3. `Mask`掩码地址，比如`255.255.255.0`
        3. 第三行
            1. `inet6 addr`ipv6地址  
        4. 第四行：
            1. `UP`代表网卡开启状态
            2. `RUNNING`代表网卡的网线被接上
            3. `MULTICAST`支持组播`
            4. `MTU`最大传输单元，比如`1500`1500字节
        5. 第五、六行：接收、发送数据包情况统计
        6. 第七行：接收、发送数据字节数统计信息

    3. `br0`or`bridge0`:网桥接口。网桥是一种在链路层实现中继，对帧进行转发的技术，根据MAC分区块，可隔离碰撞，将网络的多个网段在数据链路层连接起来的网络设备。br0可以将两个接口进行连接，如将两个以太网接口eth0进行连接，对帧进行转发。
    4. `wlan0`:无线接口。无线网卡对应的接口，无线网卡也需要对应的驱动程序才能工作。
    5. `gif0`(`Software Network Interface 0`):通用 IP-in-IP隧道(RFC2893)
        1. 参考：https://www.freebsd.org/cgi/man.cgi?gif(4)
    6. `stf0`(`6to4 tunnel interface 0`):6to4连接(RFC3056),[IPv6 to IPv4 tunnel interface](https://www.freebsd.org/cgi/man.cgi?gif(4)) to support the transition from IPv4 to the IPv6 standard.
        1. 参考：https://en.wikipedia.org/wiki/6to4
    7. `fw0`(`Firewire0`)：FireWire network interface.
    8. `vmnet1`(`Virtual Interface 0`)
    10. `vlan0`虚拟局域网络
    11. `p2p0`Point-to-Point 协议
    9. `awdl0`:airdrop peer to peer(一种mesh network), apple airdrop设备特有，可以看作是一种特殊的WIFI连接
    12. `llw0`：WLAN low-latency interface。类似于awdl,llw也是一种特殊的WiFi连接，低延迟(不允许省电)
    13. `utun0`:mac osx+用于VPN

3. 使用
    1. 启动关闭指定网卡
        
        ```bash
        ifconfig eth0 up
        ifconfig eth0 down
        ```
    2. 为网卡配置和删除IPv6地址

        ```bash
        ifconfig eth0 add 33ffe:3240:800:1005::2/64
        ifconfig eth0 del 33ffe:3240:800:1005::2/64
        ```
    3. 修改MAC地址`ifconfig  eth0  hw ether  00:AA:BB:CC:DD:EE`
    4. 修改IP地址:比如给eth0网卡配置IP地址`192.168.120.56`，`ifconfig eth0 192.168.120.56`




### 1.N 其他
查看系数中安装的所有字体：`fc-list`

## 2 文件和目录操作相关
关于linux的文件系统树:linux以分层目录来组织所有文件，第一级目录称为根目录(唯一)，对于连接到计算机的磁盘或存储设备，则是挂载到目录树的某个节点上，区别于win中的每个存储设备都有独自的文件系统

### 2.1 查看
查看目录的大小`du`：`du`用来计算文件/目录大小的命令
1. 参数
    1. `-s`:显示文件或整个目录的大小，
    2. `-h`:是用可读格式
    
```bash
# 比如查看home目录的大小
du -sh ~
48G	/Users/xxx
```

### 2.2 文件系统跳转
1. 查看当前目录：`pwd`(`print working directory`),注意该命令会在结尾加上一个换行符
2. 更改工作目录,其中`.`是当前目录,`..`是父级目录,而且几乎所有情况下都可以省略`./`,因为它是隐含的：
    1. 后面可接相对路径和绝对路径,直接`cd`则是跳转到home目录
    2. 跳到上一次的目录:`cd -`
    3. 跳到某个用户的目录:`cd ~[uerName]`
    4. 注意,跳转时路径中间必须都是目录,不能包含文件,比如`cd ./xxx.txt`就不行
### 2.3 文件创建
#### 创建文件 touch

#### 创建目录 mkdir
可跟多个参数,如`mkdir dir1 dir2 dir3`

参数说明
- `-p`(`--parents`):若所要建立目录的上层目录目前尚未建立，则会一并建立上层目录。比如`mkdir -p a/b`

2. 创建文件:
### 2.4 文件移动、复制、重命名、删除、链接
#### 复制文件和目录 cp
1. 复制单个文件或目录,如`cp item1 item2`
    1. 复制目录时,需要加上`-r`,而且对于`cp dir1 dir2`,如果dir2存在,则是把dir1复制到dir2下,如果不存在,则是把dir1复制为dir2
        
        ```bash
        # 复制dir1下的所有文件到dir2
        cp -r dir1/. dir2
        
        ├── dir2
        │   ├── file1
        │   ├── file2
        # 如果dir2不存在,则是把dir1复制为dir2，此时和上面的例子等价
        cp -r dir1 dir2
        
        ├── dir2
        │   ├── file1
        │   ├── file2
        # 如果dir2存在,则是把dir1复制到dir2下
        cp -r dir1 dir2
        
        ├── dir2
        │   ├──dir1
        │   │   ├── file1
        │   │   ├── file2
        ```
2. 复制多个文件或目录到一个目录:`cp item... dir`,此时作为"一"的dir必须存在
3. 参数`-a`(` --archive`):同时会复制他们的属性,包括所有权和权限
4. 参数`-i`(`--interactive`):重写已存在的文件前会提示用户确认,因为cp命令默认是重写不提示
5. 参数`-r`(`--recursive`):递归地复制目录及目录中的内容。当复制目录时， 需要这个选项（或者-a 选项）.注意linux中很多命令的`-r`都代表递归
6. 参数`-u`(`--update`):当把文件从一个目录复制到另一个目录时，仅复制 目标目录中不存在的文件，或者是文件内容新于目标目录中已经存在的文件。
7. 参数`-v`(`--verbose`):显示详细的命令操作信息,即会告诉用户干了什么.注意很多linux命令的`-v`都是这个意思

想拷贝一个大目录但又不想拷贝其中的一个子目录，怎么办呢？推荐使用`rsync`(待补充)

#### 跨服务器的安全复制 scp(secure copy)
用法和`cp`很像,而且`scp`可以跨服务器,传输是安全的（加密的）,还非常不占资源,当你服务器硬盘变为只读 read only system时，用scp可以帮你把文件移出来。支持本地和远程、远程和远程之间的拷贝

基本用法:`scp item user_name@remote_ip:dir`

参数：
1. `-q`：不显示进度条
2. `-r`:递归复制整个目录

```bash
# 复制同一个目录下的多个文件
cp dir/{file1,file2,file3} dir2

# 复制不同目录下的多个文件
cp {file1,file2,file3} dir2
cp $HOME/{file1,/dir/file2} dir2 # 包含子目录
cp $HOME/{file1,/dir/{file2,file3}} dir2 # 更进一步的嵌套

# 复制同一个目录下具有共同前缀的文件
cp dir/file{1..4} dir2
```

#### 移动或重命名文件 mv
使用方法和`cp`很像,但是不用加`-r`,操作成功后原来的文件或文件夹不再存在
1. 移动或重命名单个文件或目录:`mv item1 item2`
    1. 对于`mv file1 file2`,如果file2存在,则被重写为file1(**也就是旧的file2会被新的file2覆盖**);如果file2不存在,则创建file2.每种情况下file1都不会存在

        ```bash
        # 重命名dir目录下的file1为file2
        mv dir/file1 dir/file2
        # 移动dir目录下的file1到dir2
        mv dir/file1 dir2
        ```
    2. 对于`mv dir1 dir2`,如果dir2存在,移动dir1及它的内容到dir2中;如果dir2不存在,创建dir2,将dir1的内容移到dir2.
2. 移动多个文件或目录到目录:`mv item... dir`,dir必须存在
    1. 移动目录下的所有文件和文件夹：`mv dir/* dir2`
2. 参数
    1. `-i`(`--interactive`):在重写一个已经存在的文件之前，提示用户确认信息。 如果不指定这个选项，mv 命令会默认重写文件内容。
    2. `-u`(`--update`):用法同cp
    
注意：
1. 不能移动同时重命名（不使用管道等的情况下）

#### 删除文件或目录`rm`(`remove`)
该命令必须慎重使用,类unix(比如linux)的操作系统中没有复原命令,它假定操作者是聪明的,知道自己在干什么.最佳实践是:每次删除前使用ls列出要删除的文件,确认后再将ls修改成rm
1. 基本用法`rm item...`
2. 参数`-i`(`--interactive`):在删除已存在的文件前，提示用户确认信息。 如果不指定这个选项，`rm`会默默地删除文件
3. 参数`-r`(`--recursive`):递归地删除文件，这意味着，如果要删除一个目录，而此目录 又包含子目录，那么子目录也会被删除。要删除一个目录，必须指定这个选项。
4. 参数`-f`(`--force`):忽视不存在的文件，不显示提示信息。这选项覆盖了`--interactive`选项。

#### 创建链接`ln`
1. 硬链接`ln file link`,和文件本身没什么区别,硬链接有两个局限性:
    - 不能关联目录
    - 不能关联不在同一个分区的磁盘文件
2. 符号链接`ln -s file link`,为了解决硬链接的局限而生,符号链接包含关联的文件或目录的文本指针,类似于windows的快捷方式,而且出现时间比win快捷方式早很多.如果你往一个符号链接里面写入东西，那么相关联的文件也被写入。然而， 当你删除一个符号链接时，只有这个链接被删除，而不是文件自身。如果先于符号链接 删除文件，这个链接仍然存在，但是不指向任何东西。在这种情况下，这个链接被称为 坏链接。在许多实现中，ls 命令会以不同的颜色展示坏链接，比如说红色
    1. 比如指向`../fun`的某个符号链接`fun-sym`,符号链接`fun-sym`文件的长度是6，这是字符串”../fun”所包含的字符数， 而不是符号链接所指向的文件长度
    2. 大多数文件操作是针对链接的对象,而不是链接本身,但是`rm`是个特例,删除链接时就是删除链接本身
    3. gonme中,拖动文件同时按下`ctrl+shift`会创建一个链接(什么链接?)而不是移动或复制文件

#### 挂载
Linux中的根目录以外的文件要想被访问，需要将其“关联”到根目录下的某个目录来实现，这种关联操作就是“挂载”，这个目录就是“挂载点”，解除关联关系称之为“卸载”。

“挂载点”的目录需要以下几个要求：
1. 目录事先存在，可以用mkdir命令新建目录；
2. 挂载点目录不可被其他进程使用到；
3. 挂载点下原有文件将被隐藏。

`mount`用于挂载Linux系统外的文件

```bash
# 只输入 mount命令可以查看所有系统已经挂载的文件。
mount
# 如果想挂载一个新的文件，比如将 /dev/hda1 挂在 /mnt 之下，可以用 
mount /dev/hda1 /mnt
```

### 2.5 查找
查找命令多种多样，但用途不一样。大致有:
- 查找文件：`find`、`locate`，
- 在$PATH环境变量里的路径(可通过`echo $PATH`查看，基本都是`.../bin`和`.../sbin`)中查找可执行文件
    1. `which`
        ```bash
        which go 
        /usr/local/bin/go
        
        which java
        /usr/bin/java
        
        which ls
        /usr/bin/java
        ```
- 在任意目录中查找可执行文件(待整理)
    1. `whereis`
        ```bash
        whereis java
        /usr/bin/java
        ```
- 查找文本
    1. `grep`
    
#### find 在文件系统中搜索文件
递归查询目录及其子目录下的目标

语法是`find path -option xxx command {} \`，如果未指定path则默认以当前路径为path，`command {} \;`表示对查询后的所有结果进行command操作，花括号代表前面find查找出来的目标，分号似乎加不加都行，比如`rm {} \`、`ls -l {} \`，注意这个command操作是对结果一行一行的进行，不是所有行一起进行，比如打包的时候会有区别。

常用参数：

2. `-name xxx`或`-name "xxx"`:查找文件名称符合xxx的目标，xxx中`*`通配任意个字符，`?`通配单个字符
    ```bash
    # 名称是.dbeaver的目标
    find . -name .dbeaver
    find . -name ".dbeaver"
    # 文件类型是".c"的目标
    find / -name "*.c"
    # 将当前目录下所有最近20天内更新过的目标的完整路径列出
    find . -ctime -20 ls -l {} \
    ```
3. `-iname`：忽略大小写，其他和`-name`一样。
4. `-type xxx`:按文件类型查找，类型大概有
    - `f`:一般文件
    - `d`:目录
    - `l`:符号链接
    - `s`:socket
    - ...
5. 时间相关
    1. `-atime`:访问时间:
        ```bash
        # 访问时间距现在5天及以上的文件
        find /usr -atime +4
        # 访问时间距现在小于等于4天的文件
        find /usr -atime -4
        ```
    1. `-mtime`:修改时间
    1. `-ctime`:状态改动时间
6. `-size`:文件大小，比如`find / -size +10M`表示大于10M的文件
7. 条件参数
    1. `-a`、`-and`:而且，不写的话默认会带上。
    1. `-o`:或者
    1. `-not`:相反。比如查找/var/log目录下内容更改时间为30天前并且不属于root群组的文件，`find /var/log -type f -a  -mtime  +30 -not -group root`

command位置常用参数：
1. `-print`:即使不写也会默认带上的参数，写在command的位置，作用是把找到的目标的路径打印到std output
2. `-exec`：任意形式的命令可以在它后面执行，比如
    ```bash
    # 查找/var/log目录下内容更改时间为40天前并且大于100K的文件，并列出他们的路径
    find /var/log -mtime +40 -a -size +100k -exec ls -lh {} \
    # 所有文件名为“passwd”的文件,然后执行 grep 命令查看这些文件中是否存在一个 root 用户
    find /etc  -name "passwd"  -exec  grep  "root" {} \;
    # 查找文件并移动到指定目录pathA
    find  .  -name  "*.log"  -exec  mv {} pathA \;　　　
    ```
3. `-ok`:和-exec的作用相同，只不过以一种更为安全的模式来执行该参数所给出的shell命令，在执行每一个命令之前，都会给出提示，让用户来确定是否执行。比如可以`... -ok rm -rf {} \`
    
#### locate(与unix的locate有些不同，待补充)
功能和find类似，不过`locate`是在自己维护的数据库中查文件，而`find`是直接遍历目录中所有的文件进行匹配，所以它比find高效很多。默认一天更新一次文件的索引，所以它的缺点是新增的文件可能因为没加到索引中导致查不出来。

首次使用，比如`locate xxx`会提示：

常用操作：
1. 主动更新:

常用参数:

#### which
有时系统中不止安装了程序的一个版本,虽然在桌面系统中不常见,但在大型系统中却很平常.该命令对只对可执行程序有效，不包括内建命令和命令别名,有点奇特,比如对`cd`就无效

#### whereis（感觉不怎么好用，待补充）
#### grep 在文件中搜索指定的字符串
grep（global regular expression print），基本语法`grep [选项] pattern [文件...]`,如果省略文件参数，则默认从标准输入中读取数据?


常用参数:
1. `-i`:忽略字母大小写
1. `-n`:显示匹配行及行号
3. `-r`:表示搜索某个目录下面的所有文件
4. `-v`:过滤包含某个词的行（即只打印不匹配的行），即grep的逆操作

    ```bash
    # 显示所有包含 vim，但不包含 grep 的行
    ps | grep vim | grep -v grep
    ```
5. `-w`:只匹配整个单词

```bash
# 例子1：在example.txt文件中查找foo字符串
grep foo example.txt

# 例子2：在两个文件中查找以字母a结尾的单词，并打印匹配文件名、行号及行
grep -n 'a$' example1.txt example2.txt

# 例子3：从标准输入中查找字符串
echo "hello world" | grep world # 这里使用echo命令来向标准输入中输出一些文本

# 和ls结合使用的时候可以起到按文件名等方式查找的作用

```
### 2.6 压缩相关
#### tar
首先明确linux中打包和压缩是不同的，打包是把多个文件变成一个总的文件；因为linux中很多压缩程序只能对一个文件压缩，所以一般是先打包再压缩,参考:["为什么linux的包都是.tar.gz？要解压两次"](https://www.zhihu.com/question/37019479?sort=created)
>关于tar这个命令名字的来历：Initially, tar archives were used to store files conveniently on magnetic tape. The name "Tar" comes from this use（最初，tar档案被用来方便地在磁带上存储文件。 “焦油”这个名字来自这个用途。）

tar默认会覆盖

使用：不加`-z`或`-a`的话就只是打包,而没有压缩.
1. `-z`或`--gzip`或`--ungzip`：通过gzip指令处理.gz格式的文件；`-j`:针对bzip2即.bz2格式的文件。
2. `-v`(`--verbose`)：显示操作过程
3. `-f [压缩或备份的文件]`或`--file=[压缩或备份的文件]`：指定备份文件
4. `-c`或`--create`：建立新的备份文件(压缩必带参数)
5. `-x`或`--extract`或`--get`：从备份文件中还原文件(解压缩必带参数)
6. `-t`或`--list`：列出备份文件的内容
6. `-C [目录]`：在指定目录解压缩。
7. `-a`(`--auto-compress`):使用归档后缀名来决定压缩程序,也就是用了该参数就不用`-z`参数了.
8. `-k`(`--keep-old-files`): 解开备份文件时，不覆盖已有的文件。

```bash
# 最常用的例子如下
# 压缩：
tar -zcv -f filename.tar.gz 要被压缩的文件或目录名称 
# 查询：
tar -ztv -f filename.tar.gz 
# 解压缩：
tar -zxv -f filename.tar.gz -C 欲解压缩的目录
```
3. 打包
#### zip
解压`unzip`
1. 参数
    1. `-d`：指定解压的目录

压缩`zip`
1. 使用:
    1. 查看压缩文件里的内容`-l`，解压后就是看到的内容,比如看到的是`flutter/...`，解压后就是`flutter/...`

## 3 过滤器
管道线经常用来对数据完成复杂的操作。有可能会把几个命令放在一起组成一个管道线。 通常，以这种方式使用的命令被称为过滤器。
1. 排序`sort`
    `sort`对文件排序,也可获取标准输入,然后标准输出.将文件/文本的每一行作为一个单位,从首字符向后，依次按ASCII码值进行比较,最后升序输出.
2. 报道或忽略重复行`uniq`
    用于报告或忽略文件中的重复行，常与sort命令结合使用,例如`ls /bin /usr/bin | sort | uniq | less`
3. 打印行数、字数和字节数`wc`
    display the number of lines, words, and bytes contained in files.接受标准输
    1. 直接使用`wc`,接受标准输入
    2. 一般用法`wc [file]`
    3. 也可指定显示,比如`wc -l [file]`则只显示行数
4. 打印匹配行`grep`(`Globally search a Regular Expression and Print`)
    很强大的文本搜索工具,用来找到文件中的匹配文本,类似于win中的`FINDSTR`,基本用法`grep pattern [file...]`,支持正则表达式.比如想找目录中文件名包含`xiaoke`的文件,可以这样`ls | grep xiaoke`
    1. 参数`-i`:忽略大小写
    2. 参数`-v`:只显示不匹配的行。排除多个可以使用`grep -v 'args1\|args2...'`
5. 打印文件的开头/结尾部分`head`和`tail`
    1. `head`默认打印开头10行,`tail`则是结尾10行,`tail`有个选项`-f`允许实时地浏览文件,观察日志文件时很有用.
        1. 参数`-n`:指定打印的行数
        
    ```bash
    # 实时浏览最后10行
    tail -f example.txt 
    ```
6. 读取数据,同时输出到屏幕和文件`tee`
    比如`ls /usr/bin | tee xxx.txt`,会同时输出到屏幕和文件
## 4 (字符)展开
每当你输入一个命令并按下enter键，bash会在执行命令前对输入的字符处理,这背后的的过程叫做（字符）展开。通过展开，你输入的字符，在shell对它起作用之前，会展开成为别的字符,用`echo`就可以看到(字符)展开
1. 路径名展开: 文件名以圆点字符开头的文件是隐藏文件,路径名展开尊重隐藏文件,比如`echo *`,会显示当前目录所有文件和目录但不包括隐藏文件
2. 波浪线展开: 展开成指定用户的家目录名,默认是当前用户家目录,如`echo ~`
3. 算术表达式展开: 允许把shell提示当计算器来使用,因为用的bash内置运算的支持,所以只支持整数,不支持浮点运算,基本用法是`$((expression))`,其中表达式有无空格无所谓,如`echo $((2+3))`,输出5.感觉较鸡肋
    1. 算数操作符`/`(即除),因为展开只是支持整数除法，所以结果是整数,从这儿可以看出不如`bc`
4. 花括号展开
    从一个包含花括号的模式中创建多个文本字符串,常见的应用场景是:创建一系列的文件或目录列表.比如摄影师给大量的相片命名.花括号的展开模式可能包含一个开头部分叫做报头,一个结尾部分叫做附言,而花括号表达式本身可能包含一个由逗号分开的字符串列表，或者一系列的整数，或者单个的字符串,不能嵌入空白字符.
    1. 简单例子:
    ```bash
    #注意多个连续的这种简短写法是中间两个点`..`
    [me@linuxbox ~]$ echo Number_{1..5}
    Number_1  Number_2  Number_3  Number_4  Number_5 
    [me@linuxbox ~]$ echo {Z..A}
    Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
    ```
    2. 可以嵌套:
    ```bash
    [me@linuxbox ~]$ echo a{A{1,2},B{3,4}}b
    aA1b aA2b aB3b aB4b
    ```
5. 参数展开
    该特性在shell脚本中更有用,常用于:系统存储小块数据，并给每块数据命名.
    1. 查看变量名,比如`echo $USER`,如果输错变量名,展开仍会进行,不过是显示空字符串
    2. 查看有效变量列表`printenv | less`
6. 命令替换
    命令替换允许我们把一个命令的输出作为一个展开模式来使用,有两种写法:新版写法是`$(program)`,旧版是`program`(用倒引号来代替美元符号和括号)
    1. 用法一如下:

        ```bash
        [me@linuxbox ~]$ echo $(ls)
        Desktop Documents ls-output.txt Music Pictures Public Templates Videos
        [me@linuxbox ~]$ file $(ls /usr/bin/* | grep zip)
        ```
    2. 用法二如下:
    
        ```
        #``中的内容会被当做命令执行,然后结果作为cd的参数
        #所以最后的结果是仍停留在当前目录
        cd `pwd`
        ```
## 5 引用
用于控制展开.有几种类型:双引号
1. 双引号
    除了`$`、`\`和反引号(Backslash),其他字符在shell的双引号中都变成了普通字符.使用双引号，我们可以处理包含空格的文件名。(文件名含空格的受害者,笑:))
    在双引号中，参数展开、算术表达式展开和命令替换仍然有效：
    ```bash
    [me@linuxbox ~]$ echo "$USER $((2+2)) $(cal)"
    me 4    February 2008
    Su Mo Tu We Th Fr Sa
    ```
    在默认情况下，单词分割机制会在单词中寻找空格，制表符，和换行符，并把它们看作 单词之间的界定符。这意味着无引用的空格，制表符和换行符都不是文本的一部分， 它们只作为分隔符使用.在mac上的例子如下
    ```bash
    xushikedeMacBook-Pro-2:zztemp xushike$ echo $(cal)
    十二月 2017 日 一 二 三 四 五 六 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31
    xushikedeMacBook-Pro-2:zztemp xushike$ echo "$(cal)"
        十二月 2017
    日 一 二 三 四 五 六
                    1  2
    3  4  5  6  7  8  9
    10 11 12 13 14 15 16
    17 18 19 20 21 22 23
    24 25 26 27 28 29 30
    31
    ```
2. 单引号
    如果要禁用所有展开,则用单引号,如
    ```bash
    [me@linuxbox ~]$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
    text ~/*.txt  {a,b} $(echo foo) $((2+2)) $USER
    ```
3. 转义字符`\`
    有两种用法:阻止展开和反斜杠转义字符序列(Backslash Escape Sequences)
    1. 阻止展开:
        有时只想引用某个字符,在双引号中可以使用转义字符`\`来消除字符的特殊含义,而单引号则不需要
    2. 反斜杠转义字符序列
        用来表示ASCII中的控制字符,背后的思想来源于C编程语言，许多其它语言也采用了这种表示方法，包括shell。
## 6 用户和权限
1. 查看关于自己身份的信息:`id`,用户账户定义在`/etc/passwd`,用户组定义在`/etc/group`,这几个文件随着`/etc/shadow`而改变
2. 权限属性

    文件类型后的九个字符叫做文件模式，代表着文件所有者、文件组所有者和其他人的读、写和执行权限。如图,
    ![](../picture/linux/0-1-permission.png)

    |属性|	文件|	目录|
    |-|:-|:-|
    |`r`|	允许打开并读取文件内容。	|允许列出目录中的内容，前提是目录必须设置了可执行属性（x）。|
    |`w`|	允许写入文件内容或截断文件。但是不允许对文件进行重命名或删除，重命名或删除是由目录的属性决定的。 |允许在目录下新建、删除或重命名文件，前提是目录必须设置了可执行属性(x)|
    |`x`|	允许将文件作为程序来执行，使用脚本语言编写的程序必须设置为可读才能被执行。	|允许进入目录，例如：cd directory 。|
    1. 特殊权限(待理解)

        从技术层面上来讲，用四位数字来表示权限更确切,因为除了读取、写入和执行权限之外，还有其它较少用到的权限设置。
        1. `setuid`位（八进制4000）

            应用到一个可执行文件时，它把有效用户ID从真正的用户（实际运行程序的用户）设置成程序所有者的ID.通常用于超级用户拥有的程序。当一个普通用户运行一个由根用户(root) 所有并且设置了`setuid`位的程序，这个程序运行时具有超级用户的特权，这样程序就可以访问普通用户禁止访问的文件和目录。很明显，这会引起安全方面的问题，所以所有可以设置`setuid`位的程序个数，必须控制在绝对小的范围内。
            一般用法`chmod u+s program`,权限修改后类似`-rwsr-xr-x`
        2. `setgid`位（八进制2000）

            类似于`setuid`位，把有效用户组ID从真正的用户组ID更改为文件所有者的组 ID。当一个普通用户组中的成员，需要访问共享目录中的所有文件，而不管文件所有者的主用户组时，那么设置 setgid 位很有用处。
            一般用法`chmod g+s dir`,权限修改后类似`drwxrwsr-xx`
        3. `sticky`位（八进制1000）

            该位继承于Unix，在Unix中它可能把一个可执行文件标志为“不可交换的”。在 Linux 中，会忽略文件的 sticky 位，但是如果一个目录设置了 sticky 位， 那么它能阻止用户删除或重命名文件，除非用户是这个目录的所有者，或者是文件所有者，或是 超级用户。这个经常用来控制访问共享目录，比方说/tmp。
            一般用法`chmod +t dir`,权限修改后类似`drwxrwxrwt`

3. 更改文件模式:`chmod`(`change the mode (permissions)`)
    只有文件的所有者或者超级用户才 能更改文件或目录的模式。chmod 命令支持两种不同的方法来改变文件模式：八进制数字表示法或 符号表示法。
    1. 八进制法
        因为每个八进制数字代表了 3个二进制数字，这种对应关系，正好映射到用来存储文件模式所使用的方案上。下表展示了要表达的意思：

        |Octal|	Binary|	File Mode|
        |-|-|-|
        |`0`|	000|	---|
        |`1`|	001|	--x|
        |`2`|	010|	-w-|
        |`3`|	011|	-wx|
        |`4`|	100|	r--|
        |`5`|	101|	r-x|
        |`6`|	110|	rw-|
        |`7`|	111|	rwx|
        一般用法如`chmod 600 foo.txt`,常用的是7、6、5、4、0

    2. 符号表示法
        符号表示法分为三部分：更改会影响谁， 要执行哪个操作，要设置哪种权限。通过字符 “u”、“g”、“o”和 “a” 的组合来指定要影响的对象，如下

        |字符|对象|
        |-|-|
        |`u`|	"user"的简写，意思是文件或目录的所有者。|
        |`g`|	用户组。|
        |`o`|	"others"的简写，意思是其他所有的人。|
        |`a`|	"all"的简写，是"u", "g"和“o”三者的联合。|
        如果没有指定字符，则假定使用”all”。执行的操作可能是一个“＋”字符，表示加上一个权限， 一个“－”，表示删掉一个权限，或者是一个“＝”，表示只有指定的权限可用，其它所有的权限被删除。

        符号表示法实例:

        |符号|意义|
        |-|-|
        |`u+x`|	为文件所有者添加可执行权限。|
        |`u-x`|	删除文件所有者的可执行权限。|
        |`+x`|	为文件所有者，用户组，和其他所有人添加可执行权限。等价于`a+x`。|
        |`o-rw`|	除了文件所有者和用户组，删除其他人的读权限和写权限。|
        |`go=rw`|	给群组的主人和任意文件拥有者的人读写权限。如果群组的主人或全局之前已经有了执行的权限，他们将被移除。|
        |`u+x,go=rw`|	给文件拥有者执行权限并给组和其他人读和执行的权限。多种设定可以用逗号分开。|

4. 设置默认权限:`umask`

    大多数情况下不需要设置,在某些高安全权限下需要控制掩码值.
    1. 不带参数使用是查看当前的掩码值,掩码值(默认八进制)的后三位对应权限rwx的八进制,但是意思相反:掩码这儿转换成二进制后,如果某位为1,则表示关闭该该位对应的权限,如
    ```bash
    [me@linuxbox ~]$ umask
    0002
    ```
    2. 该命令设置的掩码值只能在当前shell会话中生效
4. 切换用户

    有三种方式,发行版一般都支持后两种方式,但可能会偏袒其中之一.
    1. Log out and log back in as the alternate user.(注销系统并以其他用户身份重新登录系统)

        easy但是并不方便
    2. Use the su command.(使用`su`命令)

        以其他用户身份和组 ID 运行一个 shell
        1. 一般用法`su [user_name]`
        2. 带参数`-l`的用法`su -l [user_name]`,启动一个需要登录的shell(即login shell)。这意味着会加载此用户的 shell 环境， 并且工作目录会更改到这个用户的家目录。
            1. 如果不指定用户`su -l`,则是默认超级用户
            2. 而且该参数可以缩写为`-`
        3. 带参数`-c`的用法`su -c 'command'`,执行单个命令，而不是启动一个新的可交互的shel.注意command的两边的反引号很重要,这样命令就不会在我们的shell中展开而是在新shell中展开.
            ```bash
            [me@linuxbox ~]$ su -c 'ls -l /root/*'
            Password:
            -rw------- 1 root root    754 2007-08-11 03:19 /root/anaconda-ks.cfg
            ```
    3. Use the sudo command.(使用`sudo -i`命令)，类似`su`,但是几个很重要且不同的功能:
        1. 管理员可以配置sudo命令,从而允许一个普通用户以不同的身份（通常是超级用户），通过一种非常可控的方式来执行命令。尤其是，只有一个用户可以执行一个或多个特殊命令时，（更体现了 sudo 命令的方便性）.
        2. 另一个重要差异是sudo使用用户自己的密码来认证.
        3. sudo 不会重新启动一个 shell，也不会加载另一个 用户的 shell 运行环境。这意味者命令不必用单引号引起来。
        4. 通过配置,上面的这些行为也可以被推翻.
        5. 一般`sudo`命令会相信你几分钟,意味着几分钟内不用再输入密码.
        5. 参数`-l`,显示`sudo`命令可以授予哪些权,如
            
            ```bash
            User xushike may run the following commands on xushikedeMacBook-Pro-2:
                (ALL) ALL
            ```
        7. 可以运行管道命令
            ```bash
            # sudo管道命令的写法
            sudo sh -c "echo hello"
            ```
5. 其他

    1. `chown`更改文件所有者和用户组
    2. `chgrp`更改用户组所有权
6. 关于权限的练习(待补充)

    [http://billie66.github.io/TLCL/book/chap10.html](http://billie66.github.io/TLCL/book/chap10.html)
7. 修改用户密码:`passwd`

    `passwd`命令将会试着强迫你使用“强”密码。这意味着它会拒绝接受太短的密码、与先前相似的密码、 字典中的单词作为密码或者是太容易猜到的密码
8. 维护用户和用户组
    `adduser`,`useradd`,`groupadd`

## 7 进程和服务
### 7.1 进程
进程如何工作：当系统启动的时候，内核先把一些它自己的活动初始化为进程，然后运行一个叫做 init 的程序。init， 依次地，再运行一系列的称为 init 脚本的 shell 脚本（位于/etc），它们可以启动所有的系统服务。 其中许多系统服务以守护（daemon）程序的形式实现，守护程序仅在后台运行，没有任何用户界面。 这样，即使我们没有登录系统，至少系统也在忙于执行一些例行事务。
内核维护每个进程的信息，以此来保持事情有序。例如，系统分配给每个进程一个数字，这个数字叫做 进程 ID 或 PID。PID 号按升序分配，init 进程的 PID 总是1。内核也对分配给每个进程的内存和就绪状态进行跟踪以便继续执行这个进程。

查看进程快照`ps`：
1. 该命令古老且重要,各种linux都默认安装了,不过参数可能不一样.`ps`命令支持三种使用的语法格式:
    - UNIX 风格，选项可以组合在一起，并且选项前必须有“-”连字符
    - BSD 风格，选项可以组合在一起，但是选项前不能有“-”连字符
    - GNU 风格的长选项，选项前有两个“-”连字符
1. 直接使用`ps`,只列出与当前终端会话相关的进程,其中TTY是“Teletype” 的简写，是指进程的控制终端.TIME字段表示 cumulative CPU time(进程占用的总的CPU处理时间)

    ```bash
    [me@linuxbox ~]$ ps
    PID TTY           TIME CMD
    5198 pts/1    00:00:00 bash
    10129 pts/1   00:00:00 ps
    ```
2. 带参数`x`的用法`ps x`(注意不是`-x`),展示所有进程，不管它们由什么终端（如果有的话）控制。TTY栏的问号表示没有控制终端。该用法可以看到我们所拥有的每个进程的信息。

    1. STAT是“state” 的简写，它揭示了进程当前状态

        |状态|	含义|
        |-|:-|
        |`R`|	运行中。这意味着，进程正在运行或准备运行。|
        |`S`|	正在睡眠。进程没有运行，而是，正在等待一个事件， 比如说，一个按键或者网络分组。|
        |`D`|	不可中断睡眠。进程正在等待 I/O，比方说，一个磁盘驱动器的 I/O。|
        |`T`|	已停止. 已经指示进程停止运行。稍后介绍更多。|
        |`Z`|	一个死进程或“僵尸”进程。这是一个已经终止的子进程，但是它的父进程还没有清空它。 （父进程没有把子进程从进程表中删除）|
        |`<`|	一个高优先级进程。这可能会授予一个进程更多重要的资源，给它更多的 CPU 时间。 进程的这种属性叫做 niceness。具有高优先级的进程据说是不好的（less nice）， 因为它占用了比较多的 CPU 时间，这样就给其它进程留下很少时间。|
        |`N`|	低优先级进程。 一个低优先级进程（一个“好”进程）只有当其它高优先级进程被服务了之后，才会得到处理器时间。|
3. 常用组合参数`aux`的用法`ps aux`
    - 参数`a`代表all
    - 参数`x`会显示没有控制终端的进程
    - 参数`u`根据用户过滤
4. 根据进程名过滤`-C`
5. 查看格式化的信息列表`-f`
6. 根据PID查看线程的进程`-L [PID]`
7. 参数`-e`显示所有进程信息
8. 实时监控进程状态`ps`和`watch`结合使用。`top`虽然也可以,比`top`好的地方是可以自定义显示的字段.

```bash
# ps aux 可以显示所有使用者的进程，最常用的方法是ps aux，然后再利用一个管道符号导向到grep去查找特定的进程。比如查看nginx 进程可以用
ps aux | grep nginx
```

#### linux进程种类
init是Linux系统操作中不可缺少的程序之一。所谓的init进程，它是一个由内核启动的用户级进程。内核自行启动（已经被载入内存，开始运行，并已初始化所有的设备驱动程序和数据结构等）之后，就通过启动一个用户级程序init的方式，完成引导进程。所以,init始终是第一个进程（其进程编号始终为1）。 其它所有进程都是init进程的子孙。init进程是用kill杀不死的。
    
#### 程序的后台运行及恢复
后台运行的几种方式：
1. 命令后加`&`：程序会在后台运行
2. 快捷键`ctrl+z`：将前台运行的任务放在后台挂起，此时程序是suspended状态
3. `nohup`：区别于上面的命令，即使退出shell，程序还是能执行。

查看后台运行的进程：
1. `jobs`:显示当前shell环境下后台正在运行或被挂起的任务，如果每个shell窗口有一个session的话，只能看见各自窗口的任务（区别于`top`等命令是查看整个系统环境下的）。`[num]`里的num是编号，不是pid，`+`加号表示当前任务，`-`减号表示当前任务之后下一个任务。

暂停后台的进程：
1. `kill -stop`(具体见kil部分)

继续运行进程：
1. `fg %num`：将后台的程序num放在前台继续运行。num是jobs看到的进程编号，不是pid
2. `bg %num`：将程序num放在后台继续运行。num是jobs看到的进程编号，不是pid
3. `kill -cont`：继续运行进程。(具体见kil部分)

进程的终止：常用`kill [程序]`,`[程序]`可以是PID、PGID或者工作编号，比如`kill %num`和`kill pid`

#### kill和linux信号
kill是什么:kill将指定的信息(信号)发送给程序，用于暂停、继续或终止执行中的程序。其中只有第9种信号`-9`(SIGKILL)可以无条件终止进程，其他信号进程都有权利忽略。

常见的kill操作有:
1. 终止程序
    1. 直接使用`kill [程序]`：等同于`kill -15 [程序]`或`kill -SIGTERM [程序]`，发送的信号是SIGTERM(15)，这个信号可以被进程捕获，使得进程在退出之前可以清理并释放资源，大部分程序接收到SIGTERM信号后，会先释放自己的资源，然后再停止，但是也有程序可能接收信号后，做一些其他的事情（如果程序正在等待IO，可能就不会立马做出响应，比如wkhtmltopdf转pdf中），也就是说，SIGTERM多半是会被阻塞的。所以当程序接收到该signal信号后，可能发生以下事情：
        - 程序立刻停止
        - 程序释放相应资源后再停止
        - 程序可能仍然继续运行
    2. `kill -9 [程序]`:等同于`kill -KILL [程序]`，系统给对应程序发送的信号是SIGKILL，即exit。exit信号不会被系统阻塞，所以`kill -9`能强制杀掉进程，发送该信号时必须谨慎。
    3. `ctrl+c`：发送的是`kill -2 [程序]`，表示结束进程，但不是强制性的。
2. 暂停和继续
    1. `kill -stop [程序]`:暂停进程，等同于`kill -19`和`ctrl+z`
    2. `kill -cont [程序]`：继续运行进程，等同于`kill -18`、`fg`和`bg`，作用和`kill -stop`相反。
3. 查看所有支持的信号`kill -l`(见信号部分)
    
最佳实践：在使用`kill -9`前，应该先使用`kill -15`，给目标进程一个清理善后工作的机会。如果没有，可能会留下一些不完整的文件或状态，从而影响服务的再次启动。
#### 信号
信号是 Unix 、类 Unix 以及其他 POSIX 兼容的操作系统中进程间一种有限制的通讯方式。它是一种异步的通知机制，用来提醒进程一个事件（硬件异常、程序执行异常、外部发出信号）已经发生。当一个信号发送给一个进程，操作系统中断了进程正常的控制流程。此时，任何非原子操作都将被中断。如果进程定义了信号的处理函数，那么它将被执行，否则就执行默认的处理函数

 ```bash
# 在mac上运行kill -l会显示
HUP INT QUIT ILL TRAP ABRT EMT FPE KILL BUS SEGV SYS PIPE ALRM TERM URG STOP TSTP CONT CHLD TTIN TTOU IO XCPU XFSZ VTALRM PROF WINCH INFO USR1 USR2

# 在linux上运行kill -l会显示出64中信号，其中编号为1 ~ 31的信号为传统UNIX支持的信号，是不可靠信号(非实时的)，编号为32 ~ 63的信号是后来扩充的，称做可靠信号(实时信号)。不可靠信号和可靠信号的区别在于前者不支持排队，可能会造成信号丢失，而后者不会。
```

常用信号说明:
1. `SIGHUP`（hong up，挂断）:该信号在用户终端连接(正常或非正常)结束时发出, 通常是在终端的控制进程结束时, 通知同一session内的各个作业, 这时它们与控制终端不再关联。登录Linux时，系统会分配给登录用户一个终端(Session)。在这个终端运行的所有程序，包括前台进程组和 后台进程组，一般都属于这个 Session。当用户退出Linux登录时，前台进程组和后台有对终端输出的进程将会收到SIGHUP信号。这个信号的默认操作为终止进程，因此前台进 程组和后台有终端输出的进程就会中止。不过可以捕获这个信号，比如wget能捕获SIGHUP信号，并忽略它，这样就算退出了Linux登录，wget也 能继续下载。此外，对于与终端脱离关系的守护进程，这个信号用于通知它重新读取配置文件。
2. `SIGINT`(interrupt，终止）:该信号在用户键入INTR字符(通常是Ctrl+C)时发出，用于通知**前台进程组**终止进程。
3. `SIGKILL`：用来立即结束程序的运行. 本信号不能被阻塞、处理和忽略。
4. `SIGPIPE`：管道破裂。这个信号通常在进程间通信产生，比如采用FIFO(管道)通信的两个进程，读管道没打开或者意外终止就往管道写，写进程会收到SIGPIPE信号。此外用Socket通信的两个进程，写进程在写Socket的时候，读进程已经终止。
5. `SIGTERM`(terminate):该信号与SIGKILL不同的是该信号可以被阻塞和处理。通常用来要求程序自己正常退出，shell命令kill缺省产生这个信号。如果进程终止不了，我们才会尝试SIGKILL。
6. `SIGCHLD`：子进程（child）结束时, 父进程会收到这个信号。如果父进程没有处理这个信号，也没有等待(wait)子进程，子进程虽然终止，但是还会在内核进程表中占有表项，这 时的子进程称为僵尸进程。这种情 况我们应该避免(父进程或者忽略SIGCHILD信号，或者捕捉它，或者wait它派生的子进程，或者父进程先终止，这时子进程的终止自动由init进程 来接管)。
7. `SIGCONT`:让一个停止(stopped)的进程继续执行. 本信号不能被阻塞. 可以用一个handler来让程序在由stopped状态变为继续执行时完成特定的工作. 例如, 重新显示提示符
8. `SIGSTOP`:暂停(stopped)进程的执行. 注意它和terminate以及interrupt的区别:该进程还未结束, 只是暂停执行. 本信号不能被阻塞, 处理或忽略.
9. `SIGTSTP`:停止进程的运行, 但该信号可以被处理和忽略. 用户键入SUSP字符时(通常是Ctrl+Z)发出这个信号

### 7.2 服务
如何在系统中管理服务。有两种方式:使用`service`命令，使用`systemctl`(`systemd`)命令

#### service
常见操作:
1. 查看服务状态：`service [service_name] status`
2. 启动/停止/重启服务:`service [service_name] [start|stop|restart]`
3. 重新加载服务配置文件（不重启服务）: `service [servicename] [reload]`

#### systemctl(systemd)
比较新的系统都已经采用了`systemd`，`systemctl`是`systemd`的一个工具，主要负责控制systemd系统和服务管理器。

常见操作:
1. 查看服务状态:`systemctl status [servicename]`
2. 启动/停止/重启服务:`systemctl [start|stop|restart] [servicename]`
3. 重新加载服务配置文件（不重启服务）:`systemctl [reload] [servicename]`

## 8 curl
参考：
1. https://example.net/cookbooks/curl

它的名字就是客户端（client）的 URL 工具的意思。它可以文件下载（包括发送HTTP请求），断点续传，指定cookie，设置用户代理字符串，认证等。可惜不支持多线程下载。

使用和参数：
1. 网络请求
    1. 指定请求方式request method`-X`:有`POST`、`GET`、`DELETE`等，默认是`GET`
        
        ```bash
        # GET方法相对简单，只要把数据附在网址后面就行
        curl example.com/orders?data=xxx
        # 当然GET方法的查询参数也可以结构化，使用`-G`参数
        # 可以结合`-d`,`--data-urlencode`等一起使用
        curl -G -d 'q=kitties' -d 'count=20' https://example.com/search
        curl -G --data-urlencode 'comment=this cookbook is awesome' https://example.net
        # POST方法必须把数据和网址分开，curl就要用到--data参数。
        curl -X POST --data "data=xxx" example.com/form.cgi
        ```
    2. 请求参数
        1. `-d 'xxx'`(`--data`)：HTTP POST方式传送的body数据，使用`-d`参数以后，HTTP 请求会自动加上标头`Content-Type : application/x-www-form-urlencoded`,并且会自动将请求转为 POST 方法，因此可以省略`-X POST`，`-d`可以传送本地文件中的数据。
            
            ```bash
            curl -d 'login=xxx' -d 'password=xxx' -X POST  https://example.com/login
            # -d还可以读取本地文本文件的数据，向服务器发送，比如读取本地的data.txt文件
            # 数据很多的时候更推荐用这种方式
            -d @filename.json
            curl -d '@data.txt' https://example.com/login
            ```
        2. `--data-urlencode`等同于`-d`加上对发送的数据进行URL编码
            
            ```bash
            curl -X POST--data-urlencode "date=April 1" example.com/form.cgi
            ```
        3. `–data-raw`
        4. `–data-ascii`
        5. `–data-binary`
            
            ```bash
            curl -s -XPOST '<jenkinshost>/createItem?name=<jobname>' -u username:API_TOKEN --data-binary @<jobname>.xml -H "Content-Type:text/xml"
            ```
    3. 请求头
        1. `-H 'xxx:xxx'`(`--header`):自定义头信息传递给服务器
            
            ```bash
            -H "Accept-Encoding:gzip"
            ```
    4. 响应头
        1. `-i/–include`输出包括response头信息
        2. `-I`(`--head`)只显示response的头信息
            
            ```bash
            curl -I www.example.com
            
            HTTP/1.1 200 OK
            Accept-Ranges: bytes
            Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
            Connection: keep-alive
            Content-Length: 277
            Content-Type: text/html
            Date: Mon, 01 Mar 2021 03:32:09 GMT
            Etag: "575e1f72-115"
            Last-Modified: Mon, 13 Jun 2016 02:50:26 GMT
            Pragma: no-cache
            Server: bfe/1.0.8.18
            ```
    5. 提交表单
        1. `-F 'xxx'`(`--form`):模拟http表单提交数据，也可以上传文件，它会给 HTTP 请求加上标头`Content-Type: multipart/form-data`，该参数可以指定 MIME 类型和文件名
        
            ```bash
            # 上传文件
            curl --form upload=@localfilename --form press=OK [URL]
            # 上传文件，比如上传photo.png
            curl -F 'file=@photo.png' https://example.com/profile
            # 指定MIME类型和文件名
            curl -F 'file=@photo.png;type=image/png;filename=me.png' https://example.com/profile # 原始文件名为photo.png，但是服务器接收到的文件名为me.png
            ```
    6. HTTP认证
        1. `-u`(`--user`)
        1. `--basic`
            
            ```bash
            # Authorization: Basic认证
            curl --basic -u user:password http://www.example.com/posts/1
            # 也可以写到URL中
            curl https://user:password@example.com/login
            # empty password
            curl -u 'user:' https://example.com/login
            # 如果不想显示使用密码，Make Curl Prompt for the Password
            curl -u 'user' https://example.com/login
            ```
    7. 请求来源和重定向
        1. `-e`(`--referer`)有时你需要在http request头信息中，提供一个referer字段，表示你是从哪里跳转过来的。
        
            ```bash
            curl --referer http://www.example.com http://www.example.com
            ```
        2. `-L`(`--location`)参数会让 HTTP 请求跟随服务器的重定向。curl 默认不跟随重定向。当服务器报告被请求的页面已被移动到另一个位置时（通常返回 3XX 错误代码）， 允许 curl 使用新的地址重新访问。如果跳转链接指向了一个不同的主机，curl 将不向其发送用户名和密码
        3. `--location-trusted`:该参数和`-L`参数类似，也可让 curl 继续访问跳转链接，区别在于该参数允许向跳转链接发送明文用户名和密码。 
    8. User Agent:修改客户端的设备信息
        1. `-A`(`--user-agent`):`curl --user-agent "[User Agent]" [URL]`
            
            ```bash
            # 假装是谷歌机器人(Pretend to be a Google Bot)
            curl -A 'Googlebot/2.1 (+http://www.example.com/bot.html)' https://example.com
            # 请求头不发送用户代理字段
            curl -A '' https://example.com
            # 发送空的请求头字段
            curl -A '' -H 'User-Agent;' https://example.com
            # 也可以使用`-H`来指定用户代理
            curl -H 'User-Agent: php/1.0' https://example.com # 网站认为我是PHP
            ```
    9. cookie
        1. 发送cookie:`curl --cookie "name=xxx" www.example.com`
        3. 在请求里添加cookie`-b 'nameA=valueA'`，也可以将文件作为cookie`-b fileA`
            ```bash
            # 添加多个cookie
            curl -b 'session=abcdef' -b 'loggedin=true' https://example.com
            # 添加一个空的cookie
            curl -b 'session=' https://example.com
            # 文件作为cookie
            curl -b cookies.txt https://www.example.com
            ```
        2. 保存服务器返回的cookie到文件`-c fileA`
    10. 代理
        1. `-x`
            
            ```bash
            # socks5 proxy
            curl -x socks5://user:password@myproxy.com:8080 https://example.net
            # http proxy
            curl -x user:password@myproxy.com:8080 https://example.net
            # 指定代理主机和端口
            curl -x proxysever.test.com:3128 http://example.com
            ```
    11. SSL证书
        1. `-k`：不会检查服务器的SSL证书是否正确，如果服务器的SSL证书坏了，过时了，或者有一个web服务器配置错误，这个请求仍然会通过，但不会建立信任。
            
            ```bash
            curl -k https://example.com
            # 指定SSL版本
            curl -1 https://example.com # 版本1
            curl -2 https://example.com # 版本2
            curl -3 https://example.com # 版本3
            ```
        2. `--cert`
        3. `--key`
    12. 限制带宽：curl默认使用最大带宽，为了测试，有时需要限制带宽，模拟慢网速的环境
        1. `--limit-rate`限制请求和响应的带宽
            
            ```bash
            # 将请求和响应的速率限制为
            curl --limit-rate 200k https://example.com # 每秒200千字节
            curl --limit-rate 200m https://example.com # 每秒200mb
            curl --limit-rate 200g https://example.com # 每秒200gb
            ```
2. 响应处理
    1. `-o`获取文件内容：在版本7.55之前，似乎默认会将二进制输出到终端，可以使用`-o`或`--output`将文件下载到本地(等同于`wget`)，从7.55开始，默认不会将二进制输出到终端，而是提示warn信息`Warning: Binary output can mess up your terminal. Use "--output -" to tell ...`。如果坚持要输出到终端，可以使用`-o -`，也可以使用`-o - > xxx`重定向里面的内容到本地文件中
    2. `-O`使用URL中默认的文件名保存文件到本地
    3. `-C`使用断点续传功能，如`curl -C - -O http://example.com`
    4. `-w`(`--write-out`):打印信息到标准输出流，可以输出变量`%{variable}`，也可以从文件中读取内容`@filename`，也可以输出到标准错误流`%{stderr}`，具体支持的变量参考手册。通常用于http请求的诊断
        
        ```bash
        # 查看请求的网络耗时情况
        curl -o /dev/null -s -w "time_connect: %{time_connect}\ntime_starttransfer: %{time_starttransfer}\ntime_nslookup:%{time_namelookup}\ntime_total: %{time_total}\n" "https://example.com"
        # 输出如下：网络连接时间为0.279720秒（其中DNS解析为0.016326秒），总体请求1.507秒
        # time_connect: 0.279720 
        # time_starttransfer: 1.507216
        # time_nslookup:0.016326
        # time_total: 1.507452
        ```
3. `globbing`(URL globbing parser):curl支持URL范围匹配`{}`和`[]`，意味着可以批量处理目标。
    1. 参考：https://everything.curl.dev/cmdline/globbing

    ```bash
    # 批量上传
    ## Numerical ranges: [n-m:i]，左闭右闭，i为增量
    curl -T 'image[1-99].jpg' ftp://ftp.example.com/upload/
    curl -T 'image[001-099].jpg' ftp://ftp.example.com/upload/
    curl -T 'image[1-99:2].jpg' ftp://ftp.example.com/upload/ # 每次递增2
    
    ## Alphabetical ranges
    curl -O "http://example.com/section[a-z].html"
    
    ## A list
    curl -O "http://example.com/{one,two,three}.html"
    ```
4. 协议：`curl`支持多种协议，包括`DICT`,`FILE`,`FTP`,`MQTT`,`Gopher`(因为HTTP的成功，现在Gopher协议已经很少使用了)等，默认使用`http`
    1. 查看支持的协议
        
        ```bash
        curl-config --protocols
        ```
    1. `--proto`:指定使用的协议，后面可跟`+`(默认),`-`,`=`，协议间使用逗号分隔，后面的设置会覆盖前面的设置
        
        ```bash
        # 查看支持的协议
        curl --proto -ftps  # uses the default protocols, but disables ftps
        curl --proto -all,https,+http # only enables http and https
        curl --proto =http,https # also only enables http and https
        # 如果使用mac，协议最好用单引号包裹，比如
        curl --proto '=http,https'
        # 字典的使用 
        curl dict://dict.org/d:bash # 查询bash单词的含义
        curl dict://dict.org/show:db # 列出所有可用词典
        curl dict://dict.org/d:bash:foldoc # 在foldoc词典中查询bash单词的含义
        # 读取本地文件
        curl file:/Users/xxx/fileA
        curl file:///Users/xxx/fileA
        ```
    2. ftp协议：curl的FTP连接默认使用`passive`模式
        1. `–ftp-create-dirs`：默认情况下，使用一个在服务器上当前不存在的路径将会导致失败。带上该参数后会自动创建缺少的文件夹
        2. `--ftp-method`:控制如何使用`CWD`
            1. `multicwd`：默认使用该参数。在给定的URL上的每个路径部分都执行一次CWD操作。对于深层次，这意味着很多的命令。这是在 RFC1738上面定义这样的。这是默认行为但是执行会比较慢
                
                ```bash
                # 比如
                curl --ftp-method multicwd ftp://example.com/one/two/three/file.txt
                # 等价于 
                CWD one 
                CWD two 
                CWD three 
                ```
            2. `nocwd`curl命令根本不执行CWD查找，curl命令将会做SIZE, RETR, STOR等等命令，并且给定一个绝对路径给服务器用于这些命令。这也是执行最快的，但兼容性最差
                
                ```bash
                # 比如
                curl --ftp-method nocwd ftp://example.com/one/two/three/file.txt
                # 等价于 
                RETR one/two/three/file.txt
                ```
            3. `singlecwd`curl命令在绝对目标路径执行一次CWD操作，然后在文件上进行“正常”操作（像multicwd情况下）。比'nocwd'更加标准，但是没有'multicwd'兼容性强。
            
                ```bash
                # 比如
                curl --ftp-method singlecwd ftp://example.com/one/two/three/file.txt
                # 等价于 
                CWD one/two/three
                RETR file.txt
                ```
        3. `globbing`
        
        ```bash
        ## 查看服务器文件，比如查看服务器/home/ftp目录下的文件
        curl ftp://222.221.253.170:1021/home/ftp/ -u user:password
        ## 上传文件，比如上传example.txt到服务器的/home/ftp文件夹，服务器目录必需以/结尾
        curl -T example.txt ftp://222.221.253.170:1021/home/ftp/ -u  user:password # 这样上传的话远程服务器文件名会变成example.txt, 等同于curl -T example.txt ftp://222.221.253.170:1021/home/ftp/example.txt -u  user:password 
        curl -T example.txt ftp://222.221.253.170:1021/home/ftp -u  user:password # 这样写是错的，文件夹后面的一定要带上/
        curl -T example.txt ftp://222.221.253.170:1021/home/ftp/example2.txt -u  user:password # 这样上传的话远程服务器文件名会变成example2.txt
        ## 上传文件夹
        curl -T dirA ftp://222.221.253.170:1021/home/ftp/ -u  user:password
        ## 下载文件，不支持递归下载
        curl -u ftpuser:ftppass -O ftp://home/ftp/example.txt
        ## 下载多个文件
        curl –u user:passwd ftp://home/ftp/img/[1-10].gif –O  # 下载1-10.gif连续命名的文件
        curl –u name:passwd ftp://www.xxx.com/img/[one,two,three].jpg –O
        ## 列出文件。若在url中指定的是某个文件路径而非具体的某个要下载的文件名，CURL则会列出该目录下的所有文件名而并非下载该目录下的所有文件，比如
        curl -u ftpuser:ftppass -O ftp://home/ftp/
        ## 更多操作可以使用参数 -Q/–quote  带上ftp命令， 具体命令参考ftp协议
        ## 创建文件夹 -Q "MKD dirA"
        curl -u user:password ftp://192.168.1.100 -Q "MKD dirA"
        ## 删除文件夹 -Q "RKD dirA"
        curl -u user:password ftp://192.168.1.100 -Q "RKD dirA"
        ## 删除文件 -Q "DELE fileA"
        curl -u user:password ftp://192.168.1.100 -Q "DELE fileA"
        ## 重命名, 重命名需要连续执行两条命令, 使用两个 -Q 参数连续执行两条命令（必须先 RNFR, 后 RNTO）
        curl -u user:password ftp://192.168.1.100 -Q "RNFR fileA" -Q "RNTO fileB"
        ## 选项 –ftp-create-dirs 自动创建缺少的文件夹。比如下面这样，当服务器没有home/ftp文件夹，则会自动创建对应的文件夹
        curl -u user:password --ftp-create-dirs -T file.txt ftp://192.168.1.100/home/ftp/
        ```
    3. IMTP
5. 通信过程
    1. 详细信息
        1. `-v`显示通信过程:以`>`为前缀的是发送到服务器的数据，以`<`为前缀的是从服务器接收到的数据，以`*`开头的是misc信息，如连接信息、SSL握手信息、协议信息等。通常用于调试
        2. `-vv`更详细的信息？
        2. `--trace`or`--trace-ascii`等于`-v`加上输出原始的二进制数据
        3. `--trace-time`添加时间戳
    2. 安静模式
        1. `-s`：不显示进度和错误信息，但任然打印请求到的数据，除非重定向
        2. `-S`:打印错误信息，无视`-s`
    3. `--progress`显示进度条
    4. `-m`(`--max-time <seconds>`)指定处理的最大时长
6. IP
    1. `--resolve`不需要修改`/etc/hosts`直接解析 ip 请求域名
        
        ```bash
        # 将 http://example.com 或 https://example.com 请求指定域名解析的 IP 为 127.0.0.1
        curl --resolve example.com:80:127.0.0.1 http://example.com/
        ```
7. `-v`：可以看到执行的所有命令和响应

```bash
# 更多例子
# 1
curl -X GET -H "Sign: 12345672147b8d706e7022ef862b0dec25fce20415263e48ed37b2a17385e41a" -H "Timestamp: 1542102231" -H "Cache-Control: no-cache" -H "Postman-Token: 12345678-e5a2-4c28-26fe-0bf63eeea10f" "https://xxx.com/vin?vin=WAUAMD4L2CD005389"`
# 2
curl -XPOST 'https://xxx/companies/search'

# 3 
curl 'http://example.com/foo/bar' \
  -H 'Connection: keep-alive' \
  -H 'Pragma: no-cache' \
  -H 'Cache-Control: no-cache' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'X-Org-Id: 49e8e3246000045' \
  -H 'X-App-Id: 131' \
  -H 'X-YCUBE-APPID: 131' \
  -H 'Authorization: Bearer xxx.xxx.xxx' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36' \
  -H 'Referer: http://example.com' \
  -H 'Accept-Language: zh-CN,zh;q=0.9' \
  -H 'Cookie: VARIABLES_KEY={...}; 
  YCUBE_TOKEN=xxx.xxx.xxx;' \
  --compressed \
  --insecure
# 4 获取响应的状态码
curl -I -m 10 -o /dev/null -s -w %{http_code} www.baidu.com
# 5 查看网页源代码
curl www.example.com
```

使用：
1. 判断端口连通性
    1. `curl ip:port`
        1. Connection reset by peer 表示 通的
        1. Empty reply from server 表示 通的
        1. Connection refused 表示 不通
    2. `telnet ip port`
        1. Connected to 192.168.3.132. Escape character is '^]'. 表示通的
            1. 连接后怎么退出呢：用`ctrl+c`是不行的，有两种方法
                1. 可以输入`ctrl+]`进入telnet命令界面，然后输入`quit`就可以退出
                1. 直接输入`quit`就可以退出
        1. connect to address 192.168.3.132: Connection refused. Unable to connect to remote host 表示不通
2. 利用`cip.cc`快捷查询IP地址信息
    
    ```bash
    # 查询内网
    curl cip.cc/192.168.0.3
    IP	: 192.168.0.3
    地址	: 局域网  局域网
    数据二	: 局域网 | 对方和您在同一内部网

    # 查询外网地址
    curl cip.cc/13.229.188.59
    IP	: 13.229.188.59
    地址	: 新加坡  新加坡
    数据二	: 新加坡 | Amazon数据中心
    
    curl cip.cc/14.215.177.38
    IP    : 14.215.177.38
    地址    : 中国  广东  广州
    运营商    : 电信
    数据二    : 广东省广州市 | 北京百度网讯科技有限公司电信节点
    数据三    : 中国广东省广州市 | 电信
    ```

问题：
1. 有时候已下载的百分比会变小是什么情况，比如从25%突然跳到17%？

## 9 wget
用来从指定的URL下载文件，支持断点续传。支持FTP和HTTP下载方式。支持代理且设置简单。同样不支持多线程下载。

参数：
1. `-O`:以不同的文件名保存。wget默认会以最后一个符合/的后面的字符来命令，对于动态链接的下载通常文件名会不正确。比如`wget http://www.linuxde.net/download?id=1`会下载一个文件并以名称`download.aspx?id=1080`保存。比如`wget -O wordpress.zip http://www.centos.bz/download.php?id=1080`
2. `-c`：继续执行上次终端的任务，断点续传。
3. `--spider`：测试下载链接是否有效。
4. `--limit-rate=RATE`:限制下载速度。因为它默认以全部带宽去下载，所以可能需要限速，比如`wget –limit-rate=300k http://cn.wordpress.org/wordpress-3.1-zh_CN.zip`
5. `-b`：后台下载。一般文件特别大的时候可以使用该参数，会输出如下内容，可以使用`tail -f wget-log`查看下载进度。

    ```
    Continuing in background, pid 1840.
    Output will be written to `wget-log’.`
    ```
6. `-user-agent=代理`：伪装代理，默认是`wget/VERSION`。有些网站会根据代理名称而不是浏览器来拒绝下载请求。比如`wget –user-agent="Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US) AppleWebKit/534.16 (KHTML, like Gecko) Chrome/10.0.648.204 Safari/534.16" ...`
7. `–tries=xxx`：修改重试次数，默认是20。
8. `-i`：下载本地或外部文件中的URL。可以把多个URL放在文件中，然后下载。
    
## 10 执行命令
### 10.1 exec
用于调用并执行指令的命令。exec命令通常用在shell脚本程序中，可以调用其他的命令。如果在当前终端中使用命令，则当指定的命令执行完毕后会立即退出终端。

`man exec`可知，

## 11 ssh 
ssh命令是openssh套件中的客户端连接工具，可以给予ssh加密协议实现安全的远程登录服务器。

使用说明：
1. 端口转发：端口转发功能可以加密 Client 和 Server之间的通讯数据，还可以突破防火墙的限制。
    1. `-L [bind_address:]port:host:hostport`：本地端口转发，将远程的端口转发到本地，实现正向端口代理。可以指定TCP port或者unix socket，`bind_address`如果是"localhost"则只能本地使用，如果是空或者"*"的话则所有接口都能使用。具体用法参考man。
    2. `-R`:远程端口转发，把本地的端口转发到远程机器上，实现反向端口转发。
    3. `-D`:动态端口转发

TODO：动态端口转发

## 12 网络相关
### 12.1 网络状态
查看网络状态`netstat`:显示网络状态,包括网络连接、路由表、接口统计等信息

## 13 安全相关
### OpenSSL
参考：
1. https://www.feistyduck.com/library/openssl-cookbook/online/ch-openssl.html
2. 官网：https://www.openssl.org/source/

OpenSSL是一个强大的安全套接字层密码库，Apache使用它加密HTTPS，OpenSSH使用它加密SSH，但是，你不应该只将其作为一个库来使用，它还是一个多用途的、跨平台的密码工具。

它主要包含三个组件：
1. openssl：多用途的命令行工具
2. libcrypto：加密算法库
3. libssl：加密模块应用库，实现了ssl及tls

OpenSSL的整个软件包大概可以分成三个主要的功能部分：
1. SSL协议库：SSL通信API接口（SSL/TLS 客户端以及服务器的测试，处理S/MIME 或者加密邮件）
2. 密钥和证书封装管理功能（建立 X.509 证书、证书签名请求(CSR)和CRLs(证书回收列表)）
3. 密码算法库：密码算法库（建立 RSA、DH、DSA key 参数，计算消息摘要，使用各种 Cipher加密/解密）

OpenSSL有许多的特征，而且还有SSL客户端和服务端特征，OpenSSL还有：
1. 美国联邦政府NIST FIPS 140-2一级评估确认
2. TLS，下一代SSL协议
3. X.509密钥和证书的生成
4. X.509证书权力
5. S/MIME加密
6. 文件加密和粉碎
7. 打乱UNIX密码
8. 9个不同的商业密码硬件设备
9. 密码性能测试
10. 36个命令
11. 6个消息摘要算法
12. 9个密码算法
13. 多个加密协议

常用命令和参数：
1. `-cert`:The CA certificate file
2. `-config`
3. -in filename：指定要加密的文件存放路径
4. -out filename：指定加密后的文件存放路径
5. -salt：自动插入一个随机数作为文件内容加密，默认选项
6. -e：可以指明一种加密算法，若不指的话将使用默认加密算法
7. -d：解密，解密时也可以指定算法，若不指定则使用默认算法，但一定要与加密时的算法一致
8. -a/-base64：使用-base64位编码格式



使用：
1. 生成私钥：`openssl genrsa -out key.pem 2048`
2. 加密解密
    1. 普通加密解密
    2. 对称加密`openssl enc ...`
    3. 单向加密`openssl dgst ...`，更多可支持的签名算法见`openssl dgst --help`
    
    ```bash
    # 一般加密解密
    openssl enc -e -des3 -a -salt -in fstab -out jiami
    openssl enc -d -des3 -a -salt -in fstab -out jiami
    ```
3. 生成私钥：`openssl genrsa`使用rsa算法(RSA私钥存在PKCS1和PKCS8两种格式)，`openssl ecparam`使用ECC/ECDSA算法
    1. genrsa标准命令生成私钥`openssl genrsa [-out filename] [-passout arg] [-des] [-des3] [-idea] [-f4] [-3] [-rand file(s)] [-engine id] [numbits]`:numbits表示生成私钥的大小(长度)，默认是2048。一般情况下秘钥文件的权限一定要控制好，只能自己读写，因此可以使用 umask 命令设置生成的私钥权限

        
        ```bash
        # 生成私钥
        openssl genrsa -out key.pem 2048
        ```

    2. rsa 标准命令从私钥中提取公钥`openssl rsa [-inform PEM|NET|DER] [-outform PEM|NET|DER] [-in filename] [-passin arg] [-out filename] [-passout arg] [-sgckey] [-des] [-des3] [-idea] [-text] [-noout] [-modulus] [-check] [-pubin] [-pubout] [-engine id]`,`-in filename`指明私钥文件,`-out filename`指明将提取出的公钥保存至指定文件中,`-pubout`根据私钥提取出公钥 
    3. `openssl ecparam`
        
        ```
        openssl ecparam -genkey -name secp384r1 -out server.key
        ```
4. 证书请求相关`openssl req`，主要功能有生成证书请求文件、查看验证证书请求文件、生成自签名证书。默认签名算法是sha1。不过该命令没有提供对证书文件的管理能力。
    1. 什么是证书请求文件(CSR,Certificate Signing Request):向“证书机构”申请数字证书的时候，就需要向他们提供相应的信息，这些信息以特定文件格式(.csr)提供的，这个文件就是“证书请求文件”；为了确保我提供的信息在互联网的传输过程中不会被有意或者无意的破坏掉，我们有如下的机制来对传输的内容进行保护：首先在本地生成一个私钥，利用这个私钥对“我们需要提供的信息“进行加密，从而生成 证书请求文件(`.csr`), 这个证书请求文件其实就是私钥对应的公钥证书的原始文件，**里面含有私钥所对应的公钥信息**
    1. 主要参数
        1. `-new`:生成证书请求文件
        2. `-x509`:专用于CA生成自签证书，如果不是自签证书则不需要此项。除非指定`-set-serial`选项,否则使用0作为证书序列号
        3. `-key`:指定已有的秘钥文件生成秘钥请求，只与生成证书请求选项`-new`配合。
        4. `-newkey`:`-newkey`是与`-key`互斥的，`-newkey`是指在生成证书请求或者自签名证书的时候自动生成密钥，然后生成的密钥名称由`-keyout`参数指定。当指定`-newkey`选项时，后面指定`rsa:bitsA`说明产生rsa密钥，位数由bitsA指定。 如果没有指定选项`-key`和`-newkey`，默认自动生成秘钥。
        5. `-in`:读取文件或标准输入
        5. `-out`:指定生成的证书请求或者自签名证书名称
        6. `-config`:默认参数在ubuntu上为`/etc/ssl/openssl.cnf`, 可以使用`-config`指定特殊路径的配置文件
        7. `-nodes`:如果指定`-newkey`自动生成秘钥，openssl req将总是加密该私钥文件，并提示输入加密的密码。如果不想输入密码，可以使用`-nodes`，该选项表示生成的秘钥不需要加密，即不需要输入pass phrase.   
        8. `-batch`:指定非交互模式，直接读取config文件配置参数，或者使用默认参数值 
        9. `-days`:证书的有效期限，单位是day（天），默认是365天
        10. `-verify`验证证书请求文件的数字签名,可以验证出证书请求文件是否被篡改过
        11. `-outform`输出证书的编码格式,PEM或DER,默认PEM
    2. 使用
        1. 生成根自签名证书：需要输入一些配置信息
            
            ```bash
            openssl req -new -x509 -key ca.key  -out ca.pem  -days 365
            openssl req -new -x509 -key ca.key  -out ca.crt  -days 365
            ```
        2. 生成证书请求文件:有如下信息可选(待研究)
            1. Country Name(C)
            2. State or Province Name(ST)
            3. Organization Name(O)
            4. Common Name(CN):定义的是将要申请SSL证书的域名、子域名、主机名或IP，CN必须和将要访问的网站地址一样，否则访问时就会给出警告。一般是必填。
            5. emailAddress:一般不用填
    2. 例子
    
        ```bash
        #生成自签名证书,证书名client.crt，采用自动生成秘钥的方式，指定生成秘钥长度为1024，加密，秘钥文件client.key.
        openssl req -x509 -newkey rsa:1024 -out client.crt -keyout client.key -batch -nodes
        #上面的命令加上-new选项是同样的执行效果
        openssl req -new -x509 -newkey rsa:1024 -out client.crt -keyout client.key -batch -nodes   
        #生成自签名证书，证书名client.crt，指定秘钥文件，秘钥文件为rsa_private_key.pem。
        openssl req -new -x509 -key ./rsa_private_key.pem -out client.crt -nodes -batch
        #指定秘钥文件pri_key.pem，生成证书请求文件 req.csr
        openssl req -new -key pri_key.pem -out req.csr
        #使用req命令，以文本方式查看刚生成的证书请求文件
        openssl req -in req1.csr -text
        # 验证证书请求文件,"verify OK"表示证书请求文件是完整未被篡改过
        openssl req -verify -in req2.csr
        # 只查看证书请求的文件头部分
        openssl req -in req1.csr -noout -text
        #查看证书请求文件的公钥， 如果从申请证书请求时所提供的私钥中提取出公钥，这两段公钥的内容是完全一致的
        openssl req -in req1.csr -noout -pubkey
        #查看证书请求文件的个人信息部分
        openssl req -in req1.csr -noout -subject
        ```
5. 签名、吊销`openssl ca`
    1. 签名用户证书
        1. 涉及四个文件：被签名的CSR文件（含有证书的公钥） , 签名者的证书文件(这里是CA证书，含有签名者的公钥)，签名使用的私钥(签名者的私钥，这里是CA证书的私钥)；签名完成后输出的文件
        2. 涉及的配置文件
            1. `/etc/pki/CA/index`这个文件用于跟踪已经签发的证书，如果没有签发过，那么该文件应该为0字节.
            2. `/etc/pki/CA/serial`这个文件里面里面保存的是最后一次签发的证书的序列号，初始值应该为01,也可以为00等其他的值。如果以上两个文件缺失或者内容不符合规范，会导致签名命令执行时报错.
            3. `/etc/pki/tls/openssl.cnf`:
                1. `basicConstraints=CA:FALSE`:基本约束，`CA:FALSE`表示该证书不能作为CA证书，即不能给其他人颁发证书
                2. `keyUsage = critical,keyCertSign,cRLSign`:指定证书的目的，也就是限制证书的用法。
                    1. 如果是生成CA证书可以设置为`keyUsage = cRLSign, keyCertSign`

    2. 例子
    
        ```bash
        # 如果没有指定CA证书以及CA的key, 那么会默认读取openssl.cnf的配置,另外两个文件参数是必须指定的
        openssl ca -in ./mycert.csr  -out ./my.crt -days 365 -cert ./ca.pem  -keyfile ./ca.key -config my.cnf
        
        # 查看
        ```
    3. openssl ca命令对配置文件(默认为`/etc/pki/tls/openssl.cnf`(不同系统的目录可能不一样))的依赖性非常强，所以先了解下该配置文件
        1. 目录
            1. mac下是`/System/Library/OpenSSL/openssl.cnf`和`/private/etc/ssl/openssl.cnf`
6. `openssl x509`
    1. 主要参数
        1.  `-noout`:no certificate output
        1. ` -text`:print the certificate in text form
    
    ```bash
    # 查看证书的内容
    openssl x509 -in /etc/pki/CA/certs/test.crt -text
    ```
7. 吊销证书
    1. 通过crl列表吊销
        1. 获取要吊销证书的 serial 和 subject 信息 ，对比其与index.txt 中存储的是否一致 
        2. 执行吊销`openssl ca -revoke /etc/pki/CA/newcerts/numA.pem`
        3. 生成吊销证书的吊销编号 （第一次吊销证书时才需要执行）:`echo 01 > /etc/pki/CA/crlnumber`
        4. 更新证书吊销列表`openssl ca -gencrl -out /etc/pki/CA/crl/ca.crl`
        5. 查看 crl 文件命令：`openssl crl -in /etc/pki/CA/crl/ca.crl -noout -text`
    
## N 其他
1. 别名`alias`
    1. 基本用法是`alias [name]=[string]`,比如想把`cd /usr; ls; cd -`三个命令合在一起取个别名,可以使用`alias foo='cd /usr; ls; cd -'`
    2. 删除别名`unalias [name]`
    3. 不带参数使用`alias`,则是显示系统中所有的别名命令(mac无效?)
3. 计算器`bc`(Binary Calculator)
4. 剪切板xsel

    ```bash
    cat README.TXT | xsel  
    # 如有问题可以试试-b选项
    cat README.TXT | xsel -b 
    # 将readme.txt的文本放入剪贴板
    xsel < README.TXT  
    # 清空剪贴板
    xsel -c  
    ```


# 四 高级
## 1 linux系统主要目录说明

|目录|评论|
|---|:--|
|/	|根目录，Linux文件系统的最上层目录，其他所有目录均是该目录的子目录。万物起源。|
|/bin|Binary的缩写，包含系统启动和运行所必须的二进制程序，例如cp和mv等；也存放Shell，如bash和csh。不应把该目录放到一个单独的分区中，否则LinuxRescue模式无法使用这些命令。|
|/boot|包含 Linux 内核、初始 RAM 磁盘映像（用于启动时所需的驱动）和 启动加载程序，包括vmlinuz和initrd.img等，这些文件若损坏常会导致系统无法正常启动，因此最好不要做任意改动。独立挂载/boot的好处是可以让多个Linux共享一个/boot。“/boot”目录的大小通常都很小，20MB左右。可以根据自己的硬盘空间分配一块给/boot分区，但是不要太大，否则是种浪费。|
|/dev|设备文件目录，包含设备结点的特殊目录。“一切都是文件”，也适用于设备。 在这个目录里，内核维护着所有设备的列表。例如/dev/sda表示第一块SCSI设备，/dev/sdb表示第二块SCSI设备，/dev/hda表示第一块IDE设备，以此类推。另一种表示方法为：hdn或sdn，n为数字，从0开始编号。如IDE接口的硬盘/dev/hda，也可以表示为hd0 ， SCSI 、SATA接口的 /dev/sda 可以表示成sd0。/dev/sda1 就是(sd0,0)。这种方法主要用在grub中。|
|/etc|这个目录包含所有系统层面的配置文件。它也包含一系列的 shell 脚本， 在系统启动时，这些脚本会开启每个系统服务。这个目录中的任何文件应该是可读的文本文件。有趣的文件：虽然/etc 目录中的任何文件都有趣，但这里只列出了一些我一直喜欢的文件：/etc/crontab， 定义自动运行的任务。/etc/fstab，包含存储设备的列表，以及与他们相关的挂载点。/etc/passwd，包含用户帐号列表。|
|/home|	普通用户的主目录或FTP站点目录。在通常的配置环境下，系统会在/home 下，给每个用户分配一个目录。普通用户只能 在自己的目录下写文件。这个限制保护系统免受错误的用户活动破坏。重装系统的时候，该分区的文件可以不受影响。|
|/lib|	包含核心系统程序所使用的共享库文件。这些文件与 Windows 中的动态链接库相似。|
|/lost+found|	每个使用 Linux 文件系统的格式化分区或设备，例如 ext3文件系统， 都会有这个目录。当部分恢复一个损坏的文件系统时，会用到这个目录。除非文件系统 真正的损坏了，那么这个目录会是个空目录。|
|/media|	在现在的 Linux 系统中，/media 目录会包含可移动介质的挂载点， 例如 USB 驱动器，CD-ROMs 等等。这些介质连接到计算机之后，会自动地挂载到这个目录结点下。|
|/mnt	|在早些的 Linux 系统中，/mnt 目录包含可移动介质的挂载点。|
|/opt|	这个/opt 目录被用来安装“可选的”软件。这个主要用来存储可能 安装在系统中的商业软件产品。|
|/proc|	这个/proc 目录很特殊。从存储在硬盘上的文件的意义上说，它不是真正的文件系统。 相反，它是一个由 Linux 内核维护的虚拟文件系统。它所包含的文件是内核的窥视孔。这些文件是可读的， 它们会告诉你内核是怎样监管计算机的。|
|/root|	root 帐户的家目录。|
|/sbin	|这个目录包含“系统”二进制文件。它们是完成重大系统任务的程序，通常为超级用户保留。|
|/tmp	|这个/tmp 目录，是用来存储由各种程序创建的临时文件的地方。一些配置导致系统每次 重新启动时，都会清空这个目录。|
|/usr|	在 Linux 系统中，/usr 目录可能是最大的一个。它包含普通用户所需要的所有程序和文件。|
|/usr/bin	|/usr/bin 目录包含系统安装的可执行程序。大多数系统程序的安装目录|
|/usr/lib	|包含由/usr/bin 目录中的程序所用的共享库。|
|/usr/local|	这个/usr/local 目录，是非系统发行版自带，却打算让系统使用的程序的安装目录。 通常，由源码编译的程序会安装在/usr/local/bin 目录下。新安装的 Linux 系统中，会存在这个目录， 但却是空目录，直到系统管理员放些东西到它里面。|
|/usr/sbin|	包含许多系统管理程序。|
|/usr/share|	/usr/share 目录包含许多由/usr/bin 目录中的程序使用的共享数据。 其中包括像默认的配置文件、图标、桌面背景、音频文件等等。|
|/usr/share/doc|	大多数安装在系统中的软件包会包含一些文档。在/usr/share/doc 目录下， 我们可以找到按照软件包分类的文档。|
|/var|	除了/tmp 和/home 目录之外，相对来说，目前我们看到的目录是静态的，这是说， 它们的内容不会改变。/var 目录是可能需要改动的文件存储的地方。各种数据库，假脱机文件， 用户邮件等等，都位于在这里。|
|/var/log|	这个/var/log 目录包含日志文件、各种系统活动的记录。这些文件非常重要，并且 应该时时监测它们。其中最重要的一个文件是/var/log/messages。注意，为了系统安全，在一些系统中， 你必须是超级用户才能查看这些日志文件。|

## 2 常见文件说明
1. MOTD和`~/.hushlogin`
    1. MOTD(message of the day):可以理解为每次登录系统时的欢迎界面，一般用来提示用户注意事项，或提示系统运行的概要信息，也可以是任何其他信息(图形等)。同时还可以设置颜色和背景色。
        1. 配置：为ssh访问系统用户必须配置/etc/ssh/sshd_config文件。
            
            ```bash
            # /etc/ssh/sshd_config
            PrintMotd yes   　　　　　　　　#远程用户登录时是否打印/etc/motd文件信息           
            ```
        1. 分类：动态和静态
            1. `/etc/motd`：
    2. `~/.hushlogin`：不论其内容为何,当你login时, 系统的`/etc/motd`就不会扔到你的display上,也就是每次你打完passwd成功后,显示的那一堆system manager写的注意事项.具体可以`man login`查看，注意重要的消息最好别hush了，最好显示出来。

## 3 cron

### 3.1 cron表达式
参考：https://www.cnblogs.com/linjiqin/archive/2013/07/08/3178452.html

格式有两种：
- Seconds Minutes Hours DayofMonth Month DayofWeek Year
- Seconds Minutes Hours DayofMonth Month DayofWeek

特殊字符说明：
1. 星号(*)：表示 cron 表达式能匹配该字段的所有值。如在第5个字段使用星号(month)，表示每个月
2. 斜线(/)：表示增长间隔，如第1个字段(minutes) 值是 3-59/15，表示每小时的第3分钟开始执行一次，之后每隔 15 分钟执行一次（即 3、18、33、48 这些时间点执行），这里也可以表示为：3/15
3. 逗号(,)：用于枚举值，如第6个字段值是 MON,WED,FRI，表示 星期一、三、五 执行
4. 连字号(-)：表示一个范围，如第3个字段的值为 9-17 表示 9am 到 5pm 直接每个小时（包括9和17）
5. 问号(?)：只用于日(Day of month)和星期(Day of week)，\表示不指定值，可以用于代替 *

例子：
```bash
*/2 * * * * # 每两分钟执行
```

## 4 包管理
### 4.1 snap
听说Snap将成为支持所有 GNU/Linux 发行版的通用二进制软件包格式，Snap能使一个单一的二进制程序包可以完美、安全地运行在任何Linux台式机、服务器、云或物联网设备上。大佬说的：“在一个私有仓库中维护一个 .deb 软件包是复杂而耗时的,而 Snap 更容易维护、打包和分发”，官网是：snapcraft.io

Snap：是一种安全的、易于安装的、沙盒化的软件包格式。

snapcraft：涵盖了 snap 和用来构建它们的命令行工具。

特点：
1. 包含应用所需运行的所有dependence，包含了所有它需要运行的环境。代价就是包会比较大
2. 你可以100％确定你的应用不会因为任何在应用之外的变化的改变而导致你的应用不 能正常运行，比如卸载一个Java应用不会导致其它Java应用的运行．安装一个使用不同版本的Java JDK/OpenJDK的Java应用，不会干扰现有的任何一个运行在不同JDK/OpenJDK版本的Java应用

常用操作：`find`,`list`,`install`,`refresh`,`remove`,`revert`
1. `changes`：更改记录

## 5 epoll
首先要明白select或者poll事件驱动：假设有这样一个需求场景：有10万+的客户端与一个进程保持着 TCP连接，而每一时刻只有几十个或几百个TCP连接是活跃的，与服务器有 TCP包的交互，在每一时刻，进程只需要处理这100万连接中的一小部分连接。如何才能高效地处理这种场景呢？有一种做法是这样的，进程想要获取客户端状态的时候，首先让操作系统收集那些 TCP连接上有事件发生，这个时候肯定要告诉操作系统要检查的 10万+个连接；然后操作系统找出这些连接中有事件发生的几百个连接，然后告诉进程，由进程针对这些有数据的连接进行进一步的处理。实际上，这就是 select或者 poll事件驱动方式的做法。这种做法就是忙**轮询**和无差别**轮询**，会有个非常明显的缺陷，在进程收集有事件的连接时，其实需要检查的大部分连接中是没有事件发生的。而且在每次收集事件时，都把这10万+连接的传给操作系统（这首先就是用户态内存到内核态内存的大量复制），然后操作系统遍历进程发送过来的连接一个个的进行遍历，查看那些连接上有事件发生，那些没有。这些复制传递、遍历会是巨大的资源浪费，当然也会有性能上的影响。

linux2.6开始有了epoll：linux的epoll可以理解为event poll，epoll是一种I/O事件**通知**机制(事件驱动)，是linux 内核实现IO多路复用的一个实现。不同于忙轮询和无差别轮询，epoll在 Linux内核中申请了一个简易的文件系统。在进程中使用 epoll的时候，首先调用 epoll_create创建 epoll句柄，当需要对 TCP连接进行监控时，直接调用 epoll_ctl向 epoll句柄中添加这10万+个连接的套接字即可。然后调用epoll_wait收集发生事件的连接，epoll_wait用当前准备好的事件填满一个缓冲区。只有准备好的事件添加到了缓冲区，因此没有必要遍历客户端中当前所有 监视的文件描述符，这简化了查找就绪的描述符的过程，把空间复杂度从 select 中的 O(N) 变为了 O(1)。这样，只需要在进程启动时建立1个 epoll句柄，并在需要的时候向它添加或删除连接就可以了，然后选择阻塞或者非阻塞的方式调用epoll_wait，操作系统就会返回发生事件的连接，epoll之会把哪个流发生了怎样的I/O事件通知我们。epoll和内核这种协作就是epoll高效的关键之处，此时我们对这些流的操作都是有意义的，复杂度降低到了O(1)。

所以可以知道为什么epoll比select高效: 如果在监视着 1000 个描述符，只有两个就绪， epoll_waits 返回的是 nready=2，然后修改 events 缓冲区最前面的两个元素，因此我们只需要“遍历”两个描述符。用 select 我们就需要遍历 1000 个描述符，找出哪个是就绪的。因此，在繁忙的服务器上，有许多活跃的套接字时 epoll 比 select 更加容易扩展。

epoll的实现：(待整理)

epoll高效的本质：
1. 减少用户态和内核态之间的文件句柄拷贝；
2. 减少对可读可写文件句柄的遍历。

## 6 linux的虚拟化技术:XEN,openvz和KVM
待整理

# 五 经验


# 六 问题
## 1 已解决
### 1.1 命令行换行/终端换行/参数换行：终端命令有时候很长，不换行的话显示不够直观（特别是在脚本文件中），这个时候可以使用`\`来换行

```bash
# 正确示例
## git clone --depth 1 --branch v8.1.1 https://github.com/nodejs/node
git clone --depth 1 \
              --branch v8.1.1 \
              https://github.com/nodejs/node

## less -m -N example.md
less -m -N\
 example.md
## less -m -N example.md
less -m -N \
example.md

# 正确示例但不建议这么用，正确的做法是\后面必须换行
## less -m -N example.md
less -m\ -N example.md
less -\m -N example.md
less -m -N exam\ple.md
less -m -N example\.md
less -m -N \example.md
## less -m -N example.md
less -m -N example.m\
d
```

```bash
# 错误示例
## less -m -N example.md
less -m -N\example.md
less -m -N\ example.md
```

## 2 未解决
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
16. copy的几种方式，除了cp还有什么
17. 关于软链接和硬链接
    1. 硬链接:与普通文件没什么不同，inode 都指向同一个文件在硬盘中的区块
    2. 软链接： 保存了其代表的文件的绝对路径，是另外一种文件，在硬盘上有独立的区块，访问时替换自身路径。
    3. 硬链接的实现原理是怎么样的?
    3. 参考:[http://www.jianshu.com/p/dde6a01c4094](http://www.jianshu.com/p/dde6a01c4094)
18. linux的命令一共有4中,除了type识别的三种还有:shell函数(即小型shell脚本)?
20. sftp:[https://jingyan.baidu.com/article/c910274be7bc6acd361d2da7.html](https://jingyan.baidu.com/article/c910274be7bc6acd361d2da7.html)
21. linux cheat
22. [命令行的艺术:linux bash命令大全详解](http://ourjs.com/detail/5923d49cf1239006149616a6)
23. `init.d`

24. linux tty是啥
26. 远程如何连到局域网内的机子？就是如何把linux弄成可以外网访问的?
27. tty -s