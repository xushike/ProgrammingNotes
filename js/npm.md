# npm
[TOC]
## 一. 概述
npm是世界上最大的js包管理g工具。
## 二. 安装配置
1. 直接安装nodeJS，里面带有npm
2. 使用淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm(解决了网速问题):
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
3. 或者把npm的源换成淘宝镜像(待补充)：
## 三. 基础
### 1. npm install 
包名后可以跟[@version]即包的 版本号
1. 常用参数
    - `-g, --global`:安装全局依赖，如果没有指定包名，则将当前目录中的包安装至全局。
    _ `--dry-run`:走一遍安装的流程并报告结果，但实际上没有安装任何依赖
### 2. npm uninstall 
删除制定的依赖包并且完全移除为了该包而安装的任何文件
1. 常用参数，和install一样
2. 别名:`remove 、rm、r、un、unlink`
### 3. npm update
升级所有依赖包至版本规则允许的最高版本,并安装缺失的依赖包
1. 常用参数
    - `-depth Infinity`:npm@2.6.1k开始，update命令默认只升级最顶层的依赖，即直接的依赖，加上该命令则升级所有依赖
    - `--save`:升级同时将升级的版本号记录到package.json
### 4. npm ls
## 四. 使用
### 1. 发布包的步骤
1. npmadduser登录
2. npminit
    1. 提问，根据回答生成package.json文件
3. npm publish
4. npm unpublish（不推荐使用）
5. npm deprecate:表示放弃一个包，该包在npm中没有取消，安装该包的用户会看到警告信息
6. npm view：显示一个包(在npm上)的详细信息
## 五. 问题
1. 淘宝镜像
    1. cnpm uninstall并不能生效，不知道为什么
