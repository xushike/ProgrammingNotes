# nodejs
[TOC]
## 一. 概述
## 二. 安装配置
### 1 windows
### 2 linux
1. 推荐使用n或nvm安装，但是n模块似乎不支持重定向，也就是不能换源，亲测用n安装在2至8分钟
## 三. 基础
### 1 全局对象global
十分类似js中的window
1. 常用属性 
    1. console

        提供控制台标准输出,向stdout和stderrs输出字符.大部分用法和js的console一样.

## 四. 使用
### 1. 关于n模块
n模块是专门用来管理node的
1. 安装前最好清除一下npm cache，否则可能报错:

    ```bash
    sudo npm cache clean -f 
    ```
2. 安装n模块，估计安装3分钟不到：

    ```bash
    sudo npm install -g n
    ```
3. 用n升级node到制定版本：

    ```bash
    sudo n x.x.xx   #升级到制定版本
    sudo n stable   #升级到最新稳定版
    ```
## 五 问题

