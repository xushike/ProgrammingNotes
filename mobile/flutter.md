# flutter

# 一 概述
## 1 简介
2015年5月Dart开发者峰会上，亮相了基于Dart语言的移动应用程序开发框架Sky，后更名为Flutter。

Flutter是Google下一代操作系统Fuchsia的UI框架，在保持原生性能的条件下实现了跨端编程。

### 特点
1. 自己实现GDI，所以性能比RN更好
2. Flutter 提供的 widget 都是基于 skia 来实现，与具体平台无关

## 4 文档
1. https://flutter-io.cn/
2. https://flutter.io/community/china

# 二 安装配置
## 1 mac
1. 下载后flutter SDK解压后，将flutter的bin添加到PATH中。
2. 运行`flutter doctor`查看其它依赖
3. 在android studio中安装flutter插件
4. 安装xcode
5. 设置IOS simulator

在vscode上运行debug：
1. 如果卡在`Resolving dependencies...`，运行下`./android/gradlew`
2. 如果出现`INSTALL_FAILED_USER_RESTRICTED`，应该是没有开启安装app的权限

# 三 基础


# 六 问题
# 七 未整理
1. https://blog.csdn.net/zhangzeshuai/article/details/80151710