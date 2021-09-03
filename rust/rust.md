# rust

# 一 概述
## 1 简介
特点如下(按优秀程序从大到小排序)：
1. 能够编译成二进制：意味着
    1. 易于部署/分发
    2. 方便交叉编译
2. 介于偏底层的系统语言（就像 C 或 C++ 语言）和基于运行时的语言（比如 Java 或 Python）之间，但更适用于系统编程领域。它是系统编程语言，系统编程语言说明它有直接操作硬件的能力，就像C/C++一样。(几乎)拥有对硬件的整体控制(内存布局，处理器功能)。相比之下Go 甚至不是系统编程语言，尽管使用它在后端基础架构上编写微服务和工具等非常棒，但我不希望使用它编写内核或内存分配器。
3. 内存安全（memory-safe）。安全应对空指针、竞态条件和各种低级威胁。在C/C++里面，很容易会因为内存管理的问题而出现Segmentation Fault，在Rust中，由于引入了所有权（Ownership）和生存期（Lifetime）的概念，实现了自动内存管理的同时，还避免了各种内存错误。但同时，也提供unsafe块和祼指针（Raw Pointer），提供更多的自由度。可预测的运行时行为(零代价抽象 zero cost abstractions，无垃圾回收)，free of charge。相比之下Go为了保证语言的简洁性和正交性，将很多底层的操作推迟到运行时来进行。
    1. 不使用 GC 使 Rust 奇快无比，特别是在需要保证延迟，而不仅仅是高吞吐量的时候
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
14. 非面向对象，从它所有权机制的创新可以看出这一点。但是面向对象的珍贵思想(封装和继承)可以在 Rust 实现

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
Rust 编程语言核心团队有：
1. Carol Nichols--《The Rust Programming Language》一书的合著者

Rust 是由 Mozilla 开发人员 Graydon Hoare 在 2006 年开发的个人项目，从那个时候起，该语言就像它所命名的 Rust 真菌一样，开始传播。它今天被广泛应用于构建网络、嵌入式计算机、分布式服务和命令行。

最早发布于 2014 年 9 月

2015 年，Mozilla 发布了 Rust 的首个稳定版本 v1.0。

2021年2 月 8 日，华为、微软、AWS、谷歌和 Mozilla 五大公司联合成立 Rust 基金会

## 3 常识
### 3.1 模式匹配
模式匹配：多出现在函数式编程语言之中，为其复杂的类型系统提供一个简单轻松的解构能力。比如从enum等数据结构中取出数据等等。

### 3.2 x..y
`x..y`，在rust中它是左闭右开的，即数学上的`[x,y)`
`x..=y`，等价于数学上的`[x,y]`
`..y`等价于 `0..y`
`x..`等价于位置 x 到数据结束
`..`等价于位置 0 到结束

### 3.3 深拷贝和浅拷贝
rust默认全是浅拷贝，想深拷贝使用`clone()`

## 4 文档等
1. 官方
    3. https://www.rust-lang.org/
        1. start：https://www.rust-lang.org/learn
        1. https://doc.rust-lang.org/book/
        1. 在线练习场：play.rust-lang.org
    2. https://rustlang-cn.org/
    3. 本地查看文档`rustup doc`
3. 大牛写的
    1. https://rustcc.gitbooks.io/rustprimer/content/
    2. http://www.sheshbabu.com/posts/rust-for-javascript-developers-tooling-ecosystem-overview/
    
## 6 相关项目
1. servo
2. deno

# 二 安装配置
## mac
1. 安装：有三种方式
    1. `brew install rust`：这种安装后没有`rustup`，所以不推荐
    2. `brew install rustup-init`，然后执行`rustup-init`,不过这样安装，要升级 rustup就不能用`rustup self update`，因为brew 接管了 rustup 的更新及卸载。
    3. `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
2. 查看是否成功安装`rustc --version` or `cargo --version`

## 配置
1. 设置源

# 三 基础

## 0 架构和常见词语
### 组织管理
Rust 中有三个重要的组织概念：箱(Crate)、包(Package)、模块(Module)

模块
1. 声明:使用关键字`mod`,模块默认都是私有的，除非带上`pub`

    ```rust
    // 模块
    mod nation {
        mod government {
            fn govern() {}
        }
        mod congress {
            fn legislate() {}
        }
        mod court {
            fn judicial() {}
        }
    }
    ```
2. 引入：rust默认将`.rs`文件当做一个模块，模块名就是文件名?但是普通的文件夹不能被rust编译器识别，需要在文件夹下创建`mod.rs`文件或者创建和文件夹同级的同名rs文件
    
    ```rust
    // 文件夹下模块的引入
    // 在main.rs中引用子目录
    // 方式一(推荐)：子目录中创建mod.rs文件，并在mod.rs文件中导出对应的模块
    src
    ├── main.rs
    └── user_info
        ├── mod.rs
        └── user.rs
    // user.rs
    pub fn say() {
        println!("hello")
    }
    // mod.rs
    pub mod user; // 导出模块，模块名需要和子目录下的文件名(user)相同
    // main.rs
    mod user_info; // mod 子目录名(user_info)
    fn main(){
        user_info::user::say();
    }

    // 方式二(不推荐):不使用mod.rs，而是在main.rs所在目录下创建同名的文件并导出对应的模块
    src
    ├── main.rs
    ├── user_info
    │   └── user.rs
    └── user_info.rs
    // user.rs
    pub fn say() {
        println!("hello")
    }
    // user_info.rs 文件名和子目录名需要一样
    pub mod user; // 导出模块，模块名需要和子目录下的文件名(user)相同
    // main.rs
    mod user_info; // mod 子目录名(user_info)
    fn main(){
        user_info::user::say();
    }
    ```
3. 调用

    ```rust  
    // 绝对路径从`crate`关键字开始, 相对路径从`self`或`super`关键字或一个标识符开始
    // 绝对路径
    crate::nation::government::govern();
    // 相对路径:从当前模块开始
    nation::government::govern();
    ```
4. 简写和别名:使用`use`关键字，它的作用就是简化调用的名称，比如`use std::f64::consts::PI;`然后就可以直接使用`PI`而不用加前面那么长的前缀了
    
    ```rust
    // 引用标准库
    // 所有的系统库模块都是被默认导入的，所以在使用的时候只需要使用 use 关键字简化路径就可以方便的使用了。
    use std::f64::consts::PI; 
    
    // use 关键字能够将模块标识符引入当前作用域并设置别名
    use crate::nation::govern as nation_govern;
    // use 关键字可以与 pub 关键字配合使用

    ```

### 访问权限
Rust 中有两种简单的访问权：公共（public）和私有（private），在没有声明`pub`的情况，默认都是私有的。

### 所有权(Ownership)
首先要明白的几点：
1. 内存安全
    1. 其他语言可能有的问题
        1. 空指针和悬空指针
    2. 其他语言实现内存安全大多是用垃圾回收
2. 堆栈分配：在Rust里，任何固定大小(在编译期可以知道的大小)，比如机器整数(machine integers)，浮点数类型，指针类型和一些其他类型会被存储在栈上。动态的和“不确定大小(unsized)”数据被存储在堆上。

所有权：
1. "dropped"丢弃:当某些值的所有者被“释放(freed)”，或者用Rust的术语“丢弃(dropped)”，那么这个被拥有的值也会被丢弃。这些值在什么时候被丢弃？这才是吸引人的地方。当这个程序离开了变量被生命的块(block)，这个变量就会被丢弃，变量的值也会被丢弃。一个块可以是一个函数，一个if语句，或者几乎是任何用大括号引入的代码块。
2. 如何保证每一个值都被唯一的变量拥有：Rust在进行类似赋值或者给函数传值的行为时，Rust把值移动给了新的拥有者(这是一个非常重要的概念，会影响我们在Rust中写代码的方式)
    
    ```rust
    // 例子1
    let name = "Pascal".to_string();
    let a = name;
    let b = name;
    // 在其他语言比如js中，可能会认为a和b都有一个对name的引用并且它们都指向相同的数据
    // 但在rust中会报错,因为把name赋值给b的时候，name实际上已经不再拥有值了。为什么呢？因为在这个时候，所有权已经被移动给a了
    // 额外很重要的一点是，所有的这种静态分析都是由编译器完成，而实际上并没有运行我们的代码。
    // 例子2 也是一样
    fn greet(name: String) {
        println!("Hello, {}!", name);
    }
    let name = "Pascal".to_string();
    greet(name);
    greet(name); // Move happened earlier so this won't compile
    
    // 例子3 就不会像上面那样，因为name变成了&str类型
    let name = "Pascal";
    let a = name;
    let b = name;
    ```
3. 如果我们真的想要有多个变量指向同一块数据该怎么实现。有两种方法
    1. 拷贝：对值进行拷贝或者克隆来处理这种情况可能是最简单但是开销最大的方式，因为最终还是要复制内存中的数据
        
        ```rust
        let name = "Pascal".to_string();
        let a = name;
        let b = a.clone();
        ```
    2. 借用(Borrowing)：使用借用符`&`对变量进行借用。通过`&`的借用，不会得到值的所有权，但是能够引用该变量。
        
        ```rust
        // 例子1 比如你只想打印值，而不想改变值的所有权
        fn greet(name: &String) {
            println!("Hello, {}!", name);
        }
        let name = "Pascal".to_string();
        greet(&name);
        greet(&name); // 可以多次借用
        // 例子2 
        let name = "Pascal".to_string();
        let a = &name;
        let b = a;
        ```

## 1 工具生态(Tooling Ecosystem)
1. Version Manager：`rustup` -- the Rust installer and version management tool
    1. 更新rust`rustup update`
    2. 本地查看文档`rustup doc`
2. Package：In Rust, we often refer to packages as “crates.”
    1. PackageManager：`Cargo`
        1. create your project with `cargo new projectNameA`
        2. 格式化`cargo fmt`
        3. 修复代码警告`cargo fix`
        1. build your project with `cargo build`
        2. run your project with `cargo run`
        3. test your project with `cargo test`
        4. build documentation for your project with `cargo doc`
        5. publish a library to crates.io with `cargo publish`
    2. Package Registry：`crates.io`
    3. Package Manifest：`Cargo.toml`
    4. Dependency Lockfile：`Cargo.lock`
    9. 依赖漏洞检查(Dependency Vulnerability Checker):cargo-audit
9. compilation tool：`rustc`
5. Task Runner：`make`, `cargo-make`
6. Live Reload：`cargo-watch`
7. Linter：`Clippy`
8. Formatter:`rustfmt`
9. 扩展
    1. rust search extension
        1. 参考
            1. https://rust.extension.sh/
        2. 安装后在地址栏输入rs就可以用这个扩展搜索了
        
问题
1. `cargo build`
    1. Blocking waiting for file lock on package cache
        1. 删了`~/.cargo/.package-cache`文件

## 2 变量,数据类型和运算符
Rust有自动判断变量类型的能力，但它是强类型语言

使用：
1. 类型可以使用别名，使用没区别

    ```rust
    type Age = u32 // Age可以表示u32类型了
    ```
2. 查看变量的类型：目前有两种方式，一种是借助编译器的错误提示，一种是借助代码
    
    ```rust
    // 借助std::any::type_name可以判断，但是文档说的别太依赖它，因为不同编译器版本的输出可能不一致
    fn temp() {
        let mut a = "abc";
        print_type_of(&a); // &str
    }

    fn print_type_of<T>(_: &T) {
        println!("{}", std::any::type_name::<T>())
    }
    ```

### 常量,不可变变量和可变变量
常量

变量分类：
1. 按可变性分可变变量和不可变变量
2. 按作用域分局部变量和全局变量

rust的变量分为不可变变量和可变变量：
1. 不可变变量：Rust 语言为了高并发安全而做的设计--在语言层面尽量少的让变量的值可以改变。它不可变，但可以重影/遮蔽(Shadowing)--用同一个名字重新代表另一个变量实体，其类型、可变属性和值都可以变化。

    ```rust
    // 简单例子
    let a = 123;
    // 有三个错误的写法和一个正确的写法
    a = "abc"; // incorrect,a已被确定为整型数字，不能把字符串类型的值赋给它
    a = 4.56; // incorrect,这个自动转换数字精度有损失，Rust 语言不允许精度有损失的自动数据类型转换(待确认)
    a = 456; // incorrect,a不是个可变变量
    let a = 456.2 ; // correct, Shadowing
    let mut a = "hello" ; // correct, Shadowing
    
    // Shadowing
    let mut a = Vec::new();
    let a = a; // a从可变变量变成不可变变量了
    ```
2. 可变变量：使用`mut`(英文mutable的简写)来声明，它仅仅是值可以变化。
    
    ```rust
    let mut a = 123;
    a = 456;
    let a = "hello"; // correct, Shadowing
    ```
    
变量的声明：使用`let`声明的都是局部变量，局部变量可以先声明后初始化，只要保证在使用前初始化就行了。
```rust
// 带类型的显式声明
let variable : i32 = 100;
// 声明多个变量
let (mut a, mut b)=(1,2);
// 先声明后初始化
let a;
a = 32;
```

### 2.1 基础数据类型/原始数据类型(primitive type)
原始类型的值和引用都存储在栈上

#### 字符 char
用于描述Unicode字符，大小为 4 个字节，代表 Unicode标量值

#### 字符串
rust有三种字符串类型,且他们三个是不同的数据类型:
1. `str`(`&'static str`)字符串字面量，它是基本数据类型，虽然它可以以字面量的方式来使用，但在实际使用中，字符串切片总是以引用的形式出现，也就是说使用的时候总是使用的`&str`而不是`str`--举个例子就是`"abc"`是`str`类型，`let a = "abc"`中的a就是`&str`类型。
    1. 有点难解释它是什么：它是引用自“预分配文本(preallocated text)”的字符串切片，这个预分配文本存储在可执行程序的只读内存中(即最终生成的二进制中)。换句话说，这是装载我们程序的内存并且不依赖于在堆上分配的缓冲区。
    
    ```rust
    // 字面量
    let hello: &'static str = "Hello, world!"; // They are 'static because they’re stored directly in the final binary, and so will be valid for the 'static duration.
    
    let hello = "Hello, world!"; // "Hello, world!"本身是str类型，hello变量是&str类型
    ```
2. `&str`类型：它借用了这个文本，表示字符串切片的引用，它能够引用String类型而无需复制
    1. 它占用两个字长
        1. 指向字符串值的指针
        2. 长度
    2. 它没有容量:字符串数组的值在堆上，没有在栈上存储容量信息，它只是对字符串数组的引用，它在栈上，不管理容量，`String`才管理容量。

        ```rust
        let hello = "Hello, world!"; // "Hello, world!"本身是str类型，hello变量是&str类型
        let len = hello.len(); // 获取长度
        assert!(hello.is_empty()); // 是否为空
        hello.as_bytes(); // 转换为字节切片
        hello.as_bytes_mut(); // 转换为可变字节切片
        ```
    3. 遍历
        
        ```rust
        // 通过字符迭代
        let word = "goodbye";
        let mut chars = word.chars();
        let count = word.chars().count();
        // 通过字节迭代
        let mut bytes = "bors".bytes();
        ```
    4. 经典示例
        
        ```rust
        // 例子1
        let str1 = "abc";
        let mut b = str1; // 此时b是&str类型
        b = "abd"; // pass, b是&str类型，"abd"是&'static str类型，&'static str可以赋值给&str类型，或者可以认为&'static str的赋值是借用？
        // 例子2
        let str1 = "abc";
        let mut b = &str1; // 此时b是&&str类型
        b = "abd"; // 报错, b是&&str类型，但"abd"是&'static str类型，&'static str不能赋值给&&str类型
        ```
3. `String`(`std::string::String`)类型：变量本身存储在栈上,指向的字符串值存储在堆上。因为值在堆上，所以它可以动态增长(前提是设置为mutable)。和`vec`的区别是，`String`只能存储标准UTF-8文本
    1. 对象存储在栈上，固定的三个字长(word)，分别是
        1. 实际的值指针：指向的值存储在堆上
        2. 容量
        3. 长度
    ```rust
    // 1. 声明String类型,使用"xxx".to_string()或者String::from("xxx")
    let s = "Have a nice day".to_string(); 
    let mut s = "Have a nice day".to_string();
    let b = String::from("tom");
    // 追加文本
    s.push_str( " Precht");
    ```

Rust为什么同时具有`String`和`&str`:安全性，正确性和性能。(待整理)

#### 布尔
#### 整型(Integer)

1. 声明

    ```rust
    // 不指定类型的情况下默认会被推导为32位整型
    let a = 123;
    let a: u64 = 123; // 指定类型

    // 字面量后面可以跟后缀，代表数字的具体类型
    let var1 = 123usize; // 1变量是usize类型
    let var2 = 0x_ff_u8; // 2变量是u8类型
    let var3 = 32; // 整数不写类型,默认为 i32
    let var4 = 100i64; // i64
    ```
2. 对于溢出的处理：在debug模式下，会自动插入整数溢出检查，一旦发生溢出，引发panic。在release模式下不检查整数溢出，采用自动舍弃高位的方式


#### 浮点数型(Floating-Point)
与其它语言一样支持 32 位浮点数`f32`和 64 位浮点数`f64`，默认是`f64`类型

在标准库中，有一个`std::num::FpCategory`枚举，表示了浮点数可能的状态：
```rust
enum FpCategory {
    Nan,       // 不是数字，举例：0.0f32 / 0.0
    Infinite,  // 无穷大，举例：1.0f32 / 0.0
    Zero,      // 0
    Subnormal, // 当浮点数小到无法在指定范围内合理表达的程度，进入此状态。精度会低些
    Normal,    // 表示正常浮点数
}
```

### 2.2 复合数据类型
#### 枚举 enum
初看不像其他语言那么简单

```rust
// 1. 声明
// 普通声明
 enum Book {
    Papery,
    Electronic,
}
let book = Book::Papery;
println!("{}", book);
// 元组字段声明
enum Book {
    Papery(u32),
    Electronic(String),
}
let book = Book::Papery(1001);
// 结构体字段声明
enum Book {
    Papery { index: u32 },
    Electronic { url: String },
}
let book = Book::Papery{index: 1001};

// 2. 判断和使用枚举 
// 不能直接使用枚举，比如book就不能直接使用，需要结合match使用
match book {
    Book::Papery { index } => {
        println!("Papery book {}", index);
    },
    Book::Electronic { url } => {
        println!("E-book {}", url);
    }
}
```

#### 元组
元组用一对`()`包括的一组数据来表示，可以包含不同种类的数据

```rust
// 1. 元组的声明
// 0个元素，此时称为unit tuple(单元元组)，占用0内存空间
let a = ();
// 单个元素
let a = (0);
let a = (0,);
// 多个元素
let tup: (i32, f64, u8) = (500, 6.4, 1);
println!("{}",tup.0); // 500
let (x, y, z) = tup; // 可以用js解构的方式获取其中的数据
println!("{}",y); // 500
// 不显式声明类型
let a = (2,3);
// 嵌套
let a = ("b", (1i32, 2i32));
// 2. 获取元组中的元素，有两种方式
// 数字索引
let tup: (i32, f64, u8) = (500, 6.4, 1);
println!("{}",tup.0); // 500
// 模式匹配, 类似js解构的方式
let (x, y, z) = tup; 
println!("{}",y); // 500
```

#### 数组
数组用一对`[ ]`包括的同类型数据来表示

```rust
// 声明
let a = [1, 2, 3, 4, 5];
let c: [i32; 5] = [1, 2, 3, 4, 5]; // c 是一个长度为 5 的 i32 数组
let d = [3; 5]; // 等同于 let d = [3, 3, 3, 3, 3];
a[0] = 123; // 错误：数组 a 不可变
let mut a = [1, 2, 3];
a[0] = 4; // 正确

// 在函数中传递数组
fn single_nubmer(arr: [i32; 7]) -> i32 {
    let mut res = 0;
    for e in arr.iter() {
        res = res ^ e;
    }
    return res;
}
```

使用：
1. 遍历
    
    ```rust
    // 1. 
    let a = [10, 20, 30, 40, 50];
    let mut index = 0;
    while index < 5 {
        println!("the value is: {}", a[index]);

        index += 1;
    }
    // 2. 
    let vec = vec!['a', 'b', 'c'];
    for i in 0..vec.len() {
        println!("{}", vec[i]);
    }
    
    // 3. 
    let vec = vec!['a', 'b', 'c'];
    for i in vec {
        println!("{}", i);
    }
    
    // 4. 
    for element in a.iter() {
        println!("the value is: {}", element);
    }
    ```

#### 向量
向量（Vector）是一个存放多值的单数据结构，该结构将相同类型的值线性的存放在内存中。向量是线性表，在 Rust 中的表示是 `Vec<T>`，向量类似一个数组(array)或者列表(list)，但它是动态增长的。所以向量的长度无法从逻辑上推断。

```rust
// 声明
let vector = vec![1, 2, 4, 8];     // 通过数组创建向量
let vector: Vec<i32> = Vec::new(); // 创建类型为 i32 的空向量

// 遍历
for num in vector {
    // do something
}
// 取出向量中的值
v[1]); // 不安全
v.get(0); // get是一种安全的取值方法,返回值是 Option 枚举类，有可能为空

// 追加单个元素
vector.push(16);

// 拼接两个向量
v1.append(&mut v2);
```

#### 切片(slice)
rust的切片一定是引用类型，写法是`&T[x..y]`，`T`是某个线性数据结构的变量名

```rust
// 基于字符串切片
let s = String::from("broadcast");
let part1 = &s[0..5];
let part2 = &s[5..9];
println!("{}={}+{}", s, part1, part2);
// 基于数组切片
let arr = [1, 3, 5, 7, 9];
let part = &arr[0..3];
let part2 = &arr;

// 在函数中使用切片
fn single_nubmer_slice(slice: &[i32]) -> i32 {
    let mut res = 0;
    for e in slice.iter() {
        res = res ^ e;
    }
    return res;
}
```

#### 结构体
```rust
// 一 定义结构体
// 1. 定义普通结构体
struct Site { // struct关键字只能用来定义结构体的字段
    domain: String, // 而且每个字段定义之后用逗号分隔
    name: String,
    nation: String, 
    found: u32
} // 结尾不需要分号

// 还可以定义没有字段的结构体，这种结构体称为单元结构体（Unit Struct）
struct UnitStruct;

// 2. 定义元组结构体，元组结构体的成员只有类型，没有名字
struct Color(u8, u8, u8); 
let black = Color(0, 0, 0);
println!("black = ({}, {}, {})", black.0, black.1, black.2);

// 二 声明结构体实例
let name = String::from("RUNOOB");
let runoob = Site {
    domain: String::from("www.runoob.com"),
    name, // 如果实例化的结构体字段名称和现有变量名称一样，可以简化书写(和js一样)
    nation: String::from("China"),
    found: 2013
};

// 三 声明结构体方法(Method)
impl Rectangle {
    fn area(&self) -> u32 { // 结构体方法的第一个参数必须是 &self，不需声明类型，self是关键字
        self.width * self.height
    }
    
    fn wider(&self, rect: &Rectangle) -> bool {
        self.width > rect.width
    }
}
let rect1 = Rectangle { width: 30, height: 50 };
println!("rect1's area is {}", rect1.area()); // 在调用结构体方法的时候不需要填写 self ，这是出于对使用方便性的考虑

// 四 声明结构体函数:结构体函数不依赖实例，使用的时候需要声明是在哪个impl块中，比如`String::from`就是结构体函数
impl Rectangle {
    fn create(width: u32, height: u32) -> Rectangle {
        Rectangle { width, height }
    }
}

// 五 获取结构体字段值
// 1. 普通获取
// 2. 模式匹配
let Site {
    domain,
    name,
    found,
    nation,
} = runoob; // 字段顺序可以不一致
println!("{}", found); // 2013

let Site {
    domain,
    name,
    found,
    .. // 只想获取其中部分字段的话需要省略掉其他字段
} = runoob;

let Site {
    domain: domain_a, // 绑定到新的变量
    name: name_a,
    found: found_a,
    ..
} = runoob;

// 六 结构体更新语法：利用已有的结构体实例创建新的结构体实例
// 不过这种语法不允许一成不变的复制另一个结构体实例，意思就是说至少重新设定一个字段的值才能引用其他实例的值
let site = Site {
    domain: String::from("www.runoob.com"),
    name: String::from("RUNOOB"),
    ..runoob
};

// 七 封装结构体：使用pub关键字
pub struct ClassName {
    pub field: Type,
}

impl ClassName {
    pub fn new(value: i32) -> ClassName {
        ClassName {
            field: value
        }
    }
    
    pub fn public_method(&self) {
        println!("from public method");
        self.private_method();
    }

    fn private_method(&self) {
        println!("from private method");
    }
}

fn main() {
    let object = ClassName::new(1024);
    object.public_method();
}

// 八 继承：Rust 没有提供跟继承有关的语法糖，也没有官方的继承手段（完全等同于 Java 中的类的继承），但灵活的语法依然可以通过特性（trait）实现多态
```

结构体所有权

关于`self`的几种变体：
1. `self`允许实现者移动和修改对象，对应的闭包特性为FnOnce
2. `&self`既不允许实现者移动对象也不允许修改，对应的闭包特性为Fn
3. `&mut self`允许实现者修改对象但不允许移动，对应的闭包特性为FnMut
4. 不含self参数的关联函数称为静态方法 (static method)

打印结构体：结构体不能直接打印，如果想用`{}`占位符打印变量，需要让struct实现Display这个trait
```rust
impl fmt::Display for Point {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
        write!(f, "({}, {})", self.x, self.y)
    }
}
```

### 泛型
Rust的泛型是在编译期自动推导，其他语言大多是利用反射/RTTI之类的在运行期做。(待确认)

```rust
// 1. 结构体的泛型
struct Point<T> {
    x: T,
    y: T
}
// 使用的是自动类型机制，但不允许出现类型不匹配的情况，如
let p1 = Point {x: 1, y: 2}; // correct
let p = Point {x: 1, y: 2.0}; // incorrect，因为x与 1 绑定时就已经将 T 设定为 i32，所以不允许再出现 f64 的类型。如果我们想让 x 与 y 用不同的数据类型表示，可以使用两个泛型标识符
struct Point<T1, T2> {
    x: T1,
    y: T2
}

// 2. 结构体方法的泛型
impl<T> Point<T> { // impl 关键字的后方必须有 <T>，因为它后面的 T 是以之为榜样的
    fn x(&self) -> &T {
        &self.x
    }
}
// 也可以为其中的一种泛型添加方法
impl Point<f64> {
    fn x(&self) -> f64 {
        self.x
    }
}

// 3. 函数的泛型
fn max<T>(array: &[T]) -> T {
    let mut max_index = 0;
    let mut i = 1;
    while i < array.len() {
        if array[i] > array[max_index] {
            max_index = i;
        }
        i += 1;
    }
    array[max_index]
}
```

### 特性
类似于其他语言中接口(interface)的概念，区别在于默认特性: 特性可以定义方法作为默认方法
```rust
// 定义特性
trait Descriptive {
    fn describe(&self) -> String;
}

// 定义结构体并实现该特性：语法是 impl <特性名> for <所实现的类型名>
// 同一个类可以实现多个特性，但每个impl块只能实现一个
struct Person {
    name: String,
    age: u8
}

impl Descriptive for Person {
    fn describe(&self) -> String {
        format!("{} {}", self.name, self.age)
    }
}

// 默认特性
impl Descriptive for Person {} // 块的内容为空

// 特性作为入参: 任何实现了 Descriptive 特性的对象都可以作为这个函数的参数
fn output(object: impl Descriptive) {
    println!("{}", object.describe());
}
```
    
### 变量的引用(references)
有两种方式:
1. 不可变的`&T`
2. 可变的`&mut T`

### 类型转换
类型转换有几种方式
1. 使用内置的方法
    ```rust
    // 1. 基础类型转换成字符串，使用to_string() ，得到是String类型
    // str => String, 使用"xxx".to_string()或者String::from("xxx")
    ```
2. 使用关键字`as`
    
    ```rust
    let i = 42;
    // 先转为 *const i32,再转为 *mut i32
    let p = &i as *const i32 as *mut i32;
    println!("{:p}", p);
    ```
### 运算符
#### 一元运算符
1. `-`：取负，专门用于数值类型。实现了 `std::ops::Neg`。
2. `* `：解引用。实现了 `std::ops::Deref` 或 `std::ops::DerefMut`。
3. `!`：取反。例如`!false`等于`true`。如果这个操作符对数字类型使用，会将其每一位都置反！也就是说，对一个 1u8 进行 ! 操作，将得到一个 254u8。实现了 std::ops::Not。
4. `&`和`&mut`：租借，borrow。向一个 owner 租借其使用权，分别租借一个只读使用权和读写使用权。

#### 算数操作符：加减乘除余

```rust
println!("{}",10/4) // 2 因为rust是强类型语言，在定义变量时就指定了变量的类型为i32，那么系统推导出来的运算结果也会为i32。同样的在go,java中也是一样，但是在python、js中就不会。如果想输出2.5，需要两个变量的类型改为浮点型
println!("{}",10.0/4.0) // 2.5
```

#### 位运算符：
1. `&` ：与操作。实现了 std::ops::BitAnd。
1. `|` ：或操作。实现了 std::ops::BitOr。
1. `-^` ：异或。实现了 std::ops::BitXor。
1. `<<` ：左移运算符。实现了 std::ops::Shl。
1. `>>` ：右移运算符。实现了 std::ops::Shr。

#### 逻辑运算符:
1. 惰性 boolean 运算符:和其他类 C 语言一样会逻辑短路，但Rust 里这个运算符只能用在 bool 类型上
    1. `&&`
    2. `||`
2. `!`
#### 比较运算符
==和!= 实现的是 PartialEq，<、>、>= 和 <=实现的是 PartialOrd

#### 类型转换
`as`

#### 重载运算符
## 3 流程控制(Control Flow)
没有switch：摒弃 switch 的原因是因为 switch 容易存在因忘记添加 break 而产生的串接运行问题

### 3.1 match
match的功能仅仅是匹配，和其他编程语言的switch类似，要想发挥出它全部的威力，需要结合"模式匹配"来使用，从而实现解构等。和switch有两点不同：
1. match所罗列的匹配，必须穷举出其所有可能。当然，你也可以用 _ 这个符号来代表其余的所有可能性情况，就类似于switch中的default语句。
2. match的每一个分支都必须是一个表达式，并且，除非一个分支一定会触发panic，这些分支的所有表达式的最终返回值类型必须相同。可以简单理解为整个match是一个表达式，既然是一个表达式，那么它的结果就一定是某个类型的变量。

```rust
// 对枚举类和非枚举类使用是不一样的
// 对枚举类使用是类型判断
// 对非枚举类使用是的判断值，且必须注意处理例外情况，即使在例外情况下没有任何要做的事。例外情况用下划线 _ 表示
let t = "abc";
match t {
    "abc" => println!("Yes"),
    _ => {}, // 例外情况 do nothing
}
```

## 13 错误处理

## 15 注释

## 20 并发
首先，rust本身并没有支持协程。

### 20.1 线程

使用：
1. 线程的创建:被创建后，子线程将和父线程不再有关系，父线程终止不会导致子线程终止(子线程可能比父线程存活更久)，除非父线程是主线程

    ```rust
    // 方法1 使用spawn函数
     // 创建一个线程
    let new_thread = thread::spawn(move || {
        println!("I am a new thread.");
    });
    // 等待新建线程执行完成
    new_thread.join().unwrap();
    
    // 方法2 使用Builder类，可以设置线程名称、堆栈大小
    // 创建一个线程，线程名称为 thread1, 堆栈大小为4k
    let new_thread_result = thread::Builder::new()
                            .name("thread1".to_string())
                            .stack_size(4*1024*1024).spawn(move || {
        println!("I am thread1.");
    });
    // 等待新创建的线程执行完成
    new_thread_result.unwrap().join().unwrap();
    ```
2. 等待线程执行结束`thread.join()`
3. 
    
### 20.2 管道 channel
通道(channel)可以把一个线程的消息(数据)传递到另一个线程，从而让信息在不同的线程中流动，从而实现协作。通道的两端分别是发送者(Sender)和接收者(Receiver)，发送者负责从一个线程发送消息，接收者则在另一个线程中接收该消息。

分类：异步通道和同步通道
1. 异步通道`channel()`：不管接收者是否正在接收消息，消息发送者在发送消息时都不会阻塞。异步通道具备消息缓存的功能，理论上无上限,但是缓存大量的消息得不到即使处理，就会占用大量的内存，最终导致内存耗尽

    ```rust
    use std::sync::mpsc; // mpsc就是多生产者单消费者(Multiple Producers Single Consumer)的简写
    use std::thread;

    // 创建一个异步通道
    let (tx, rx): (mpsc::Sender<i32>, mpsc::Receiver<i32>) = mpsc::channel();

    // 创建线程用于发送消息
    // move的作用相当于把 || { tx do something} 里面的tx限制在了{}中，当tx do something 执行完后，tx就会被drop掉，在这里是关闭掉tx
    thread::spawn(move || { 
        // 发送一个消息，此处是数字id
        // do something
        tx.send(1).unwrap();
    });

    // 在主线程中接收子线程发送的消息并输出
    println!("receive {}", rx.recv().unwrap()); // 接收者的recv方法应该会阻塞当前线程
    ```
2. 同步通道`sync_channel(msg_num)`

    ```rust
    use std::sync::mpsc;
    use std::thread;
    
    // 创建一个同步通道
    let (tx, rx): (mpsc::SyncSender<i32>, mpsc::Receiver<i32>) = mpsc::sync_channel(0);

    // 创建线程用于发送消息
    let new_thread = thread::spawn(move || {
        // 发送一个消息，此处是数字id
        println!("before send");
        tx.send(1).unwrap();
        println!("after send");
    });

    println!("before sleep");
    thread::sleep_ms(5000);
    println!("after sleep");
    // 在主线程中接收子线程发送的消息并输出
    println!("receive {}", rx.recv().unwrap());
    new_thread.join().unwrap();
    ```

使用：
1. 概述
    1. 管道可以发送什么类型的消息:实现了`marker trait Send`的类型，这样做是为了并发安全考虑
    2. 通道如果被释放了，接收者的recv方法就会立即返回
2. 多个发送者和多个接收者：每个发送者或接收者只能被一个线程使用，如果想被多个线程使用，使用`clone()`克隆发送者和接收者，底层的channel还是同一个

# 五 经验
## 2 常用标准库 std

### fmt
### format!
参数可以是任意类型，而且可以 position 参数和 key-value 参数混合使用。但要注意一点，key-value 的值只能出现在 position 值之后并且不占用 position。
    
```rust
// 格式化单个变量
format!("{}", 1);
// 格式化多个变量
format!("{} {}", 1, 2);
// position和默认的混合使用
format!("{1} {} {0} {}", 1, 2); // 2 1 1 2
// Named parameters 命名式
format!("{value}", value=4); // 4
// 填充 Fill/Alignment 具体见文档
format!("{:04}", 42);             // => "0042" with leading zeros
// position和key-value 混合使用
let s = format!("今天是{0}年{1}月{2}日, {week:?}, 气温{3:>0width$} ~ {4:>0width$} 摄氏度。",
    2016, 11, 24, 3, -6, week = "Thursday", width = 2);

print!("{}", s);
```

2. `format_arg!`
2. print宏：这两个宏只是将`format!`的结果输出
    3. `print!`
    4. `println!`
5. `write！`
6. `Debug`
7. `Display`

### println!
```rust
// 直接打印字符串
println!("Hello World");
// 打印单个变量
println!("{}", 1);
// 打印多个变量
println!("{} {}", 1, 2);
```

动词：
1. `{:?}`：实现了`Debug`这个trait的可以用这个动词打印，比如字符串，切片,`Err()`等
2. `{#?}`打印成更漂亮的格式

### thread

### Rayon
for writing parallel & data race-free code.

### serializing
for serializing and deserializing data.

### string

### Tokio/async-std
for writing non-blocking, low-latency network services.

### tracing
for instrumenting Rust programs to collect structured, event-based diagnostic information.

### 其他

# 六 问题
## 1 warning: spurious network error (2 tries remaining)...

## 2 borrow of moved value

# 七 未整理
1. 使用region式内存管理？
2. 没有runtime？