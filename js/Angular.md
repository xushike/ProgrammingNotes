# Angular
## 一 概述
1. 本笔记主要记录angular2及以上版本
## 三. 基础
### 1 表达式
#### 1.1 ngfor
在angular1.x中是ngrepeat，从angular2.x开始就是ngFor了它们的语法非常相似，但需要注意的一点在遍历集合是，Angular 2 使用 of 代替了 in 。
### 1 表单
### 2 模块
1. 模块定义了一个应用程序，模块控制器通常属于一个应用程序。
2. 模块的好处：JavaScript 中应避免使用全局函数。因为他们很容易被其他脚本文件覆盖。AngularJS 模块让所有函数的作用域在该模块下，避免了该问题。
2. 创建模块的方法：
```javascript
<script>
var app = angular.module("myApp", []); 
</script>
```
### 3 指令
#### 3.1 ngif
1. 
### 4 管道
1. http://blog.csdn.net/qq451354/article/details/54141024
## 四. 使用
## 五. 问题
1. 表单验证
2. 声明周期
3. npm run start \ maven install \ng server \node xxx等命令的场景和用法？