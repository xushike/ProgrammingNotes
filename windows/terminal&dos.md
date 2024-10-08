# terminal&DOS


# 一 概述
不仅仅是DOS，还包括所有和命令行相关的

## 3 常识
### 3.1 如果是以管理员身份运行的
再命令行的标题栏会显示出来：标题栏包含"Administrator"或者"管理员"

# 二 安装配置

## N 配置和基本使用
cmd和powershell通用操作(todo)
1. 环境变量名称：都不区分大小写

cmd：
5. 环境变量
    1. 查看环境变量
        1. 查看全部环境变量`set`
        2. 查看指定环境变量`set env_name`,比如`set goroot`,`set GOROOT`(不区分大小写)
    1. 编辑环境变量：分为临时设置(只对当前cmd窗口有效)和持久化设置
        1. 临时设置(只对当前cmd窗口有效)
            1. 设置为空`set env_name=`
            1. 新增或覆盖之前的环境变量`set env_name=value`，比如`set temp="c:\temp"`
            3. 追加到之前的环境变量`set env_name=%env_name%;value`，比如`set path=%path%;c:\temp`
        2. 持久化设置：有两种方法
            1. 我的电脑 -> 右键属性 -> 高级 -> 环境变量
            2. 修改注册表
            3. 函数调用
    2. 使用环境变量`%env_name%`

        ```bash
        # 打印环境变量
        echo %USERPROFILE%
        # 在路径中使用环境变量 %env_name%
        cd $env:USERPROFILE
        ```
6. 清屏:`cls`or`clear`

powershell:
1. 设置以管理员身份启动
    1. 右键快捷方式 -> 高级 -> 勾选"以管理员身份运行"
2. 自动补全:比如输入`get-ch`按tab键会自动补全成`Get-ChildItem`,`remove-it`自动补全成`Remove-Item`
3. 查看版本`$PSVersionTable`
4. 管道
    1. 几个操作符
        1. `&&`和`||`：v7.0以下的版本不支持`&&`和`||`
        2. `$$`表示前一个执行指令的最后一部分
        3. `$^`表示前一个执行指令的第一部分
        4. `$?`表示前一个指令执行的结果，成功了将是True,失败了将是False
            
            ```bash
            Get-ChildItem -path "c:\windows\" -Filter "*.log"
            $$ # 返回是*.log
            $^ # 返回是Get-ChildItem
            ```
        5. `;`和linux的`;`效果一样：顺序执行,不管command1执行是否成功,command2都会执行。配合`$?`可以达到`&&`和`||`的效果

            ```bash
            # 实现linux &&的管道操作
            command1; if ($?) {command2}
            # 比如
            docker build . -t bridge;if($?) {docker run -p 8081:8081 --env-file .env.local bridge}
            ```
5. 环境变量：实测发现`env:env_name`是环境变量本身，`$env:env_name`是对环境变量值的引用，比如`ls env:USERPROFILE`只是列出环境变量的值，而`ls $env:USERPROFILE`是列出所在目录下的文件。
    1. 查看环境变量
        1. 查看全部环境变量
            1. `Get-ChildItem env:`(冒号不能省略)
            2. `ls env:`
        2. 查看环境变量
            1. 查看指定环境变量`$env:env_name`,比如`$env:USERPROFILE`
            2. 搜索环境变量`ls env:env_name`

                ```bash
                # 模糊搜索java开头的环境变量
                ls env:java*
                ```
    1. 编辑环境变量分为临时设置(只对当前powershell窗口有效)和持久化设置
        1. 临时设置(只对当前powershell窗口有效)
            1. 设置为空`$env:env_name=`
            1. 新增或覆盖之前的环境变量`$env:env_name=value`
            3. 追加到之前的环境变量`$env:env_name+=";value"`，比如`$env:Path+=";C:temp"`
            4. 删除`del env:env_name`
        2. 持久化设置
            1. 我的电脑 -> 右键属性 -> 高级 -> 环境变量
            2. 函数调用
    2. 使用环境变量`$env:env_name`

        ```bash
        # 打印环境变量
        echo $env:USERPROFILE # 通常显示 C:\Users\<UserName>
        #在路径中使用环境变量 
        cd $env:USERPROFILE
        ```
6. 清屏:`cls`,`clear`or`ctrl+l`

windows terminal: 主要功能包括多选项卡、窗格、Unicode/UTF-8字符支持、GPU加速文本渲染引擎，运行速度更快，自定义主题、样式和配置等。
1. 参考：https://learn.microsoft.com/zh-cn/windows/terminal/install

# 三 基础
## 0 架构
powershell的Verb-Noun

查看某个命令的用法
1. `help cmd_name`
2. `cmd_name /?`

## 1 文件和目录操作
### 1.1 查看和查找
1. 目录和文件
    1. `dir`
    2. `tree`:快速梳理目录结构、掌握文件信息。
        1. 不带参数直接使用：以树状结构显示当前文件夹及所有后续文件夹
        2. 常见参数
            1. `/f`：同时显示每个文件夹里文件的名称(带扩展名)
            2. `/a`：使用ASCII码字符，而不是用扩展字符
        3. 常见用法
            
            ```bash
            # 指定目录查找指定文件（能用但显示结果不友好，不推荐这么使用）
            tree a: /f /a | findstr "WinNTSetup.exe" 
            # 导出当前目录的文件夹/文件的目录树到tree.txt文件中
            tree /f >tree.txt
            ```
2. 查看文件内容
    1. 在powershell中：`Get-Content`（alias `gc`, `cat` and `type`）
2. 文本
    1. `find`:not work in powershell
    2. `findstr`
5. 查找可执行文件的位置
    1. 在cmd中：`where.exe`(也可以直接`where`)

        ```bash
        where.exe go
        C:\Program Files\Go\bin\go.exe
        ```
    2. 在powershell中:`where.exe`,`get-command`和`gcm`(是`get-command`的别名)，直接输入`where`的话优先匹配的是`Where-Object`命令而不是`where.exe`，默认不区分大小写和扩展名

        ```bash
        # 使用where.exe在c盘查找"git"
        where.exe /R c:\ "git"
        # gcm
        gcm go
        CommandType     Name                                               Version    Source
        -----------     ----                                               -------    ------
        Application     go.exe                                             0.0.0.0    C:\Program Files\Go\bin\go.exe
        ```
3. 用资源管理器打开当前路径
    1. cmd和powershell公用
        1. `explorer .`
        1. `start .`
    2. powershell
        1. `ii .`

### 1.2 其他
1. `cd`，路径分隔使用正反斜杠都行

    ```
    # 例子1
    cd C:\Users\xxx\scoop\persist\mysql
    ```
4. 删除文件夹或文件
    1. cmd
        1. `rd`


## 2 网络相关
### 2.1 tracert
### 2.2 netstat 
显示与IP、TCP、UDP和ICMP协议相关的统计数据,一般用于检验本机各端口的网络连接情况

使用：
1. 参数
    1. `-a`或`–all` 显示所有连线中的Socket。
    2. `-n`或`–numeric` 直接使用IP地址，而不通过域名服务器。


```bash
# 执行netstat -na的显示结果示例
协议 本地地址 外部地址 状态
TCP    127.0.0.1:58046        127.0.0.1:58047        ESTABLISHED
TCP    172.20.40.1:4860        117.187.236.212:4860        SYN_RECEIVED # 172.20.40.1:4860是局域网地址和端口，117.187.236.212:4860是对外的IP和端口
UDP    [fe80::2de0:2709:cb2f:d7a8%3]:1900  *:*
```

## 3 服务管理
1. `net`
    1. 启动服务`net start service_name`，不带`service_name`的话是列出所有已启动的服务
2. `sc`：在命令在cmd中可以直接执行，如果是powershell，需要用`sc.exe`代替，因为在powershell中sc is an alias to Set-Content.
    1. 列出服务

        ```bash
        # 列出所有服务
        sc.exe query state=all
        # 查看所有未启动服务
        sc.exe query state=inactive
        ```
    2. 卸载服务`sc delete service_name`
3. powershell
    1. 列出服务`Get-Service`

## 4 进程管理
1. `tasklist`:用来显示运行在本地或远程计算机上的所有进程的命令行工具，可以根据进程ID或image_name来结束进程
    1. 使用
        1. 直接使用：列出本机所有的进程信息，显示结果由五部分组成：图像名（进程名）、PID、会话名、会话＃、内存使用。
    2. 筛选器`/FI`:使用筛选器查找指定的进程
        
        ```bash
        # 
        TASKLIST    /FI     "USERNAME ne NT AUTHORITY\SYSTEM"      /FI "STATUS eq running"
        # 搜索内存占用大于指定值的进程
        TASKLIST    /FI     "MEMUSAGE gt 10240"
        # 查找goland64.exe
        TASKLIST    /FI     "IMAGENAME eq goland64.exe"
        # 查找名称包含go的进程
        tasklist | findstr "go"
        ```
2. `taskkill`:kill 进程
    1. 使用
        1. `/PID processid`    指定要终止的进程的 PID
        2. `/F`指定强制终止进程
        3. `/T`终止指定的进程和由它启用的子进程


## n 其他
1. `curl`：在powershell中，curl为 ps 原生命令 Invoke-WebRequest的别名，如果想使用linux的curl，需要用`curl.exe`

# 四 运行程序
1. `osk`虚拟键盘
2. `msconfig`打开system configuration，里面可以配置启动项，服务等。

# 五 脚本
运行一个自定义脚本的步骤 todo
1. xxx
2. 修改执行策略

    ```bash
    # 查看当前执行策略
    Get-ExecutionPolicy # RemoteSigned
    # 修改当前执行策略
    Set-ExecutionPolicy Unrestricted
    ```
3. 终端中通过键入脚本的路径（相对or绝对路径皆可）来执行脚本