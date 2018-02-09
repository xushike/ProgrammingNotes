# 2.svn

## 一 概述
### 1 简介
没有git的时候可能觉得不错,但是用了git之后感觉SVN真的该退休了.

## 二 安装配置
### 1 win
1. 下载服务器端SVN

    [http://subversion.apache.org/packages.html](http://subversion.apache.org/packages.html),找到VisualSVN,点进去可以看到好几个,推荐只装VisualSVN Server:
    - VisualSVN Server:服务端

        1. 安装时`Location`是VisualSVN Server的安装目录,`Repositorys`是指定你的版本库目录.`Server Port`指定一个端口,`Use secure connection`勾山表示使用安全连接
        2. 在VisualSVN Server Manager中右键Repositores选择新建Repository
        3. 右键Users选择Create User
        4. 右键Groups选择Create Group,然后将刚才的User加进去(?)
        5. 然后设置Repository的Security,赋予用户权限
    - Apache Subversion command line tools
    - VisualSVN for Visual Studio 2017
    - VisualSVN Repository Configurator

2. 下载客户端SVN(svn小乌龟)

    搜TortoiseSVN就能找到官网下载,安装过程注意有一步是选择关闭所有应用,我手贱点了,然后电脑开始关机了.安装完成后右键能看到SVN...就对了.

## 三 基础
### 1 最重要的几个概念
- `checkout`:将SVN仓库的代码烤到本地
- `update`:从服务器端拉取代码,更新代码
- `commit`:推送代码.记得先update再commit
- 日常操作
    1. add
    2. delete
        - 如果被删除的文件还未入版本库，则可以直接使用操作系统的删除操作删除该文件。
        - 如果被删除的文件已入版本库，则删除的方法如下

            选择被删除文件，右键svn菜单执行”delete”操作，然后选择被删除文件的父目录，右键svn菜单执行”SVN Commit”.使用操作系统的删除操作删除该文件，然后选择被删除文件的父目录，右键svn菜单执行”SVN Commit”,在变更列表中选择被删除的文件。
    3. Rename
    4. SVN还原(SVN Revert)

        右击想要回退的文件或者文件夹，在TortoiseSVN弹出菜单中选择”Update to reversion…” 然后会弹出一个窗口,比如说我们要回退到第10个版本只需要在Revision中填写相应的版本号，然后点击ok即可。
    5. 检查更新(Check for modifications)

        所有的变化都能看到

    6. 其他...

- `.svn`:工作文件的基准版本和一个本地副本最后更新的时间戳，千万不要手动修改或者删除这个.svn隐藏目录和里面的文件!!,否则将会导致你本地的工作拷贝(静态试图)被破坏
- 图标
    - 绿色勾:状态正常
    - 红色叹号:文件被编辑过
    - 黄色叹号:有冲突

## 六 问题