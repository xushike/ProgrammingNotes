# nodejs
[TOC]
## 一. 概述
## 二. 安装配置
## 三. 基础
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

