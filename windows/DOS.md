# DOS

# 一 概述
DOS和命令行相关

# 二 安装配置

## N 配置和使用
windows terminal:
1. 安装：从应用商店安装

powershell:
1. 设置以管理员身份启动
    1. 右键快捷方式 -> 高级 -> 勾选"以管理员身份运行"
2. 查看版本`$PSVersionTable`
3. 管道
    1. 几个变量
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

# 三 基础(命令)
# 1 文件和目录操作
1. `cd`，路径分隔使用正反斜杠都行

    ```
    # 例子1
    cd C:\Users\xxx\scoop\persist\mysql
    ```
2. 查找
    1. `find`:not work in powershell
    2. `findstr`

## 2 网络相关
### 2.1 tracert

## 3 服务管理
1. `net`
    1. 启动服务`net start service_name`，不带`service_name`的话是列出所有已启动的服务
2. `sc`：在命令在cmd中可以直接执行，如果是powershell，需要用`sc.exe`代替，因为在powershell中sc is an alias to Set-Content.
    1. 列出服务

        ```bash
        # 列出所有服务
        sc.exe query state=all
        # 查看所有未启动服务
        sc query state=inactive
        ```
3. powershell
    1. 列出服务`Get-Service`

# 四 运行程序
1. `osk`虚拟键盘
2. `msconfig`打开system configuration，里面可以配置启动项，服务等。