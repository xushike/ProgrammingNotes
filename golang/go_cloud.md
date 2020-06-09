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
https://github.com/goadesign/goa

Goa是一个基于中间件的golang web框架，其整体思想来源于koajs，并且结合了golang的特性。Goa致力于成为 web 应用和 API 开发领域中的一个更轻量、更高效的框架。Goa 并没有捆绑任何中间件，而是提供了一套优雅的方法，帮助您快速而愉快地编写服务端应用程序。

Goa采用了许多koajs的特性，部分API参照了gin源码。 goa-router则是完全基于高效、内存占用低的httprouter二次开发。

特点：轻量、灵活、高效、内置错误处理、多种格式支持

### gin
https://github.com/gin-gonic/gin

Gin的词源是金酒, 又称琴酒, 是来自荷兰的一种烈性酒

### hugo
https://github.com/gohugoio/hugo

### iris

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

## 静态网站生成 hugo
https://github.com/gohugoio/hugo

## ORM
### gorm
https://github.com/go-gorm/gorm

## JWT
https://github.com/dgrijalva/jwt-go

## NoSQL
### Redis
https://github.com/go-redis/redis

## 容器相关
### kubernetes
https://github.com/kubernetes/kubernetes

# 五 经验
## 1 为什么需要框架
对于golang而言，web框架的依赖要远比Python，Java之类的要小。自身的net/http足够简单，性能也非常不错。框架更像是一些常用函数或者工具的集合。借助框架开发，不仅可以省去很多常用的封装带来的时间，也有助于团队的编码风格和形成规范。

# 七 未整理
## 2 未整理
1. Google Cloud Platform是干嘛的