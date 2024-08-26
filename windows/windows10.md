# windows10
# 一 概述
## 3 常识
### 3.1 快捷键
1. 多桌面切换:`Ctrl+windows键+左右方向键`
2. 截图
    1. 快捷键`win+shift+s`:优点是系统原生支持,缺点是不能编辑,没有像素提示
    2. 利用windows lnk工作区的屏幕草图:优点是可以编辑,缺点是操作有点繁琐.
    3. 快捷键`alt+PrtScn`:截图最前面的窗口
    4. `PrtScn`:直接截取全屏
    5. Edge网页长截图:钢笔(添加笔记)=>剪辑=>拖动可截网页长图
    
## 4 文档视频网址等
1. Windows 10 ISO 映像官方下载地址：https://www.microsoft.com/zh-cn/software-download/windows10ISO

# 三 基础
## 1 工具生态
### shell
1. cmd
2. powershell
3. (推荐)windows terminal
4. fluent terminal: win store直接可以安装

### 分屏
自带的分屏：可以分二分之一或者四分之一，快捷键win+方向。想恢复原窗口大小，从屏幕一角拖离即可。

PowerToys的FancyZones分屏：
1. 使用
    1. 设置布局:快捷键`win+shift+~`。支持多个布局方案，每个布局的区域大小随意调整，且可以重叠
    2. 拖动应用到对应的区域:拖动的时候按住shift键
    3. 恢复原窗口大小：取消贴靠
    4. 替代windows snap
2. 缺点
    1. "记录应用上次分屏的位置"不是对所有应用生效
    2. 分配不是对所有应用都有效

### PowerToys
参考：
1. 官方
    1. https://github.com/microsoft/PowerToys
    2. https://docs.microsoft.com/zh-cn/windows/powertoys/

微软为Windows系统推出的一系列免费实用工具合集(比如分屏--FancyZones窗口增强管理器)。PowerToys早在win95年代就已经推出，更新到了winXP以后就悄无声息了，到了win10时代，微软官方再次重启了这个项目，并将其开源。

优缺点：
1. 优点
    1. 支持第三方集成
    2. 资源占用非常低
2. 缺点
    2. only support win10

主要工具：
3. awake:防止操作系统进入睡眠状态，并提供设置计时器的选项，以便何时可以重新进入睡眠状态
2. 颜色选择器
1. FancyZones窗口增强管理器：分屏神器，见分屏部分笔记
2. Windows Key Shortcut Guide (Win热键快捷键指南)：可以让用户在长按 Windows 键超过 1 秒时，显示出当前桌面状态下可用的快捷键列表。
3. PowerToys Run：类似于anywhere，默认快捷键`alt+空格`
4. 键盘管理器：可以对按键重新映射：也可以把按键映射到`undefined`从而使得按键无效
4. 图片处理：支持一键修改图片尺寸
5. 文件批量重命名

# 四 高级
## 1 windows to go
能将win8和win10装在U盘里跑,根据网友的评价来看,效果还可以

## 2 WSL和WSL2
Windows WSL2和常规虚拟机方式在Windows上运行Linux系统方案的对比：都是使用虚拟化技术，但WSL性能更强、占用资源更少、和Windows共享文件。

相比第一代，新的 WSL2 重新设计了架构，使用真正的 Linux 内核，几乎具有 Linux 的所有完整功能。启用WSL2的 Linux 系统启动时间非常快，内存占用很少，并且，WSL 2 还可以直接原生运行 Docker，VS Code 编辑器还有 Remote-WSL 插件，相对于完整的linux虚拟机只是不支持systemctl、systemd。
1. 参考：https://learn.microsoft.com/zh-cn/windows/wsl/compare-versions

安装使用：
1. 先决条件precondition
    1. 检查Windows版本是否符合要求（略），win+r运行`winver`
    2. 启用必要的功能：控制面板-程序和功能-启用或关闭Windows功能
        1. Hyper-V
        2. 适用于Linux的Windows子系统：如果没打开这个功能就运行发行版，会提示"WslRegisterDistribution failed with error: 0x8004032d"
        3. 虚拟机平台
3. 安装WSL2
    1. 参考：https://learn.microsoft.com/zh-cn/windows/wsl/install#install-wsl-command
    1. 部分重要步骤
        1. `wsl --install`，如果提示无法解析服务器的名称或地址，多半是运营商DNS问题，需要手动修改DNS。正常情况下重启后就会自动安装了。
        1. 查看 Linux 发行版是设置为 WSL 1 还是 WSL 2，请使用命令`wsl -l -v`
        2. 安装适用于Linux的子系统有两种方式，一种是应用商店，另外一种是命令行。
    3. 子系统默认安装位置：貌似是`C:\Users\<UserName>\AppData\Local\Packages\...`
4. ~~WSL2设置~~
    1. 参考：https://learn.microsoft.com/en-us/windows/wsl/wsl-config#per-distribution-configuration-options-with-wslconf
    1. 设置文件权限
    2. 设置完之后需要等子系统完全退出才会生效

        ```bash
        # 退出指定子系统或退出所有子系统
        wsl --terminate <distroName>
        wsl --shutdown
        # 查看仍在运行的子系统。
        wsl --list --running
        ```
4. 打开Linux子系统
    1. 点击开始菜单的快捷方式打开
    2. 在终端输入`wsl`打开默认的Linux子系统
    3. 在终端输入已安装的发行版子系统的名称，如`ubuntu`
5. 在windows的终端里，不进入子系统但以默认的linux发行版子系统运行命令`wsl [command]`
    
    ```bash
    # 在windows的终端中
    # pwd 查看当前windows系统的路径，而 wsl pwd 查看当前目录路径在 WSL 中的装载位置
    # 又比如git --version查看windows系统中git的版本，而wsl git --version查看默认子系统中git的版本
    git --version # git version 2.35.1.windows.2
    wsl git --version # git version 2.25.1
    # 在PowerShell 中，命令 get-date 将提供 Windows 文件系统中的日期，而 wsl date 将提供 Linux 文件系统中的日期。
    ```
6. WSL配合VS Code使用
    1. 参考：https://learn.microsoft.com/zh-cn/windows/wsl/tutorials/wsl-vscode

发行版文件系统
1. 参考：https://learn.microsoft.com/zh-cn/windows/wsl/filesystems#file-storage-and-performance-across-file-systems
    1. 在存储WSL项目文件时：推荐使用 Linux 文件系统根目录：`\\wsl$\<DistroName>\home\<UserName>\Project`，而不使用 Windows 文件系统根目录：`C:\Users\<UserName>\Project 或 /mnt/c/Users/<UserName>/Project`
1. 在 Windows 文件资源管理器中查看所有可用的 Linux 发行版及其根文件系统，请在地址栏中输入：`\\wsl.localhost`或(`\\wsl$`)

安装桌面软件吗？看需求，一般来说没必要，因为子系统和windows的资源是共享的。不过为了方便copy文件，可以建立软链接当做共享文件夹，比如:
1. ` ln -s /mnt/c/Users/my_username/LinuxShare ~/LinuxShare`
2. ` ln -s /mnt/c/Users/my_username/study ~/study`  
2. ` ln -s /mnt/c/Users/my_username/go ~/go`
2. ` ln -s /mnt/c/Users/my_username/Downloads ~/Downloads`

设置windows下IDE的terminal为wsl.exe就可以使用子系统的终端了。

需要手动安装的工具:
1. 输入`code`安装vscode-server

## 3 edge

# 五 经验
# 六 问题
## 1 已解决
### 1.1 如何将剪切板中的图片保存下来
比较简单的方式是粘贴到Word,画图等工具中,然后另存为

## 2 未解决
1. 网友:在 windows10 创造者更新之前，创建软链接需要管理员权限，请确保通过使用带有管理员权限的命令行来克隆仓库
2. 网友:windows 下的软链接只在 Vista 以上的 windows 系统中起作用

# 七 待整理
1. windows10贴吧中说的esd安装系统