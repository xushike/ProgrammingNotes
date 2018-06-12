# hydra

# 一 概述
目前项目中用到的hydra框架的笔记

# 三 基础
## 1 常用命令
### 1.1 新建项目
使用gaea,如`gaea new project gpscm/apiserver -m "coordinate/collection coordinate/list" -s api-mqc`

生成的目录是针对当前gopath的,所以如果gopath配置了多个路径,就会出问题

# 六 问题
## 1 已解决
### 1.1 用新版gaea生成hydra项目的时候报错:panic: runtime error: slice bounds out of range [recovered]
因为我在`-m "xxx "`的xxx后面多写了个空格,导致识别不出来

