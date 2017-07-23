## 一. 概述  
## 二. 安装配置
### 1. windows下的安装
1. 下载git for windows
2. 安装过程大同小异，注意设置git环境的时候选择第二项"use git from the windows command prompt"，如果选第一项就不能在cmd中使用git，要自己去配置path。自己配置的时候添git安装目录下的bin目录或者cmd目录都可以
3. 关于ssh Key,安装完之后记得配置global username和useremail，这样才可以提交到远程，如果是github等提交的时候还需要输入账号密码

### 2. mac下的安装
### 3. linux下的安装
## 三. 基础
1. 添加跟踪  
- git add [被跟踪的文件名] 如果文件暂存后又被修改了，需要再次暂存然后提交
2. 查看状态和历史
- git status
- git log
3. git pull = git fetch +merge

## 四. 使用
1. 本地和远程的关联
    1. 本地和远程都建好库，然后在本地
    ```git
    git remote add origin git@github.com:xushike/xxx.git
    ```
    2. 这样仓库就关联上了，然后
    ```git
    git push -u origin master 或者 git push --set-upstream origin master
    ```
    这样本地的这个分支就和远程的master（也可以换成其他分支）关联（tracking ）上了，在git中tracking就意味着可以用简化的命令而不用加上-u等，而且这个push会把代码推送上去，如果只想关联，可以用
    ```git
    git branch --set-upstream my_local_branch_name origin/my_remote_branch_name
    ```
2. 仓库基本文件

## 五. 经验

## 六. 问题

1. git clone时用什么命令或软件可以显示进度？
2. git 可以只clone分支而不是master吗？
3. 写到一半，要切换到另外一个分支怎么弄？

