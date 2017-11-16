# gitbook
[TOC]
## 一. 安装配置
1. 安装了npm之后，直接npm install gitbook-cli -g全局安装gitbook
2. 安装了gitbook-cli之后执行gitbook的命令
    1. 如果没有安装node，此时会显示node的提示
    2. 然后会显示installing gitbook 3.2.3，等它装完了之后命令才执行(大概安装1至5分钟)（安装的这个算不算npm模块呢？待补充）
3. README.md 和 SUMMARY.md 是两个必须文件  
README.md 是对书籍的简单介绍，SUMMARY.md 是书籍的目录结构
## 二. 基础

1. 网上大神说的：
    >“好像从 3.0.0 版起, gitbook build 生成的 website 就不支持 local 打开了, 必需要 webserver 开启; 
    >实在要完全静态的, 就安装 2.6.7 版吧( 在有些浏览器下估计不太完美 )”

## 三. 使用

基本上暂时只需要掌握两个命令就行了：gitbook init 和gitbook build，前者根据summary.md生成目录和文件，后者是生成静态网页文件
## 五. 问题
1. gitbook和cli都安装了，为什么输命令后还显示installing gitbook 3.2.2?

