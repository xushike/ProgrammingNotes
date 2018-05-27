# Computer计算机相关

# 一 概述
计算机相关的笔记,包括计算机原理,重装系统等.

## 1 简介

## 3 常识
### 3.1 真随机和伪随机
java,javascript等语言的`random()`方法生成的都是伪随机.

javascript:
1. `Math.random()`:生成0到1(左闭右开)的浮点数.不能提供像密码一样安全的随机数字.
2. `window.crypto.getRandomValues(typedArray)`:往类型化数组中填充符合密码学要求的安全的随机值.(为了确保足够的性能，所以不使用真正的随机数生成器)

# 三 基础