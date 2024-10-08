# cs计算机科学
[TOC]

# 一 概述
关于计算机、软件工程的大杂烩

## 4 文档资料等
1. 代码可读性心理学：https://medium.com/@egonelbre/psychology-of-code-readability-d23b1ff1258a

# 三 基础
## 1 一些概念和术语
### 1.1 MVC、MVVM
#### 模型-视图-控制器 (MVC) 
我们开发人员开发顺序是从底层（DB）往上面开发

#### 模型-视图-视图模型 (Model-View-ViewModel,MVVM) 
通俗易懂的解释：https://objccn.io/issue-13-1/

MVVM核心的思想就是视图是状态的函数：View = ViewModel(Model)，所以当Model发生改变时，ViewModel会来操作View来怎么做，而非是自己写代码来做。Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。

### 1.2 new,工厂模式和依赖注入的通俗易懂比较
参考：
1. [Spring依赖注入和实例化(new)的差别](http://blog.csdn.net/mrli113/article/details/70792498)

依赖注入使得我们面向接口而不是实现进行编程，大大降低了代码的耦合性，提高了可测试性。在小型系统里可有可无，但是在大型系统里，随着应用复杂度的增加，使用依赖注入会越来越重要.

不过依赖注入也是有争议的，缺点是降低了可读性

### 1.3 桩方法method stub
桩方法的维基百科:[https://en.wikipedia.org/wiki/Method_stub](https://en.wikipedia.org/wiki/Method_stub)
知乎网友的解释:[https://www.zhihu.com/question/24844900/answer/35126766](https://www.zhihu.com/question/24844900/answer/35126766)
看了基本就很容易理解了.

### 1.4 区块链
[比特币的技术缺陷：区块链信息越来越大怎么办？](http://ourjs.com/detail/59264ed1f1239006149616af)

### 1.5 框架
#### 他人评价
1. 而所谓框架，往往就是把大量重复的、琐碎的、做了一次就不想再来第二次的脏活、累活进行良好而优雅的封装，让使用框架的人可以只关注于自己的核心逻辑。
2. 在当今世界，对各种框架的了解是非常重要的。它们使你可以快速开发原型和实际项目。如果你在创业公司工作，那么你肯定希望能够立马装备一些炫酷的东西，那正是框架知识发光发热的地方。
### 1.6 压单

### 1.7 RPC
[如何编写高性能的 RPC 框架](https://my.oschina.net/u/1014759/blog/1618972)

### 1.8 分布式系统
### 1.9 中间件
### 1.10 用户从终端的输入
系统接收到的都是字符串

### 1.11 Hybrid App（混合模式移动应用）
是指介于web-app、native-app这两者之间的app，兼具“Native App良好用户交互体验的优势”和“Web App跨平台开发的优势”,一般将这个称谓混合开发

### 1.12 热修复补丁(hotfix)
热补丁的主要优势是不会使设备当前正在运行的业务中断，即在不重启设备的情况下，可以对设备当前软件版本的缺陷进行修复。

### 1.13 冷启动和热启动
冷启动:电脑断电后重启,内存的东西全部丢失
热启动:不断电重启(win的快捷键是`...`),所以叫热启动,内存的东西还在

### 1.14 纯函数
纯函数:简单来说，一个函数的返回结果只依赖于它的参数，并且在执行过程里面没有副作用，我们就把这个函数叫做纯函数。

副作用:修改在函数内容创建的变量不会产生副作用,但是修改传入的参数,修改外部变量,刷新浏览器,调用DOM改变了页面,以及console.log 往控制台打印数据都是产生了副作用.

纯函数的意义:因为纯函数非常“靠谱”，执行一个纯函数你不用担心它会干什么坏事，它不会产生不可预料的行为，也不会对外部产生影响。不管何时何地，你给它什么它就会乖乖地吐出什么。如果你的应用程序大多数函数都是由纯函数组成，那么你的程序测试、调试起来会非常方便。

### 1.15 IaaS,SaaS,PaaS,CaaS,FaaS和Serverless Architecture等
IaaS(Infrastructure-as-a-Service):基础设施即服务

PaaS(Platform-as-a-Service):平台即服务

SaaS(Software-as-a-Service):软件即服务

Functions as a Service:功能即服务，代表有k8s

CaaS（Communications-as-a-Service）：通讯即服务，代表有docker

Serverless Architecture:无服务架构，Serverless容器的特点：
1. 第一个特点是运行时沙箱会更频繁地创建和销毁
2. 第二个特点是切分的粒度会非常非常细, 细中细就是 FaaS, 一个函数就要一个沙箱. 因此就要求两点:
    1. 沙箱启动删除必须飞快
    2. 沙箱占用的资源越少越好

通俗点理解就是(可能不是非常准确):IaaS就是服务器和设备,PaaS就是操作系统和开发环境,SaaS就是软件

### 1.16 入参和出参
入参应该是传进来的参数,出参应该是返回的参数

### 1.17 串行（Serial），并行（Parallel）和并发（Concurrent）
简单图示参考：http://www.cnblogs.com/goxcheer/p/9299181.html

为什么需要并发：
1. 提升性能：
    1. 单核vs多核
    2. 降低系统的响应时间：比如一万个用户访问服务器，如果是单线程，我可能排队到9999...
2. 提升系统容错能力：某个线程出错，其他线程还能继续
3. 方便编写某些代码

并发的缺点：
1. 增加复杂度
2. 系统进行线程上下文切换时会消耗少量的系统资源

### 1.18 文本流和二进制流
我们在写C程序的时候经常会涉及到对流的操作，比如说从标准输入流读取一串字符串，然后通过标准输出流输出显示在屏幕上，这也就是所谓的IO操作。那么流究竟是什么东西？下面首先对流这个概念做一下解释。

#### 流（stream）的概念
计算机有很多外部设备，比如键盘、鼠标、CD-ROM驱动器、硬盘、网络接口、视频适配器等。这些设备都和IO操作有关系，而每种设备都具有不同的特性和操作协议。操作系统负责实现微处理器和和这些外设的通信细节，并向应用开发程序员提供更为简单和统一的IO接口，比如Linux操作系统下的`open()`，`read()`，`write()`等系统调用使我们可以以文件的形式打开并读写一个设备。
ANSI C进一步对IO的概念进行抽象。就C程序而言，所有的IO操作只是简单地从程序移进或者移出字节，这种字节流便被称为流（stream）。程序员只需要关心创建正确的输出字节数据，以及正确的解释从输入读取的字节数据，特定IO设备的细节对程序员是隐藏的。
因此流是一个高度抽象的概念，它将数据的输入和输出看作是数据的流入和流出，这样不管是什么IO设备：显示器、键盘还是硬盘，都被视为同一种东西。所以文件，socket，pipe等可以进行I/O操作的内核对象，都被视为同一种东西。都可以作为流的源和目的，对它们的操作，就是数据的流入和流出。

计算机等级考试的题目，答案是D：
```
A．流动的字节
B．流动的对象
C．流动的文件
D．流动的数据缓冲区
```

在LINUX系统中，文件分为两种：文本文件和二进制文件。在C语言中流分为两种类型：文本流（text stream）和二进制流（binary stream）。

#### 文本流
文本流是指在流中流动的数据是以字符的形式出现的。流中的每一个字符对应一个字节，用于存放对应的ASCII码值，因此文本流中的数据可以显示和打印出来，都是用户可以读懂的信息。比如数5678在文本流中的存放形式是：
ASCII码： 00110101 00110110 00110111 00111000
　　　　　↓ 　　　　↓　　　　↓ 　　　↓
十进制码： 5　　　　　6　　　　7　　　　8 
一共占用4个字节。
文本流的有些特性在不同的系统中可能不同。其中之一是文本行的最大长度，标准规定至少允许254个字符。文本流以EOF结束，另一个可能的不同是文本行的结束方式。例如在MS-DOS系统中，文本文件约定以一个回车符和一个换行符（也叫行反馈符）结尾；不过UNIX系统只使用一个换行符结尾。文本流中不能包含空字符（即ASCII码中的NULL）。

文本文件所占存储空间大，速度慢，但是便于对字符操作。
#### 二进制流
二进制流中的字节将完全根据程序编写它们的形式写入到文件或者设备中，而且完全根据它们从文件或者设备读取的形式读入到程序中。它们并未做任何改变，这种类型的流适于非文本数据，但是如果你不希望IO函数修改文本文件的行末字符，也可以把它用于文本文件。
二进制流中的数据是按照二进制编码的方式来存放文件的。比如数5678的二进制流中的存储形式为：00010110 00101110只占二个字节。二进制数据也可在屏幕上显示， 但其内容无法读懂。
二进制流比文本流更节省空间，且不用对换行符进行转换，这样可以大大加快流的速度，提高效率，二进制流没有行长度的限制，也可以包含空字符（NULL）。因此，对于含有大量数据信息的数字流，可以采用二进制流的方式；对于含有大量字符信息的流，则采用文本流的方式。

二进制文件所占存储空间小，速度快，便于存放中间结果。
#### 两种流的比较
二进制流是以二进制为最小单位进行编码，例如多少个bit代表什么，文本流是以字符来进行编码，约定好多少个字节（通常是以字节为单位）代表什么。

#### 流的两种访问方式
参考：
1. https://blog.csdn.net/u011402017/article/details/53747232

根据程序对文件的访问方式，分为两类：
1. 带缓冲区的文件操作（用户空间自动为正在使用的文件开辟内存缓冲区）：只需要少量的cpu状态切换
2. 不带缓冲区的文件操作：每次需要进行系统调用

额外的:
1. 标准io缓冲区类型：
  1. 行缓冲
  2. 全缓冲
  3. 无缓冲

### 1.19 序列化/串行化（serialization）和反序列化
通常所说的序列化就是将变量或对象转换为二进制数据

为什么需要序列化，而不直接传递对象：以java举例，在内存里可以直接传递对象，传递的是对象的引用。但要将对象传递到其他环境时(比如前端)，传对象过去对方可能就不知道怎么解析了，这个时候需要一个统一的协议，与语言无关，平台无关--序列化。

序列化的作用：（待整理）
1. 持久化
2. 远程方法调用（RPC）

常见协议序列化协议：
1. json
2. protobuf
3. xml

序列化和编码的区别：编码也是一种约定数据的含义的方式。与序列化不同，其约定的是更底层一些的数据含义，例如字符的表示，有ASCII、UTF-8、GBK等等，例如整数的表示，1=00000001一个字节，编码约定了数据格式的最小单元，序列化是依赖于字符编码之上的一种数据格式。

### 1.20 Host OS 和 Guest OS 是什麼
Host (或是叫做 Host OS )指的是用來安裝虛擬機器軟體的作業系統，而 Guest ( 也叫做 Guest OS) 則是指安裝在虛擬機器上的作業系統，舉例來說，阿舍在筆電上裝了 Winodws 7，然後在 Windows 7 上安裝了 VirtualBox 或 VMWare，接著，再把 Ubuntu 或 Windows XP 裝在 由 VirtualBox 或是 VMWare 建立的虛擬機器上，那麼，這個裝在 VirtualBox 或是 VMWare 虛擬機器的 Ubuntu 或是 Windows XP 就叫做 Guest OS，而阿舍原本筆電上安裝的 Windows 7 就是 Host OS

### 1.12 方法签名（method signature）
编程语言中的方法签名是什么：方法声明的两个组件构成了方法签名 - 方法的名称和参数类型。（Two of the components of a method declaration comprise the method signature—the method's name and the parameter types.）

比如，对于例子1的golang的方法，它的方法签名就是`func Add(int64,int64) bool`
```go
// 例子1
func Add(a int64, b int64) bool{
    return true
}
```

### 1.21 模块化

#### fan-in（扇入）和fan-out（扇出）
模块化编程，往细了说就是重复代码尽量提炼成函数。就涉及到扇入和扇出，扇入表示一个模块被多个模块调用，扇出表示一个模块调用多个模块。

设计函数的时候，要设计**高扇入合理扇出（3到4）**的函数。通俗点就是设计可以被很多函数调用，而它本身最好只调用3到4个下层函数的函数。

#### 柯里化(currying)
参考：
1. http://www.ruanyifeng.com/blog/2017/02/fp-tutorial.html


所谓"柯里化"，就是把一个多参数的函数，转化为单参数函数。

一般来讲优化代码有两个目的：
1. 提高性能
2. 使代码模块化，减少耦合增强其可维护性

柯里化的作用的就是第二种(?)。比如
```javascript
// 举个例子，你有一家商店，然后你想给你的优惠顾客10%的折扣：
function discount (price, discount) {
  return price * discount
}
// 当一个顾客消费了500元
const price = discount(500, 0.1) // $50

// 将这个函数柯里化，然后我们就不用每次都写那0.1了
function discount (discount) {
  return (price) => {
    return price * discount
  }
}
const tenPercentDiscount = discount(0.1)

// 现在，我们只需用商品价格来计算就可以了：
tenPercentDiscount(500) // $50

// 接下来，有些优惠顾客越来越重要，让我们称为vip顾客，然后我们要给20%的折扣，我们这样来使用柯里化了的discount函数：
const twentyPercentDiscount = discount(0.2)

// 我们为vip顾客使用0.2调用柯里化discount函数来配置了一个新的函数。这个twentyPercentDiscount函数会被用来计算vip顾客的折扣：
twentyPercentDiscount(500) // $100
```

柯里化的其他作用：（待补充）

我们很可能日常编码中已经用到了柯里化，只是自己没注意。

### 1.22 同步和异步（待补充）
在异步编程模式中，有两种获得上一个任务执行结果的方式，一个就是主动轮训，我们把它称为 Proactive 方式。另一个就是被动接收反馈，我们称为 Reactive。


依赖链（Dependency chain）：假定我们有一个事件依赖链是这样：睡觉 -> 吃饭 -> 饿了，很直觉的是，在这个依赖链中，只有满足了后面的条件，前面的才会执行。

这种依赖链是这个世界普遍的一种场景，一种正向的处理模式是，每隔一段时间就轮训检测是否满足睡觉的条件，在检查是否能睡觉的时候，会先检查是否已经吃饭，检查是否已经吃饭的时候，又会先检查是否饿了。那么这就是 Proactive 模式！而 Reactive 模式则反过来，先有事件的触发，然后事件来到响应方，响应方进行处理，这种方式也叫 Pub/Sub 模式。我们在 OOP 语言中，也会用到同样的概念和逻辑，我们把之叫做 Observer 模式。

### 1.23 事务

### 1.24 LAMP
LAMP是指一组通常一起使用来运行动态网站或者服务器的自由软件名称首字母缩写：
- Linux，操作系统
- Apache，网页服务器
- MariaDB或MySQL，数据库管理系统（或者数据库服务器）
- PHP、Perl或Python，脚本语言

虽然这些开放源代码程序本身并不是专门设计成同另几个程序一起工作的，但由于它们的廉价和普遍，这个组合开始流行（大多数Linux发行版本捆绑了这些软件）。当一起使用的时候，它们表现的像一个具有活力的“解决方案包”（Solution Packages）。其他的方案包有苹果的WebObjects（最初是应用服务器），Java/J2EE和微软的.NET架构。

### 1.25 信息茧房
信息茧房是指人们的信息领域会习惯性地被自己的兴趣所引导，从而将自己的生活桎梏于像蚕茧一般的“茧房”中的现象。由于信息技术提供了更自我的思想空间和任何领域的巨量知识，一些人还可能进一步逃避社会中的种种矛盾，成为与世隔绝的孤立者。在社群内的交流更加高效的同时，社群之间的沟通并不见得一定会比信息匮乏的时代来得顺畅和有效。

### 1.26 CVE
CVE 的英文全称是“Common Vulnerabilities & Exposures”通用漏洞披露。

### 1.27 实时系统和非实时系统
实时操作系统对一些中断的响应的时效性非常高，即使在内核态的时候。非实时反之。目前像VxWorks属于实时操作系统，大家常用的windows和linux都属于非实时操作系统，也叫做分时操作系统。

### 1.28 web工程师和软件工程师
来自西雅图的工程师John Washam认为：相较于web工程师，软件工程师需要掌握数据结构、算法、编译语言、内存优化等更深层次的编程知识。

之后，John 便开始投入精力学习，并将进入 Google 工作视为其成功掌握这项技能的判定标准。在学习的过程中，他开始接触大量与编程相关的知识与教学资源，秉着前人栽树后人乘凉的精神，John 在 GitHub 上开源了这份学习指南，并将其命名为「Google Interview University」（现已更名「Coding Interview University」）

即https://github.com/jwasham/coding-interview-university，谷歌面试大学

### 1.29 消息传递
首先了解消息从发送者到接收者的两种方式：
1. **即时消息通讯**：也就是说消息从一端发出后（消息发送者）立即就可以达到另一端（消息接收者），RPC就是方式的具体实现之一（当然单纯的http通讯也满足这个定义）
2. **延迟消息通讯**：即消息从某一端发出后，首先进入一个容器进行临时存储，当达到某种条件后，再由这个容器发送给另一端。 这个容器的一种具体实现就是消息队列，如RabbitMQ。

#### 消息队列
见MQ部分笔记

#### RPC(Remote Procedure Call)
首先要了解RPC协议和RPC实现是不同的，我们通常所说的RPC指的是RPC实现。

什么是RPC：RPC，远程过程调用，它是一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的思想。它是一种技术思想而非一种规范或协议。通俗地说，RPC允许跨机器、跨语言调用计算机程序方法。比如我用go语言写了个获取用户信息的方法getUserInfo，并把go程序部署在阿里云服务器上面，现在我有一个部署在腾讯云上面的php项目，需要调用golang的getUserInfo方法获取用户信息，php跨机器调用go方法的过程就是RPC调用。

为什么需要RPC：RPC是相对于LPC(本地过程调用)来说的，因为分布式的出现，促使了RPC的出现。

常见 RPC 技术和框架有：
1. 应用级的服务框架：
	1. 阿里的 Dubbo/Dubbox：阿里集团开源的一个极为出名的 RPC 框架，在很多互联网公司和企业应用中广泛使用。协议和序列化框架都可以插拔是极其鲜明的特色。
	2. Google gRPC：基于HTTP 2.0 协议，并支持常见的众多编程语言。RPC 框架是基于 HTTP 协议实现的，底层使用到了 Netty 框架的支持。
	3. Spring Boot/Spring Cloud
	4. Facebook的Thrift
	5. Twitter的Finagle
2. 远程通信协议：指明了程序如何进行网络传输和序列化。有RMI、Socket、SOAP(HTTP XML)、REST(HTTP JSON)。
  1. 实际情况是很少用HTTP协议，能用二进制传输为什么要用文本传输协议呢
3. 通信框架：MINA 和 Netty。

### 1.30 PKI(Public Key Infrastructure,公钥基础设施)
参考：
1. https://tools.ietf.org/html/rfc3280#section-4.1.2.2
2. golang
    2. https://golang.org/src/crypto/tls/generate_cert.go
    3. https://golang.org/src/crypto/x509/example_test.go

公钥基础设施是一个包括硬件、软件、人员、策略和规程的集合，用来实现基于公钥密码体制的密钥和证书的产生、管理、存储、分发和撤销等功能。

证书机构CA:证书机构CA是PKI的信任基础，它管理公钥的整个生命周期，其作用包括：发放证书、规定证书的有效期和通过发布证书废除列表(CRL)确保必要时可以废除证书。

注册机构RA:注册机构RA提供用户和CA之间的一个接口，它获取并认证用户的身份，向CA提出证书请求。它主要完成收集用户信息和确认用户身份的功能。注册机构并不给用户签发证书，而只是对用户进行资格审查。当然，对于一个规模较小的PKI应用系统来说，可把注册管理的职能由认证中心CA来完成，而不设立独立运行的RA。

数字证书的主流格式：
1. 通常都基于两种基础密码库：OpenSSL和Java。
    1. Tomcat、Weblogic、JBoss等，使用Java提供的密码库。通过Java的Keytool工具，生成Java Keystore（JKS）格式的证书文件。
    2. Apache、Nginx等，使用OpenSSL提供的密码库，生成PEM、KEY、CRT等格式的证书文件。
    3. 此外，IBM的产品，如Websphere、IBM Http Server（IHS）等，使用IBM产品自带的iKeyman工具，生成KDB格式的证书文件。微软Windows Server中的Internet Information Services（IIS），使用Windows自带的证书库生成PFX格式的证书文件。
2. 文件后缀和编码方式：(待整理)
    1. 编码方式主要有两种:`pem`和`der`，`pem`(Privacy Enhance Mail)PEM实质上是Base64编码的二进制内容(即对字符串格式私钥的文件化处理)，再加上开始和结束行，它是文本格式，Apache和*NIX服务器偏向于使用这种编码格式；`der`是二进制格式，Java和Windows服务器偏向于使用这种编码格式。不同文件后缀都可以用这两种编码方式
    1. 文件后缀
        1. `*.DER`、`*.CER`: 这样的证书文件是二进制格式，只含有证书信息，不包含私钥。
        2. `.CRT`: 这样的文件可以是二进制格式，也可以是文本格式，一般均为文本格式，功能与`.DER`、`*.CER`相同。
        3. `*.PEM`: 一般是文本格式，可以放证书或私钥，或者两者都包含。 `*.PEM`如果只包含私钥，那一般用`*.KEY`代替。
        4. `*.PFX`、`*.P12`、`.pkcs12`:一般有密码保护，存储的是已加密后的内容，是二进制格式，同时含证书和私钥，可以通过openssl转换成pem文件后进行处理。
    1. 格式之间可以转换
    2. 怎么判断是文本格式还是二进制？用文本工具打开，如果是规则的数字字母，如
        
        ```txt
        —–BEGIN CERTIFICATE—–
        MIIE5zCCA8+gAwIBAgIQN+whYc2BgzAogau0dc3PtzANBgkqh…
        —–END CERTIFICATE—–
        ```
        
        就是文本的，上面的BEGIN CERTIFICATE，说明这是一个证书,如果是—–BEGIN RSA PRIVATE KEY—–，说明这是一个私钥。还有更具体的区别：`-----BEGIN RSA PRIVATE KEY-----`是RSA直接生成没有进行转换的密钥格式，公钥可以直接使用，私钥需要转换格式；`-----BEGIN PRIVATE KEY-----`就是上面的密钥`PKCS#8`格式化后的密钥格式,java中用的私钥一般就是这种格式,但是公钥就不需要转换,可以直接使用。几种格式间都是可以转换的。
3. x509：X.509是一种非常通用的证书格式。所有的证书都符合ITU-T X.509国际标准，因此(理论上)为一种应用创建的证书可以用于任何其他符合X.509标准的应用。x509证书一般会用到三类文，key，csr，crt。
    1. Key 是私用密钥openssl格，通常是rsa算法。
    2. Csr 是证书请求文件，用于申请证书。在制作csr文件的时，必须使用自己的私钥来签署申，还可以设定一个密钥。
    3. crt是CA认证后的证书文，（windows下面的，其实是crt），签署人用自己的key给你签署的凭证。
    
### 1.31 UUID、GUID
参考：
1. [RFC 4122](https://tools.ietf.org/html/rfc4122)

UUID:UUID（全局唯一标识符，Universally Unique Identifier）是一个标准，由开放软件基金会(Open Software Foundation,OSF)制定,在分布式计算环境 (Distributed Computing Environment, DCE) 领域的一部份。UUID 的目的，是让分布式系统中的所有元素，都能有唯一的辨识资讯，而不需要透过中央控制端来做辨识资讯的指定。通常平台会提供生成UUID的API，用到了以太网卡地址、纳秒级时间、芯片ID码和许多可能的数字。格式为xxxxxxxx-xxxx-Mxxx-Nxxx-xxxxxxxxxxxxxxxx(8-4-4-16)(16进制)
1. M表示UUID的版本，有 5 个可选项：
    1. 版本 1：UUID 是根据时间和 MAC 地址生成的；
    1. 版本 2：UUID 是根据标识符（通常是组或用户 ID）、时间和节点 ID生成的；
    1. 版本 3：UUID 是通过散列（MD5 作为散列算法）名字空间（namespace）标识符和名称生成的；
    1. 版本 4 - UUID 使用随机性或伪随机性生成；
    1. 版本 5 类似于版本 3（SHA1 作为散列算法）
2. N表示UUID的变体。为了能兼容过去的 UUID，以及应对未来的变化，因此有了变体（Variants）这一概念。目前已知的变体有下面 4 种：
    1. 变体0：格式为 0xxx，为了向后兼容预留。
    1. 变体1：格式为 10xx，目前大多数使用的 UUID 大都是变体 1，N 的取值是 8、9、a、b 中的一个。8 的二进制为 1000，9 的二进制为 1001，a 的二进制为 1010，b 的二进制为 1011，都符合 10xx 的格式。
    1. 变体2：格式为 11xx，为早期微软的 GUID 预留。
    1. 变体3：格式为 111x，为将来的扩展预留，目前暂未使用
1. 标准实现：UUID标准的实现有很多，最常用的就是微软的GUID，其他还有COMB等。
2. 应用场景：UUID 的其他应用有文件系统，例如 GUID 分区表（UEFI 的一部分），或在数据库中用于取代传统整数作为记录主键。在互联网广告的上下文中，它们经常用于唯一地标识在 Web 上查看广告的用户。

GUID;GUID(全局唯一标识符，Globally Unique Identifier)是微软对UUID标准的实现。是一种由算法生成的二进制**长度为128位**(32位的16进制数字所构成)的数字标识符。GUID主要用于在拥有多个节点、多台计算机的网络或系统中,分配必须具有唯一性的标识符。在理想情况下，任何计算机和计算机集群都不会生成两个相同的GUID。GUID 的总数达到了2^128（3.4×10^38）个，所以随机生成两个相同GUID的可能性非常小(理论上能产生全宇宙唯一的值)，但并不为0。所以，用于生成GUID的算法通常都加入了非随机的参数（如时间），以保证这种重复的情况不会发生。
1. GUID 的格式为“xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx”(8-4-4-4-12)(16进制)，其中每个 x 是 0-9 或 a-f 范围内的一个十六进制数。例如：6F9619FF-8B86-D011-B42D-00C04FC964FF 即为有效的 GUID 值。

COMB:COMB（combine）型是数据库特有的一种设计思想，可以理解为一种改进的GUID，它通过组合GUID和系统时间，以使其在索引和检索事有更优的性能。它是由Jimmy Nilsson在他的“The Cost of GUIDs as Primary Keys”一文中设计出来的。基本设计思路是这样的：既然UniqueIdentifier数据因毫无规律可言造成索引效率低下，影响了系统的性能，那么我们 能不能通过组合的方式，保留UniqueIdentifier的前10个字节，用后6个字节表示GUID生成的时间（DateTime），这样我们将时间 信息与UniqueIdentifier组合起来，在保留UniqueIdentifier的唯一性的同时增加了有序性，以此来提高索引效率。

### 1.32 OCR(Optical Character Recognition,光学字符识别)
### 1.33 项目构建、依赖管理
gradle、maven、ant等

### 1.34 工作流
1. zeebe
    1. 参考
        1. https://zeebe.io/what-is-zeebe/
        1. https://github.com/zeebe-io/zeebe-get-started-go-client

### 1.35 web
web1: read 
web2: read, write
Web3: read, write, own

# 四 高级
## 1 未来方向
### 无服务器
[http://www.oschina.net/news/93020/talk-about-severless](http://www.oschina.net/news/93020/talk-about-severless)

## 3 DevOps
建DevOps目录

## 4 容器
## 5 微服务
### 5.1 经验

### Service Mesh(服务网格技术)
## 6 OpenStack

# 五 经验
1. 性能优化的常见手段：并发，预处理，缓存
    1. 池化：比如，创建一个 100 个元素的池，然后就可以在池子里面直接获取到元素，免去了申请和初始化的流程，大大提高了性能。释放元素也是直接丢回池子而免去了真正释放元素带来的开销。

## 1 coding style guideline
公司或者项目组最好能有一个这样的东西

# 六 问题
## 1 已解决
## 2 未解决
1. 可做笔记:[http://blog.csdn.net/lcg910978041/article/details/50696196](http://blog.csdn.net/lcg910978041/article/details/50696196)
2. "file should end with a newline (eofline)"

    参考stackoverflow:[https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline/729712#729712](https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline/729712#729712)

# 七 学习
1. [京东活动系统--亿级流量架构应对之术](https://my.oschina.net/u/3772106/blog/1611971)