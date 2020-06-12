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

# 四 高级
## 1 windows to go
能将win8和win10装在U盘里跑,根据网友的评价来看,效果还可以

## 2 WSL和WSL2
相比第一代，新的 WSL2 重新设计了架构，使用真正的 Linux 内核，几乎具有 Linux 的所有完整功能。启用WSL2的 Linux 系统启动时间非常快，内存占用很少，并且，WSL 2 还可以直接原生运行 Docker，VS Code 编辑器还有 Remote-WSL 插件，相对于完整的linux虚拟机只是不支持systemctl、systemd。

子系统所在的目录是`C:\Users\my_username\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu16.04onWindows_79rhkp1fndgsc\LocalState\rootfs`

查看已经安装的子系统:``

换源，然后`sudo apt update`。如果不换源，安装软件的时候可能出现`The following packages have unmet dependencies: ... but it is not going to be installed`

安装桌面软件吗？看需求，一般来说没必要，因为子系统和windows的资源是共享的。不过为了方便copy文件，可以建立软链接当做共享文件夹，比如:
1. ` ln -s /mnt/c/Users/my_username/LinuxShare ~/LinuxShare`
2. ` ln -s /mnt/c/Users/my_username/study ~/study`
2. ` ln -s /mnt/c/Users/my_username/go ~/go`
2. ` ln -s /mnt/c/Users/my_username/Downloads ~/Downloads`

设置windows下IDE的terminal为wsl.exe就可以使用子系统的终端了。

需要手动安装的工具:
1. 输入`code`安装vscode-server

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