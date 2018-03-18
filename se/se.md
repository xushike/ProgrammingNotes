# softwareEngineering软件工程
[TOC]
## 三 基础
### 1 一些概念和术语
#### 1.1 MVC、MVVM
##### 模型-视图-控制器 (MVC) 
我们开发人员开发顺序是从底层（DB）往上面开发

##### 模型-视图-视图模型 (Model-View-ViewModel,MVVM) 

#### 1.2 new,工厂模式和依赖注入的通俗易懂比较
[http://blog.csdn.net/mrli113/article/details/70792498](http://blog.csdn.net/mrli113/article/details/70792498)

依赖注入使得我们面向接口而不是实现进行编程，大大降低了代码的耦合性，提高了可测试性。随着应用复杂度的增加，使用依赖注入会越来越重要.

#### 1.3 桩方法method stub
桩方法的维基百科:[https://en.wikipedia.org/wiki/Method_stub](https://en.wikipedia.org/wiki/Method_stub)
知乎网友的解释:[https://www.zhihu.com/question/24844900/answer/35126766](https://www.zhihu.com/question/24844900/answer/35126766)
看了基本就很容易理解了.

#### 1.4 区块链
[比特币的技术缺陷：区块链信息越来越大怎么办？](http://ourjs.com/detail/59264ed1f1239006149616af)

#### 1.5 框架
##### 他人评价
1. 而所谓框架，往往就是把大量重复的、琐碎的、做了一次就不想再来第二次的脏活、累活进行良好而优雅的封装，让使用框架的人可以只关注于自己的核心逻辑。
2. 在当今世界，对各种框架的了解是非常重要的。它们使你可以快速开发原型和实际项目。如果你在创业公司工作，那么你肯定希望能够立马装备一些炫酷的东西，那正是框架知识发光发热的地方。
#### 1.6 压单

#### 1.7 RPC
[如何编写高性能的 RPC 框架](https://my.oschina.net/u/1014759/blog/1618972)

#### 1.8 分布式系统
#### 1.9 中间件
#### 1.10 用户从终端的输入
系统接收到的都是字符串

#### 1.11 Hybrid App（混合模式移动应用）
是指介于web-app、native-app这两者之间的app，兼具“Native App良好用户交互体验的优势”和“Web App跨平台开发的优势”,一般将这个称谓混合开发

## 四 高级
### 1 未来方向
#### 无服务器
[http://www.oschina.net/news/93020/talk-about-severless](http://www.oschina.net/news/93020/talk-about-severless)

### 2 JIT(Just in time compiling)
#### V8中的JIT
1. 缺点
    1. JIT 基于运行期分析编译，而 Javascript 是一个没有类型的语言，于是， 大部分时间，JIT 编译器其实是在猜测 Javascript 中的类型
#### AOT(Ahead of time)
### 3 DevOps
### 4 容器
### 5 微服务
#### Service Mesh(服务网格技术)
### 6 OpenStack

## 五 经验
### 1 coding style guideline
公司或者项目组最好能有一个这样的东西

## 六 问题
### 1 已解决
### 2 未解决
1. 可做笔记:[http://blog.csdn.net/lcg910978041/article/details/50696196](http://blog.csdn.net/lcg910978041/article/details/50696196)
2. "file should end with a newline (eofline)"

    参考stackoverflow:[https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline/729712#729712](https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline/729712#729712)

## 七 学习
1. [京东活动系统--亿级流量架构应对之术](https://my.oschina.net/u/3772106/blog/1611971)