# flutter

# 一 概述
## 1 简介
### 优点
1. 自己实现GDI，所以性能比RN更好
2. Flutter 提供的 widget 都是基于 skia 来实现，与具体平台无关
3. 开源和免费使用：Flutter 及其底层编程语言 Dart 都是开源的，可以免费使用。
4. 热重载功能：Flutter 之所以受到移动应用程序开发机构青睐，最重要的原因之一就是它提供的热重载功能。这一功能使任何人都可以更轻松地在后端做出各种更改，并即时在前端查看更改的效果。通过这种方式，开发人员可以轻松判断更改是否与应用程序的其他元素完美地结合在一起。
5. 高度可定制

### 缺点
1. 应用体积大
2. 学习成本：Dart、流程

## 2 历史
2015年5月Dart开发者峰会上，亮相了基于Dart语言的移动应用程序开发框架Sky，后更名为Flutter。

Flutter是Google下一代操作系统Fuchsia的UI框架，在保持原生性能的条件下实现了跨端编程。

## 3 常识
### 3.1 flutter vs kotlin
参考：
1. https://blog.csdn.net/guolin_blog/article/details/104010508
    1. https://goobar.io/2019/06/13/kotlin-vs-flutter-are-you-comparing-them-fairly
    
首先，kotlin是一种语言，flutter是基于dart的工具集(或者说framework)

## 4 文档
1. https://flutter-io.cn/
2. https://flutter.io/community/china

# 二 安装配置
## 1 mac
1. 下载后flutter SDK解压(比如我放在`~/opt/flutter`)后，将flutter的bin添加到PATH中。
2. 安装jdk
3. 运行`flutter doctor`查看其它依赖
4. 配置vscode
    1. `"dart.flutterSdkPath": "~/opt/flutter"`（需要手动填吗）
4. 在android studio中安装flutter插件,以及许可`flutter doctor --android-licenses`
5. 安装xcode
6. 设置IOS simulator

在vscode上运行debug：
1. 如果卡在`Resolving dependencies...`，运行下`./android/gradlew`
2. 如果出现`INSTALL_FAILED_USER_RESTRICTED`，应该是没有开启安装app的权限

# 三 基础

# 五 经验
## 1 《万物起源》
动画使用2Dimensions发布的flutter动画制作工具Flare制作，这个应用的灵感来源于 Kurzgesagt – In a Nutshell 频道的一个相当出名的视频：The History and Future of Everything。原视频链接：https://www.youtube.com/watch?v=5TbUxGZtwGI，原视频中作者说动画是通过Adobe After Effects和多年的经验制作的，skillsshare网站有制作过程的视频

# 六 问题

# 七 未整理
1. https://blog.csdn.net/zhangzeshuai/article/details/80151710