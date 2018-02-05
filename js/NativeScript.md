# NativeScript
[TOC]
## 一 概述
### 1 简介
NativeScript在Android采用v8；在iOS上采用JavaScriptCore。由于NativeScript使用JavaScript虚拟机，你访问原生API的所有JavaScript代码，仍然需要遵守JavaScript的语法结构和规范。
在Android中的情​​况下，NativeScript运行的C++代码不能直接访问Java API，如android.text.format.Time。然而，Android的JNI ，或Java本地接口，提供了C++和Java之间的桥接能力，所以NativeScript使用JNI完成转发。在iOS中这个桥梁是不必要的，因为C++代码可以直接调用Objective-C的API。
### 3 常识
#### tns和nativescript两个命令等价
## 二 安装配置
### 1 win
1. 需要有node,然后`npm i nativescript -g`
    1. 官网说前两个都是no
### 2 mac
"you should add the path to node@6/bin manually by running echo 'export PATH="/usr/local/opt/node@6/bin:$PATH"' >> ~/.bash_profile and restart your terminal."
## 三 基础
## 四 高级
### 1 TNS(Telerik NativeScript)
1. `tns doctor`
    
    run momentarily and flag the problem so you can upgrade.
## 五 经验
## 六 问题
1. `tns debug android`

    what is android emulator?
2. NativeScript Sidekick.
3. [NativeScript的工作原理：用JavaScript调用原生API实现跨平台](http://ourjs.com/detail/550138f51e8c708516000005)