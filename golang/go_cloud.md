# go-cloud

# 一 概述
go_cloud、第三方包和开源项目的笔记

## 1 简介
Go Cloud Project是一项计划，允许应用程序开发人员在任何云提供商组合上无缝部署云应用程序。它通过为存储和数据库等常见用途提供稳定的惯用接口来实现此目的，旨在为各种云中最常用的服务提供中立于厂商的 API，这样可以轻松地将 Go 应用程序进行跨云迁移。

该项目的一个关键部分是提供一个名为Wire的代码生成器 。它创建了人类可读的代码，仅为您使用的提供程序导入云SDK。这允许Go Cloud增长以支持任意数量的云提供商，而不会增加编译时间或二进制大小，并避免init()功能的不良影响。Wire使用依赖注入自动连接组件。组件依赖关系表示为函数参数，并鼓励开发人员进行显式初始化，而不是使用全局变量。Wire可以在没有运行时状态或反射的情况下执行，从而可以使用手写的初始化代码。

目前，主要提供对 AWS 和 Google Cloud Platform 的支持。

Go Cloud 是一个可在开放云平台上进行开发的库和工具集

## 4 文档网址等

# 三 基础

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

Raphael Simon 是来自于 RightScale 的一位高级系统架构师，他创建了一种基于 Go 语言的 HTTP 微服务框架，名为“goa”。这一框架允许开发者通过基于golang的领域特定语言（DSL(Domain-specific Language)）定义服务的API，并且通过自动代码生成功能创建“样板”式的服务端和客户端代码以及文档。

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
2. 理念时髦:
    1. 设计优先(Design-Based)
    2. 基于API设计
    3. 利用插件来扩展业务逻辑:DSL，代码生成器，用户代码均使用Go语言编写，并且前两者使用plugin实现，可以替换
3. 遵循单一数据源(Single Source of Truth, SSOT)原则，任何对设计的改变，都将自动反映到系统各处

#### 使用
参考：
1. 基本使用的简单示例：https://github.com/goadesign/examples
    1. 比如upload_download

它的使用分为三个部分，分别是：
1. goa的设计语言是内置DSL，用于描述微服务的设计
2. goa代码生成器，用于根据DSL描述生成代码模块(框架代码，胶水代码，测试代码)，辅助工具，和文档等
3. goa利用生成代码和用户代码来实现一个服务，并提供一个完全可插拨的框架

两个命令：
1. `goa gen moduleNameA [--out DIRECTORY] [--debug]`: Generate service interfaces, endpoints, transport code and OpenAPI spec.
    
    ```bash
    goa gen projectA/design -o xxx
    # 会在xxx目录下生成形如这样的目录
    gen
    ├── apidoc.html
    ├── apps
    │   ├── client.go
    │   ├── endpoints.go
    │   ├── service.go
    │   └── views
    ├── grpc
    │   ├── apps
    │   └── cli
    └── http
        ├── apps
        ├── cli
        ├── openapi.json
        ├── openapi.yaml
        ├── openapi3.json
        └── openapi3.yaml
    ```
2. `goa example moduleNameA [--out DIRECTORY] [--debug]`: Generate example server and client tool.
    
    ```bash
    # 比如`goa example projectA/design -o .，会生成如下cmd目录，同时根据design的接口在当前目录生成对应的接口impl文件
    .
    ├── http_broker.go
    └── cmd
        ├── http_broker
        │   ├── grpc.go
        │   ├── http.go
        │   └── main.go
        └── http_broker-cli
            ├── grpc.go
            ├── http.go
            └── main.go
    ```

#### DSL说明
##### 老版本的DSL
goa基于服务提供功能，每个API定义一个服务(Service)，每个服务有若干资源(Resource)，每个资源对应若干操作(Action)，每个操作(Action)有多种响应(Response)，每个响应可能返回不同媒介(Media)的不同视图(View)。当然goa提供了更好的层级控制和继承关系，如Response返回的视图继承于Resource中定义的默认媒介(BottleMedia)的默认视图(default))
1. API: 描述一个Service及其地址，协议规范等
2. Resource: 定义一个资源及其一系列相关的操作(Action)，以及这些操作所共用的一些属性
3. Action: 定义针对于某个资源的操作，包括方法(GET,POST等)，URL(可有多个)，参数(goa自动做类型检查，值检查等)等
4. Response: 定义一个响应，包括响应模板和承载内容(payload)，在代码中决定调用那个响应模板
5. MediaType: 定义Response返回的数据结构，一个Media可以有多个View，可在Response中指定返回的View

##### 新版本的DSL
![dsl](../picture/golang/goa-dsl.png)

1. 数据类型
    1. `Enum()`枚举
2. `API`：描述一个服务，可以对应多个环境或服务器
3. `Pattern`:todo
4. `View()`：设置不同的可见字段
    
    ```go
    View("tiny", func() {
		Attribute("id")
    })
    
    View("default", func() {
		Attribute("id")
		Attribute("name")
    })
    ```
5. 字段复用

问题：
1. attribute does not have "rpc:tag" defined in the meta
2. 在windows下执行相关命令报错：failed to run protoc: exit status 1: 'protoc-gen-go-grpc' .... --go-grpc_out: protoc-gen-go-grpc: Plugin failed with status code 1.
    1. 可能是protoc-gen-go-grpc没有安装，执行`go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@v1.1`安装一下

问题
1. panic: view "default" on field "nextNode" cannot be computed: view "default" on field "branches" cannot be computed: unknown view "default"
2. invalid CollectionOf argument: not a result type and not a known result type identifier (top level)
3. 文档中输入参数名称后面显示的是`any`
    1. `type(name, ...)`中name是`application/vnd.tsl.template`，应该把前缀``application/vnd.`去掉
4. collectionof 和arrayof

### gin
https://github.com/gin-gonic/gin

Gin的词源是金酒, 又称琴酒, 是来自荷兰的一种烈性酒

使用：
1. 遇到错误需要返回的时候要用`gin.Context.AbortXxx()`系列方法
    
    ```go
    if err != nil {
		c.AbortWithStatus(500)
		return
	}
    ```

### 静态网站工具 hugo
https://github.com/gohugoio/hugo

### echo
参考
1. 官方
    1. https://github.com/labstack/echo
    2. https://echo.labstack.com/

主要面向API

### micro/go-micro
#### asim/nitro
https://github.com/asim/nitro

由`micro/go-micro`的v1和v2转变而来，也就是现在的`asim/nitro`，变成了个人项目（go-micro所属公司的ceo名下）。

#### micro/micro
参考：
1. https://m3o.com/
1. https://micro.mu/
1. https://juejin.cn/post/6844903780736057357
4. https://github.com/micro/services:包含了很多真实示例的仓库
5. https://www.kancloud.cn/linimbus/go-micro

由`micro/go-micro`v3转变而来，不过有巨大变化：
1. 不再是一个纯粹的微服务框架，而是云原生开发/托管平台
2. 一般我们将 go-micro 视为框架，将 micro 视为工具箱，但这样的划分似乎没有意义。

micro是一个工具包toolkit合集，能帮助我们快速开发、调试微服务。

Micro解决了构建云本地系统的关键需求。它采用了微服务体系结构模式,并将其转换为一组工具,作为可伸缩平台的构建块。Micro隐藏了分布式系统的复杂性,并为开发人员提供了很好的理解概念。Micro是一个专注于简化分布式系统开发的微服务生态系统。是一个工具集合, 通过将微服务架构抽象成一组工具。隐藏了分布式系统的复杂性,为开发人员提供了更简洁的概念。Micro是一个微服务架构的一个框架，是一个插件化的框架，默认支持protobuf、grpc、consul。

Micro 采用插件化的架构设计，用户可以替换底层的实现，而不更改任何底层的代码。每个 Go-Micro 框架的底层模块定义了相应的接口，registry作为服务发现，transport 作为同步通信，broker 作为异步通信/异步消息总线。
```go
type Transport interface {
    Dial(addr string, opts ...DialOption) (Client, error)
    Listen(addr string, opts ...ListenOption) (Listener, error)
    String() string
}

type Registry interface {
    Register(*Service, ...RegisterOption) error
    Deregister(*Service) error
    GetService(string) ([]*Service, error)
    ListServices() ([]*Service, error)
    Watch() (Watcher, error)
    String() string
}

type Broker interface {
    Options() Options
    Address() string
    Connect() error
    Disconnect() error
    Init(...Option) error
    Publish(string, *Message, ...PublishOption) error
    Subscribe(string, Handler, ...SubscribeOption) (Subscriber, error)
    String() string
}
```

常用服务类型(待整理):
1. api：http接口服务，供用户访问
2. fnc（函数）
3. srv：内网的后台服务，供其他微服务内部访问
4. web
5. cli：用来写客户端, 生成command line程序，接口测试等

命名：micro中微服务的名字定义为[命名空间].[资源类型].[服务名]的，而micro api代理访问api类型的资源，比如go.micro.api.greeter，micro web代理访问web类型的资源，比如go.micro.web.greeter

broker代理：go-micro支持http/nats/memory三种broker,其中http是默认的broker。

使用：
1. 安装：`go get -u github.com/micro/micro`
2. 测试安装成功`micro --version`

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
   
通常我们见到的命令是怎么使用的：
1. `server version`中`server`是command，`version`是subCommand,同理`server help`中`help`是subCommand
2. `git clone URL --bare`,`clone`是一个subCommand，`URL`是参数，`--bare`是选项
2. `server -h`或`server --help`中的`-h`和`--help`是flags

cobra cmd的使用：
1. 初始化`cobra init --pkg-name projectNameA`
2. 增加子命令`cobra add subCmdA`，会在cmd子目录下创建`subCmdA.go`文件

cobra库的使用：
1. 结构体
    1. `cobra.Command`
        1. `PreRun func(cmd *Command, args []string)`
        2. `Run func(cmd *Command, args []string)`
3. `Flags().String(name string, value string, usage string) *string`:name是参数名称，value是默认值，usage是使用说明
4. `Flags().StringVarP(p *string, name, shorthand string, value string, usage string)`


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

## ORM And Driver
### gorm
https://github.com/go-gorm/gorm

中文参考：
1. https://gorm.io/zh_CN/docs/create.html

优缺点：
1. 优点
    1. 存储关系数据时，比Sqlx要少写许多代码
2. 缺点
    1. 文档稍微差了一点(细节不够)
    2. bug略多

使用：
1. 连接不同数据库的DSN格式和常用参数(todo)
    1. 参考：
        1. 官方：
            1. https://gorm.io/docs/connecting_to_the_database.html
        1. https://godoc.org/github.com/lib/pq
        1. https://www.postgresql.org/docs/current/external-interfaces.html
        1. https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING
    1. mysql:
        1. `charset=utf8` 客户端字符集为utf8
        2. `parseTime=true` 支持把数据库datetime和date类型转换为golang的time.Time类型
        3. `loc=Local` 使用系统本地时区
        1. `timeout`：建立连接超时时间，比如"30s", "0.5m" or "1m30s",比如`timeout=10s`
        2. `readTimeout`、`writeTimeout`:I/O读写超时时间
        6. `interpolateParams`默认为false
            1. 为true的时候，表示：
                1. 不会隐式地使用Prepared Statement，即在`db.Query()`和`db.Exec()`中不会使用Prepared Statement，但会自动转义来防止SQL注入，不能和多字节编码一起使用。
                2. 但可以显式地使用Prepared Statement，即`DB.Prepare`and `Stmt.Exec`
            2. 什么时候需要这个
                1. 在读写分离的架构下，如果prepare的时候sql发给了从库1，但是execute的时候因为从库1压力较大，sql命令发给了从库2，就会报错，这个时候就不能用Prepared Statement
        7. `maxAllowedPacket`：最大数据包大小，默认4Mb，如果设置为0，则会自动获取服务器的`max_allowed_packet`设置
            
        ```bash
        mysql://root:123456@tcp(127.0.0.1:3306)/yourdbname
        ```
    2. postgres
        1. 可知dsn的scheme使用`postgres`或`postgresql`都可以，但是调用`sql.Open(driverName, dataSourceName string) (*DB, error)`方法的时候，driverName要根据驱动来，比如使用`github.com/lib/pq`这个驱动，因为注册的时候使用的`	sql.Register("postgres", &Driver{})`，所以driverName必须是`postgres`
2. 预编译
    
    ```go
    // 它支持?作为预编译占位符，这样写的话会用到预编译
    db = db.Where("merchant_id = ?", merchantId)
    // 这样写的话就不会用到预编译，可能有SQL注入风险
    db = db.Where(fmt.Sprintf("merchant_id = %s", merchantId))
    ```
    
2. 查询
    1. 使用`join()`
    
        ```go
        db.Table("go_service_info").Select("go_service_info.serviceId as service_id, go_service_info.serviceName as service_name, go_system_info.systemId as system_id, go_system_info.systemName as system_name").Joins("left join go_system_info on go_service_info.systemId = go_system_info.systemId").Scan(&results)
        ```
    1. 使用原生语句查询
        
        ```go
        db.Raw("SELECT a.serviceId as service_id,a.serviceName as service_name, b.systemId as system_id, b.systemName as system_name FROM go_service_info a LEFT JOIN go_system_info b ON a.systemId = b.systemId").Scan(&results)
        ```
    3. 使用关联查询(https://gorm.io/zh_CN/docs/preload.html)
        1. 比如user表和profile表，profile表的UserID是外键，一般情况下，想要把user和对应的profile信息一起查出来，需要先查一次user表，再查一次profile表，再手动整合数据，但是用gorm自带的两种方式会更加便捷(虽然本质上也是查询的两次)

            ```sql
            -- 两种方式本质是一样的
            -- 方式一：使用Related
            DB.Model(&user).Related(&user.Profile, "UserID")

            -- 方式二：使用预加载Preload
            DB.Model(&user).Preload("Profile").First(&user) -- 单条
            DB.Model(&user).Preload("Profile").Find(&users) -- 列表
            ```
3. 创建：版本v2开始才支持批量创建
1. upsert的实现：有两种，区别在于`FirstOrCreate()`会执行两次SQL，而第二种方式只会执行一次
    1. `FirstOrCreate()`:
    2. 使用`gorm:insert_option`
    
        ```go
        db.Set(
            "gorm:insert_option",
            "ON DUPLICATE KEY UPDATE value = VALUES(value), updated_at = Values(updated_at)",
        ).Create(&model).Error
        ```
2. 常用配置
    1. 全局禁用表名复数:`SingularTable(true)`，不设置的话`User`的默认表名为`users`,设置后变成`user`。使用`TableName`设置的表名不受影响
    2. 日志：Gorm有内置的日志记录器支持，默认情况下，它会打印发生的错误。当启用`db.LogMode(true)`时，它会打印执行的每一条SQL

        ```go
        // 启用Logger，显示详细日志
        db.LogMode(true)
        // 也可以在每条db的开头单独打印
        xxx.db.Debug().Create()...
        ```
    4. `SetMaxOpenConns(100)`设置数据库连接池最大连接数
    4. `SetMaxIdleConns(20)`连接池最大允许的空闲连接数，如果没有sql任务需要执行的连接数大于20，超过的连接会被连接池关闭。
6. `DB.AutoMigrate(values ...interface{}) *DB`自动迁移,只会创建表、列和缺失索引的缺失，并不会改变现有的列的类型或删除未使用的列
7. 插入数组
    1. `插入text[]`可以使用`pq.StringArray`
    
问题：
1. `Record Not Found`错误会打印出来
2. 什么时候会出现`ErrRecordNotFound`这个错?当结果是struct类型，而没有查询到数据的时候就会抛出这个错误；当结果是slice类型，则不会抛出这个错误
3. all expectations were already fulfilled, call to Query ... was not expected
    1. 正常情况下是写漏了expect才会出现，但我当时是因为忘了mock方法出现的

### SQLX
https://github.com/jmoiron/sqlx

兼容sql原生包，同时又提供了更为强大的、优雅的查询、插入函数，高性能。

优缺点
- 优点：
    1. 文档优秀
    2. 支持问号(?)或命名的Prepared Statements，避免SQL注入的安全问题
- 缺点
    1. 因为它是SQL Builder不是ORM，所以不提供`Upsert`等函数

结构体
1. `sqlx.NamedStmt` – 对特定参数命名并绑定生成 SQL 语句操作。

使用：
1. 查询
    1. 查询单个：`db.Get()`
    2. 查询多个: `db.Select()`


### SQL Builer
有好几个：
1. dbr: https://github.com/gocraft/dbr
2. squirrel: https://github.com/lann/squirrel
3. sqrl: https://github.com/elgris/sqrl
4. gocu: github.com/doug-martin/goqu - just for SELECT query


#### squirrel
使用：
1. 如何实现`Upsert`:没有内置方法，但是可以借助`Suffix()`来实现
    
    ```go
    InsertBuilder.Suffix(ON DUPLICATE KEY UPDATE a = values.a ...)
    ```
2. 如何实现`IN`:借助`Or{}`

### mysql
github.com/go-sql-driver/mysql

![连接池架构图](../picture/golang/mysql_driver_architecture.jpg)

问题：
1. packets.go: busy buffer
    1. 解决办法
        1. tx 在执行Query()操作后，rows会维护这个数据库连接，当 tx 想再次调用当前连接进行数据库操作的时候，因为连接还没有断开，没有调用 rows.Close()，tx 无法再从连接池里获取当前连接，所以会提示 busy buffer。

### postgresql 
1. github.com/lib/pq
2. github.com/jackc/pgx
    1. It supports the PostgreSQL logical replication protocol.

### redis
github.com/go-redis/redis

参考：
1. https://redis.uptrace.dev/

使用：
1. 连接
    ```go
    opt, err := redis.ParseURL("redis://localhost:6379/<db>")
    if err != nil {
        panic(err)
    }

    rdb := redis.NewClient(opt)
    ```
2. 迭代hash
    
    ```go
    iterator := rdb.HScan(keyA, 0, "", numA).Iterator() // numA只影响第一次取出的数量(且依然不是百分百准备的数量)，后续迭代依然可以把keyA对应的所有hash迭代完，而不是仅仅迭代完第一次取的数量
	for iterator.Next() { 
		fmt.Println(iterator.Val())
	}
    ```


#### redis分布式锁
github.com/bsm/redislock

### mongodb
参考：
1. driver:
    1. https://github.com/mongodb/mongo-go-driver
    2. https://pkg.go.dev/go.mongodb.org/mongo-driver#section-readme
1. BSON类型
    1. https://docs.mongodb.com/manual/reference/bson-types/
    2. https://www.mongodb.com/json-and-bson


几个类型的区别：
1. `bson.M`:无序的bson文档，是一个map，属性是`bson.E`类型
1. `bson.D`:有序的bson文档，元素是`bson.E`类型
1. `bson.A`:bson文档中的数组类型
1. `bson.E`：

    ```go
    type E struct {
        Key   string
        Value interface{}
    }
    ```

使用：
1. json转bson：使用`func UnmarshalExtJSON(data []byte, canonical bool, val interface{}) error`
    1. 参数canonical参考：https://docs.mongodb.com/manual/reference/mongodb-extended-json/


## JWT
1. https://github.com/dgrijalva/jwt-go

使用
1. 生成签名

    ```go

    ```
1. 解析

    ```go
    // parse without validation and secret
    var (
    tokenString = ""
    )

    token, _, err := new(jwt.Parser).ParseUnverified(tokenString, jwt.MapClaims{})
    if err != nil {
        fmt.Println(err)
        return
    }

    if claims, ok := token.Claims.(jwt.MapClaims); ok {
        fmt.Println(claims)
    } else {
        fmt.Println(err)
    }
    ```

问题：
1. key is of invalid type
    1. key要用`[]byte`类型

## migrate工具
参考：
1. 主页：https://github.com/golang-migrate/migrate
2. 针对不同db的页面：https://github.com/golang-migrate/migrate/tree/master/database

使用后会在public下创建表schema_migrations表，里面存放的是当前migration的版本(version)以及状态(dirty)。

缺点：
1. 就算migrate up操作失败了，这个version还是会被up
2. golang-migrate只会记录最高的版本号，在协同开发的过程中，其他同事后创建的migrate不会执行

安装：貌似不能通过`go get`安装
1. win上的安装我是使用的scoop
2. mac使用brew

基本用法:
1. 创建迁移文件:`migrate create -ext sql -dir migrations create_users_table`,执行完这个命令会在migrations文件夹下创建两个文件，分别是：
    
    ```bash
    20190617061102_create_users_table.down.sql 
    20190617061102_create_users_table.up.sql
    # 20190617061102 是和时间有关的一个标识，用来区分migration的版本
    # 这两个文件都是空的，需要我们自己去填充
    ```
2. 升级
    1. 升级到最新版本:`migrate -source file://fileDirA -database xxx up`
        
        ```bash
        # postgresql in mac 
        migrate -source file://./migrations -database "postgres://postgres:@localhost:5432/hello?sslmode=disable" up 
        
        # postgresql in win
        migrate -source file://./migrations -database "postgres://postgres:@localhost:5432/example?sslmode=disable" up

        # mysql in mac
        migrate -source file://./migrations -database "mysql://root:123456@tcp(localhost:3306)/hello?" up
        ```
3. 回滚
    1. 回滚到最开始版本
    2. 回滚最新的一个版本:`migrate -source file://fileDirA -database xxx down 1`，同理，回滚前n个版本是`migrate -source fileDirA -database xxx down n`
    
参数：
1. `-verbose`

问题：
1. Dirty database version xxx. Fix and force version
    1. 需要解决对应的错误：修改SQL语句或者修改表数据，然后再强制操作`force xxx`,比如
        
        ```bash
        migrate -source file://./migrations -database "postgres://postgres:@localhost:5432/hello?sslmode=disable" force 20190617062220
        ```

## lint工具 
### golint
参考：https://pkg.go.dev/golang.org/x/lint

该包由官方提供但未包含在标准库中。不支持定制

关于不支持定制
1. 原因可见该讨论：https://github.com/golang/lint/issues/263
2. 比较中肯的观点：在社区中保证一致的编程规范是一件非常有益的事情，不过对于很多公司内部的服务或者项目，可能在业务服务上就会发生一些比较棘手的情况，使用这种过强的约束没有太多明显地收益。

### golangci-lint
https://github.com/golangci/golangci-lint

目前唯一的选择，缺点是坑很多：安装，使用各种坑

参考：
1. https://golangci-lint.run/
2. https://go-critic.github.io/overview

安装:
1. windows
    1. 去[release](https://github.com/golangci/golangci-lint/releases)下载对应版本,mac可以使用`brew install golangci-lint`，官方不建议使用`go get`安装(https://golangci-lint.run/usage/install/#local-installation)。
    2. 使用命令安装`curl.exe -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $env:GOPATH/bin latest`
    2. 本人实测，`go get`安装的确实可能有bug。比如
        1. 用release安装1.20.1，输入`golangci-lint version`显示`golangci-lint has version 1.20.1 built from 849044b on 2019-10-15T19:11:27Z`,然后检测a.go得到`ifElseChain`语法提示
        2. go1.14，使用`go get -u github.com/golangci/golangci-lint/cmd/golangci-lint@v1.20.1`安装后，输入`golangci-lint version`显示的是`golangci-lint has version v1.20.1 built from (unknown, mod sum: "h1:4aSxf2HvuoMNnaT4QMDpSLjoUBxgTn9q98ZKtEdtUW0=") on (unknown)`，然后检测相同的a.go文件却什么问题都没有(实际应该是有语法提示的才对)，并且对`.golangci-lint.yml`文件的支持也有问题。

使用
1. 指定配置文件运行，比如`golangci-lint run -c .golangci.yml ./...`

问题:
1. 安装问题
    1. 安装时提示"undefined: bidichk.Analyzer"等。主要是golang版本和golangci-lint版本不一致导致的
2. 使用问题
    1. "File is not `goimports`-ed with -local (goimports)"
        1. 可能原因1：包的引入代码的位置格式化不对
        2. 可能原因2：格式化方式配置得不正确。如果在goland中可能需要把Group勾选上
    2. 指定文件运行和...运行结果不一样，比如`golangci-lint run -c .golangci.yml a/...`和`golangci-lint run -c .golangci.yml a/b.go`,都包含b.go，但是输出结果不一样：前者输出有格式化，后者有时候却没有。(待研究)
    3. no such linter xxx
        1. 可能原因:golangci-lint版本太低。我当时是在go1.17下用的1.20的golangci-lint，把golangci-lint升级到1.43就好了。
    4. level=error msg="Running error: context loading failed: no go files to analyze"
        1. 场景一：更新了win的环境变量后运行lint就报这个错，然后执行下go build又好了
        2. 场景二：更新了go mod的某个包之后出现，同样执行下go build就好了
        3. 场景三：运行下go test后又好了
            1. 参考：https://github.com/golangci/golangci-lint/issues/825
    5. Can't run linter goanalysis_metalinter: failed prerequisites: buildssa ...
        1. 我是go1.14下出现的这个问题，除非切换回go1.13，否则目前无解，参考：https://github.com/golangci/golangci-lint/issues/827
    6. ERRO Running error: context loading failed: failed to load program with go/packages: could not determine GOARCH and Go compiler
    7. 2021-01-04:只是更新了go.mod的包，代码未改动，结果执行`golangci-lint`结果就不一样了

## sonyflake
参考
1. https://github.com/sony/sonyflake
1. https://blog.twitter.com/engineering/en_us/a/2010/announcing-snowflake.html

雪花算法snowflake是Twitter公司提出的唯一ID算法，广泛应用在各种业务系统中，而由snowflake的启发，衍生出很多改进算法，比如索尼公司的sonyflake算法。对比两种算法，sonyflake对于snowflake的改进有些像是用空间换时间，时间戳位数减少，以从69年升至174年。但是1秒最多生成的ID从409.6w降至2.56w条。(待确认)

twitter的雪花算法在一个机器，在1秒内 最多可以生成4096*1000约 400万个id，生成的id的二进制格式为`0 00100011100111101001100101110101111101000 0000000001 000000000000`

索尼雪花算法标准格式如下：id 是64位整型的
```
| 1 Bit Unused | 39 Bit Timestamp | 8 Bit sequence number  |   16 Bit machine 
```

结构体：
1. `Settings`

    ```go
    type Settings struct {
        StartTime      time.Time //起始时间，类似于snowflake的epoch，默认为2014-09-01 00:00:00 +0000 UTC
        MachineID      func() (uint16, error) //可自定义当前的机器id（或者线程id），默认是本机ip的低16位
        CheckMachineID func(uint16) bool // 可自定义检查machineid是否合法或冲突的函数。默认不做验证
    }
    ```

使用:
1. 生成的id是18位+的数字

```go
// 初始化
var sf = sonyflake.NewSonyflake(sonyflake.Settings{})

// 生成id
id, err := sf.NextID()
if err != nil {
    return "", err
}
return strconv.FormatUint(id, 16), nil
```

## 测试相关
参考：
1. https://www.jianshu.com/p/2f675d5e334e?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation

### 单元测试辅助工具 mock
https://github.com/golang/mock

能够对接口进行Mock，它主要包含两个部分：gomock库和辅助代码生成工具mockgen

使用：
1. gomock库
    1. 调用`EXPECT()`为你的模拟设置他们的期望值和返回值
    2. `Return(...)`模拟期望的返回值
    3. `Times(number)`预计调用次数
    4. `Do()`类似于钩子的作用
2. gomock代码生成工具
    1. 安装配置
        1. 安装`go install github.com/golang/mock/mockgen@v1.6.0`(注意不要使用`go install github.com/golang/mock/mockgen`来安装，安装完版本是`v1.4.4`)
        2. 查看版本`mockgen -version`
    1. 生成mock代码:生成的代码格式和命令以及mockgen的版本有关，注意保持mockgen的版本一致
        1. 直接命令行使用，比如`mockgen --source .../xxx.go --destination .../xxx.go`
        2. (推荐)mockgen还提供了一种通过注释及`go generate`生成mock文件的方式，比如在接口文件的注释里面增加：`//go:generatemockgen --source .../xxx.go --destination .../xxx.go`，然后执行`go generate`命令就可以自动生成mock文件了。
    2. 常用参数
        1. `-source`：指定接口文件
        2. `-destination`: 生成的文件名
        3. `-package`:生成文件的包名
        4. `-imports`: 依赖的需要import的包
        5. `-aux_files`:接口文件不止一个文件时附加文件
        6. `-build_flags`: 传递给build工具的参数

问题：
1. has already been called the max number of times
    1. `Call.Times(int)`:expected execute timers
2. Loading input failed: loading package failed certificate.go:1: running "mockgen": exit status 1
    1. 可能原因：我的文件名称是certificate.go，但是要generate的文件名称是cert.go。最后把我的文件改成cert.go就好了
3. `mockgen`生成的空xxx.mock.go引用了`gomock "github.com/golang/mock/gomock"`但是并没有使用
    1. 当时的版本是v1.4.3,升级到v1.6.0就好了
    
### sqlmock
https://github.com/DATA-DOG/go-sqlmock

模拟数据库的连接。

使用：
1. 最常用的几个方法就是 `ExpectQuery` 和 `ExpectExec`，前者主要用于模拟 SQL 的查询语句，后者用于模拟 SQL 的增删
    
    ```go
    func (s *suiteServerTester) TestRemovePost() {
        entry := pb.Post{
            Id: 1,
        }

        rows := sqlmock.NewRows([]string{"id", "author"}).AddRow(1, "draveness")

        s.Mock.ExpectQuery(`SELECT (.+) FROM "posts"`).WillReturnRows(rows)
        s.Mock.ExpectExec(`DELETE FROM "posts"`).
            WithArgs(1).
            WillReturnResult(sqlmock.NewResult(1, 1))

        response, err := s.server.RemovePost(context.Background(), &entry)

        s.NoError(err)
        s.EqualValues(response, &entry)
        s.NoError(s.Mock.ExpectationsWereMet())
    }
    ```
    
### httpmock 
https://github.com/jarcoal/httpmock

用于 Mock 所有 HTTP 依赖的包，它使用模式匹配的方式匹配 HTTP 请求的 URL，在匹配到特定的请求时就会返回预先设置好的响应。

```go
func TestFetchArticles(t *testing.T) {
	httpmock.Activate()
	defer httpmock.DeactivateAndReset()

	httpmock.RegisterResponder("GET", "https://api.mybiz.com/articles",
		httpmock.NewStringResponder(200, `[{"id": 1, "name": "My Great Article"}]`))

	httpmock.RegisterResponder("GET", `=~^https://api\.mybiz\.com/articles/id/\d+\z`,
		httpmock.NewStringResponder(200, `{"id": 1, "name": "My Great Article"}`))

	...
}
```

### testify
https://github.com/stretchr/testify

可以对测试代码按照簇进行组织

主要包和函数：
1. `assert`和`require`:都是断言，区别是`assert`如果失败不会退出，还是会继续往下执行，而`require`失败会直接结束
    1. `NoError()`
    2. `Equal()`
    3. `Panics()`
        
        ```go
        func TestOtherFunctionThatPanics(t *testing.T) {
            assert.Panics(t, OtherFunctionThatPanics, "The code did not panic")
        }
        
        func TestOtherFunctionThatPanics(t *testing.T) {
           assert.Panics(t, func() { OtherFunctionThatPanics(arg) }, "The code did not panic")
        }
        ```
    4. `Error(t TestingT, err error, msgAndArgs ...interface{})`:断言一个err不是nil，看源码可知它是直接跟nil比较的，感觉有时候会不准确，所以尽量少用。更推荐使用`Equal()`或者`EqualError()`
2. suite
    1. `SetupSuite`和`TearDownSuite`:是执行测试前后以及执行测试簇前后的钩子方法，我们能在其中完成一些共享资源的初始化，减少测试中的初始化代码。
3. mock


使用：
1. 简单示例
    
    ```go
    import (
        "testing"
        "github.com/stretchr/testify/suite"
    )

    type ExampleTestSuite struct {
        suite.Suite
        VariableThatShouldStartAtFive int
    }

    func (suite *ExampleTestSuite) SetupTest() {
        suite.VariableThatShouldStartAtFive = 5
    }

    func (suite *ExampleTestSuite) TestExample() {
        suite.Equal(suite.VariableThatShouldStartAtFive, 5)
    }

    func TestExampleTestSuite(t *testing.T) {
        suite.Run(t, new(ExampleTestSuite))
    }
    ```
### 打桩 gostub
github.com/prashantv/gostub

接口友好，可以对全局变量、函数或过程打桩。

原理：Stub方法先在map中保存变量指针和变量初始值，然后修改变量指针指向的值为桩。Reset方法将map中保存的所有变量指针指向的值修改为初始值。

使用：
1. 为变量打桩`sutbs := Stub(targetVar, mockVar)`:用mockVar代替targetVar，sutbs提供了`Reset`方法用于恢复targetVar。(Reset需要放在defer中吗？)
2. 为函数打桩:首先它不能对定义的函数(形如`func xxx(){}`)打桩，必须要声明成匿名函数，比如有匿名函数`var funcA = func (){}`，然后使用`StubFunc(&funcA, returnA, returnB...)`来打桩，当然也可以使用`Stub()`来打桩，不过`StubFunc`更简洁
3. `Stubs.Reset()`对所有全局变量或函数变量的桩进行回滚

最佳实践：
1. 因为不能直接对第三方库的代码进行打桩，所以可以在项目中增加adapter目录用于适配层，然后对适配层的代码进行打桩

    ```go
    // adapter适配层代码
    package adapter

    var FuncA = github.com/xxx/xxx

    // 实际使用代码
    xxx = adapter.FuncA()

    // 打桩代码
    stubs := StubFunc(&adapter.FuncA, returnA, returnB...)
    defer stubs.Reset()
    stubs.StubFunc(&adapter.FuncB, ...)
    stubs.StubFunc(&adapter.FuncC, ...)
    ```
    
### 猴子补丁
https://github.com/bouk/monkey

很强，能够通过替换函数指针的方式修改任意函数的实现，可以作为提供测试依赖的最终解决方案

注意下载和引入是`bou.ke/monkey`，github地址只是放的代码，而不是引入用的地址。

```go
monkey.Patch(fmt.Println, func(a ...interface{}) (n int, err error) {
    s := make([]interface{}, len(a))
    for i, v := range a {
        s[i] = strings.Replace(fmt.Sprint(v), "hell", "*bleep*", -1)
    }
    return fmt.Fprintln(os.Stdout, s...)
})
fmt.Println("what the hell?") // what the *bleep*?
```

注意：
1. 这种方法的使用其实有一些限制，由于它是在运行时替换了函数的指针，所以如果遇到一些简单的函数，例如 `rand.Int63n` 和 `time.Now`，编译器可能会直接将这种函数内联到调用实际发生的代码处并不会调用原有的方法，所以使用这种方式往往需要我们在测试时额外指定 `-gcflags=-l`(`go test -gcflags=-l ./...`) 禁止编译器的内联优化(实测指定了似乎也未必会生效)
2. 应该只在必要的时候使用这种方法，且不要在单元测试之外的地方使用猴子补丁

### ginkgo
https://github.com/onsi/ginkgo

社区中较常见的BDD框架，虽然不一定要使用 BDD/TDD 的思想对项目进行开发，但是却可以使用 BDD 的风格方式组织非常易读的测试代码。

BDD 框架中一般都包含 Describe、Context 以及 It 等代码块，其中 Describe 的作用是描述代码的独立行为、Context 是在一个独立行为中的多个不同上下文，最后的 It 用于描述期望的行为，这些代码块最终都构成了类似『描述……，当……时，它应该……』的句式帮助我们快速地理解测试代码。如下

```go
var _ = Describe("Book", func() {
    var (
        book Book
        err error
    )

    BeforeEach(func() {
        book, err = NewBookFromJSON(`{
            "title":"Les Miserables",
            "author":"Victor Hugo",
            "pages":1488
        }`)
    })

    Describe("loading from JSON", func() {
        Context("when the JSON fails to parse", func() {
            BeforeEach(func() {
                book, err = NewBookFromJSON(`{
                    "title":"Les Miserables",
                    "author":"Victor Hugo",
                    "pages":1488oops
                }`)
            })

            It("should return the zero-value for the book", func() {
                Expect(book).To(BeZero())
            })

            It("should error", func() {
                Expect(err).To(HaveOccurred())
            })
        })
    })
})
```

## 容器相关
### kubernetes
https://github.com/kubernetes/kubernetes

## IoT
### Paho
Paho是 Eclipse 的一个开源 MQTT 项目，包含多种语言实现，比如JAVA、golang

## cron
https://github.com/robfig/cron

```go
// 1. 最简单的使用
c := cron.New()
fn := func() {
    fmt.Println("hello")
}
if _, err := c.AddFunc("*/1 * * * *", fn); err != nil {
    log.Fatal(err)
}

c.Start()
defer c.Stop()
select {}
```

使用：
1. cron表达式：它的cron表达式是五个单位(从左到右分别是Minutes Hours DayofMonth Month DayofWeek)(待确认)，和linux的cron表达式不一样，linux的cron表达式是6个或7个单位
1. 关闭`(*Cron) Stop() context.Context`

问题：
1. expected exactly 5 fields, found 6

## HTTP&REST
### Resty
https://github.com/go-resty/resty

使用:
1. SetDebug
1. 客户端
    1. 设置代理

        ```go
        client := resty.New()
        client.SetProxy("http://proxyserver:8888")
        client.RemoveProxy()
        ```

2. 生成新的实例`R()`
1. 请求设置
    1. 请求头
        1. 请求头的`User-Agent`默认是"go-resty/2.3.0 (https://github.com/go-resty/resty)"
        2. `Authorization`：使用`SetAuthToken()`
    2. 请求体
        1. SetBody 参数类型为结构体或 map[string]interface{} 时， Resty 自动附加HTTP头 Content-Type: application/json ，当参数为string或[]byte类型时由于很难推断内容的类型，所以需要手动设置 Content-Type 请求头
    2. 请求结果
        1. 自动Unmarshal`SetResult(res)`:resty可以自动将响应数据 Unmarshal到res，如果res是结构体或者`map[string]interface{}`时，Resty自动附加HTTP头Content-Type: application/json，当参数为string或[]byte类型时由于很难推断内容的类型，所以需要手动设置Content-Type请求头

            ```go
            resty Request.Result
            ```
        2. `SetErro()`设置响应状态码非正常时返回的存储结构。if response status code is greater than 399 and content type either JSON or XML.
        3. `body`
            1. 需要defer 关闭吗
5. 钩子操作
    1. OnBeforeRequest 和 OnAfterResponse 回调方法，可以在请求之前和响应之后加入自定义逻辑

## rpc
### protoc
安装：
1. win(待补充)
1. mac：`brew install protobuf`

### protoc-gen-go
https://github.com/golang/protobuf/tree/master/protoc-gen-go

介绍：按照Go的代码风格，protoc-gen-go源码主要包含一下几个包：
1. main包
    1. doc.go 主要是说明。
    2. link_grpc.go 显式引用protoc-gen-go/grpc包，触发grpc的init函数。
    3. main.go 代码不到50行，初始化generator，并调用generator相应的方法输出protobuf的Go语言文件。
2. generator包
    1. generator.go 包含了大部分由protobuf原生结构到Go语言文件的渲染方法，其中 func (g *Generator) P(str ...interface{}) 这个方法会把渲染输出到generator的output（generator匿名嵌套了bytes.Buffer，因此有Buffer的方法）。
    2. name_test.go 测试，主要包含generator中名称相关方法的测试。
3. grpc包
    1. grpc.go 与generator相似，但是包含了很多生成grpc相关方法的方法，比如渲染转译protobuf中定义的rpc方法（在generator中不包含，其默认不转译service的定义）
4. descriptor 包含protobuf的描述文件（.proto文件及其对应的Go编译文件），其中proto文件来自于proto库（参见这里）
5. plugin 包含plugin的描述文件（.proto文件及其对应的Go编译文件），其中proto文件来自于proto库，参见这里

使用：
1. 安装`go get -u github.com/golang/protobuf/protoc-gen-go`
2. 查看版本`-version`：在较新的版本才支持

问题：
1. The import path must contain at least one forward slash ('/') character.
    1. 网友说的,2020年4月14日发布的v1.4.0以上的版本就要求必须加/了。所以最简单的解决办法是降级版本，比如`go get github.com/golang/protobuf/protoc-gen-go@v1.1.0`

### grpc

问题:
1. undefined: resolver.BuildOption 以及 undefined: grpc.SupportPackageIsVersion6
    1. 指定grpc版本`replace google.golang.org/grpc => google.golang.org/grpc v1.26.0`，然后重新生成.pb文件，不行的话再降级protoc-gen-go的版本`go get github.com/golang/protobuf/protoc-gen-go@v1.3.2`
2. rpc error: code = DeadlineExceeded desc = context deadline exceeded
    1. 可能原因：超时时间设置得太短

## 日志 
日志设计：
1. 

### zap
https://github.com/uber-go/zap

高性能

首先了解下常见日志级别：
1. debug：需要在调试过程中输出的信息，用于分析应用执行逻辑，不要在生产环境开启
2. info：需要持续输出的信息（无论调试还是发布状态），一般通过该信息可以看到每个请求的主要执行过程
3. warn：警告级别的信息（不严重），潜在的危险或值得关注的信息，系统还可以继续运行下去
4. error：错误信息（较严重），可能导致部分系统异常但不会影响核心业务和系统正常运行
5. fatal：严重错误（特别严重，比如引起崩溃式的错误），遇到此种错误应当立即报警并人工介入处理

使用：
1. 首先性能上分几种模式
    1. sugar：性能差点，但编码友好，适合一般后台业务场景
    2. desugar：编码稍微麻烦，但性能较好，适合高并发场景
2. 环境上分几种模式

    ```go
    var logger *zap.Logger
	if debug {
		logger, _ = zap.NewDevelopment()
	} else {
		logger, _ = zap.NewProduction()
	}
	zap.ReplaceGlobals(logger)
    ```
3. 注册全局的logger`ReplaceGlobals(logger *Logger) func()`
3. 重定向标准log库的输出到zap的logger
    1. `RedirectStdLog(l *Logger) func()`：把标准库的log.Logger的info级别的输出重定向到zap.Logger
    2. `RedirectStdLogAt(l *Logger, level zapcore.Level) (func(), error)`:把标准库的log.Logger的指定级别的输出重定向到zap.Logger
    
```go
logger, _ := zap.NewProduction()
defer logger.Sync() // flushes buffer, if any
zap.ReplaceGlobals(logger)
zap.S().Info("hello")

stdLog := zap.NewStdLog(logger)
stdLog.Println("this is standard logger but log with output to zap logger")

undo := zap.RedirectStdLog(logger)
log.Println("standard log will redirect to zap.Logger")
undo()
log.Println("standard log with original output")
```

```
// 基本使用：生成一个全局的logger然后传递给后续的服务
```

### sirupsen/logrus
https://github.com/sirupsen/logrus

## 证书
### mkcert
https://github.com/FiloSottile/mkcert

谷歌的Filippo Valsorda使用Golang开发的一个开源工具，使用非常简单，不需要进行任何配置，就可以生成任何你喜欢的域名的本地可信赖的开发证书。`mkcert`不会生成自签证书，它似乎只支持在本地环境使用。

使用：
1. 基本使用
    1. `mkcert -install`:创建并安装本地CA
    1. `mkcert ipA 域名A ...`：会生成基于这些地址的证书和私钥
        
        ```bash
        mkcert example.com "*.example.com" example.test localhost 127.0.0.1 ::1
        ```
2. 生成S/MIME邮件证书`mkcert myEmailA`
3. 移动设备：如果你想让你的证书在移动设备上面受信任，那么就必须安装rootCA。你可以使用`mkcert -CAROOT`来生成一个rootCA.pem的文件。

## json
### jsoniter
https://github.com/json-iterator/go

### Jeffail/gabs
https://github.com/Jeffail/gabs

用于处理冬天或未知json结构

### gjson

## kafka
### Shopify/sarama
https://github.com/Shopify/sarama

most popular,但不支持context

结构体等：
1. `ConsumerGroupHandler`

    ```go
    type ConsumerGroupHandler interface {
        // Setup is run at the beginning of a new session, before ConsumeClaim.
        Setup(ConsumerGroupSession) error

        // Cleanup is run at the end of a session, once all ConsumeClaim goroutines have exited
        // but before the offsets are committed for the very last time.
        Cleanup(ConsumerGroupSession) error

        // ConsumeClaim must start a consumer loop of ConsumerGroupClaim's Messages().
        // Once the Messages() channel is closed, the Handler must finish its processing
        // loop and exit.
        ConsumeClaim(ConsumerGroupSession, ConsumerGroupClaim) error
    }
    ```

使用：
1. 连接:golang连接kafka有三种client认证方式：
    - 无认证
    - TLS认证
    - SASL/PLAIN认证, (其他SASL/SCRAM, SASL/GSSAPI都不支持)
2. 生产
3. 消费
4. error的处理:建议放在单独的一个协程处理，防止影响了message的处理

### segmentio/kafka-go
https://github.com/segmentio/kafka-go

同时支持集群和context
    
## 依赖注入
uber的dig和Facebook的inject，这两个都是通过运行时注入的，使用运行时注入，会有一些问题，比如不好调试，错误提示不及时等，而wire采用不同的方式来实现，通过生成依赖注入的代码来解决问题，这样就和手写是一样的，只是减轻手写的麻烦

### google的wire
https://github.com/google/wire

```go
// model.go
type Foo struct {

}

func NewFoo() *Foo{
    return &Foo{}
}

type Bar struct {
    foo *Foo
}

func NewBar(foo *Foo) *Bar {
    return &Bar{
        foo:foo,
    }
}

func (p *Bar) Test(){
    fmt.Println("hello")
}

// wire.go：
package wire

import (
    wire "github.com/google/wire"
)

type Instance struct {
    Foo *Foo
    Bar *Bar
}

var SuperSet = wire.NewSet(NewFoo, NewBar)

func InitializeAllInstance() *Instance { // 方法名随意
    wire.Build(SuperSet, Instance{})
    return &Instance{}
}

// 执行wire命令，会读取到wire.NewSet里面的ProviderSet，通过分析各个函数的参数和返回值，来自行解决依赖，可以生成wire_gen.go：
func InitializeAllInstance() *Instance {
    foo := NewFoo()
    bar := NewBar(foo)
    instance := &Instance{
        Foo: foo,
        Bar: bar,
    }

    return instance
}
```

### uber的dig
### fackbook的inject
https://github.com/facebookarchive/inject

## 时间
### jinzhu/now
https://github.com/jinzhu/now

## 监控 prometheus 
参考：
1. 官方
    1. github.com/labstack/echo-contrib/prometheus
    2. 客户端库：github.com/prometheus/client_golang
2. 优秀文章
    1. https://studygolang.com/articles/17959
    2. https://blog.csdn.net/u012223939/article/details/88568477

Prometheus使用Go语言开发，是Google BorgMon监控系统的开源版本，它是开源监控报警系统和时序列数据库(TSDB)。最初由前谷歌SRE Matt T. Proud开发，并转为一个研究项目。在Proud加入SoundCloud之后，他与另一位工程师Julius Volz合作开发了Prometheus。后来其他开发人员陆续加入了这个项目，并在SoundCloud(SoundCloud是Prometheus的早期采用者)内部继续开发，最终于2015年1月公开发布。与Borgmon一样，Prometheus主要用于提供近实时的，针对动态云环境下的和基于容器的微服务、服务和应用程序的检测监控。

Prometheus专注于现在正在发生的事情，而不是追踪数周或数月前的数据。它基于这样一个前提，即大多数监控查询和警报都是从最近的，通常是一天内的数据生成的。Facebook在其内部时间序列数据库Gorilla的论文中验证了这一观点。Facebook发现85％的查询是针对26小时内的数据。Prometheus假定你尝试修复的问题可能是最近出现的，因此最有价值的是最近时间的数据，这反映在强大的查询语言和通常有限的监控数据保留期上。

部分架构：

![prometheus_architecture](../picture/golang/prometheus_architecture.jpg)

![prometheus_redundancy](../picture/golang/prometheus_redundancy.jpg)

架构及组件说明：
1. Prometheus Server ：主程序，负责抓取和存储时序数据；
2. Client Libraries：客户端库，负责检测应用程序代码；
3. Push Gateway：Push 网关，接收短生命周期的 Job 主动推送的时序数据；
4. Exporters：为不同服务定制的Exporter(如：HAProxy、StatsD、Graphite等) ，从而抓取它们的Metris指标数据；
5. Alert Manage：告警管理器，处理不同的告警；

概述：
1. 指标收集：Prometheus称其可以抓取的指标来源为端点（endpoint）。端点通常对应于单个进程、主机、服务或应用程序。为了抓取端点数据，Prometheus定义了名为目标（target）的配置。这是执行抓取所需的信息 - 例如，如何进行连接，要应用哪些元数据，连接需要哪些身份验证，或定义抓取将如何执行的其他信息。一组目标被称为作业（job）。作业通常是具有相同角色的目标组 - 例如，负载均衡器后面的Apache服务器集群，它们实际上是一组相似的进程。生成的时间序列数据将被收集并存储在Prometheus服务器本地，也可以设置从服务器发送数据到外部存储器或其他时间序列数据库。
    1. 使用 Prometheus 生成服务级别的指标时，有两个典型的方法
        1. 拉:内嵌地运行在一个服务里并在 HTTP 服务器上暴露一个`/metrics`端点,允许通过HTTP来暴露注册的metric
        2. 推:或者创建一个独立运行的进程，建立一个所谓的导出器。将注册的metric推送到Pushgateway?
2. 服务发现：可以通过多种方式处理要监控的资源的发现，包括：
    1. 用户提供的静态资源列表
    2. 基于文件的发现。例如，使用配置管理工具生成在Prometheus中可以自动更新的资源列表
    3. 自动发现。例如，查询Consul等数据存储，在Amazon或Google中运行实例，或使用DNS SRV记录生成资源列表
3. 聚合和警报：
    1. 聚合：服务器还可以查询和聚合时间序列数据，并创建规则来记录常用的查询和聚合。这允许你从现有的时间序列创建新的时间序列，例如计算变化率和比率或求和等聚合。这样就不必重新创建常用的聚合，例如用于调试，并且预计算可能比每次需要时运行查询性能更好。
    2. 报警：Prometheus还可以定义警报规则。这些是为系统配置在满足条件时触发警报的标准，例如，资源时间序列开始显示异常的CPU使用率。Prometheus服务器没有内置警报工具，而是将警报从Prometheus服务器推送到名为警报管理器（Alertmanager）的单独服务器。Alertmanager可以管理、整合和分发各种警报到不同目的地 - 例如，它可以在发出警报时发送电子邮件，并能够防止重复发送。
4. 查询数据和可视化
    1. 查询数据：Prometheus服务器还提供了一套内置查询语言PromQL，一个表达式浏览器以及用于浏览服务器上数据的图形界面。
    2. 可视化：可视化通过内置表达式浏览器提供，并与开源仪表板Grafana集成。此外，Prometheus也支持其他仪表板。
5. 自治：每个Prometheus服务器都设计为尽可能自治，旨在支持扩展到数千台主机的数百万个时间序列的规模。数据存储格式被设计尽可能降低磁盘的使用率，并在查询和聚合期间快速检索时间序列。
6. 冗余和高可用性：冗余和高可用性侧重弹性而不是数据持久性。Prometheus团队建议将Prometheus服务器部署到特定环境和团队，而不是仅部署一个单体Prometheus服务器。如果你确实要部署高可用模式，则可以使用两个或多个配置相同的Prometheus服务器收集时间序列数据，并且所有生成的警报都由可消除重复警报的高可用Alertmanager集群处理。

Prometheus有五种指标(metric)类型(时序数据)：前四种类型都有对应的Vector版本，GaugeVec, CounterVec, SummaryVec, HistogramVec，vector版本细化了prometheus数据模型，增加了label维度。
1. Counter(计数器)：表示单调递增的指标数据。它的值只会增加或在重启时重置为零。比如可以用来代表请求次数，错误数量，完成任务数等。
2. Gauge(计量器)：代表一个可以任意变化的指标数据，可增可减。比如协程数量，内存，队列数量，温度等。
3. Histogram(累积直方图/分布图/柱状图)：主要是样本观测数据，一段时间范围内对数据进行采样。比如请求持续时间，响应大小等。比如一个API里调用另外一个API，常可用于配合链路追踪系统。
    1. 字段
        1. `Buckets`表示duration的分布区间
4. Summary(摘要统计)：和Histogram类似，也是样本观测。但是它提供样本值的分位数，所有样本值的大小总和，样本总量。
5. 第5种metric为Untyped，它的运作方式类似Gauge，区别在于它只向prometheus服务器发送类型信号

客户端使用：
1. 创建指标
2. 实现指标
    1. 基于
3. 注册指标
    1. 基于Collector来注册：Collector用于采集prometheus metric，如果运行多个相同的实例，则需要使用ConstLabels来注册这些实例。实现collector接口需要实现Describe和Collect方法，并注册collector
    1. 默认注册
    3. 自定义注册
4. 收集指标

    ```go
    totalCounterVec.WithLabelValues(workerID, job.Type).Inc()
    ```
5. 暴露指标

```go
// 简单使用示例
// 创建指标模型
var counter = prometheus.NewCounterVec(
    prometheus.CounterOpts{
        Name: "test total", // 名称
    },
    []string{"method", "path"}, // 带上两个label
)

// 注册指标
prometheus.MustRegister(counter) // 可以注册多个

// 中间件使用，以gin为例
r := gin.New()
r.Use(func(ctx *gin.Context) {
    // 收集指标
    counter.With(prometheus.Labels{
        // 这里使用之前带上的label，可以只带其中部分
        "method": ctx.Request.Method,
        "path":   ctx.Request.RequestURI,
    }).Inc() // 加1 也可以用Add(1)
    ctx.Next()
})

// 自定义Collector todo
```

## 哈希
哈希和加密的区别(HASHING VS ENCRYPTION):哈希是摘要而不是加密，哈希也是一种单向函数。加密将明文数据转换为密文，然后在提供正确密钥后将其转换回明文，这是一种双向函数。与哈希不同，哈希不能逆转。 这是一个重要的区别。

### 慢哈希
为什么需要慢哈希：盐使攻击者无法采用特定的查询表和彩虹表快速破解大量哈希值，但是却不能阻止他们使用字典攻击或暴力攻击。高端的显卡（GPU）和定制的硬件可以每秒进行数十亿次哈希计算，因此这类攻击依然可以很高效。为了降低攻击者的效率，我们可以使用一种叫做密钥扩展的技术。这种技术的思想就是把哈希函数变得很慢，于是即使有着超高性能的GPU或定制硬件，字典攻击和暴力攻击也会慢得让攻击者无法接受。最终的目标是把哈希函数的速度降到足以让攻击者望而却步，但造成的延迟又不至于引起用户的注意。

慢哈希实现原理：todo

密码设计参考：
1. 在Web程序中，永远在服务器端进行哈希加密
    1. 如果在客户端加密，如果有人获取了这个哈希值，他甚至可以在不知道用户密码的情况通过认证
    2. 兼容性，客户端可能不支持js
    3. 不能代替HTTPS：如果浏览器和服务器之间的连接是不安全的，那么中间人攻击可以修改JavaScript代码，删除加密函数，从而获取用户密码
2. 如何重置密码
    1. 首先，需要随机生成一个一次性的令牌(不要把账户信息和失效时间存储在里面)，它直接关联到用户的账户。然后将这个令牌混入一个重置密码的链接中，发送到用户的电子邮箱。最后当用户点击这个包含有效令牌的链接时，提示他们可以设置新的密码。要确保这个令牌只对一个账户有效，以防攻击者从邮箱获取到令牌后，用来重置其他用户的密码。令牌有失效时间，且使用后立即就失效，当用户重新请求令牌时，或用户登录成功时，使原令牌失效。
    2. 不要通过电子邮件向用户发送新密码，同时也记得在用户重置密码的时候随机生成一个新的盐值用于加密，不要重复使用之前密码的那个盐值。
#### bcrypt
golang.org/x/crypto/bcrypt

使用：
1. 加密明文`GenerateFromPassword(password []byte, cost int) ([]byte, error)`
    
    ```go
    bcrypt.GenerateFromPassword([]byte(plainPwd), bcrypt.DefaultCost)
    ```
2. 比较明文和`CompareHashAndPassword(hashedPassword, password []byte) error`:将哈希密码与其纯文本进行比较


## OCR
### [gosseract](https://github.com/otiai10/gosseract)
基于Tesseract C++ library

## 数据类型
### 精确的浮点数
github.com/shopspring/decimal

方法：
1. `(d Decimal) Exponent() int32`: 首先判断是不是小数，如果是小数，返回小数的位数；其次判断原始数据是不是指数，如果是指数，返回末尾0的个数；其他返回0

使用：
1. 生成decimal
    1. 从字符串生成decimal:`.0`, `0.`, `.1`, `1.`, `001`可以正确生成，`.`不能正确生成

        ```go
        decimal.NewFromString("1e3") // 1000
        ```
2. 小数操作
    1. 保留小数位数

        ```go
        decimal.DivisionPrecision = 2 // 保留两位小数，如有更多位，则进行四舍五入保留两位小数
        ```
    1. 获取小数位数`decimal.Exponent()`

        ```go
        a := "-1.1e-3"
        float, err := decimal.NewFromString(a)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Println(float) // -0.0022
        fmt.Println(float.Exponent()) // -4

        float, _ := decimal.NewFromString("11011.00")
        fmt.Println(float) // 11011
        fmt.Println(float.Exponent()) // -2 
        ```
3. 指数：可使用`decimal.Exponent()`，但该函数不一定是获取指数

    ```go
    // 原始数据是指数表示，返回末尾0的个数
    float, _ := decimal.NewFromString("11011e3")
	fmt.Println(float.Exponent()) // 3

    // 虽然值一样，但原始数据不是指数表示，所以返回0
    float, _ := decimal.NewFromString("11011000") 
	fmt.Println(float.Exponent()) // 0

    float, _ := decimal.NewFromString("-6.55e50")
	fmt.Println(float.Exponent()) // 48
    ```
4. 系数：

    ```go
    // 正数
    -6.55e50 的系数是 -655
    -6.55 的系数也是 -655
    ```
3. 类型转换：从decimal转换为常见的数据类型`.String()`,`.Float64()`

## zip
github.com/alexmullins/zip

支持加密的zip包

```go
// 基本使用
zipFile, err := os.Create(zipPath)
if err != nil {
    svc.logger.Error("create zip file failed", zap.Error(err), zap.String("文件名", zipName))
    return nil
}
defer zipFile.Close()
archive := zip.NewWriter(zipFile)
defer archive.Close()
for _, fileName := range files {
    f, err := os.Open(filepath.Join(config.C.FilePath, fileName))
    if err != nil {
        svc.logger.Error("open csv file failed", zap.Error(err))
        return "", err
    }
    // 加密
    writer, err := archive.Encrypt(fileName, config.C.Password)
    if err != nil {
        svc.logger.Error("create zip writer failed", zap.Error(err), zap.String("文件名", zipName))
        return "", err
    }
    _, err = io.Copy(writer, f)
    if err != nil {
        svc.logger.Error("write zip data failed", zap.Error(err), zap.String("文件名", zipName))
        return "", err
    }
}
```

## ftp
### ftp server
https://github.com/fclairamb/ftpserver

### ftp client
1. https://github.com/jlaffaye/ftp
    1. 概述：
    3. 经验
        1. 报错
            1. 登录时EOF
            1. 上传文件:如果文件读取出错了或者`CWD`失败了，返回的是"553 Could not create file."而不是最开始的错误
2. https://github.com/secsy/goftp

## 文本和编码处理
golang.org/x/text

## 文件传输 croc
https://github.com/schollz/croc

概述：
1. 简单，安全，快速，跨平台
2. 传输中断可以恢复
1. 由于此工具是通过 relay server 方式来进行传送，所以指令会预设连到官方所搭建的服务器。


使用：
1. 传送和接收文件

    ```bash
    croc send ~/Downloads/file.txt # 默认会生成随机的secret code
    # 接收的时候就使用这个secret code来接收
    croc secret-code

    # 也可以自定义secret code(必需超过6个字符)
    croc send --code abcdef ~/Downloads/file.txt
    ```
2. 自己架设relay server：`croc relay`，默认会启动多个端口，也可以指定单一端口`croc relay --ports 8001`
2. 使用自己搭建的relay server`croc --relay 127.0.0.1:8001 send ~/Downloads/file.txt`

## 规则引擎

### gengine
https://github.com/bilibili/gengine


## WebSocket
https://github.com/gorilla/websocket

# 五 经验
## 1 为什么需要框架
对于golang而言，web框架的依赖要远比Python，Java之类的要小。自身的net/http足够简单，性能也非常不错。框架更像是一些常用函数或者工具的集合。借助框架开发，不仅可以省去很多常用的封装带来的时间，也有助于团队的编码风格和形成规范。

# 七 未整理
## 2 未整理
1. Google Cloud Platform是干嘛的