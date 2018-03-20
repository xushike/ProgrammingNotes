# nodejs
[TOC]
## 一 概述
### 4 文档
1. [Node也许不是构建大型服务的最佳选择—Node之父Ryan Dahl访谈录](http://ourjs.com/detail/59c32968f1239006149617f8)
### 5 网站
## 二 安装配置
### 1 windows
### 2 linux
1. 推荐使用n或nvm安装，但是n模块似乎不支持重定向，也就是不能换源，亲测用n安装在2至8分钟

## 三. 基础
### 1 全局对象global
十分类似js中的window
1. 常用属性 
    1. console

        提供控制台标准输出,向stdout和stderrs输出字符.大部分用法和js的console一样.

## 四 高级
### 1 关于n模块
n模块是专门用来管理node的,不过不支持win系统
1. 安装前最好清除一下npm cache:`sudo npm cache clean -f`,否则可能报错,但是该命令也很危险(慎用).
2. 安装n模块，估计安装3分钟不到：`sudo npm install -g n`
3. 用n升级node的版本：
    - `sudo n x.x.xx`:升级到制定版本
    - `sudo n stable`:升级到最新稳定版

## 六 问题
1. 网友:node8之后性能飙升.
2. [Node.JS读取中文TXT编码文件显示乱码问题解决方案](http://ourjs.com/detail/5a195f8f3506837194998b76)