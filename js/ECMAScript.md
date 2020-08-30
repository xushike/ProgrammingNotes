# ECMAScript
# 一 概述
## 1 简介
ECMAScript 是 ECMA 国际组织（www.ecma-international.org）负责的各种标准（/publications/standards/Standard）之一

## 2 历史
和 ECMAScript 有关的标准有 ECMA262，ECMA290，ECMA327，ECMA357，ECMA402，ECMA404，ECMA414等等。其中290，327，357等等没有推广开来，被废弃。ECMA 262 是语言规范本身。ECMA 402 则是制定一些基于 ECMAScript 5 或者之后版本的一些国际化 API 标准。ECMA 404 是 JSON 规范。ECMA 414 则规定了哪些规范是和 ECMAScript 有关的。目前内部就包含了 262，402和404。(待验证)

### 2.1 ECMA-262
狭义的 ECMAScript 规范。

由 ECMA-262 定义的 ECMAScript 与 Web 浏览器没有依赖关系。实际上，这门语言本身并不包含输 入和输出定义。ECMA-262 定义的只是这门语言的基础，而在此基础之上可以构建更完善的脚本语言。 我们常见的 Web 浏览器只是 ECMAScript 实现可能的宿主环境之一。宿主环境不仅提供基本的 2 ECMAScript 实现，同时也会提供该语言的扩展，以便语言与环境之间对接交互。而这些扩展——如 DOM，则利用 ECMAScript 的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。其他 宿主环境包括 Node(一种服务端 JavaScript 平台)和 Adobe Flash。
ECMA-262 标准没有参照 Web 浏览器，那它都规定了些什么内容呢?大致说来，它规定了这 门语言的下列组成部分:
- 语法
- 类型
- 语句
- 关键字
- 保留字
- 操作符
ECMA-262 要求 支持 Unicode 标准(从而支持多语言开发)
ECMA-262 第 3 版:修改的内容涉及字符串处理、错误定义和数 值输出。这一版还新增了对正则表达式、新控制语句、try-catch 异常处理的支持，并围绕标准的 10 国际化做出了一些小的修改。从各方面综合来看，第 3 版标志着 ECMAScript 成为了一门真正的编程 语言。
ECMA-262 第 4 版对这门语言进行了一次全面的检核修订。由于 JavaScript 在 Web 上日益流行，开 发人员纷纷建议修订 ECMAScript，以使其能够满足不断增长的 Web 开发需求。作为回应，ECMA TC39 重新召集相关人员共同谋划这门语言的未来。结果，出台后的标准几乎在第 3 版基础上完全定义了一门 新语言。第 4 版不仅包含了强类型变量、新语句和新数据结构、真正的类和经典继承，还定义了与数据 交互的新方式。
ECMAScript 3.1 成为 ECMA-262 第 5 版，并于 2009 年 12 月 3 日正式发布。第 5 版力求澄清第 3 版中已知的歧义并增添了新的功能。新功能包括原生 JSON 对象(用于解析和序列化 JSON 数据)、继 承的方法和高级属性定义，另外还包含一种严格模式，对 ECMAScript 引擎解释和执行代码进行了补充 说明。

### ECMA-402
规定了虽然不属于 ECMAScript 本身、但各种实现应当统一做法的“地区差异化的接口”。比如`Intl`是一个命名空间，它提供了精确的字符串对比、数字格式化，和日期时间格式化。

### ECMA-404
规定了 ECMAScript 需要用到、产生自 ECMAScript 却成为独立通用标准的“JSON”。

### ECMA-414
规定了和 ECMAScript 相关的标准有哪些（即262，402和404）。

## 3 常识
### 3.1 JS和ES的关系
1. JavaScript 是 ECMAScript 语法的一种最为流行的具体实现（除此之外比如 Flash 里的 ActionScript 也是一种实现）；
2. JavaScript 有浏览器、Node.js 等多种宿主环境，是一种日常的通称，各种宿主所扩充的 API 有差异，比如浏览器有 document，而 Node.js 有 process，这些在统一语法规范 ECMAScript 中没有规定；

## 4 文档网址等
1. 官方
    1. http://ecma-international.org/ecma-262/5.1
# 三 基础
## 1 函数
函数是ECMAScript的核心.
### 函数的声明
...
1. 如果函数无明确的返回值，或调用了没有参数的 return 语句，那么它真正返回的值是 undefined
# 五 问题