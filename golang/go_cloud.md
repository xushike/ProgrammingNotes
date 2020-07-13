# go-cloud

# 一 概述
go_cloud、第三方包和开源项目的笔记

## 1 简介
Go Cloud Project是一项计划，允许应用程序开发人员在任何云提供商组合上无缝部署云应用程序。它通过为存储和数据库等常见用途提供稳定的惯用接口来实现此目的，旨在为各种云中最常用的服务提供中立于厂商的 API，这样可以轻松地将 Go 应用程序进行跨云迁移。

该项目的一个关键部分是提供一个名为Wire的代码生成器 。它创建了人类可读的代码，仅为您使用的提供程序导入云SDK。这允许Go Cloud增长以支持任意数量的云提供商，而不会增加编译时间或二进制大小，并避免init()功能的不良影响。Wire使用依赖注入自动连接组件。组件依赖关系表示为函数参数，并鼓励开发人员进行显式初始化，而不是使用全局变量。Wire可以在没有运行时状态或反射的情况下执行，从而可以使用手写的初始化代码。

目前，主要提供对 AWS 和 Google Cloud Platform 的支持。

Go Cloud 是一个可在开放云平台上进行开发的库和工具集

# 四 高级
## 常见web框架

### goa
参考：
1. https://github.com/goadesign/goa
2. https://goa.design/learn/getting-started/
3. https://blog.gopheracademy.com/advent-2015/goauntanglingmicroservices/
4. DSL参考 
    2. 查看所有的API：https://goa.design/reference/goa/design/apidsl/
    1. https://goa.design/design/overview/
    3. https://godoc.org/goa.design/goa/dsl

Raphael Simon 是来自于 RightScale 的一位高级系统架构师，他创建了一种基于 Go 语言的 HTTP 微服务框架，名为“goa”。这一框架允许开发者通过领域特定语言（DSL）定义服务的API，并且通过自动代码生成功能创建“样板”式的服务端和客户端代码以及文档。

#### 特点
1. 与 goa 框架一同推出的还有一个 goagen 工具，它能够通过设计代码生成各种输出，包括 http 服务器的封装、代码脚手架、文档、js客户端，甚至是自定义的输出。
    1. goa 框架能够描述 API 的意图。通过使用 goa 设计语言，开发者能够定义 API 所暴露的资源与行为（即 API 的终结点）。对于每种行为的描述包括所期待的请求状态，以及各种可能产生的响应。这种方式能够带来许多益处：举例来说，它在设计阶段就能够起到很大的作用，各个团队能够通过 Swagger UI 生成 Swagger 的规格说明，从而提出反馈意见。这一反馈循环能够为负责生成 UI 或编写面向用户的文档的团队带来极大的便利。最大的优点在于，这一切都发生在实际编写代码实现之前。
        1. 它减轻了对反射的依赖，否则的话，实现相同的功能可能要写上几千行代码
        2. 所生成的代码始终处于一个不同的包中，而无需进行手动修改，从而清晰地区分了用户代码与生成的代码。goagen 将始终重新生成整个包，因此不可能出现用户代码与生成代码相混合的情况。
        3. 只会生成必要的代码，所生成的代码将使用 goa 包实现各种通用的功能，例如日志记录、通用的错误处理等等。可以将这种生成代码想象为一种 goa 包的“插件”，并暴露相应的调节器以修改它的行为。
    2. 一旦设计完成之后，goa 就将负责生成所有样板逻辑，包括请求的验证以及用于描述请求状态的自定义数据结构。这样一来，设计就变成了实现所必需的一部分。
    3. 它还有助于维护多个客户端之间的一致性，并且保持他们与 API 的同步。
2. goa 包还包括大量的支持性模块，服务本身与生成的代码都能够利用这些模块进行服务的实现。
    1. 利用go的跨接口传递上下文的特性实现了一些强大的功能，比如设置deadline，以及在goroutine 之间共享状态信息
    2. 提供默认实现，但也支持自定义。比如错误处理
    3. 提供了中间件，部分中间件也支持自定义
3. 插件系统:整个项目最令人惊讶的部分就在于通过代码（以及其他功能）生成所带来的各种可能性。
    1. 它实质上就是一种标准的 Go 包，其中包含了一个公开的 Generate 函数。由 Brian Ketelsen 所编写的 gorma 插件是对这一项目最早的贡献之一，它能够通过 API 设计中所描述的类型生成 gorm 模型。

特点总结：
1. 代码自动生成（自动生成的代码可以热更新，因为生成代码和自己写的代码是分开的）
2. 理念时髦，基于API设计，利用插件来扩展业务逻辑

#### 使用
`goagen `

`goa exmaple`:
1. 比如`goa exqmple serverA/design`


#### DSL说明
goa基于服务提供功能，每个API定义一个服务(Service)，每个服务有若干资源(Resource)，每个资源对应若干操作(Action)，每个操作(Action)有多种响应(Response)，每个响应可能返回不同媒介(Media)的不同视图(View)。当然goa提供了更好的层级控制和继承关系(如上例，Response返回的视图继承于Resource中定义的默认媒介(BottleMedia)的默认视图(default))
1. API: 描述一个Service及其地址，协议规范等
2. Resource: 定义一个资源及其一系列相关的操作(Action)，以及这些操作所共用的一些属性
3. Action: 定义针对于某个资源的操作，包括方法(GET,POST等)，URL(可有多个)，参数(goa自动做类型检查，值检查等)等
4. Response: 定义一个响应，包括响应模板和承载内容(payload)，在代码中决定调用那个响应模板
5. MediaType: 定义Response返回的数据结构，一个Media可以有多个View，可在Response中指定返回的View

### gin
https://github.com/gin-gonic/gin

Gin的词源是金酒, 又称琴酒, 是来自荷兰的一种烈性酒

### 静态网站工具 hugo
https://github.com/gohugoio/hugo

### echo
主要面向API

### iris
创建者称其为“真正属于Go的Express.js”，也就是说，它是JavaScript / Node.js的Web框架的Go语言版，它使用最小设计，绝大部分功能都由插件提供。Iris提供基本的MVC功能，自带对中间件、会话、路由和缓存的支持。

以下文档包含很多Iris的示例，包括与React前端的交互，或在Docker/Kubernetes环境中运行的项目：https://iris-go.com/v10/recipe

### beego

## groupcache

## 验证工具 validator
https://github.com/go-playground/validator/tree/v9.24.0

文档地址：https://godoc.org/gopkg.in/go-playground/validator.v9

## 页面转pdf go-wkhtmltopdf
github.com/SebastiaanKlippert/go-wkhtmltopdf

## 猴子补丁
在测试用例中挺好用的：https://github.com/bouk/monkey。注意下载和引入是`bou.ke/monkey`，github地址只是放的代码，而不是引入用的地址。

参考：https://www.jianshu.com/p/2f675d5e334e?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation

但有时候可能不生效，比如有内敛优化的时候，此时可以加上`-gcflags=-l`禁用内敛优化来测试，但也未必会生效。

## 结构体工具 structs
https://github.com/fatih/structs

go 结构体的一些工具化封装，比如:
1. 结构体转map（转之后似乎key是字段的名字，不受tag影响）

## 拼音 go-pinyin
https://github.com/mozillazg/go-pinyin

Heteronym

## 调试 go-spew
https://github.com/davecgh/go-spew

为go数据结构实现了一个深漂亮的打印机来帮助调试，是变量数据结构调试的利器

## 命令行交互工具 cobra
https://github.com/spf13/cobra

用来编写命令行程序，同时它也提供了一个脚手架用于生成基于 cobra 的应用程序框架。非常多知名的开源项目使用了 cobra 库构建命令行，如Kubernetes、Hugo、etcd等。

每个 cobra 程序都有一个根命令，可以给它添加任意多个子命令。

首先要明确几个基本概念：
1. 命令（Command）:就是需要执行的操作
1. 子命令（SubCommand）：需要执行的子操作；
2. 参数（Arg，args,arguments）：命令的参数，即要操作的对象；
3. 选项（Flag,flags）：命令选项可以调整命令的行为。
    1. 一般有两种表示方法
        1. single dash，比如`-h`
        2. double dash,比如`--help`
   
例子
1. `server version`中`server`是command，`version`是subCommand,同理`server help`中`help`是subCommand
2. `git clone URL --bare`,`clone`是一个subCommand，`URL`是参数，`--bare`是选项
2. `server -h`或`server --help`中的`-h`和`--help`是flags

## flag包增强 pflag
https://github.com/spf13/pflag

基本的使用和内置的flag包基本相同，它特点如下:
1. 支持更多参数类型：
    1. 例如，flag 只支持 uint 和 uint64，而 pflag 额外支持 uint8、uint16、int32 等类型。
    2. 以及ip、ip mask、ip net、count、以及所有类型的 slice 类型。
2. 兼容内置flag库
3. 更丰富的功能
    1. shorthand参数
    2. 可以设置非必须选项的默认值
    3. flag定制化
    4. 弃用flag或者它的shothand
    5. 隐藏flag:例如希望保持使用flagA参数，但在help文档中隐藏这个参数的说明
4. 支持bash和zsh的自动补全

```golang
// 设置非必须选项的默认值
flag.Lookup("flagname").NoOptDefVal = "4321"

// flag定制化:例如希望使用“-”，“_”或者“.”，像--my-flag == --my_flag == --my.flag
func wordSepNormalizeFunc(f *pflag.FlagSet, name string) pflag.NormalizedName {
	from := []string{"-", "_"}
	to := "."
	for _, sep := range from {
		name = strings.Replace(name, sep, to, -1)
	}
	return pflag.NormalizedName(name)
}

myFlagSet.SetNormalizeFunc(wordSepNormalizeFunc)

// 弃用flag或者它的shothand
// deprecate a flag by specifying its name and a usage message
flags.MarkDeprecated("badflag", "please use --good-flag instead")
// deprecate a flag shorthand by specifying its flag name and a usage message
flags.MarkShorthandDeprecated("noshorthandflag", "please use --noshorthandflag only")

// 隐藏flag
// hide a flag by specifying its name
flags.MarkHidden("secretFlag")

```

## 配置解决方案 viper
https://github.com/spf13/viper

完整的配置解决方案。 完美支持 JSON/TOML/YAML/HCL/envfile/Java properties 配置文件等格式，还有一些比较实用的特性，如配置热更新、多查找目录、配置保存等

viper提供的配置方式的优先级顺序如下(由高到低)：
1. 设置显示调用(explicit call to Set)
2. 命令行标志(flag)
3. 环境变量(env)
4. 配置文件(config)
5. 远程键/值存储(key/value store)
6. 默认值(default)

使用:
1. 设置默认值:默认值不是必须的，如果配置文件、环境变量、远程配置系统、命令行参数、Set函数都没有指定时，默认值将起作用。

    ```go
    viper.SetDefault("name", "xiaoming")
    viper.SetDefault("age", "12")
    viper.SetDefault("notifyList", []string{"xiaohong","xiaoli","xiaowang"})
    ```
2. 环境变量
    1. `AutomaticEnv()`
    2. `SetEnvKeyReplacer`

## 静态网站生成 hugo
https://github.com/gohugoio/hugo

## ORM
### gorm
https://github.com/go-gorm/gorm

中文参考：
1. https://gorm.io/zh_CN/docs/create.html

## JWT
https://github.com/dgrijalva/jwt-go

## NoSQL
### Redis
https://github.com/go-redis/redis

## migrate工具
https://github.com/golang-migrate/migrate

win上的安装我是使用的scoop

基本用法:
1. 创建迁移文件:`migrate create -ext sql -dir migrations create_users_table`,执行完这个命令会在migrations文件夹下创建两个文件，分别是：
    
    ```bash
    20190617061102_create_users_table.down.sql 
    20190617061102_create_users_table.up.sql
    # 20190617061102 是和时间有关的一个标识，用来区分migration的版本
    # 这两个文件都是空的，需要我们自己去填充
    ```
2. 升级
    1. 升级到最新版本:`migrate -source fileDirA -database xxx up`
3. 回滚
    1. 回滚到最开始版本
    2. 回滚最新的一个版本:`migrate -source fileDirA -database xxx down 1`，同理，回滚前n个版本是`migrate -source fileDirA -database xxx down n`

## lint工具 
https://github.com/golangci/golangci-lint

参考：
1. https://golangci-lint.run/
2. https://go-critic.github.io/overview

安装:windows的话可以去https://github.com/golangci/golangci-lint/releases下载对应版本。官方不建议使用`go get`安装(https://golangci-lint.run/usage/install/#local-installation)。
1. 本人实测，`go get`安装的确实可能有bug。比如
    1. 用release安装1.20.1，输入`golangci-lint version`显示`golangci-lint has version 1.20.1 built from 849044b on 2019-10-15T19:11:27Z`,然后检测a.go得到`ifElseChain`语法提示
    2. go1.14，使用`go get -u github.com/golangci/golangci-lint/cmd/golangci-lint@v1.20.1`安装后，输入`golangci-lint version`显示的是`golangci-lint has version v1.20.1 built from (unknown, mod sum: "h1:4aSxf2HvuoMNnaT4QMDpSLjoUBxgTn9q98ZKtEdtUW0=") on (unknown)`，然后检测相同的a.go文件却什么问题都没有(实际应该是有语法提示的才对)，并且对`.golangci-lint.yml`文件的支持也有问题。

基本使用
1. 指定配置文件运行，比如`golangci-lint run -c .golangci.yml ./...`

问题:
1. "File is not `goimports`-ed with -local (goimports)"
    1. 可能原因，包的引入代码的位置格式化不对
2. 指定文件运行和...运行结果不一样，比如`golangci-lint run -c .golangci.yml a/...`和`golangci-lint run -c .golangci.yml a/b.go`,都包含b.go，但是输出结果不一样：前者输出有格式化，后者有时候却没有。(待研究)
3. no such linter goerr113
    1. 可能原因:golangci-lint版本太低

## 单元测试相关
### 单元测试辅助工具 mock
https://github.com/golang/mock

gomock主要包含两个部分：gomock库和辅助代码生成工具mockgen

使用方式：
1. 直接命令行使用，比如`mockgen --source .../xxx.go --destination .../xxx.go`
2. (推荐)mockgen还提供了一种通过注释及`go generate`生成mock文件的方式，比如在接口文件的注释里面增加：`//go:generatemockgen --source .../xxx.go --destination .../xxx.go`，然后执行`go generate`命令就可以自动生成mock文件了。

其他参数:
1. `-source`：指定接口文件
2. `-destination`: 生成的文件名
3. `-package`:生成文件的包名
4. `-imports`: 依赖的需要import的包
5. `-aux_files`:接口文件不止一个文件时附加文件
6. `-build_flags`: 传递给build工具的参数

mock文件使用:

问题：
1. has already been called the max number of times
    1. `Call.Times(int)`:expected execute timers

### testify
https://github.com/stretchr/testify

主要功能(常用函数)：
1. 断言
    1. `assert`:如果失败，不会退出
    2. `require`:失败会直接结束
2. mock

## 容器相关
### kubernetes
https://github.com/kubernetes/kubernetes

## IoT
### Paho
Paho是 Eclipse 的一个开源 MQTT 项目，包含多种语言实现，比如JAVA、golang

## cron
https://github.com/robfig/cron

## rpc
### protoc
安装并加入环境变量

### protocbuf源码生成插件 protoc-gen-g
https://github.com/golang/protobuf/tree/master/protoc-gen-go

`github.com/golang/protobuf/protoc-gen-go`

### grpc

问题:
1. undefined: resolver.BuildOption 以及 undefined: grpc.SupportPackageIsVersion6
    1. 指定grpc版本`replace google.golang.org/grpc => google.golang.org/grpc v1.26.0`，然后重新生成.pb文件，不行的话再降级protoc-gen-go的版本`go get github.com/golang/protobuf/protoc-gen-go@v1.3.2`

## 日志 zap
https://github.com/uber-go/zap

# 五 经验
## 1 为什么需要框架
对于golang而言，web框架的依赖要远比Python，Java之类的要小。自身的net/http足够简单，性能也非常不错。框架更像是一些常用函数或者工具的集合。借助框架开发，不仅可以省去很多常用的封装带来的时间，也有助于团队的编码风格和形成规范。

# 七 未整理
## 2 未整理
1. Google Cloud Platform是干嘛的