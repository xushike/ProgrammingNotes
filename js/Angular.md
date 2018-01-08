# Angular
## 一 概述
1. 本笔记主要记录angular2及以上版本
2. 中文官网,感觉做的不错:[https://www.angular.cn/](https://www.angular.cn/)
### 1 简介
### 2 历史
### 3 常识
### 4 angular-cli常用命令
1. `ng serve`:启动开发服务器并监听文件变化,变化时重构
    1. 参数`-o`(`--open`):启动后打开地址
2. `ng lint`:保持代码风格的统一
## 二 安装配置
### 1 win
1. 
### 3 mac
1. 需要先安装node和npm
## 三. 基础
### 1 架构
### 2 模板和数据绑定
#### 显示数据
#### 模板语法
简单来说,组件扮演着控制器或视图模型的角色,模板则扮演视图的角色.html是angular模板的语言.
1. angular模板的特殊html元素

    - 被禁用的:`<script>`,防止恶意内容,写了也会被angular过滤
    - 没用的:`<html>`、`<body>`和`<base>`
2. 模板表达式

    angular会对模板表达式**求值**,然后**转换成字符串**.
    1. 使用方法:
        1. 插值表达式:即写在双花括号之间,如`{{hero.name}}`
        2. 属性绑定(`[property]="expression"`):如`<img [src]="heroImageUrl">`
    1. 表达式上下文:典型的表达式上下文是这个组件实例,但也可包含组件之外的对象,比如模板输入变量 (`let hero`)和模板引用变量(`#heroInput`),如,

        ```html
        <div *ngFor="let hero of heroes">{{hero.name}}</div>
        <input #heroInput> {{heroInput.value}}
        ```
    2. 表达式上下文变量(优先级从高到低):
        - 模板变量
        - 指令的上下文变量
        - 组件的成员
    3. 只能引用表达式上下文中的成员,不能做的是:
        - 不能引用全局命名空间中的任何东西，比如`window`或`document`
        - 不能调用`console.log`或`Math.max`
        - 不能使用部分js表达式,参考[https://angular.cn/guide/template-syntax](https://angular.cn/guide/template-syntax)
    4. 请遵循下列指南：
        - 没有可见的副作用:除了目标属性的值以外，不应该改变应用的任何状态
        - 执行迅速:计算代价较高时，应该考虑缓存那些从其它值计算得出的值。
        - 尽量简单
        - 幂等性:没有副作用
3. 模板语句

    用于响应事件,出现在=号右侧的引号中,就像这样:`(event)="statement"`,其中`statement`是组件实例的方法.能改变应用状态,即有副作用,这也是它的主要作用.
    1. 语句上下文

        可以引用模板上下文中的属性,包括模板的`$event`对象等.
4. 绑定语法

    模板绑定是通过dom的`property`和事件来工作的，而不是通过html的`attribute`.(这两者的区别参考本人的前端笔记)
    1. 单向绑定(源到视图):用于插值表达式,property,attribute,类和样式,如

        ```
        {{expression}}
        [target]="expression"
        bind-target="expression"
        ```
        1. 对于属性绑定:
            1. 也可写成`bind-`前缀的可选形式,如,

                ```html
                <img [src]="heroImageUrl">
                <img bind-src="heroImageUrl">
                ```

            2. 返回恰当的类型,即左边需要什么类型,右边就给什么类型,如,

                ```html
                <!-- 需要Hero类型就给Hero类型 -->
                <app-hero-detail [hero]="currentHero"></app-hero-detail>
                ```
            3. 不要随便省略方括号,否则右边的内容会被当做普通字符串,除了以下两种情况:
                1. 目标属性接受字符串值,可省略方括号,如,

                    ```html
                    <app-hero-detail prefix="You are my" [hero]="currentHero"></app-hero-detail>
                    ```
                2. 使用了插值表达式,如,

                    ```html
                    <p><img src="{{heroImageUrl}}"> is the <i>interpolated</i> image.</p>
                    <p><img [src]="heroImageUrl"> is the <i>property bound</i> image.</p>
                    ```
            4. 属性绑定和插值表达式的比较:类型是字符串时,用哪种都ok,只不过后者写起来更方便,如,

                ```html
                <p><span>{{title}} is the <i>interpolated</i> title.</span></p>
                <p><span [innerHTML]="title"></span> is the <i>property bound</i> title.</p>
                ```

        2. 对于`attribute`:在angular中,`attribute`唯一的作用是用来初始化元素和指令的状态.如,(待补充)

            ```html
            <button [attr.aria-label]="help">help</button>
            ```
    2. 单向绑定(视图到源):用于事件,如,

        ```
        (target)="statement"
        on-target="statement"
        ```
    3. 双向绑定:如,

        ```
        [(target)]="expression"
        bindon-target="expression"
        ```
#### 生命周期钩子
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
4. 关于`ngOninit()`钩子和构造函数
    1. 构造函数会在所有钩子之前执行,且构造函数里不应有复杂的逻辑(特别是那些需要从服务器获取数据的逻辑),最好只有对局部变量进行简单的初始化(例如把构造函数的参数赋值给属性).
    2. 指令的构造函数完成之前，那些被绑定的输入属性还都没有值。 如果我们需要基于这些属性的值来初始化这个指令，这种情况就会出问题。 而当`ngOnInit()`执行的时候，这些属性都已经被正确的赋值过了。
    3. 构造函数里dom还没渲染出来;而`ogOninit()`时dom已经渲染完成了,可以访问dom(待测试)
#### 组件交互
#### 组件样式
#### 动态组件
#### 指令
1. 结构型指令
2. 属性型指令
3. 组件
#### 管道
#### 动画
### 3 表单
### 4 引导启动


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
6. [https://material.angular.io/](https://material.angular.io/)
7. [https://segmentfault.com/a/1190000009126012](https://segmentfault.com/a/1190000009126012)
8. [https://segmentfault.com/a/1190000006222169](https://segmentfault.com/a/1190000006222169)