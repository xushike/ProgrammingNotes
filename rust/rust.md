# rust

# 一 概述
## 1 简介
特点如下(按优秀程序从大到小排序)：
1. 能够编译成二进制：意味着
    1. 易于部署/分发
    2. 方便交叉编译
2. 介于偏底层的系统语言（就像 C 或 C++ 语言）和基于运行时的语言（比如 Java 或 Python）之间，但更适用于系统编程领域。它是系统编程语言，系统编程语言说明它有直接操作硬件的能力，就像C/C++一样。(几乎)拥有对硬件的整体控制(内存布局，处理器功能)。相比之下Go 甚至不是系统编程语言，尽管使用它在后端基础架构上编写微服务和工具等非常棒，但我不希望使用它编写内核或内存分配器。
3. 内存安全。安全应对空指针、竞态条件和各种低级威胁。在C/C++里面，很容易会因为内存管理的问题而出现Segmentation Fault，在Rust中，由于引入了所有权（Ownership）和生存期（Lifetime）的概念，实现了自动内存管理的同时，还避免了各种内存错误。但同时，也提供unsafe块和祼指针（Raw Pointer），提供更多的自由度。可预测的运行时行为(零代价抽象 zero cost abstractions，无垃圾回收)，free of charge。相比之下Go为了保证语言的简洁性和正交性，将很多底层的操作推迟到运行时来进行。
4. 高性能高并发
    1. 具备更简单的多线程模型，类似于 C++ 或 Java。与go相比，具有更好的线程间通信能力，比如 MPSC channel（非常类似于 Go channel）
5. 工具:
    1. Rust 的 [cargo](https://github.com/rust-lang/cargo) 相当出色，完善的文档，并且可以轻松扩展子命令。
5. 高阶函数（闭包，Closure），C++11 之后也提供了Lambda来支持闭包，但在C中还没有。
6. 模式匹配（Pattern Match）和ADT（Algebraic Data Type），在C/C++中都没有提供。模式匹配和ADT在许多函数式编程语言中都作为标准来提供了。有了ADT，可以把许多操作都统一起来，并且利用模式匹配可以很方便地把其中的数据取出来。
7. 默认情况下不可变，这在C/C++中是完全相反。默认不可变更有利于编译器优化，而且不可变对于写并发程序有不少的好处。
8. Trait based OO（基于特征的面向对象），和普通OO不一样。
9. 具有强大的类型系统并支持泛型。它的设计哲学不同于 Go ，类型系统方面借鉴了 Haskell 和 C++
10. 发布周期:更加透明；核心团队在 YouTube 上记录了所有团队会议，你可以实实在在看到他们的讨论。特别是看到语言背后的设计思考和决策很有趣。Rust 具有明确的滚动发布周期，具有良好的稳定/测试版/尝鲜版说明。
9. 大家都说它学习曲线陡峭。开始确实比较难
    1. 独特的内存模型
    2. Rust 现在朝 Future 模型发展，其实就是我们已经熟悉的 async/await 模型，以同步的方式和思维编写代码，但以异步方式执行。
    3. Rust 还有一个功能非常强大的宏（macro）系统，可以使编译器做很多工作，比如生成代码，除此之外还有更多可以细粒度控制的细节。所以这意味着 Rust 的学习挑战很大。
12. Rust 的低开销非常适合嵌入式编程
13. Rust 已成为编写编译为 WebAssembly 的代码的首选语言

### 1.4 他人评价
网友:
1. Rust 更像是一个“实用的 Haskell (pragmatic Haskell)”，而不是“更安全的 C (safer C)”.
2. rust更像C++
3. 适用于对时间/空间要求苛刻的场景，比如微控制器。另一个重要场景就是 Web Assembly。在 Rust 社区中，构建编译成 Web Assembly 并跑在浏览器中工具非常多。于这一点我认为 Rust 更类似于C++。

亚马逊的 AWS 也在博客上发文表示赞助 Rust 语言，至于选择 Rust 的原因，其表示(https://amazonaws-china.com/cn/blogs/opensource/aws-sponsorship-of-the-rust-project/):
1. 性能。Rust 非常快且内存效率高：没有运行时或垃圾收集器，它可以为关键性能服务提供支持，可以在嵌入式设备上运行，并且可以轻松地与其他语言集成；
2. 可靠性。Rust 的丰富类型系统和所有权模型保证了内存安全性和线程安全性，并能使开发者在编译时消除许多类的错误。
3. 生产率。Rust 拥有出色的文档，友好的编译器以及有用的错误消息以及一流的工具——集成的软件包管理器和构建工具，具有自动完成和类型检查的智能多编辑器支持，自动格式化程序等。

## 2 历史
Rust 是由 Mozilla 开发人员 Graydon Hoare 在 2006 年开发的个人项目，从那个时候起，该语言就像它所命名的 Rust 真菌一样，开始传播，它今天被广泛应用于构建网络、嵌入式计算机、分布式服务和命令行。

Rust 编程语言核心团队有：
1. Carol Nichols--《The Rust Programming Language》一书的合著者

## 3 常识
### 3.1 模式匹配
模式匹配：多出现在函数式编程语言之中，为其复杂的类型系统提供一个简单轻松的解构能力。比如从enum等数据结构中取出数据等等。

## 4 文档等
1. 官方
    3. https://www.rust-lang.org/
    1. start：https://www.rust-lang.org/learn
    1. 在线练习场：play.rust-lang.org
2. https://rustlang-cn.org/
3. 大牛写的：https://rustcc.gitbooks.io/rustprimer/content/

# 三 基础

## 3 流程控制
### 3.1 match
match的功能仅仅是匹配，和其他编程语言的switch类似，要想发挥出它全部的威力，需要结合"模式匹配"来使用，从而实现解构等。和switch有两点不同：
1. match所罗列的匹配，必须穷举出其所有可能。当然，你也可以用 _ 这个符号来代表其余的所有可能性情况，就类似于switch中的default语句。
2. match的每一个分支都必须是一个表达式，并且，除非一个分支一定会触发panic，这些分支的所有表达式的最终返回值类型必须相同。可以简单理解为整个match是一个表达式，既然是一个表达式，那么它的结果就一定是某个类型的变量。

## 13 错误处理

## 15 注释

# 五 经验
## 1. 常用标准库
### Rayon
for writing parallel & data race-free code.

### serializing
for serializing and deserializing data.

### Tokio/async-std
for writing non-blocking, low-latency network services.

### tracing
for instrumenting Rust programs to collect structured, event-based diagnostic information.


# 七 未整理
1. 使用region式内存管理？
2. 没有runtime？