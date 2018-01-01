# Angular
## 一 概述
1. 本笔记主要记录angular2及以上版本
2. 中文官网,感觉做的不错:[https://www.angular.cn/](https://www.angular.cn/)
### 1 历史
### 2 常识
### 3 常用命令
1. `ng serve`:启动开发服务器并监听文件变化,变化时重构
    1. 参数`-o`(`--open`):启动后打开地址
2. `ng lint`:保持代码风格的统一
## 二 安装配置
### 3 mac
1. 需要先安装node和npm
## 三. 基础
### 1 架构
### 2 模板和数据绑定
#### 1.1 显示数据
#### 1.2 模板语法
#### 1.3 生命周期钩子
1. 所有钩子(按顺序排列)
    1. `ngOnChanges()`

        每次变化时调用,首次调用一定在`ngOninit()`之前
    2. `ngOnInit()`:
    
        只调用一次.
    3. `ngAfterContentInit()`

        只适用于组件
    4. `ngAfterContentChecked()`

        只适用于组件
    5. `ngAfterViewInit()`

        只适用于组件
    6. `ngAfterViewChecked()`

        只适用于组件
    7. `ngOnDestroy()`

        在Angular销毁指令/组件之前调用
2. 组件和指令拥有不同钩子
3. 使用钩子

    钩子的名字:钩子方法由接口名加上`ng`前缀构成,比如`OnInit`接口的钩子方法是`ngOnInit`.只有在指令/组件中定义过才会被angular调用.
4. 关于钩子和构造函数
    1. 构造函数会在所有钩子之前执行,且构造函数里不应有复杂的逻辑(特别是那些需要从服务器获取数据的逻辑),最好只有对局部变量进行简单的初始化(例如把构造函数的参数赋值给属性).
    2. 指令的构造函数完成之前，那些被绑定的输入属性还都没有值。 如果我们需要基于这些属性的值来初始化这个指令，这种情况就会出问题。 而当`ngOnInit()`执行的时候，这些属性都已经被正确的赋值过了。



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
1. 双向绑定中某方的数据延迟取得也会生效
## 五. 问题
1. 表单验证
2. 声明周期
3. npm run start \ maven install \ng server \node xxx等命令的场景和用法？
4. angular为什么重量？vue和react
5. search`webpack和ngmodule`