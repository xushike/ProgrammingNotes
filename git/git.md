# git
[TOC]
## 一 概述
git开源免费的分布式版本控制系统。除了版本,最核心的操作应该都是围绕分支进行的.

### 1 简介
### 2 历史
#### 2.1 为什么需要版本控制
在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容

### 3 常识
#### 3.1 commit id（版本号）
就是commit信息里的那一长串数字,SHA1计算出来的一个非常大的数字，用十六进制表示.

#### 3.2 三棵树
官方参考资料:[https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E7%BD%AE%E6%8F%AD%E5%AF%86#_git_reset)

#### 3.3 git支持多种协议:https,git和ssh
git允许我们用ssh url或者http url来管理代码,两种不同的协议.如果是https,则默认每次都要输入密码,但可以使用git提供的credential helper来存储密码

#### 3.4 凭证助手credential helper(待测试)
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

#### 3.5 ssh-agent
安装了git之后就会有ssh-agent(windows是),ssh-agent 是用于管理SSH private keys的, 长时间持续运行的守护进程（daemon）. 唯一目的就是对解密的私钥进行高速缓存.

#### 3.7 关于HEAD的指向(重点,易错点)
**`HEAD`表示当前版本,即最新的那个commit**,`HEAD~1`(或者`HEAD^`)是上个版本(前一个commit),是当前所在commit的前一个或父commit.以此类推,上上个版本是`HEAD~2`(或`HEAD^^`)...

#### 3.8 git名字来源
作者是linus,他说过他是个自负的混蛋,所有项目都以他的名字命名,先有linux,现在是git.

### 4 文档

### 5 网站
1. git的官方中文book,应该大部分问题都能在上面找到答案,推荐阅读,但是有些内容并不生效(?):[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)

## 二 安装配置
### 1 win
#### 1.1 安装
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

#### 1.2 配置ssh Key(可选)
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

#### 1.3 git自身的更新(待补充)

### 2 mac
#### 2.1 方式一(最简单):用Xcode的Command Line Tools
#### 2.2 方式二:Homebrew安装
#### 2.3 方式三:在[https://git-scm.com/download/mac](https://git-scm.com/download/mac)下载安装

### 3 linux
#### 3.1 未整理
1. linux下ssh-agent的全局配置文件是`/etc/ssh/ssh_config`?
2. linux下启动命令是:eval `ssh-agent`?

### 4 配置
#### 4.1 Git仓库的配制文件
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

## 三 基础
### 1 开始
#### 1.1 `git init`:初始化仓库
如果在Windows系统，请确保目录名（包括父目录）不包含中文  

注意初始化之后本地是没有分支的，这个时候`git branch`为空，只有第一次commit之后才会有分支，而且只有有分支之后才能和远程仓库关联。

#### 1.2 `git clone`:克隆仓库
克隆后默认只有master分支,此时需要执行拉取命令,获取远程仓库的所有最新分支

`git clone <远程仓库地址> [本地仓库名称]`:克隆同时放到新建的`[本地仓库名称]`文件夹中.

#### 1.3 `git remote`:远程仓库相关
查看远程仓库:
- `git remote -v`:查看所有关联的远程仓库的名称和地址(拉取和推送)
- `git remote show <远程仓库名>`:查看远程仓库详细信息,包括:
    * 哪些远程分支没有同步到本地
    * 哪些已同步到本地的远端分支在远端服务器上已被删除
    * 拉取和推送关联的分支

添加到新的远程仓库:`git remote add <远程仓库名> <远程仓库地址>`

可以设置多个远程仓库,拉取的时候指定仓库和分支名就行了,如`git pull <远程仓库名> <分支名>`

重命名远程仓库:`git remote rename <原名称> <新名称>`
删除远程仓库:`git remote rm <远端别名>`

### 2 查看
#### 2.1 `git status`:检查更新和工作区状态

#### 2.2 `git log`:查看提交日志
查看远程的提交日志：`git log [origin]/[master]`，本地很久没有更新过远程仓库的信息了，看到的日志可能就不是最新的，所以在查看之前需要先运行`git fetch `或者`git fetch origin`(待补充)

参数说明:
- `--oneline --graph --decorate --all`:查看所有的提交
- `--pretty=oneline`:只看commit的`-m`信息

#### 2.3 `git config --list`:查看配置文件
- 查看项目的配置文件`git config --local --list`
- 查看用户的配置文件`git config --global --list`
- 查看系统的配置文件`git config --system --list`

上面的三个命令似乎只能显示自己额外设置的配置,对于git本身的一些配置不会显示.要想显示用`git config --list`.(待补充)

#### 2.5 `git diff`:查看变更(主要用于查看冲突)
`git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式.后面可跟某个文件名,不跟的话就默认列出当前目录的所有更改.

`git diff HEAD`:对比workspace与最后一次commit
`git diff <分支1> <分支2>`:对比差异

#### 2.6 `git show`:查看提交的内容

### 3 拉取
#### 3.1 `git fetch`:抓取远端
会将远程仓库的所有分支都抓取下来,但是需要自己手动去合并

#### 3.1 `git pull`:等于执行`git fetch`和`git merge`
快速合并(fast-forward)

### 4 `git add`添加跟踪(stage,即暂存)
`git add <被跟踪的文件名>`:用于把文件放入暂存区(放入暂存区的文件会被关联)，如果文件暂存后又被修改了，需要再次暂存然后提交。

参数说明：
- `-u`:暂存所有已关联的文件(新建的文件不受影响)
- `-f`:如果想暂存的文件被ignore了，加上该命令可以强制暂存
- `-i`:逐个确认

### 5 `git commit`
作动词时表示做一个版本,作名词表示版本.
最佳实践:请确保在对项目 commit 更改时，使用短小的 commit。不要进行大量 commit，记录 10 多个文件和数百行代码的更改。最好频繁多次地进行小的 commit，只记录很少数量的文件和代码更改。

参数说明:
- `--amend`:与上次commit合并

#### 5.1 `git rebase`:压制
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

### 6 `git push`:推送
如果在推送的同一时刻有其他人也在推,那么自己的推送就会被驳回,需要先合并别人的更新再推送

参数说明:
- `-f`:用于强制推送,比如本地进行过压制操作,可能导致远程服务器上有本地没有的commit此时普通的push会被拒绝,需要加上该参数.
    
### 7 `git reset`:撤销更改(难点)
理解这几个命令之前最好先了解git的三棵树。
1. `git reset [xxx1] [xxx2] [xxx3]`:
    [xxx1]参数说明:
    1. 
    4. `--patch`：一块块的选择自己要撤销的内容

    [xxx2]参数说明:
    1. `[path]` or `-- [path]`：这里的path是要撤销的目录或者文件名，如果有该参数(在[xxx1]是`--mixed`或空 的情况下)，则会跳过移动HEAD指针这个操作，直接复制到index，比如`git reset [path]`；如果没有该参数，则不会跳过移动HEAD指针这个操作

    [xxx3]参数说明:

### 8 `git branch`:分支管理(重点)
Git鼓励大量使用分支,分支可以说是git最核心的内容了.因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
#### 8.0 未整理
1. 工作区的修改和分支不绑定?意思我当前分支有10个修改,创建新分支并push之后,再切回来这10个修改就没了,
2. git add是暂存吗
3. git log是显示所有分支的记录?
4. git add和stash的区别
5. git stash不会缓存新建的文件或二进制文件?
#### 8.1 创建分支
查看分支:`git branch`,列出本地的所有分支,在当前分支前面会有一个星号

新建分支:`git branch <分支名>`:通过复制当前分支的所有commit来生成一个新分支,不会复制工作区的文件

创建并切换分支:`git checkout -b <分支名>`,等于执行`git branch <分支名>`加`git checkout <分支名>`

更新远程

#### 8.2 切换分支
切换分支:`git checkout xxx`

#### 8.3 缓存修改(常用)
当某个分支改到一半需要切换到另一个分支时,有两种解决方法:commit和stash,如果没改完,更推荐使用stash的方式.

创建缓存:`git stash`会将上一个commit之后的所有内容缓存起来并生成一个hash版本值,或者使用`git stash save “修改的信息"`缓存版本,其中"修改的信息"就是版本值.

查看缓存:使用`git stash list`可以查看缓存版本信息.

恢复缓存:然后使用`git stash pop`可以从最新的缓存版本恢复,有多个缓存版本时使用`git stash apply stash@{0}`指定版本中恢复.注意缓存是不区别分支的,也就是可以恢复到任何分支上,所以分支很多时的最佳实践是缓存时带上当前分支的信息.

#### 8.3 删除分支
不能删除当前分支,所以要删除的时候需要先切换到其他分支.

删除分支:`git branch -d <分支名>`

只删除远程的分支:....

同时操作本地和远程的分支:...

#### 8.4 合并分支
合并目标分支到当前分支:`git merge <分支名>`,默认是快进模式(Fast-forward)

#### 8.5 分支命名
大概围绕以下几种来命名

![](../picture/git/git-branch-name.jpg)

- master:主分支
- hotfix:热修复
- release:发布分支
- develop:开发
- feature:功能分支

### 9 多人协作
1. 查看每位贡献者的commit统计`git shortlog`:会显示commit数量和信息,按作者排序
    1. 参数`--author="[user_name]"`:根据名字筛选
2. 根据commit来筛选:
    1. 形如`git show 5966b66`
    2. 形如`git log --grep=bug`:搜索的方式来查找,注意如果写成不含等号的,如`git log --grep "fort"`,则Git 将显示顺序包含字符 f、o、r、t 的 commit.
3. README

    最后，如果你添加的任何代码更改会使项目发生极大的变化，则应更新 README 文件以向其他人说明此更改。
4. pull request




### 10 不常用命令
1. `fsck`:文件系统检测


## 四. 高级
### 1 github
#### 1.1 项目操作
- star:作用是收藏,不会看到项目的实时更新
- watch:作用是关注,更新时会收到通知
- fork:将项目复制一份到自己账户,会显示"forked from ...",然后可以对自己的项目进行各种修改.最佳实践是新建一个分支(通常称为特性分支)再修改.

    注意git是没有`fork`这个命令的,

#### 1.2 文件操作
- raw:在浏览器中以 text/plain 查看原始文件

#### 1.3 Issue
Issues（问题）"并不代表实际存在错误，它可以是需要对项目进行的任何改变。GitHub 的问题跟踪器相当高级。每个问题都可以：
- 应用一个或多个标签
- 被分配给个人
- 确定一个里程碑（例如问题将由下一个主要版本解决）
**但问题跟踪器最重要的一个方面在于，每个问题都可以有自己的评论区，使开发者围绕这个问题展开对话。**

Issue 的另一个很棒的功能在于：
- 你可以订阅某个 Issue ，这样你便会获得新评论和代码更改的通知
- 你可以就具体变更与项目维护者持续交流

如果你查看了 Issues 列表，没有看到与你要做的事情类似的内容，那么你可以创建自己的新 Issue

#### 1.4 展示 Demo
GitHub 仓库开通 GitHub Pages 后，其中的 HTML 文件就可以被浏览器正确渲染了，因此这个功能不仅可以作为项目的展示页，也可以展示各种 HTML demo 文件。

#### 1.5 添加 LICENSE
创建项目时，有添加 LICENSE 选项；
创建项目后，添加新文件，输入文件名 LICENSE 时右侧会出现 LICENSE 模板选项。

### 2 本地和远程的关联(待整理)
#### 2.1 本地和远程仓库的关联
如果本地和远程都建好了仓库,则可以:`git remote add origin https://github.com:xushike/xxx.git`来关联,其中的origin是远程默认的名字，也可以换成其他名字.

查看关联仓库的详细信息(包括分支的关联):`git remote show xxx`

取消关联:`git remote remove origin`

注意:每次remove origin再重新关联远程仓库之后,都需要重新推送并关联分支.

#### 2.2 分支关联
用了上面的命令只是仓库关联上，还需要把分支关联(tracking)上，这样以后push的时候就可以只输`git push`：
1.  关联并且推送(--set-upstream已经不推荐使用了，推荐的是--set-upstream-to和--track,-u也可以?):`git push -u origin master` 或者 `git push --track origin master`
2. 如果只想关联，可以使用:`git branch --track local_branch_name origin/remote_branch_name`

#### 2.3 多远程库的关联
常用语种子库或核心库,一般是
```git
git remote add upstream https://github.com/mgechev/angular-seed.git 
git fetch upstream
git merge upstream/master
```

### 3 撤销和回滚(难点)

#### 3.1 未整理
所有没有 commit 的本地改动，都会随着 reset --hard 丢掉，无法恢复。不带`--hard`参数就没事.(?)
参考[廖雪峰的版本回退](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)

#### 3.2 取消本地未push的commit
有三个重要的参数,不同参数影响...,操作后重置后取消暂存的变更

##### 默认参数`mixed`
取消,同时工作区的代码恢复到commit之前的状态，可以直接通过git commit 重新提交对本地代码的修改.形如`git reset [commit_id]`或`git reset HEAD~n`.比如`git reset HEAD`会..

##### 参数`hard`

### 4 git自带的图形界面
#### 4.1 `gitk`
主要用于查看查看历史

如果出现中文乱码,可以修改设置`git config --global gui.encoding utf-8`

#### 4.1 `git gui`
主要用于制作提交

### 5 `.gitignore`文件
该文件只要在主目录(?)下就会生效
1. 规则
    - 以斜杠“/”开头表示目录；
    - 以星号“*”通配多个字符；
    - 以问号“?”通配单个字符
    - 以方括号“[]”包含单个字符的匹配列表；
    - 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；

    此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

### 5 github pages
用来做网站的 

## 五 经验
### 1 已整理
1. Git上手并不难，深入学习还是建议多实践
2. 虽然做了这么多笔记,但是最佳实践还是使用工具,比输命令可靠

### 2 推送的正确做法
1. 先commit
2. 然后pull(如果没有commit就pull，当pull和本地修改的文件冲突时会提示“和本地文件有冲突，需要先commit”，此时先commit然后pull),
3. 如果pull后文件冲突，需要解决冲突
4. 然后push

### 3 .gitkeep
它不是官方git的一部分,而是大家约定成俗的一种习惯.因为linus最开始把git的快照设计成只由文件组成,导致git不跟踪空文件夹(算是设计失误吧),然后想到我们能用假文件来占位,所以就没有改它.

后来大家想跟踪空文件夹,就在里面放一个`.gitkeep`文件,会被解析成占位符.当然,放其他文件(`.nofile`等随意文件)也可以,或者放`.gitignore`文件也可以

## 六 问题
### 1 已解决
#### 1.1 git pull 时`cannot lock ref ...`
1. 第一种可能:就是我经常遇到的,网络或者什么不太重要原因,会出现这个,再git pull一下就好了.

#### 1.2 `git log`未按时间顺序排序?
默认是按时间顺序排序,但我实测pull下来的时候调用该命令发现并没有按时间顺序排，过了一段时间再去看发现又按时间排了(也可能是我几个提交的用户名密码不一样看错了，待补充)


### 2 未解决
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

## 七 待整理
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