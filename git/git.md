# git
[TOC]
## 一. 概述
git开源免费的分布式版本控制系统。
### 1.git的一些常识
1. git的官方中文book[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)
### 2.三棵树
官方参考资料:[https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset)
## 二. 安装配置
### 1. windows下的安装
1. 下载git for windows
2. 安装过程大同小异，注意设置git环境的时候选择第二项"use git from the windows command prompt"，如果选第一项就不能在cmd中使用git，要自己去配置path。自己配置的时候添git安装目录下的bin目录或者cmd目录都可以
3. 安装完之后记得配置global username和useremail，这两样就是提交时需要记录的名字和邮箱，这样才可以提交到本地仓库；然后就是推送，如果是需要登录的服务器(github等)推送的时候还需要输入账号密码

    ```bash
    #注意没配置的话会报错:unable to auto-detect email address
    #查看所有配置
    git congfig -l #mac
    #查看git user.name和email
    git config user.name
    git config user.email
    #配置全局的git user.name和email
    git config --global user.name "xxx"
    git config --global user.email "xxx"
    ```
为每个项目单独配置:(待补充)
4. 关于ssh Key,（待补充）
5. 关于git自身的更新：
### 2. mac下的几种安装
#### 2.1 最简单的是用Xcode的Command Line Tools
#### 2.1 用Homebrew安装
#### 2.3 在[https://git-scm.com/download/mac](https://git-scm.com/download/mac)下载安装
### 3. linux下的安装
## 三. 基础
### 1. 初始化仓库
1. 如果在Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文  
2. 注意初始化之后本地是没有分支的，这个时候`git branch`为空，只有第一次commit之后才会有分支，而且只有有分支之后才能和远程仓库关联。
### 2. 添加跟踪(放入暂存区)和修改  
1. `git add [被跟踪的文件名]`:用于把文件放入暂存区(放入暂存区的文件会被关联)，如果文件暂存后又被修改了，需要再次暂存然后提交。参数说明：
    1. `-u`:暂存所有已关联的文件(新建的文件不受影响)
    2. `-f`:如果想暂存的文件被ignore了，加上该命令可以强制暂存
### 2. 撤销更改
理解这几个命令之前最好先了解git的三棵树。
1. `git reset [xxx1] [xxx2] [xxx3]`:
    [xxx1]参数说明:
    1. 
    4. `--patch`：一块块的选择自己要撤销的内容

    [xxx2]参数说明:
    1. `[path]` or `-- [path]`：这里的path是要撤销的目录或者文件名，如果有该参数(在[xxx1]是`--mixed`或空 的情况下)，则会跳过移动HEAD指针这个操作，直接复制到index，比如`git reset [path]`；如果没有该参数，则不会跳过移动HEAD指针这个操作

    [xxx3]参数说明:
    1. 
### 3. 查看状态和历史
1. `git status`
2. 查看提交日志：`git log`，查看远程的提交日志：`git log [origin]/[master]`，本地很久没有更新过远程仓库的信息了，看到的日志可能就不是最新的，所以在查看之前需要先运行`git fetch `或者`git fetch origin`(待补充)
    1. `git log`默认是按时间顺序排序,但我实测pull下来的时候调用该命令发现并没有按时间顺序排，过了一段时间再去看发现又按时间排了(也可能是我几个提交的用户名密码不一样看错了，待补充)
### 4. git pull = git fetch +merge

## 四. 高级
### 1. 本地和远程的关联
1. 本地和远程仓库的关联（本地和远程都建好了仓库）:
    1. 本地和远程关联

        ```bash
        #sshkey的方式，其中的origin是远程默认的名字，也可以换成其他名字(不是必须跟项目名一样)
        git remote add origin https://github.com:xushike/xxx.git
        #或者https的方式（待补充）
        ...
        ```
    2. 查看关联

        ```bash
        #查看关联的远程仓库
        git remote 
        #查看关联仓库xxx的详细信息(包括分之的关联)
        git remote show xxx
        ```

    3. 取消关联:`git remote remove origin`

2. 分支关联，用了上面的命令只是仓库关联上，还需要把分支关联(tracking)上，这样以后push的时候就可以只输`git push`：
    ```bash
    #关联并且推送(--set-upstream已经不推荐使用了，推荐的是--set-upstream-to和--track,-u也可以?)
    git push -u origin master 或者 git push --track origin master
    #如果只想关联，可以如下使用(远程分支前是/还是空格?)
    git branch --track my_local_branch_name origin my_remote_branch_name
    ```
### 2. 仓库基本文件
#### 1. .gitignore文件
该文件只要在主目录(?)下就会生效
1. 规则
    >以斜杠“/”开头表示目录；
    以星号“*”通配多个字符；
    以问号“?”通配单个字符
    以方括号“[]”包含单个字符的匹配列表；
    以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；

    此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；


## 五. 使用经验
### 1 推送的正确做法
1. 先commit
2. 然后pull(如果没有commit就pull，当pull和本地修改的文件冲突时会提示“和本地文件有冲突，需要先commit”，此时先commit然后pull),
3. 如果pull后文件冲突，需要解决冲突
4. 然后push
## 六. 问题

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