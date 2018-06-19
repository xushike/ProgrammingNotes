# git
[TOC]
# 一 概述
git开源免费的分布式版本控制系统。除了版本,最核心的操作应该都是围绕分支进行的.

## 1 简介
## 2 历史
### 2.1 为什么需要版本控制
在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容

## 3 常识
### 3.1 commit id（版本号）
就是commit信息里的那一长串数字,SHA1计算出来的一个非常大的数字，用十六进制表示.

### 3.2 三棵树
官方参考资料:[https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset)

从git的官方中文book来看,三棵树是:工作目录(Working Directory,似乎对应我们说的工作区work space),暂存区(Index)和HEAD(当前分支所在的commit).感觉这三个的名字跟我之前理解的不太一样,暂时还是以官网的为准吧.

### 3.3 git支持多种协议:https,git和ssh
git允许我们用ssh url或者http url来管理代码,两种不同的协议.如果是https,则默认每次都要输入密码,但可以使用git提供的credential helper来存储密码

### 3.4 凭证助手credential helper(待测试)
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

取消设置凭证助手命令形如:`git config --<级别,如system> --unset credential.helper`


### 3.5 ssh-agent
安装了git之后就会有ssh-agent(windows是),ssh-agent 是用于管理SSH private keys的, 长时间持续运行的守护进程（daemon）. 唯一目的就是对解密的私钥进行高速缓存.

### 3.7 关于HEAD的指向(重点,易错点)
**HEAD表示当前版本,即最近的那个commit**,`HEAD~1`(或者`HEAD^`)是上个版本(前一个commit),是当前所在commit的前一个或父commit.以此类推,上上个版本是`HEAD~2`(或`HEAD^^`)...

### 3.8 git名字来源
作者是linus,他说过他是个自负的混蛋,所有项目都以他的名字命名,先有linux,现在是git.

### 3.9 git命令弹出的shell
似乎跟系统的shell有关,本人用vim的使用方式去使用暂时没发现什么问题(待补充).

## 4 文档

## 5 网站
1. git的官方中文book,应该大部分问题都能在上面找到答案,推荐阅读,但是有些内容并不生效(?):[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)

# 二 安装配置
## 1 win
### 1.1 安装
1. 下载git for windows
2. 安装过程大同小异，注意设置git环境的时候选择第二项"use git from the windows command prompt"，如果选第一项就不能在cmd中使用git，要自己去配置path。自己配置的时候添git安装目录下的bin目录或者cmd目录都可以
3. 安装完之后记得配置global username和useremail，这两样就是提交时需要记录的名字和邮箱，这样才可以提交到本地仓库；然后就是推送，如果是需要登录的服务器(github等)推送的时候还需要输入账号密码

    ```bash
    #注意没配置的话会报错:unable to auto-detect email address
    #查看git的user.name和email
    git config user.name
    git config user.email
    #配置用户级的git user.name和email
    git config --global user.name "<用户名>"
    git config --global user.email "<邮箱>"
    ```
    为每个项目单独配置:(待补充)

### 1.2 配置ssh Key(可选)
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

### 1.3 git自身的更新(待补充)

## 2 mac
### 2.1 方式一(最简单):用Xcode的Command Line Tools
### 2.2 方式二:Homebrew安装
### 2.3 方式三:在[https://git-scm.com/download/mac](https://git-scm.com/download/mac)下载安装

## 3 linux
### 3.1 未整理
1. linux下ssh-agent的全局配置文件是`/etc/ssh/ssh_config`?
2. linux下启动命令是:eval `ssh-agent`?

## 4 配置
### 4.1 Git仓库的配制文件
Git共有三个级别的config文件，分别是system、global和local:
1. .git/config：指定仓库配置（特定于某个仓库），获取或设置时使用--local参数（或者省去）。
2. ~/.gitconfig：用户级别仓库配置（适用用于特定用户下的所有仓库），获取或设置时使用--global参数。
3. /etc/gitconfig：系统级别仓库配置（适用于所有仓库），获取或设置时使用--system参数。

覆写关系为：自上到下，作用范围越大;小范围优先级高于大范围。

打开一个配置文件,大概长这个样子:
```
[user] 
name = John Smith
email = john@example.com
[alias]
st = status
co = checkout
br = branch
up = rebase
ci = commit
[core]
editor = vim
```

修改配置的命令形如:`git config --global alias.st status`

# 三 基础
## 1 开始
### 1.1 `git init`:初始化仓库
官网说的初始化命令默认会创建master分支,但实践发现,在第一次commit之前很多命令都报错(比如`git branch`,`git checkout`,远程仓库的命令等),所以最佳实践是第一次commit之后再去操作分支和远程仓库。

注意:如果在Windows系统，请确保目录名（包括父目录）不包含中文

### 1.2 `git clone`:克隆仓库
克隆仓库的所有内容,克隆后当前在默认分支(一般是master分支).

使用:`git clone <远程仓库地址> [本地仓库名称]`:克隆,并将库放到`[本地仓库名称]`文件夹中.例子如`git clone https://github.com/xushike/study.git studyNote`

### 1.3 `git remote`:远程仓库相关
查看远程仓库:
- `git remote -v`:查看所有关联的远程仓库的名称和地址(拉取和推送)
- `git remote show <远程仓库名>`:查看远程仓库详细信息,包括:
    * 哪些远程分支没有同步到本地
    * 哪些已同步到本地的远端分支在远端服务器上已被删除
    * 拉取和推送关联的分支

添加到新的远程仓库:`git remote add <远程仓库名> <远程仓库地址>`,多远程库的做法常用于种子库或核心库.

可以设置多个远程仓库,拉取的时候指定仓库和分支名就行了,如`git pull <远程仓库名> <分支名>`

重命名远程仓库:`git remote rename <原名称> <新名称>`

取消远程仓库:`git remote rm <远程仓库名>`,注意每次取消再重新关联远程仓库之后,都需要重新推送并关联分支.

## 2 查看
### 2.1 `git status`:检查更新和工作区状态

### 2.2 `git log`:查看提交日志
直接使用是查看当前分支的本地提交日志.

查看远程分支的提交日志：`git log [origin]/[master]`，本地很久没有更新过远程仓库的信息了，看到的日志可能就不是最新的，所以在查看之前需要先运行`git fetch `或者`git fetch origin`(待补充)

查看具体某个文件的提交日志:`git log -- <文件名>`

参数说明:
- `--oneline --graph --decorate --all`:查看所有的提交
- `--pretty=oneline`:只看commit的`-m`信息

### 2.3 `git config --list`:查看配置文件
- 查看项目的配置文件`git config --local --list`
- 查看用户的配置文件`git config --global --list`
- 查看系统的配置文件`git config --system --list`

上面的三个命令似乎只能显示自己额外设置的配置,对于git本身的一些配置不会显示.要想显示用`git config --list`.它会显示包括上面三个配置在内的所有配置(如果有的话)

### 2.5 `git diff`:查看变更(主要用于查看冲突)
`git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式.后面可跟某个文件名,不跟的话就默认列出当前目录的所有更改.

`git diff HEAD`:对比workspace与最后一次commit
`git diff <分支1> <分支2>`:对比差异

### 2.6 `git show`:查看提交的内容
直接使用是查看当前commit的内容

查看某次commit的内容:`git show <commit id>`

查看某次commit中某个文件的变化:`git show <commit id> <文件名>`

### 2.7 `git <命令名> --help`:查看某个命令的用法,比如`git fetch --help`

### 2.8 `git reflog`:查看关键命令(commit,pull,checkout)的记录

## 3 拉取
### 3.1 `git fetch`:抓取远端
会将指定分支的更新都抓取下来,但是需要自己手动去合并

### 3.1 `git pull`:等于执行`git fetch`和`git merge`
快速合并(fast-forward)

拉取指定分支的更新:`git pull <远程仓库名> <分支名>`,注意拉取这个命令似乎不能像`git push`那样关联.也就是说只有等push命令关联之后才可以使用简化的`git pull`

## 4 `git add`:暂存(stage)
工作目录的文件只有两种状态:已跟踪(tracked)和未跟踪(untracked),加入过暂存的都是已跟踪文件,初次clone后的所有文件都是已跟踪的.

所以暂存有两层意思:对于未跟踪的文件是将其跟踪,对于已跟踪的,是跟踪其最新变动.

`git add <被跟踪的文件名>`:用于把文件放入暂存区,放入过暂存区的文件会被跟踪(tracked),这个跟踪表示会被git管理,而且会被commit以及其他一些命令影响到.

如果文件暂存后又被修改了，需要再次暂存然后提交。

参数说明：
- `-u`:暂存所有已关联的文件(新建的文件不受影响)
- `-f`:如果想暂存的文件被ignore了，加上该命令可以强制暂存
- `-i`:逐个确认

取消暂存:`git reset HEAD <文件名>...`

删除文件并添加到暂存:`git rm <文件名>`,等价于:直接删除文件+添加到暂存(即`git add <文件名>`)

移动或重命名文件并添加到暂存:`git mv <文件名>`,等价于:移动或重命名文件+添加到暂存(即`git add <文件名>`)

`git rm --cached <file_path>`:删除暂存区或分支上的文件, 但本地又需要使用, 只是不希望这个文件被版本控制

## 5 `git commit`
作动词时表示做一个版本,作名词表示版本.
最佳实践:请确保在对项目 commit 更改时，使用短小的 commit。不要进行大量 commit，记录 10 多个文件和数百行代码的更改。最好频繁多次地进行小的 commit，只记录很少数量的文件和代码更改。

参数说明:
- `--amend`:与上次commit合并提交,可修改commit信息,最终只会有一个提交.(很好用)

### 5.1 `git rebase`:压制(衍合)
将 commit结合在一起是一个称为压制(squash)的过程,我的理解就是将多个commit合成一个commit(会生成新的SHA,同时原来的多个就会消失掉),当然该命令是强大且危险的.
也可以在压制前新建一个分支备份下.
1. 比如压制最后的三个commit:`git rebase -i HEAD~3`,参数`-i`表示交互式,推荐加上
2. 交互式参数`p`(`pick`):使 commit 保持原样
2. 交互式参数`r`(`reword`):保留commit的内容，但修改 commit 说明
3. 交互式参数`s`(`squash`):将此 commit 的更改结合到之前的 commit 中（列表中位于其上面的 commit ）
3. 交互式参数`f`(`fixup`):将此 commit 的更改结合到前一个 commit 中，但删除提交说明
3. 交互式参数`x`(`exec`):运行 shell 命令
3. 交互式参数`d`(`drop`):删除 commit

注意,多人合作的情况下,压制**不应包含已push的commit**,因为其他人可能已经pull了你准备压制的commit,如果你再压制,其他人可能需要做非常麻烦的修改才能同步.

问题
1. 暂停commit等的意义是什么
2. 取消`git rebase`事务是用`git rebase –abort`?

## 6 `git push`:推送
默认是推送当前所在的分支.注意如果在推送的同一时刻有其他人也在推,那么自己的推送就会被驳回,需要先合并别人的更新再推送.

参数说明:
- `-f`:用于强制推送,比如本地进行过压制操作,可能导致远程服务器上有本地没有的commit此时普通的push会被拒绝,需要加上该参数.
    
推送到远程的某个分支(不关联):`git push <远程仓库名> <远程分支名>`,如果远程没有该分支会自动创建.

**关联**:关联了之后拉取和推送可以简化为`git pull`和`git push`,会自动拉取或推送到关联的分支,很方便.现在新分支第一次推送的时候必须手动关联一个远程分支.

- 分支关联:`git branch --track <本地分支名> <远程仓库名>/<远程分支名>`.
- 关联并推送:`git push -u/--track/--set-upstream-to <远程仓库名> <远程分支名>`.

## 7 撤销和回滚(难点)
### 7.1 `git reset`:重置
分为已push和未push两种情况

#### 未push
参数说明:
- `--mixed`(不带参数时的默认参数):
    - `git reset <commit id>`或`git reset <HEAD~n>`:会将HEAD从当前commit指向某个commit,**仅仅重置暂存区**,即丢弃当前暂存区,然后将当前commit到某个commit之间的所有修改移动到暂存区,工作区的内容保持不变
    <!-- 也意味着可以直接`git commit`重新提交对本地代码的修改. -->
    - 也可以作用于单个文件(待测试)
- `--soft`:保留暂存区和工作区,同时将当前commit到某个commit之间的所有修改移动到暂存区

- `--hard`:重置暂存区、工作区及版本库,也就是说工作区和暂存区以及某个commit之后的所有修改都会丢失,慎用!

注意成功执行`git reset`并push后会创建一个新的commit.

`git reset`似乎可以作用于单个文件,如果是作用域单个文件,则HEAD不会移动,其他和上面一样.(待验证)

#### 已push
对于已经push到远程的,调用上面的`reset`命令可以本地回滚,但是push的时候会被拒绝.这个时候就要用`git revert <HEAD~n>`命令.

该命令和`reset`不同的地方在于:`revert`不是让指针移回去,而是新增一个表示撤销的commit,该commit的内容是对`<HEAD~n>`的撤销.

### 7.2 丢弃(discard)工作区的修改:`git checkout -- <文件名>`
会将文件工作区的修改全部丢弃(不影响暂存区),慎用!

还有一种情况,就是误删了某个文件,可以用该命令恢复,但是会丢失该文件上所有未提交的修改.

## 8 `git branch`:分支管理(重点)
Git鼓励大量使用分支,分支可以说是git最核心的内容了.因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
### 8.0 未整理
1. 工作区的修改和分支不绑定?意思我当前分支有10个修改,创建新分支并push之后,再切回来这10个修改就没了,
2. git add是暂存吗
3. git log是显示所有分支的记录?
4. git add和stash的区别
5. git stash不会缓存新建的文件或二进制文件?
### 8.1 创建和查看分支
查看分支:`git branch`,列出本地的所有分支,在当前分支前面会有一个星号.注意才clone完之后只会显示默认分支,实际上其他分支还是存在的.

参数说明:
- `-r`:只列出远程分支
- `-a`:列出包含远程在内的所有分支

新建分支:`git branch <分支名>`:通过复制当前分支的所有commit和暂存区来生成一个新分支,不会复制工作区的文件

创建并切换分支:`git checkout -b <分支名>`,等于执行`git branch <分支名>`加`git checkout <分支名>`

更新所有分支:`git remote update [远程分支名]`,会更新远程仓库的所有分支,没用过,感觉可能会有问题,(待研究).

查看所有分支最后一次commit信息:`git branch -v`

### 8.2 切换分支
切换分支:`git checkout xxx`,工作目录会恢复到该分支最后一次提交时的样子(暂存区和工作目录是干净的),如果Git不能干净利落地完成这个任务，它将禁止切换分支。

### 8.3 `git stash`:储藏修改(常用)
当某个分支改到一半需要切换到另一个分支时,有些文件只更改到一半,这个时候有两种解决方法:commit和stash,使用stash最好.注意新增的文件不受影响.

创建储藏:`git stash`会将上一个commit之后的所有已跟踪的内容储藏起来并生成一个hash版本值,或者使用`git stash save <"修改的信息">`储藏版本,其中"修改的信息"就是版本值.

查看储藏:使用`git stash list`可以查看储藏版本信息.

恢复储藏:`git stash apply <储藏的名字>`从指定版本中恢复,如`git stash apply stash@{3}`.注意储藏是不区别分支的,也就是可以恢复到任何分支上,所以分支很多时的最佳实践是储藏时带上当前分支的信息.
恢复(并删除?)最前面的储藏:`git stash pop`.

删除暂存:`git stash drop <储藏的名字>`,比如`git stash drop stash@{0}`

几个有用的变种储藏:
- `git stash --keep-index`:不储藏暂存区的内容
- `git stash -u`:也会储藏创建的未跟踪文件

### 8.3 删除分支
不能删除当前分支,所以要删除的时候需要先切换到其他分支.

删除分支:`git branch -d <分支名>`;如果想强制删除需要用`git branch -D <分支名>`

只删除远程的分支:`git push origin --delete <远程分支名>`

同时操作本地和远程的分支:...

### 8.4 合并分支
合并目标分支到当前分支:`git merge <分支名>`,默认是快进模式(Fast-forward)

### 8.5 分支命名
大概围绕以下几种来命名

![](../picture/git/git-branch-name.jpg)

- master:主分支
- hotfix:热修复
- release:发布分支
- develop:开发
- feature:功能分支

## 9 多人协作
1. 查看每位贡献者的commit统计`git shortlog`:会显示commit数量和信息,按作者排序
    1. 参数`--author="[user_name]"`:根据名字筛选
2. 根据commit来筛选:
    1. 形如`git show 5966b66`
    2. 形如`git log --grep=bug`:搜索的方式来查找,注意如果写成不含等号的,如`git log --grep "fort"`,则Git 将显示顺序包含字符 f、o、r、t 的 commit.
3. README

    最后，如果你添加的任何代码更改会使项目发生极大的变化，则应更新 README 文件以向其他人说明此更改。
4. pull request

### 9.1 规范
1. 多人协作时，不要各自在自己的 Git 分支开发，然后发文件合并。正确的方法应该是开一个远程分支，然后一起在远程分支里协作。不然，容易出现代码回溯（即别人的代码被覆盖的情况）

## 10 不常用命令
### 10.1 `git fsck`:文件系统检测
`git fsck --lost-found`:找回git add过但是已经不存在文件中的内容(待测试)

# 四. 高级
## 4 git自带的图形界面工具
### 4.1 `gitk`(常用)
主要用于查看查看历史,该工具可能需要自己安装

如果出现中文乱码,可以修改设置`git config --global gui.encoding utf-8`

以图形化的界面显示文件修改记录:`gitk --follow <文件名>`

注意:mac上和liunx需要自己安装,mac可用brew:`brew install gitk`
### 4.1 `git gui`
主要用于制作提交

### 4.3 `git mergetool`
主要用于解决冲突,似乎只有存在冲突文件时才会出现(待测试)

## 5 `.gitignore`文件
**该文件只能作用于 Untracked Files，也就是那些从来没有被 Git 记录过的文件（自添加以后，从未 add 及 commit 过的文件）**

规则:
- 以斜杠“/”开头表示目录；
- 以星号“*”通配多个字符；
- 以问号“?”通配单个字符
- 以方括号“[]”包含单个字符的匹配列表；
- 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；

此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

## 5 github pages
用来做网站的 

# 五 经验
## 1 已整理
1. Git上手并不难，深入学习还是建议多实践
2. 虽然做了这么多笔记,但是最佳实践还是使用工具,比输命令可靠
3. 记住，在 Git 中任何 已提交的 东西几乎总是可以恢复的。--git官方book
4. stackoverflow大牛说的多人合作注意事项:
    - 不要用强制推送
    - 不要破坏commit history和别人的pull

## 2 推送的正确做法
1. 先commit
2. 然后pull(如果没有commit就pull，当pull和本地修改的文件冲突时会提示“和本地文件有冲突，需要先commit”，此时先commit然后pull),
3. 如果pull后文件冲突，需要解决冲突
4. 然后push

## 3 .gitkeep
它不是官方git的一部分,而是大家约定成俗的一种习惯.因为linus最开始把git的快照设计成只由文件组成,导致git不跟踪空文件夹(算是设计失误吧),然后想到反正我们能用假文件来占位,所以最后也没改它.

后来大家想跟踪空文件夹,就在空文件夹里面放一个`.gitkeep`空文件,会被解析成占位符.当然,放其他文件(`.nofile`,`.gitignore`等任意空文件都可以)也可以

# 六 问题
## 1 已解决
### 1.1 git pull 时`cannot lock ref ...`
1. 第一种可能:就是我经常遇到的,网络或者什么不太重要原因,会出现这个,再git pull一下就好了.

### 1.2 `git log`未按时间顺序排序?
默认是按时间顺序排序,但我实测pull下来的时候调用该命令发现并没有按时间顺序排，过了一段时间再去看发现又按时间排了(也可能是我几个提交的用户名密码不一样看错了，待补充)

### 1.3 You have not concluded your merge (MERGE_HEAD exists)
原因可能有多种.我当时大概是先push了一次,然后使用修改了一些文件然后使用`git commit --amend`并且修改了commit信息,然后push,然后pull下来有冲突,然后我合并并且解决了冲突,但这个时候就出问题了,我把解决完的那个文件加入暂存区,结果暂存区里没有那个文件,然后不管执行pull还是push都提示这个错误.重新试了一次还是这样,估计不是冲突的原因,而是`git commit --amend`相关操作出错了.

因为我本地的修改是最新的,可以舍弃远程的,所以先`git push -f`强制推送,然后`git pull`还是报错,于是再执行`git reset HEAD`,就不会再报错了.但是注意此时不能再用`git commit --amend`命令,如果想用的话必须另外push一个新的commit然后再用.

### 1.4 如果你在创建.gitignore文件之前就已经push项目了，那么即时你在.gitignore文件中写入新的规则，这些规则也不会起作用。
如果文件曾经被 Git 记录过，那么.gitignore 就对它们完全无效.

解决方法就是先把本地缓存删除（改变成未track状态），然后再提交,比如
```
git rm -r --cached <文件路径>
git add <文件路径>
git commit -m 'update .gitignore'
```
如果还是不行的话,在先将想要取消追踪的文件移到项目目录外)，并提交，然后提交后再将刚刚移出的文件再移入项目中即可

(该解决办法为测试,但感觉比较靠谱)

### 1.5 unable to get credential storage lock: File exists
我当时出现这个问题可能是因为我配置了凭证助手,但github的账号密码和gitlab的账号密码不一样,所以`git pull`后提示我输入gitlab的密码,我输入之后就出现这个错误.

最后我取消了凭证助手就好了.

### 1.6 Your configuration specifies to merge with the ref 'refs/heads/master' from the remote, but no such ref was fetched.
我当时出现这种情况是github上新建了一个空的项目,然后clone,然后pull就会报这个错

### 1.7 fatal: unable to access 'https://xxx': Empty reply from server
我当时是重装系统后没有配置user.name和user.email出现的这个问题

### 1.8 文件内容没变,但是git显示文件的被修改
因为文件的权限被修改了.可以设置忽略检查文件的权限:`git config core.filemode false`

## 2 未解决
### 2.1 Permission denied (publickey)...
这个问题应该有些复杂(待补充)

临时解决方法是,将git协议换成https协议

### 2.N 其他
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
26. vscode的git没有显示远程有多少个更新的pull是什么情况

# 七 待整理
1. 关于ssh的配置,可参考官方文档:[https://help.github.com/articles/connecting-to-github-with-ssh/](https://help.github.com/articles/connecting-to-github-with-ssh/)
2. 有时项目会对特性分支的命名有特定要求。例如，如果一个分支将要解决错误修复，那么许多项目会要求添加一个 bugfix- 前缀。回到我们处理登录表单错误的分支，它得被命名为 bugfix-login-form。

3. mac上是我github账户下的所有项目的提交都不需要输入账号密码吗?

    原因是什么,为什么win我没配置对?

4. RawGit 作为一个缓存代理，提供的功能是缓存 GitHub 中 raw 文件并添加上正确的 Content-Type header，从而使文件能被浏览器正确渲染。

RawGit 对未开通 GitHub Pages 的项目中的任意 HTML/CSS/JS 文件以及 Gist 代码的渲染展示提供了方便。

使用方法：https://rawgit.com/ 或 https://raw.githack.com/

5. 保存了ssh之后不要了怎么清除?
6. 如何查看其他人提交的更新
7. gitlab的clone需要权限吗
8. feature分支和普通分支的区别是啥?

9. [廖雪峰的git](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840202368c74be33fbd884e71b570f2cc3c0d1dcf000),有空整理完
10. 网友的一些总结,感觉写的不错:[http://classfoo.com/ccby/article/j4HZbSN](http://classfoo.com/ccby/article/j4HZbSN)
