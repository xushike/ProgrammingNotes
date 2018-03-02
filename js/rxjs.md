# rxjs
## 一 概述
### 1 简介
作者Ben Lesh
1. prerequisites:最好先掌握typescript和js
## 三 基础

## 六 问题

1. rxjs和promise的关系,用来解决什么问题,系统学习?
2. [https://zhuanlan.zhihu.com/p/23331432](https://zhuanlan.zhihu.com/p/23331432)
3. [https://segmentfault.com/a/1190000005051034#articleHeader0](https://segmentfault.com/a/1190000005051034#articleHeader0)

## 七 待整理
1. 网友:许多Rxjs方法实际上适合流数据，但是对于单值请求来说太过度设计。

    一个Ajax请求是单次的，使用运行类似方法Observable.prototype.map时候会永远只能在管道中得到一个值，显然这是没有语义意义的。Promises另一方面表示一个尚未完成的值，这正是HTTP请求给出的。我花了几个小时迫使Observable行为转换回一个Promise，只是极简单地使用Promise.all ，它的效果要比Rx.js好得多。