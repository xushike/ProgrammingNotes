# golang
[TOC]
## 一. 概述
1. 目前Go语言已经成为受欢迎的作为无类型的脚本语言的替代者： 因为Go编写的程序通常比脚本语言运行的更快也更安全，而且很少会发生意外的类型错误。
2. “如果一个特性并不对解决任何问题有显著的价值，那么Go就不提供它”的原则
3. Go语言在语言层面解决软件工程问题的设计哲学
### 1. go的一些常识
1. Go语言的标准库（通常被称为语言自带的电池）
2. Go语言原生支持Unicode，它可以处理全世界任何语言的文本。
3. Go语言反对函数和操作符重载（overload）
4. 支持匿名函数与闭包
5. Go程序并不要求开发者在每个语句后面加上分号表示语句结束，这是与C和C++的一个明显不同之处。
6. 以囊地鼠（Gopher）作为它的吉祥物,Rob Pike的妻子 Renee French绘制的
### 2. go的工具(命令)
Go语言提供的工具都通过一个单独的命令go调用
#### 2.1 run
#### 2.2 install
1. 首先说一下一般的go项目在GOPATH下的目录结构：
```bash
goWorkSpace  #goWorkSpace为GOPATH目录
  -- bin  #golang编译可执行文件的存放路径，可自动生成。
  -- pkg  #golang将可执行文件所依赖的各种package编译后的.a中间文件存放路径，可自动生成
  -- src  #源码路径。按照golang默认约定，go run，go install等命令的当前工作路径（即在此路径下执行上述命令）。
```
#### 2.3 build
#### 2.4 (格式化代码)
一般是在项目所在的目录下(不是GOPATH/src，当然也可以)执行该命令
2. 只需要有src目录，bin和pkg自动生成；install后是跟main.go的父级目录名，生成的可执行文件也是父级目录名；
### 3. go的工具
#### 3.1 Cgo
编译(静态编译?)一个或多个以.go结尾的源文件，链接库文件，并运行最终生成的可执行文件
### 4. go相关网站
1. 网友写的Go web编程gitbook，比较详细，应该很值得读：[https://astaxie.gitbooks.io/build-web-application-with-golang/zh/](https://astaxie.gitbooks.io/build-web-application-with-golang/zh/)
## 二. 安装配置
### 1 windows下的安装
1. ...
3. 配置GOROOT(C:\Go)和PATH(添加%GOROOT%\bin)，这样就可以在任意地方运行go开头的命令了
4. 配置GOPATH:系统默认的gopath是GOROOT，`fmt`等包在GOROOT中，所以可以直接`import`；当安装了gocode和gopkgs等工具时，还会算上安装工具的目录；但是如果`import`的目录不在这两者当中，那么就会报错找不到，所以要把自己go代码的目录加入到GOPATH中
>设置GOPATH的时候只需要写src前面的目录，会自动去src下找；设置了GOPATH之后，`import`时就只会去GOROOT和GOPATH中找；添加多个目录的时候Windows是分号，Linux系统是冒号，当有多个GOPATH时，大部分情况下会是第一个路径优先，比如：查找包、go get的内容默认放在第一个目录下

5.配置gobin(需不需要看情况)
### 2 mac下的安装
#### 2.1 二进制发行版安装
#### 2.2 第三方工具安装(homebrew等)
### 3 linux下的安装
#### 3.1 安装包（二进制发行版）安装(**推荐**)
1. 下载xxx.tar.gz，安装到`/usr/local`下:
```bash
#查看压缩文件内容
tar -ztvf xxx.tar.gz
#解压到目录下
sudo tar -zxvf xxx.tar.gz -C /usr/local 
```
2. 环境变量设置：
    1. 设置GOROOT:
        1. 只有go没安装在默认位置时才需要设置GOROOT，设置方式类似于JAVA_HOME，如`export GOROOT=$HOME/xxx`
        2. 不管go安没安装在默认位置都需要把`$GOROOT/bin`加入PATH：`export PATH=$PATH:$GOROOT/bin`
        
    1. 设置GOPATH：这个目录用来存放Go源码(src)，Go的可运行文件(bin)，以及相应的编译之后的包文件(pkg)
    >在go1.1到1.7，该变量必须设置，且不能和go安装目录一样;从1.8开始有默认值，在Unix上默认为`$HOME/go`,在Windows上默认为`%USERPROFILE%/go`
    
2. 有4个环境变量需要设置：GOROOT、GOPATH、GOBIN以及PATH，需要设置到某一个profile文件中(单一用户选择~./bash_profile，所有用户选择/etc/profile)
3. 关于GOBIN:
将`$GOPATH/bin`加入PATH中，这样可以方便的运行`go install`好的二进制程序。然而，当存在GOPATH中存在多个路径时，这种写法只会将最后一个路径跟上bin。在mac或linux下可以通过这种方式解决：
`${GOPATH//://bin:}/bin`
#### 3.2 源码安装
#### 3.3 第三方工具安装（apt、wget等）
## 三. 基础
### 1. 程序结构
#### 1.3 变量
1. 声明变量的语法
```go
//声明变量的方式1
var 变量名字 类型 = 表达式
```
其中“类型”或“= 表达式”两个部分可以省略其中的一个。如果省略的是类型信息，那么将根据初始化表达式来推导变量的类型信息。如果初始化表达式被省略，那么将用零值初始化该变量。
>数值类型变量对应的零值是0，布尔类型变量对应的零值是false，字符串类型对应的零值是空字符串，接口或引用类型（包括slice、map、chan和函数）变量对应的零值是nil。数组或结构体等聚合类型对应的零值是每个元素或字段都是对应该类型的零值。
零值初始化机制可以确保每个声明的变量总是有一个良好定义的值，因此在Go语言中不存在未初始化的变量。这个特性可以简化很多代码，而且可以在没有增加额外工作的前提下确保边界条件下的合理行为。

```go
//声明变量的方式2
var i, j, k int                 // int, int, int
var b, f, s = true, 2.3, "four" // bool, float64, string
```

初始化表达式可以是字面量或任意的表达式。在包级别声明的变量会在main入口函数执行前完成初始化，局部变量将在声明语句被执行到的时候完成初始化。例子如下：
```go
var f, err = os.Open(name) // os.Open returns a file and an error
```
在**函数内部**，有一种称为简短变量声明语句的形式可用于声明和初始化局部变量：
```go
//声明变量的方式3:简短变量声明
//注意":="是一个变量声明且赋值(如果已经声明，则只有赋值;)语句，而"="是一个变量赋值操作
anim := gif.GIF{LoopCount: nframes}
freq := rand.Float64() * 3.0
t := 0.0
i, j := 0, 1//这种同时声明多个变量的方式应该限制只在可以提高代码可读性的地方使用，比如for语句的循环的初始化语句部分
```
注意：`:=`是一个变量声明且赋值语句，而`=`是一个变量赋值操作;如果左边的变量已经声明，则只有赋值操作；简短变量声明语句中必须至少要声明一个新的变量
#### 1.6 包和文件
1. 网友推荐的包目录结构如下：
```bash
dir      
  -- goWorkSpace1   #主要是为了区分自己的鼓捣的一些东西和工作上的项目
  -- goWorkSpace2   #需要把两个workspace都加入gopath
        -- bin
        -- pkg
        -- src                  
           -- myApp1    #src下最好每个项目一个目录
              -- .git
              -- models
              -- controllers
              -- main.go 
           -- myApp2
              -- .git
              -- models
              -- controllers
              -- main.go 
           -- myApp3
              -- .git
              -- models
              -- controllers
              -- main.go
```

2. 同级目录下的文件不能定义不同package
3. 一般的: 
```bash
--config
    -- config.go    #假设config目录下有config.go文件
```
config.go中的package名称~~必须~~最好和目录config一致，而文件名可以随便。main.go表示main包，文件名建议为main.go。（注：**不一致时，生成的.a文件名和目录名一致，这样，在import 时，应该是目录名，而引用包时，需要包名。例如：目录为myconfig，包名为config，则生产的静态包文件是：myconfig.a，引用该包：import “myconfig”，使用包中成员：config.LoadConfig()**）
4. 简单总结就是:
```go
package 最后一层目录名(最好)or其他名字
import 源文件所在目录src后的完整路径名(go的import查找的是包的路径，并不是包名)
//使用时最后一层目录名or其他名字来调用
```
5. 可以用`./xxx`来import，这种方式不依赖GOPATH，但是不推荐
6. GOPATH和GOPATH下的src目录不应该添加到源代码管理中
### 1.x 注释
go的注释与C++保持一致
### 2. 数据类型
Go语言将数据类型分为四类：
1. 基础类型：包括数字、字符串和布尔型。
2. 复合类型(聚合)：通过组合简单类型，来表达更加复杂的数据结构，包括数组和结构体
3. 引用类型：包括指针、切片、字典、函数、通道，虽然数据种类很多，但它们都是对程序中一个变量或状态的间接引用
4. 接口类型：就是接口
#### 2.1 基础数据类型
#### 2.2 复合数据类型
##### 2.2.3 map

#### 2.3 引用数据类型
### 4. 函数
1. 所有go函数以`func`开头，
### 5. 方法
### 6. 接口
1. go的接口是非侵入式的，只要实现了接口里要求的全部方法，就实现了接口
    带来的优点是：
    1. 不用绘制类库的继承树图
    2. 不用纠结接口需要拆的多细
    3. 不用为了实现一个接口而专门导入一个包
2. 
### 7. Goroutines和Channels
#### 7.1 goroutine
是一种比线程更加轻盈、更省资源的协程.
### 8. 基于共享变量的并发
### 9. 包和工具
### 10. 测试
### 11. 反射
### 12. 底层编程
### 13. 错误处理
Golang 没有传统的异常机制。
对于非致命的错误，Golang 使用返回值来报告(Golang 支持多返回值).
对于致命的错误，Golang 直接选择“崩溃”掉(当然也有恢复机制), 不过按照 Golang 的哲学，既然是致命错误，就应当挂掉。
还有 defer 关键字，用于将一个语句“绑定”到函数退出时执行，无论是通过各种途径退出，这可是 C/C++ 里面的大问题。
## 五. 问题
1. 因式分解
2. lua
3. 编程范式
4. Erlang风格的并发模型
5. go支持Erlang语言为代表的面向消息编程思想
6. 不清楚go的稳定性，所以目前很多公司还不太敢用
7. 从源码安装软件怎么操作？二进制发行版和安装版的区别？
8. return的几种用法
9. go省略返回值形参，只有形参类型的写法