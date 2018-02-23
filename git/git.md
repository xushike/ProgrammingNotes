# git
[TOC]
## 一 概述
git开源免费的分布式版本控制系统。
### 1 简介
### 2 历史
### 3 常识
#### 三棵树
官方参考资料:[https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset)

#### git的ssh和https
git允许我们用ssh url或者http url来管理代码,两种不同的协议.如果是https,则默认每次都要输入密码,但可以使用git提供的credential helper来存储密码
##### 凭证助手credential helper(待测试)
用于存储git的凭证,Git现在默认包含如下几个helper:
- Cache
    
    将凭据在内存中进行短时间的缓存,默认15分钟
    1. 使用`git config --global credential.helper cache`
    2. 参数`cache –timeout=[num]`:设置时间,如`git config credential.helper cache –timeout=3600`
- Store(待测试)
    
    将凭据保存在磁盘上,明文存储,所以不安全.
    1. 指定凭证助手:`git config --global credential.helper store`    
    2. 指定明文密码保存位置
        可以为不同项目指定不同的文件从而达到使用多账号的目的.
        1. `git config --global credential.helper store --file=~/cred.txt`,但是该命令似乎并不生效,可以通过修改config文件达到目的,

            ```
            [credential]
            helper = store --file=D:/credential/cred1.txt
            ```
            
            再次push，便会将账户信息存至`D:/credential/cred1.txt`中.如果想清除账户，删除指定的文件即可。.

- mananger

    安装了GitGUI，自动会在system级别中设置credential.helper为manager
- wincred

#### ssh-agent
安装了git之后就会有ssh-agent(windows是),ssh-agent 是用于管理SSH private keys的, 长时间持续运行的守护进程（daemon）. 唯一目的就是对解密的私钥进行高速缓存.
### 4 文档
### 5 网站
1. git的官方中文book,但是有些内容并不生效:[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)

## 二 安装配置
### 1 win
1. 下载git for windows
2. 安装过程大同小异，注意设置git环境的时候选择第二项"use git from the windows command prompt"，如果选第一项就不能在cmd中使用git，要自己去配置path。自己配置的时候添git安装目录下的bin目录或者cmd目录都可以
3. 安装完之后记得配置global username和useremail，这两样就是提交时需要记录的名字和邮箱，这样才可以提交到本地仓库；然后就是推送，如果是需要登录的服务器(github等)推送的时候还需要输入账号密码

    ```bash
    #注意没配置的话会报错:unable to auto-detect email address
    #查看git user.name和email
    git config user.name
    git config user.email
    #配置用户级的git user.name和email
    git config --global user.name "xxx"
    git config --global user.email "xxx"
    ```
    为每个项目单独配置:(待补充)

4. 配置ssh Key(可选)

    主要用于ssh方式的秘密吗登录.    
    1. 查看目录下是否有公钥
        
        SSH 公钥默认储存在账户的主目录下的 `~/.ssh` 目录,进入该目录查看是否有`xxx`和 `xxx.pub` 来命名的一对文件，这个 `xxx`通常就是`id_dsa`或`id_rsa`.有`.pub`后缀的文件就是公钥，另一个文件则是密钥。

    2. 没有则交互式创建:`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`,会在`~/.ssh`下生成公钥和密钥.或者直接输入`ssh-keygen`也行,但是选项有点多.

        会要求输入密码,应该是用于ssh登录服务器命令行界面的(待确认),所以只是使用git的话可以不用输入.

    3. 添加到ssh-agent(多账户时才用)

        比如上面新建了个人的key,如果我还需要再创建一个公司的key,可以:
        1. 创建ssh key:`ssh-keygen -t rsa -b 4096 -f $home/.ssh/company -C "wdwangtw@gmail.com"`
        2. 开启ssh-agent:`eval  "ssh-agent -s"`
        3. 添加私钥到ssh-agent:`ssh-add ~/.ssh/conpany/xxx`,如果报错"could not open a connection to your authentication agent",则输入`ssh-agent bash`,再输入`ssh-add ~/.ssh/conpany/xxx`
        4. 创建或修改ssh-agent的配置文件(默认是在`~/.ssh`目录下的`config`文件)

            ```
            Host myhost personal 
            User xushike
            HostName github.com
            IdentityFile ~/.ssh/id_rsa

            Host myhost company
            User wdwangtw
            HostName github.com
            IdentityFile ~/.ssh/company
            ```

            其格式为:

            ```
            Host myhost USER_HOST     ;USER_HOST为自定义host名字，如上面的personal和company
            User USER_NAME                 ;USER_NAME为自定义名称
            HostName SERVER_HOST   ;SERVER_HOST为实际服务器host，此时为GitHub
            IdentityFile PRIVATE_KEY      ;PRIVATE_KEY为本地key
            ```

            当再次clone一个新Repos时，如果其ssh地址为git@github.com:wdwangtw/xxx.git，使用git clone git@company:wdwangtw/TestUserwd.git即可clone到本地（注意github.com换成了自定义的company），并且push时也不用输入任何验证。
        5. 告诉ssh 允许 ssh-agent 转发(可选)

            加入我有a和b两个服务器的钥匙,此时在a服务器上想不输入密码的连到b服务器,就需要配置转发功能.添加`ForwardAgent yes`到`config`文件中.然后每个服务器都需要这样设置.
            
    4. 将公钥添加到github或者gitlab等服务器的账户里
        
        Copies the contents of the id_rsa.pub file to your clipboard,然后粘贴到服务器需要你填入的地方.
        1. 如果换电脑,可以把本地的key拷过去,也可以重新生成key.

    5. 如果之前用的https协议,此时需要remote origin,然后重新设置origin:`git remote add origin git@github.com:xushike/study.git`
    6. 对于github,可以测试是否成功设置ssh key:`ssh -T git@github.com`
5. 关于git自身的更新：

### 2 mac
#### 方式一(最简单):用Xcode的Command Line Tools
#### 方式二:Homebrew安装
#### 方式三:在[https://git-scm.com/download/mac](https://git-scm.com/download/mac)下载安装

### 3 linux
1. 未整理
    1. linux下ssh-agent的全局配置文件是`/etc/ssh/ssh_config`?
    2. linux下启动命令是:eval `ssh-agent`?

## 三 基础
### 1 初始化仓库
1. 如果在Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文  
2. 注意初始化之后本地是没有分支的，这个时候`git branch`为空，只有第一次commit之后才会有分支，而且只有有分支之后才能和远程仓库关联。

### 2 添加跟踪(放入暂存区)和修改  
1. `git add [被跟踪的文件名]`:用于把文件放入暂存区(放入暂存区的文件会被关联)，如果文件暂存后又被修改了，需要再次暂存然后提交。参数说明：
    1. `-u`:暂存所有已关联的文件(新建的文件不受影响)
    2. `-f`:如果想暂存的文件被ignore了，加上该命令可以强制暂存
    
### 3 撤销更改
理解这几个命令之前最好先了解git的三棵树。
1. `git reset [xxx1] [xxx2] [xxx3]`:
    [xxx1]参数说明:
    1. 
    4. `--patch`：一块块的选择自己要撤销的内容

    [xxx2]参数说明:
    1. `[path]` or `-- [path]`：这里的path是要撤销的目录或者文件名，如果有该参数(在[xxx1]是`--mixed`或空 的情况下)，则会跳过移动HEAD指针这个操作，直接复制到index，比如`git reset [path]`；如果没有该参数，则不会跳过移动HEAD指针这个操作

    [xxx3]参数说明:
    1. 
### 4 查看
1. 查看工作区状态`git status`
2. 查看提交日志：`git log`
    1. 查看远程的提交日志：`git log [origin]/[master]`，本地很久没有更新过远程仓库的信息了，看到的日志可能就不是最新的，所以在查看之前需要先运行`git fetch `或者`git fetch origin`(待补充)
    2. `git log`默认是按时间顺序排序,但我实测pull下来的时候调用该命令发现并没有按时间顺序排，过了一段时间再去看发现又按时间排了(也可能是我几个提交的用户名密码不一样看错了，待补充)

3. 查看配置文件
    - 查看项目的配置文件`git config --local --list`
    - 查看用户的配置文件`git config --global --list`
    - 查看系统的配置文件`git config --system --list`

    上面的三个命令似乎只能显示自己额外设置的配置,对于git本身的一些配置不会显示.要想显示用`git config --list`.(待补充)

4. 查看远程信息
    - 查看关联的仓库`git remote -v`

### 4. git pull = git fetch +merge

### 5 配置
#### Git仓库的配制文件
Git共有三个级别的config文件，分别是system、global和local:
1. .git/config：指定仓库配置（特定于某个仓库），获取或设置时使用--local参数（或者省去）。
2. ~/.gitconfig：用户级别仓库配置（适用用于特定用户下的所有仓库），获取或设置时使用--global参数。
3. /etc/gitconfig：系统级别仓库配置（适用于所有仓库），获取或设置时使用--system参数。

覆写关系为：小范围覆盖大范围属性；自上到下，作用范围越大。

## 四. 高级
### 1 github
#### 项目操作
- star:作用是收藏
- watch:作用是关注,更新时会收到通知(?)
- fork:可以pull request

#### 文件操作
- raw:在浏览器中以 text/plain 查看原始文件

### 2 本地和远程的关联
1. 本地和远程仓库的关联（本地和远程都建好了仓库）:
    1. 本地和远程关联

        ```bash
        #其中的origin是远程默认的名字，也可以换成其他名字
        git remote add origin https://github.com:xushike/xxx.git
        ```
    2. 查看关联

        ```bash
        #查看关联的远程仓库
        git remote 
        #查看关联仓库xxx的详细信息(包括分之的关联)
        git remote show xxx
        ```

    3. 取消关联:`git remote remove origin`
    4. 注意,每次remove origin再重新关联远程仓库之后,都需要重新推送并关联分支.

2. 分支关联，用了上面的命令只是仓库关联上，还需要把分支关联(tracking)上，这样以后push的时候就可以只输`git push`：
    ```bash
    #关联并且推送(--set-upstream已经不推荐使用了，推荐的是--set-upstream-to和--track,-u也可以?)
    git push -u origin master 或者 git push --track origin master
    #如果只想关联，可以如下使用
    git branch --track local_branch_name origin/remote_branch_name
    ```
### 2 `.gitignore`文件
该文件只要在主目录(?)下就会生效
1. 规则
    - 以斜杠“/”开头表示目录；
    - 以星号“*”通配多个字符；
    - 以问号“?”通配单个字符
    - 以方括号“[]”包含单个字符的匹配列表；
    - 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；

    此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

## 五 经验
### 1 推送的正确做法
1. 先commit
2. 然后pull(如果没有commit就pull，当pull和本地修改的文件冲突时会提示“和本地文件有冲突，需要先commit”，此时先commit然后pull),
3. 如果pull后文件冲突，需要解决冲突
4. 然后push

## 六 问题
### 1 已解决
1. git pull 时`cannot lock ref ...`

    1. 第一种可能:就是我经常遇到的,网络或者什么不太重要原因,会出现这个,再git pull一下就好了.
    

### 2 未解决
1. git clone时用什么命令或软件可以显示进度？
2. git 可以只clone分支而不是master吗？
3. 写到一半，要切换到另外一个分支怎么弄？
4. win7 64位旗舰版下使用git reset --hard HEAD^无法恢复到上个版本
网友的回答是:
    >你用的shell把^当做换行转义了, 类似于`\`;
    使用"包起来即可, 如:
    `git reset --hard "HEAD^"`
    也可以用~代替, 如:
    `git reset --hard HEAD~1`
5. unknown revision or path not in the working tree.
我是自己新建的仓库，然后直接add了一些文件，并没有commit，然后调用`git reset HEAD`命令出现的这个错。后面了解了git三棵树和该命令原理之后明白了：是因为初始化后没有commit,HEAD就是空的，所以无法移动HEAD指针。这种情况下，可以直接`git reset [path]`，因为这个命令可以跳过"移动HEAD指针"这一步，直接把HEAD复制到index
6. 关于HEAD和分支指针的那张图片，一目了然

7. LF will be replaced by CRLF
8. git是如何判断冲突和不冲突的，界限在哪儿？
9. 在maste分支上写了东西，然后想提交到develop分支上
10. 切换关联的远程分支
11. git的feature
12. github的提交请求是怎么操作 
13.  --global              使用全局配置文件
    --system              使用系统级配置文件
    --local               使用仓库级配置文件

14. 为什么我 mac上的git config user.name等没有配置但是不输入密码 就可以提交，因为sshkey？ 
15. 可以绑定多个远程仓库吗？
16. Pull Request 的命令行管理:[http://www.ruanyifeng.com/blog/2017/07/pull_request.html](http://www.ruanyifeng.com/blog/2017/07/pull_request.html)

17. ip前的git和https有什么区别
18. git移除remote再重新添加，然后识别好像就有点问题，指令能够正常使用，vscode的状态看不了了。
19. git提交多了会导致变慢吗?
20. global和本地都配置了,则优先使用的哪个?
21. 网友的文章:[https://segmentfault.com/a/1190000011168654](https://segmentfault.com/a/1190000011168654)
22. git的分支合并等操作
23. 笔记
    1. [Pro Git（中文版）](https://git.oschina.net/progit/)

24. git hook
25. merge的时候,保存信息时不知道怎么操作,最后出现`Merge made by the 'recursive' strategy.`