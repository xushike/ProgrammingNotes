# android
[TOC]
# 一 概述
## 1 简介
Android系统是由Andy Rubin创建的，后来被Google收购了.有趣的是Android系统的命名都是以点心来命名的.

## 3 常识
### xml文件开头的声明
形如`xmlns:xxx="..."`:因为XML文件不仅仅用于Android,还可以用于很多地方,所以这句声明表示该XML文件用于Android的开发和布局(这也就是所有属性前都加了`android:`的原因),也可以理解为命名空间(?)
1. 而且,所有的布局文件中都需要加入xmlns开头的两个声明,否则不能正确运行.
2. 更多信息(待研究):[What does “xmlns” in XML mean?](https://stackoverflow.com/questions/1181888/what-does-xmlns-in-xml-mean)
3. 还可以使用tools命名空间,帮助很大 

    比如`tools:text`,相当于占位符,在预览的时候不会显示,而是用于动态展示.

### 代码的`@`
一般表示指定某种资源

- 指定id:`android:id = " @+id/ben_text_view"`

    指定id时,值以字母开头,不能有空格和特殊符号;其中的"+"号只有在第一次声明id的时候用到
- 指定图片路径:`android:src = " @drawable/[pic_name]"`,不需要图片的扩展名
- 指定颜色
    1. 值`@android:color/[color_name]`:指定Android标准颜色,比较有限
    2. 十六进制,支持所有颜色

### Android Go
谷歌推出的专为低配手机用的系统,相当于Android8的精简版

### Android Instant Apps和微信小程序
两者都是免安装的应用.只不过 Instant Apps 是基于 Android 操作系统的，微信小程序是基于微信 App 生态的，但本质上还是不一样的，Instant Apps 本质上还是原生 App，只不过允许你在下载安装之前，先体验下 App 部分模块的功能，觉得不错，适合你，那么你可以再下载安装，而微信小程序本质上不是原生应用，他是基于一种类似 React Native 的框架来达到原生的体验，而且只能在微信内部运行。
Instant Apps 体验更好，功能更强大，可以独立运行在手机上，而微信小程序没法独立运行，是基于微信生态下的应用，而且技术上也有一些限制。
1. Instant Apps的缺点
    1. Instant Apps 深度链接的识别需要依赖 Google Play(但是国内需要梯子)
    2. 只支持 Android 平台，iOS 不支持

## 4 文档网站
1. 官方
    1. https://www.android.com/
1. 菜鸟教程for Android:[Android 基础入门教程](http://www.runoob.com/w3cnote/android-tutorial-android-studio.html)
2. 关于设计规范(排版,文字大小,颜色,布局等),可以参考google的:[Material Design](https://material.io/guidelines/style/typography.html#)

    值得好好研究,特别是没有产品经理的时候.

    1. 大量使用无边框图片
    2. 元素间最好留一些空隙
    3. 不建议使用太多的风格和字体,一般3到4种即可
    4. 颜色也不要太多,特别是材料(倾向于使用大片的饱和色)
    5. 对于重要元素可以使用浮动,高亮等
    6. 关于文本和设备边缘的间隔:16dp最佳;文件之间的间隔:8dp最佳.
    7. 最好不要有启动动画

3. 某机构收集的android学习资料:[Android 学习资料收集](https://github.com/Freelander/Android_Data)


# 二 安装配置
## 1 win
## 2 mac
### 新建项目
1. Company Domain:应用的唯一标识符,看起来像一个网址,一般填入的是`[my_name].com`,这个值反转后就是应用发布后的包名(package name)(google app和手机会根据这个来识别你的应用?),所以必须是在全世界发布的app中都是唯一的才行.
3. project location:AS会创建一个默认位置,一般用它就好.
4. 选择设备和版本

    设备有手机和平板,TV,Wear,Glass等选项.选版本时选"help me choose"会出现不同版本的使用情况

5. 选择模板

    blank activity和empty activity

6. 创建后的文件结构查看方式:推荐用Android
7. 在手机上运行
    大神推荐Nexus 5
    1. 开启开发者选项和USB调试
        
        第一次需要点击版本号好几次(?),然后设置里就有开发者选项了.
    2. usb连接
    3. install derver(windows only):因为mac下默认是允许连接的
    4. install apo

8. 在模拟器上运行

    第一次运行模拟器的时候可能会不正常,大部分问题都可以解决,但更推荐使用真机.

# 三 基础
## 1 未整理
1. Android应用的界面使用布局（ViewGroup 对象）和微件（View 对象）层次结构构建。布局是一种不可见的容器，用于控制其子视图在屏幕上的位置。微件是界面组件，例如按钮和文本框。
2. 嵌套布局会增加绘制界面所需的时间。
3. 您还可以使用顶部或底部边缘创建水平对齐，不过，按钮在其图像周围包含内边距，因此如果您按照这种方式对齐这些视图，视觉对齐将是错误的。
4. 关于接口,抽象类和具体类
    接口是完全没有实现,抽象类是部分实现,具体类是完全实现;编写代码的时候具体用哪个要看情况.

## 2 文件结构
### 2.1 android视图模式
该视图模式也是google官方推荐的模式,app目录里的文件大概如下
1. mainfests
    - AndroidManifest.xml

        视图主文件,包含:
        1. 包名(package name)
        2. 应用组件:如activity name,intents,通知权限,最低api等
2. java
3. res:包含应用外观的所有内容
    1. drawable:放置图片
    1. layout:包含app设计和布局的xml
    2. menu
    3. mipmap:放置应用图标
    4. values

## 3 Intent
分为隐式和显式Intent,显式就是指定具体的Intent,隐式就是不知道具体的,比如打开一个网页,不管哪个浏览器app,只要能打开网页就行.
### 3.1 隐式Intent
可以设置更具体的一些信息,同时还要对没有可选的情况进行处理

## 4 布局
### 4.1 ViewGroups
类似于视图的容器,分类如下

- 线性布局（LinearLayout）
    1. 位置权重

        类似于比例布局
        1. 如果权重为0,则宽高会使用设置的值

- 相对布局（RelativeLayout）

    其中的子元素不设置的话默认会放在左上角.
    1. 子元素布局

        用`layout_xxx`来设置,比如相对于某个兄弟元素的左边可以用`layout_toLeftOf`,较某兄弟元素下面用`layout_below`,和父元素的右对齐可以用`layout_alignParentRight`

- 约束布局(ConstraintLayout)

    Android Studio默认使用约束布局

## 5 日志
根据日志的严重情况分为五个类别,分别是xxx,都接受两个参数,第一个是消息来自何处,一般填类名,第二个参数就是消息内容.

## 6 可回收的视图
### 6.1 ListView
1. 视图回收
3. ArrayAdapter

### GridView
### RecyclcerView

## 7 Activity

## 15 注释

### 其他注释
`.nomedia`:作用是告诉系统和其他程序不要索引当前目录下的媒体文件。当然它只是一个约定，而不是强制性的，其他APP依然可以不遵守这个约定。

# 四 高级
## 1 adb
参考：
1. https://github.com/mzlogin/awesome-adb

ADB是什么：全称为Android Debug Bridge：android调试桥梁。具有安装卸载apk、拷贝推送文件、查看设备硬件信息、查看应用程序占用资源、在设备执行shell命令等功能

安装下载：
1. 我们可以在android sdk安装目录的platform-tools目录下找到adb工具
2. `brew cask install android-platform-tools`

配置：环境变量

架构：ADB是一个C/S架构的应用程序，由三部分组成：
1. 运行在pc端的adb client：命令行程序”adb”用于从shell或脚本中运行adb命令。首先，“adb”程序尝试定位主机上的ADB服务器，如果找不到ADB服务器，“adb”程序自动启动一个ADB服务器。接下来，当设备的adbd和pc端的adb server建立连接后，adb client就可以向ADB servcer发送服务请求；
2. 运行在pc端的adb server：ADB Server是运行在主机上的一个后台进程。它的作用在于检测USB端口感知设备的连接和拔除，以及模拟器实例的启动或停止，ADB Server还需要将adb client的请求通过usb或者tcp的方式发送到对应的adbd上；
3. 运行在设备端的常驻进程adb demon (adbd)：程序“adbd”作为一个后台进程在Android设备或模拟器系统中运行。它的作用是连接ADB服务器，并且为运行在主机上的客户端提供一些服务；

使用：
1. 查询已连接的设备和状态`adb devices`，输出格式一般为`serialNumberA stateA`
    1. serialNumber 即我们常说的 SN
    2. state 有如下几种：
        1. offline —— 表示设备未连接成功或无响应。
        2. device —— 设备已连接。注意这个状态并不能标识 Android 系统已经完全启动和可操作，在设备启动过程中设备实例就可连接到 adb，但启动完毕后系统才处于可操作状态。
        3. no device —— 没有设备/模拟器连接。
    
    ```bash
    # 示例
    List of devices attached
    cf264b8f	device
    emulator-5554	device
    10.129.164.6:5555	device
    # cf264b8f、emulator-5554 和 10.129.164.6:5555 分别是它们的 SN。从 emulator-5554 这个名字可以看出它是一个 Android 模拟器，而 10.129.164.6:5555 这种形为 <IP>:<Port> 的 serialNumber 一般是无线连接的设备或 Genymotion 等第三方 Android 模拟器。
    ```
2. 连接设备和电脑：
    1. USB连接
        1. Android 设备的开发者选项和 USB 调试模式已开启。
            1. 一般情况下会自动连接，如果没有，则关闭USB调试后再重新打开
        2. 连接成功后通过`adb devices`可以看到该设备
    2. 无线连接：
        1. prerequisites：设备和PC机已经接入局域网，并且设备有局域网的IP地址
        1. 让设备在某个端口监听TCP/IP连接
            1. 方法一：这一步可以借助USB连接来操作`adb tcpip <port>`，比如`adb tcpip 5555`，之后就不需要USB了
            1. 方法二：也可以不借助USB，在设备的终端模拟器上操作
                
                ```bash
                su # 需要root权限
                setprop service.adb.tcp.port 5555
                stop adbd
                start adbd
                ```
        2. 连接设备
            1. 断开 USB 连接(如果没用USB则忽略此步)
            2. 找到设备的 IP 地址,通过 IP 地址连接设备`adb connect <device-ip-address>`，如`adb connect 192.168.2.157`，连接成功后通过`adb devices`可以看到该设备
            1. 使用完后断开连接`adb disconnect <device-ip-address>`
            2. 恢复USB调试`adb usb`(没有则忽略此步)
4. `adb shell`:发出shell命令，有两种使用方式，`adb shell shellCommandA`是发出单个shell命令(无需进入远程shell)，`adb shell`是启动交互式shell(需要进入远程shell)。
    1. 使用shell命令之前，推荐先`adb root`:以 root 权限运行 adbd,再运行 `adb shell`，命令行提示符变成`#`.相应地，如果要恢复 adbd 为非 root 权限的话，可以使用 adb unroot 命令。
        1. 有些手机 root 后也无法通过 adb root 命令让 adbd 以 root 权限执行，比如三星的部分机型，会提示"adbd cannot run as root in production builds"，此时可以先安装 adbd Insecure，然后 adb root 试试。
        2. 参数`-s`：多个设备的时候用于指定具体某个设备`adb -s emulator-5554 shell`
    2. 查看可用的Unix命令行工具列表`adb shell ls /system/bin`：Android 提供了大多数常见的 Unix 命令行工具，`--help`参数可获得大多数命令的帮助。许多 shell 命令都由 toybox 提供.
    3. 调用 Activity 管理器 (am)：可以执行各种系统操作，如启动 Activity、强行停止进程、广播 intent、修改设备屏幕属性，等等。语法可以是`adb shell am xxx`(无需进入远程shell)，也可以是`am xxx`(需要先进入远程shell)
        1. 打开app`adb shell am start `
            1. `-n componentA`：通过组件名，即`软件包名/activity名`打开app
                
                ```bash
                adb shell am start com.hypergryph.arknights/com.u8.sdk.U8UnityContext
                ```
        2. 终止app
            1. 正常终止`adb shell am kill pkgA`:终止与 package（应用的软件包名称）关联的所有进程。此命令仅终止可安全终止且不会影响用户体验的进程。也就是说如果应用在前台使用，是不会终止的，只有应用在后台的时候才会被终止。
            1. 强行终止`adb shell am force-stop pkgA`:强行停止与 package（应用的软件包名称）关联的所有进程
    4. 实时查看正在运行的app的包名和activity
        1. 方法一`adb shell dumpsys activity activities`(推荐)
        2. 方法二`adb shell logcat | grep ActivityManager`
        
            ```bash
            # 比如启动mrfz，可以发现一串字符 
            Start proc 3027:com.hypergryph.arknights/u0a447 for activity {com.hypergryph.arknights/com.u8.sdk.U8UnityContext} caller=com.android.shell
            # 其中com.hypergryph.arknights是包名，com.u8.sdk.U8UnityContext是当前活动的Activity
            ```
    7. `dumpsys`:等同`getprop`，获取在连接的设备上运行的所有系统服务的诊断输出，就是从系统的各种配置文件中读取信息。
        1. 查看屏幕密度
            1. `adb shell getprop ro.sf.lcd_density`
            2. `adb shell wm density`
        2. 查看屏幕尺寸`adb shell wm size`
    8. `ps`
        1. 根据包名获取运行进程的pid`adb shell pidof pkgA`，如`com.hypergryph.arknights`，未运行时返回空字符串
5. 应用管理
    1. 查看应用列表
        1. `adb shell pm list packages`
    1. 安装apk`adb install [-lrtsdg] <path_to_apk>`，比如`adb install xxx.apk`
        1. 安装原理：adb install 实际是分三步完成：
            1. push apk 文件到 /data/local/tmp。
            2. 调用 pm install 安装。
            3. 删除 /data/local/tmp 下的对应 apk 文件。
        1. 安装状态
            1. 成功
                
                ```bash
                Performing Streamed Install
                Success
                ```
            2. 失败
                
                ```bash
                Performing Streamed Install
                # 可能出现的错误很多，比如
                # 空间不足
                Failure [INSTALL_FAILED_INSUFFICIENT_STORAGE] 
                ```
    3. 卸载`adb uninstall 包名A`，比如`adb uninstall com.xxx.xxx`
6. 文件管理
    1. 复制设备里的文件到电脑`adb pull <设备里的文件路径> [电脑上的目录]`，如果省略电脑上的目录，则默认复制到当前目录。
        1. 设备上的文件路径可能需要 root 权限才能访问，如果你的设备已经 root 过，可以先使用 adb shell 和 su 命令在 adb shell 里获取 root 权限后，先 cp /path/on/device /sdcard/filename 将文件复制到 sdcard，然后 adb pull /sdcard/filename /path/on/pc。
    2. 复制电脑里的文件到设备`adb push <电脑上的文件路径> <设备里的目录>`
        
        ```bash
        adb push 393ac486.0 /system/etc/security/cacerts/
        ```
7. 模拟按键/输入
    1. 比如模拟点击：//在屏幕上点击坐标点x=50 y=250的位置。`adb shell input tap 50 250`
    2. 比如使用 `adb shell input keyevent keyCodeA`命令，不同的 keycode 能实现不同的功能
        1. 滑动解锁:如果锁屏没有密码，是通过滑动手势解锁，那么可以通过 input swipe 来解锁。
            1. 向上滑动手势解锁举例:`adb shell input swipe 300 1000 300 500`
        2. 输入文本:在焦点处于某文本框时，可以通过 input 命令来输入文本`adb shell input text hello`
8. 查看日志:Android 系统的日志分为两部分，底层的 Linux 内核日志输出到 /proc/kmsg，Android 的日志输出到 /dev/log。
9. 录制屏幕:录制屏幕以 mp4 格式保存到 /sdcard：`adb shell screenrecord /sdcard/filename.mp4`
10. 重新挂载 system 分区为可写(需要 root 权限):/system 分区默认挂载为只读，但有些操作比如给 Android 系统添加命令、删除自带应用等需要对 /system 进行写操作，所以需要重新挂载它为可读写。
    1. 进入 shell 并切换到 root 用户权限。`adb shell`、`su`
    2. 查看当前分区挂载情况:`mount`
11. 查看连接过的 WiFi 密码(需要 root 权限)`adb shell su cat /data/misc/wifi/*.conf`
    
问题：
1. 5037为adb默认端口，若5037端口被占用
    1. 以win为例
        1. 找到使用该端口的进程Pid`netstat -aon|findstr 5037`
        2. 通过PID找到对应的进程名（便于定位，可以跳过）`tasklist /fi "PID eq pidA"`
        3. 终止pid`taskkill /pid 3172 /f`

## 2 Udacity的google Android课程
### 课程1 入门课程
#### 课程1A:视图VIEWS
使用大驼峰写法
1. 显示文字的叫TextView

    1. 默认背景颜色是透明色
    2. 宽高参数值`wrap_content`:根据文字的长度自动调整宽高
    3. 属性`textStyle`:指定文字是粗体或斜体
    4. 属性`textAlignment`:文字在视图中对齐的方式
    5. 属性`textSize`:文字大小,推荐使用sp
    6. 属性`fontFamily`:设置字体
    7. 属性`textColor`:文字颜色

2. 图片=>ImageView
    1. 属性`scaleType`:图片的对齐方式
        1. `center`:居中,不会对图片大小做修改
        2. `centerCrop`:居中,同时自动调整图片大小填充满整个屏幕(保持原有的纵横比?)
    2. 
3. 按钮=>Button
4. others
#### XML语法
1. 一般这样写:`<xxx ... />`;有子元素的时候,这样写阅读体验更好:`<xxx ... > /xxx>`
2. 属性

    因为是XML,所以属性要用引号(双引号)包裹

3. [XML可视化工具链接](http://labs.udacity.com/android-visualizer/#/android/xml-syntax-errors)
#### 更改TextView
1. 推荐使用dp单位,这样在不同分辨率的手机上看到的大小是一样的;如果用px就不一样.
2. 推荐所有可触摸的目标,比如button的宽高最少为48dp
3. 关于文字外观(待阅读):[Text appearance and theme attributes on Android](http://discussions.youdaxue.com/t/text-appearance-and-theme-attributes-on-android/6947)
4. 修改颜色

    Android自带的颜色是一个有限集,比如`blue`就没有,但是支持十六进制的所有颜色(Hex color).写法是`#xxxxxx`

#### 解决错误
1. [常见视图备忘单](http://cn-static.udacity.com/nd801/Common_Android_Views_Cheat_Sheet.pdf)


#### 宽度和高度
"子视图的高宽和位置是由父视图决定的"这句话如何理解
#### 内外边距
内外边距可用于所有视图,padding和margin的默认值是0;设置了margin之后就像在视图的周围有一道防护,阻止其他元素进入.
#### 课程1C:课程实践
### 课程2 用户输入
#### 课程2A:制作一款交互性应用
#### 课程3B:面向对象编程
##### intent
android框架的重点之一,调用其他应用.comment intents.


## 3 Android官网的培训
[https://developer.android.com/training](https://developer.android.com/training)

## 4 ARCore 
## 5 Google Lens
能实时识别用智能手机相机所拍摄的物品并提供与之相关的内容，都是通过利用强大的计算机视觉算法实现的

# 五 经验
## 1 app推荐
洋葱数学

## 2 各机型的一些笔记
### 2.1 魅族
SmartBar

### 2.2 小米

# 六 问题
## 1 dl.google.com 无法下载的问题
不需要科学上网，修改DNS就可以解决：去[http://ip.tool.chinaz.com](http://ip.tool.chinaz.com/)查询`dl.google.com`的ip，然后ping一个可用的，将其放到hosts文件中就可以了。

# 七 待整理
1. android framwork和anfroid sdk
2. 统一推送联盟
3. Hybrid App（混合模式移动应用）是指介于web-app、native-app这两者之间的app，兼具“Native App良好用户交互体验的优势”和“Web App跨平台开发的优势”。

    其他信息可先参考百度百科.
4. android的c++开发包叫做ndk,就是native开发包
5. Android上页面推荐使用rem单位?
6. [Listview与Adapter的关系和简单应用](http://blog.sina.com.cn/s/blog_a364999b01014kzl.html)

7. ViewGroup中设置的属性是干嘛的
8. dimens文件
9. `layout_padding`和`margin`的区别,我怎么感觉两者差不多呢?
10. 不同视图的id可以相同?
12. 如何给xml中的属性注释
1. 临时文件目录是`/data/local/tmp`?
1. [去哪儿查找android资料](https://classroom.udacity.com/courses/ud836/lessons/4329970891/concepts/43237591300923)
2. 导入项目的几种方式
4. [Android 性能优达学城课程，其中也介绍了Memory Monitor](https://classroom.udacity.com/courses/ud825/lessons/3846748822/concepts/37868186490923)

5. 微信公众平台接口测试帐号申请 
6. JuiceSSH

7.  12 栏响应式栅格布局?
8. Jetpack
9. 真机调试
[http://expelliarmus923.github.io/2017/03/31/%E7%9C%9F%E6%9C%BA%E8%B0%83%E8%AF%95%E5%90%84%E7%A7%8D%E6%96%B9%E6%B3%95/](http://expelliarmus923.github.io/2017/03/31/%E7%9C%9F%E6%9C%BA%E8%B0%83%E8%AF%95%E5%90%84%E7%A7%8D%E6%96%B9%E6%B3%95/)