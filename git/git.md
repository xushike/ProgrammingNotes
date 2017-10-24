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
4. 关于ssh Key,（待补充）
### 2. mac下的几种安装
#### 2.1 最简单的是用Xcode的Command Line Tools
#### 2.1 用Homebrew安装
#### 2.3 在[https://git-scm.com/download/mac](https://git-scm.com/download/mac)下载安装
### 3. linux下的安装
## 三. 基础
### 1. 初始化仓库
如果在Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文  
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
2. `git log`
默认是按时间顺序排序,但我新pull下来的时候调用该命令发现并没有按时间顺序排，过了一下午再去看发现又按时间排了
### 4. git pull = git fetch +merge

## 四. 使用
### 1. 本地和远程的关联
1. 本地和远程都建好了库，如果想两者关联上，用下面的命令：
```bash
#sshkey的方式，其中的origin是远程默认的名字，也可以换成其他名字(不是必须跟项目名一样)
git remote add origin git@github.com:xushike/xxx.git
#或者https的方式（待补充）
...
```
2. 用了上面的命令后只是仓库关联上了，还需要把分支关联(tracking)上：
```bash
#这样当前分支就关联并且推送到远程的master分支，以后push的时候就可以只输入简化的git push，而不用加上-u等
git push -u origin master 或者 git push --set-upstream origin master
#如果只想关联，可以用
git branch --set-upstream my_local_branch_name origin/my_remote_branch_name
```
### 2. 仓库基本文件
#### 1. .gitignore文件
该文件只要在主目录下就会生效

## 五. 经验

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


