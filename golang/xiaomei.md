# 一 概述

# 三 基础
xiaomei app exec
xiaomei app run

参数：
1. 使用不同的环境：`GOENV=`

关于`err.New() 、err.WithStack()、err.WithStack()`的使用：
New 返回业务错误，不会发报警邮件。（对于不想报警的错误可以使用它，比如验证码错误就不想报警）
WithStack 在单元测试中用，用来打印 错误栈。
Trace用来跟踪错误栈。

## 3.1 环境说明
先qa2再qa

qa2：内部联调
qa：测试
dev：
production

## 3.2 项目一般结构说明
- misc：存放创建本地数据库的脚本等
    - 

## 3.3 数据库
company_parts:配件
company_skus:配件的sku,主键比上面多了一个porperty




# 六 问题
## 2 未解决
开发的流程：
1. sql是直接写到代码里面吗，没有单独放到一个文件中？
1. cache是干嘛的
1. helpers充当什么角色
2. 获取上下文
3. 获取db
4. 错误的种类和方法
5. token
6. xxx.sql和xxx.sh是什么时候使用的

发布部署的流程：
1. docker
2. 测试编译打包

测试怎么写

业务问题

# 七 未整理
1. 定时任务
2. vendor

# 八 任务
20180809：
上架
下架
价格同步
库存同步