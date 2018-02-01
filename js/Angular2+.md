# Angular2+
[TOC]
## 一 概述
1. 本笔记主要记录angular2及以上版本
### 1 简介
1. 特性与优点:[https://v2.angular.cn/features.html](https://v2.angular.cn/features.html)
### 2 历史
1. 从网友口中得知angular2未来会致力于3d和vr,感觉有盼头.
### 3 常识
#### angular风格指南
[风格指南](http://origin.angular.live/docs/ts/latest/guide/style-guide.html#!#naming)

### 4 angular-cli常用命令
1. `ng serve`:启动开发服务器并监听文件变化,变化时重构
    1. 参数`-o`(`--open`):启动后打开地址
2. `ng lint`:保持代码风格的统一
### 5 angular第三方组件简介
1. [http://shark.mail.netease.com/shark-angular2/index.html](http://shark.mail.netease.com/shark-angular2/index.html)
2. [https://ng-bootstrap.github.io/#/home](https://ng-bootstrap.github.io/#/home)
3. [https://material.angular.io/](https://material.angular.io/)
4. [https://valor-software.com/ngx-bootstrap/#/](https://valor-software.com/ngx-bootstrap/#/)
### 6 网站
1. 中文官网,感觉做的不错:[https://www.angular.cn/](https://www.angular.cn/)
1. Angular2资源大全,感觉比较全面:[https://github.com/lightningtgc/awesome-ng2](https://github.com/lightningtgc/awesome-ng2)
2. Angular2優質學習資源收集:[https://hk.saowen.com/a/53955f7eb930c2ddc880fbff0713dd3861ed79eb455f5e9c7f09509dcad1864d](https://hk.saowen.com/a/53955f7eb930c2ddc880fbff0713dd3861ed79eb455f5e9c7f09509dcad1864d)
3. [http://plnkr.co/](http://plnkr.co/)
4. 大神的博客:[https://orangexc.xyz/](https://orangexc.xyz/)
5. 网友的项目:[https://github.com/liepeng328/angular-base](https://github.com/liepeng328/angular-base)
6. 网友的组件库:[https://github.com/ElemeFE/element-angular](https://github.com/ElemeFE/element-angular)
### 7 文档
## 二 安装配置
### 1 win
1. 
### 3 mac
1. 需要先安装node和npm
## 三. 核心基础知识
### 1 架构
1. 通过引导根模块来启动应用。 在开发期间，你通常在一个main.ts文件中引导AppModule

    ```typescript
    import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
    import { AppModule } from './app/app.module';   
    platformBrowserDynamic().bootstrapModule(AppModule);
    ```
1. 当应用启动时，Angular 会从根组件开始启动，并解析整棵组件树，数据由上而下流下下一级子组件。
#### 常见错误
写的很好很详细:[https://segmentfault.com/a/1190000004969541](https://segmentfault.com/a/1190000004969541)
1. 直接调用DOM APIs

    会导致几个问题:
    - 测试复杂度会增加,测试用例变慢
    - 无法从浏览器中解藕,不能兼容其他环境比如`web worker`,服务端或者`Electron`
    - 代码不易读
### 2 模块和组件
#### 模块
angular模块是一个带有`@NgModule`装饰器的类,和js中的模块完全无关,但是实际使用是两者互补,初学时容易混淆.
1. 模块的好处
    - js中应避免使用全局函数。因为他们很容易被其他脚本文件覆盖。AngularJS 模块让所有函数的作用域在该模块下，避免了该问题。
    - 将一些特性做成模块,方便组织
1. 根模块
    
    angular要求至少有一个模块,也就是根模块,用来引导并运行应用.
2. 自带模块

    Angular 自身的许多特性也是通过 Angular 模块组织的
    1. HttpModule:HTTP服务
    2. RouterModule:路由器
#### 组件
1. 网友总结的angular组件的几点使用经验:
    1. 好的命名
        1. "玫瑰无论叫什么名字都一样香。"--莎士比亚
        2. 常见的命名约定就是在特征后面加上类型（例如：feature.type.js）
    2. 不要太过复杂,记住`Rule of One`
        1. 简易性在程序的每个层面都是很有益的。通常更好的是集中精力去做一件事，并在简单、可重用的代码的前提下把这一件事做到极致。
### 3 模板
#### 显示数据
#### 模板语法
简单来说,组件扮演着控制器或视图模型的角色,模板则扮演视图的角色.模板以HTML形式存在(html是angular模板的语言)，告诉Angular如何渲染组件.
1. angular模板的特殊html元素

    - 被禁用的:`<script>`,防止恶意内容,写了也会被angular过滤
    - 没用的:`<html>`、`<body>`和`<base>`
2. 模板表达式

    angular会对模板表达式**求值**,然后**转换成字符串**.
    1. 使用方法:
        1. 插值表达式:即写在双花括号之间,如`{{hero.name}}`
        2. 属性绑定(`[property]="expression"`):如`<img [src]="heroImageUrl">`,且右边可用三目运算符(?).
    1. 表达式上下文:典型的表达式上下文是这个组件实例,但也可包含组件之外的对象,比如模板输入变量 (`let hero`)和模板引用变量(`#heroInput`),如,

        ```html
        <div *ngFor="let hero of heroes">{{hero.name}}</div>
        <input #heroInput> {{heroInput.value}}
        ```

        1. 模板输入变量:比如`*ngFor`中的`let hero`是模板输入变量,不同于模板引用变量.
        2. 模板引用变量
            
            通常是加`#`前缀来声明(比如`#elseBlock`)模板引用变量(也可以加`ref-`前缀),引用的是它所附着到的DOM元素、组件或指令,可以在整个模板的任意位置访问(所以模板引用变量不应该重复).通过`xxx.value`来获取它的值.如,

            ```html
            <input #phone placeholder="phone number">
            <button (click)="callPhone(phone.value)">Call</button>
            ```


    2. 表达式上下文变量(优先级从高到低):
        - 模板变量
        - 指令的上下文变量
        - 组件的成员
    3. 空属性路径和安全导航操作符`?.`

        对于`<div>The article is {{title}}<div>`,如果title为空,该div依然会被渲染出来,只不过只显示"The article is"(在非angular环境中也是如此).但是,如果是`{{obj.title}}`,当obj为undefined或null时,会抛出错误.有几种解决方法:
        1. `NgIf`
        2. `&&`,如`hero && hero.name`
        3. 安全导航操作符`?.`

            会在第一个空值的时候跳出,显示是空的,但应用正常工作.如`a?.b?.c?.d`.比上面两者更好用.

    4. 非空断言操作符`!`

        ts2开始，我们可以使用`--strictNullChecks`标志强制开启严格空值检.当确定某个值不会为空时,可以通过该操作符就可以告诉编译器某些值不为空,避免被编译器抛出错误.如,
        ```html
        <div *ngIf="hero">
            The hero's name is {{hero!.name}}
        </div>
        ```
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

        2. 对于`attribute`:在angular中,默认使用的是`property`而不是`attribute`(stackoverflow的回答,大意是`attribute`会消耗更多资源:[Why is colspan not a known native attribute in Angular 2?](https://stackoverflow.com/questions/35615751/why-is-colspan-not-a-known-native-attribute-in-angular-2/35616510)).如果要使用html的`attribute`,则需写成`[attr.xxx]`,`attribute`在angular中的唯一的作用是用来初始化元素和指令的状态.如,

            ```html
            <!-- ARIA指可访问性，用于给残障人士访问互联网提供便利 -->
            <button [attr.aria-label]="help">help</button>
            ```
        3. css类绑定(待补充):是添加或删除单个class的最佳实践,多个则推荐用ngClass.

            ```html
            <div [class.special]="isSpecial">The class binding is special</div>
            ```
        4. 样式绑定

            可设置内联样式,形如`[style.xxx]`.其中`xxx`是css样式的属性名,可以用中线命名法,也可以用驼峰式命名法.例子如下,

            ```html
            <button [style.color]="isSpecial ? 'red': 'green'">Red</button>
            ```
            
            对于有单位的(比如“em” 和 “%” )还可以带上单位,

            ```html
            <button [style.font-size.em]="isSpecial ? 3 : 1" >Big</button>
            <button [style.font-size.%]="!isSpecial ? 150 : 50" >Small</button>
            <button [style.fontSize.%]="!isSpecial ? 150 : 50" >Small</button>
            ```
            如果有多个样式,推荐使用`NgStyle`
    2. 单向绑定(视图到源):
            
        **用于事件**,事件绑定语法由等号左侧带圆括号的**目标事件**和右侧引号中的模板语句组成.如,

        ```
        <!-- 一般写法 -->
        (target)="statement"
        <!-- 也可用规范写法,带`on-`前缀 -->
        on-target="statement"
        ```

        angular会优先匹配指令的事件属性(即带`@Output`的事件属性).
        1. `$event`(事件对象)

            事件对象有三种形态,取决于目标事件:
            1. 如果目标事件是原生DOM元素事件,`$event`就是DOM事件对象,有target和target.value这样的属性。似乎angular封装的事件也是这样,比如`ngSubmit($event)`
            2. 如果事件属于自定义指令(即`@Output`声明的事件属性),`$event`则是`emit(xxx)`的`xxx`.
                1. 特殊情况:`ngModelChange($event)`
                    
                    其`$event`是表单元素对应的value值,比如`<input name="first_name" ngModel (ngModelChange)="onShow($event)">`中`$event`就是input的value值.

        2. `EventEmitter`

            实现自定义事件,可用于父子组件交互
    3. 双向绑定
        
        语法`[(xxx)]="expression"`,也被称为`banana in a box`语法,

        ![](../picture/js/angula-1-banana-in-box.png
        )

        实际上是属性绑定和事件绑定的语法糖,比如`[num]`和`(numChange)`,使用非常方便.

        ```
        [(target)]="expression"
        bindon-target="expression"
        ```
        1. `ngModule`指令(参考表单)


#### 生命周期钩子
1. 所有钩子(按顺序排列)
    1. `ngOnChanges()`

        - `@input()`属性(输入属性)发生变化时，会调用。非此属性，不会调用。
        - 当输入属性为对象时，当对象的属性值发生变化时，不会调用，当对象的引用变化时会触发。
        - 首次调用一定在`ngOninit()`之前.
    2. `ngOnInit()`:
    
        只调用一次.该方法里可操作dom,可操作`@input()`的值.最常用.
    3. `ngDoCheck`

        自定义的方法，用于检测和处理值的改变,由zone.js实现,会检查整个组件树,一般会非常频繁且难以预料.
    3. `ngAfterContentInit()`

        只适用于组件.在组件内容初始化之后调用
    4. `ngAfterContentChecked()`

        只适用于组件.内容投影：父组件写在子标签之间的内容会被渲染到子模板的ng-content中去，类似vue的slot.组件每次检查内容时调用.(?)
    5. `ngAfterViewInit()`

        只适用于组件.组件相应的视图初始化之后调用,不允许修改`@input()`
    6. `ngAfterViewChecked()`

        只适用于组件.组件每次检查视图时调用,不允许修改`@input()`
    7. `ngOnDestroy()`

        在Angular销毁指令/组件之前调用
2. 组件和指令拥有不同钩子
3. 使用钩子

    钩子的名字:钩子方法由接口名加上`ng`前缀构成,比如`OnInit`接口的钩子方法是`ngOnInit`.只有在指令/组件中定义过才会被angular调用.
4. 关于`ngOninit()`钩子和`constructor`构造函数
    1. 构造函数会在所有钩子之前执行,子组件的构造函数中不能获取input()输入的值.构造函数里不应有复杂的逻辑(特别是那些需要从服务器获取数据的逻辑),最好只有对局部变量进行简单的初始化(例如把构造函数的参数赋值给属性)和依赖注入.
    2. 指令的构造函数完成之前，那些被绑定的输入属性还都没有值。 如果我们需要基于这些属性的值来初始化这个指令，这种情况就会出问题。 而当`ngOnInit()`执行的时候，这些属性都已经被正确的赋值过了。
    3. 构造函数里dom还没渲染出来;而`ogOninit()`时dom已经渲染完成了,可以访问dom(待测试),而且构造函数也不能获取组件输入属性的值.
    4. 关于构造函数中的参数
        1. 常用于引入服务,angular会自动去完成依赖注入,如`constructor(private userService: UserService) {}`
    5. 参考:[https://segmentfault.com/a/1190000008685752](https://segmentfault.com/a/1190000008685752)
    6. 最佳实践

        构造函数用于依赖注入或执行一些简单的初始化操作,`ngOnInit()`钩子主要用于执行组件的其它初始化操作或获取组件输入的属性值。
#### 组件交互
#### 组件样式
#### 动态组件
#### 指令
angular1.x包含了超过70个内置指令,实际上不需要那么多,angular2.x开始,用绑定就能达到原来的效果.angular有三种指令:属性指令,结构型指令和组件指令.
1. 属性型指令

    用于监听和修改其它HTML元素或组件的行为,包括attribute,property等.常用的有:
    1. `ngClass`
        
        添加或移除多个 CSS 类时，NgClass指令可能是更好的选择
    2. `NgStyle`

        可以同时设置多个内联样式
    3. `NgModel`
2. 结构型指令

    塑造或重塑DOM的结构，这通常是通过添加、移除和操纵它们所附加到的宿主元素来实现.在angular中,结构型指令使用的是**微语法**.一个宿主元素可以有多个属性型指令,但只能有一个结构型指令.常见结构指令有:
    1. `NgIf`

        为false时,会从DOM中物理删除(移除它的宿主元素，取消它监听过的DOM事件,移除变更检测),而不是使用CSS来隐藏元素.这些组件和DOM节点可以被当做垃圾收集起来，并且释放它们占用的内存。该指令还可防范空指针错误.
        1. 关于移除(remove)和隐藏(hide)的对比

            - 隐藏时,组件仍然附加在所属的DOM上,仍在监听事件,仍然会有变更检测,即仍然占用着资源,只是看不见而已.但是重新显示会很快.
            - 移除时,释放占用的资源,但是重新显示会比hide慢

            除非有特别理由,否则angular推荐使用移除.
        2. 关于`*ngIf`

            这个`*`其实是语法糖(其他几个结构指令也是如此),Angular把`*ngIf`属性翻译成一个`<ng-template>`元素并用它来包裹宿主元素,其中`NgIf`是类名,`ngIf`是属性名.(结合官方文档和我的实际测试，应该只有能带`*`的支持`<ng-template>`的,其他包括`NgSwitch`都不支持)如,

            ```html
            <div *ngIf="hero" >{{hero.name}}</div>
            <!-- 会被翻译成下面这样,也意味着要用NgIf的话就要写成下面这种形式 -->
            <ng-template [ngIf]="hero">
                <div>{{hero.name}}</div>
            </ng-template>
            ```

            **最终`<ng-template>`不会被渲染出来,而是渲染里面的内容**.
        3. `else`,`then`和`as`

            ```html
            <!-- else用法 -->
            <div *ngIf="condition; else elseBlock">...</div>
            <ng-template #elseBlock>...</ng-template>
            <!-- then和else用法 -->
            <div *ngIf="condition; then thenBlock else elseBlock"></div>
            <ng-template #thenBlock>...</ng-template>
            <ng-template #elseBlock>...</ng-template>
            <!-- as用法 -->
            <div *ngIf="condition as value; else elseBlock">{{value}}</div>
            <ng-template #elseBlock>...</ng-template>
            ```
    2. `NgFor`

        根据模板，渲染列表中的每个条目。在angular1.x中的语法是`ngrepeat`
        1. 一般用法

            ```html
            <div *ngFor="let hero of heroes; let i=index; let odd=odd; trackBy: trackById" [class.odd]="odd">
            ({{i}}) {{hero.name}}
            </div>
        2. `trackBy`

            因为列表每次有元素变化就会重新渲染整个列表,开销较大,所以有`trackBy`来追踪,基本用法`trackBy:trackByFun`,其中`trackByFun`必须是方法名.(待实践和补充)(从服务器拉取的时候一般都是重新渲染全部,因为引用改变了?直接添加和删除某个元素只渲染单独一个元素?假如追踪的是元素的id,当元素value变化时,是只渲染变化的元素,还是什么都不渲染?)

    3. `NgSwitch`

        语法类似js的switch.本质和`NgIf`一样,即false时从DOM中移除.`NgSwitch`,`NgSwitchCase`和`NgSwitchDefault`协作使用.注意`NgSwitch`是属性指令,所以**不能写成`*ngSwitch`,而必须写成`ngSwitch`**.例子如下,

        ```html
        <div [ngSwitch]="currentHero.emotion">
            <app-happy-hero    *ngSwitchCase="'happy'"    [hero]="currentHero"></app-happy-hero>
            <app-sad-hero      *ngSwitchCase="'sad'"      [hero]="currentHero"></app-sad-hero>
            <app-confused-hero *ngSwitchCase="'confused'" [hero]="currentHero"></app-confused-hero>
            <app-unknown-hero  *ngSwitchDefault           [hero]="currentHero"></app-unknown-hero>
        </div>
        ```
        
        
        实测发现,`ngSwitch`没带星号,**所以不能写到`ng-template`上**,但是`*ngSwitchCase`和`*ngSwitchDefault`能,而且不管哪种形式,`*ngSwitchCase`和`*ngSwitchDefault`都要写在`ngSwitch`所在的元素块的内部.如下:

        ```html
        <div [ngSwitch]="currentHero.emotion">
            <ng-template [ngSwitchCase]="'happy'">
                <app-happy-hero [hero]="currentHero"></app-happy-hero>
            </ng-template>
            <ng-template [ngSwitchCase]="'sad'">
                <app-sad-hero [hero]="currentHero"></app-sad-hero>
            </ng-template>
            <ng-template [ngSwitchCase]="'confused'">
                <app-confused-hero [hero]="currentHero"></app-confused-hero>
            </ng-template>
            <ng-template ngSwitchDefault>
                <app-unknown-hero [hero]="currentHero"></app-unknown-hero>
            </ng-template>
        </div>
        ```

    4. `ngNonBindable`:告诉Angular不要绑定页面的某个部分,如

        ```html
        <div ngNonBindable>
        {{我不会被绑定}}
        </div>
        ```
    4. 其他:微语法:需要自己写结构指令时可参考微语法的源码.
    5. 其他:`<ng-container>`

        angular提供的语法元素，不会污染样式或元素布局，因为Angular压根不会把它放进DOM中(就像是js中if块中的花括号).如,

        ```html
        <select [(ngModel)]="hero">
            <ng-container *ngFor="let h of heroes">
                <ng-container *ngIf="showSad || h.emotion !== 'sad'">
                <option [ngValue]="h">{{h.name}} ({{h.emotion}})</option>
                </ng-container>
            </ng-container>
        </select>
        ```
3. 组件指令

    组件是一个带模板的指令,虽然严格来说组件就是一个指令，但是组件非常独特，在Angular中位于中心地位.
#### 管道
管道的源码部分:[https://segmentfault.com/a/1190000008646187](https://segmentfault.com/a/1190000008646187)
作用不必多说,angular4又加入了`async pipe`,默认是只能在angular的模板中使用,如果要在js中使用,推荐使用DI的方式.
1. 关于纯管道(Pure Pipe)和非纯管道(Impure Pipe)

    首先需要了解什么是纯变更和非纯变更:
    - 纯变更:原始类型值(`String`,`Number`,`Boolean`,`Symbol`)的改变，或者对象引用的改变(对象的值改变不是)
    - 非纯变更:...

    Angular会在每个组件的变更检测周期(如鼠标点击或移动)执行非纯管道。所以，如果使用非纯管道，性能可能是个问题,推荐都用纯管道.
2. 自定义管道

    分为两步:
    - 使用`@Pipe`装饰器定义Pipe的metadata信息
    - 实现 PipeTransform 接口中定义的 transform 方法

    ```typescript
    //取自网上的例子
    import { Pipe, PipeTransform } from '@angular/core';

    @Pipe({ name: 'welcome' })
    export class WelcomePipe implements PipeTransform {
        transform(value: string): string {
            if(!value) return value;
            if(typeof value !== 'string') {
            throw new Error('Invalid pipe argument for WelcomePipe');
            }
            return "Welcome to " + value;
        }
    } 
    ```

    然后就可以用`welcome`了,如`{{ 'semlinker' | welcome }}`会变成`Welcome to semlinker`
##### 普通`pipe`
用法如下,可带参数,多个参数用冒号分隔

```html
<div>Birthdate: {{currentHero?.birthdate | date:'longDate'}}</div>
```

1. 內建管道
    1. Object管道
        - JsonPipe的`json`:转成json对象,对调试很有帮助.例如`{{ { name: 'semlinker' } | json }}`会变成`{ "name": "semlinker" }`
        - DatePipe的`date`
    2. String管道
        - UpperCasePipe的`uppercase`,LowerCasePipe的`lowercase`
        - TitleCasePipe的`titlecase`:转换成每个单词字母大写的形式.比如"i like use SSH"会变成"I Like Use Ssh"
    3. Number管道
        - DecimalPipe的`number:'a.b-c'`:`a`为整数部分保留的最小位数,`b`为小数部分保留的最小位数,`c`为小数部分保留的最大位数;默认是`1.0-3`.不会四舍五入,是直接截取,不够的部分补0,使用千分位表示.
        - PercentPipe的`percent:'a.b-c'`:会先将数字乘以100,然后abc和DecimalPipe类似,最后加上百分号,比如`{{215| percent:'6.2-3'}}`会变成`021,500.00%`
        - CurrencyPipe的`currency:'USD':true:'4.2-2'`:货币单位
    4. Tools管道
        - SlicePipe的`slice`:如`{{ 'semlinker' | slice:0:3 }}`会变成`sem`
        
2. 链式管道(chain pipes),即多级管道(multiple pipes)

    ```html
    <div>
        Title through a pipe chain:
        {{title | uppercase | lowercase}}
    </div>
    ```
##### `async pipe`
1. 待研究:[http://blog.csdn.net/zsz459520690/article/details/72356709](http://blog.csdn.net/zsz459520690/article/details/72356709)
2. 也有人说async可以自动取消订阅

#### 动画
### 3 表单
表单处理是angular的核心能力,本人感觉优于其他两个框架.angular为每个`<form>`表单都附加了一个`NgForm`指令.angular有两种表单.
#### 模板驱动表单(Template-Driven Forms,对应的是FormsModule模块)
1. 简介

    异步,操控时需要等待指令/视图渲染完成,因为有`ngModule`,所以代码量更少,但是异步可能会让开发变得更复杂.比如，如果我们用@ViewChild(NgForm)查询来注入表单控件，并在生命周期钩子ngAfterViewInit中检查它，就会发现它没有子控件。 我们必须使用setTimeout等待一个节拍才能从控件中提取值、测试有效性，或把它设置为新值。

    使用该指令之前必须导入FormsModule并把它添加到Angular模块的imports列表中,导入之后所有的`<form>`都可以直接使用其中的指令了.
1. `ngModule`

    该指令只能用于表单元素,比如`input`,`select`等
    1. 用法1:直接单独使用:`ngModel`
        
        将自动关联表单控件(`input`,`select`等)的`name`属性(必须设置`name`属性),来并使用该值作为`ngForm`对象的属性名,然后`ngForm`就可以控制该控件(跟踪值的变化,用户的交互,验证状态以及保持视图和领域对象的同步等工作).比如`<input name="first_name" ngModel>`,可以通过`ngForm.value.first_name`来获取控件的值.

    1. 用法2:单绑或双绑
        我们希望能在像`<input>`和`<select>`这样的HTML元素上使用双向数据绑定,但是原生HTML不支持.所以Angular提供了`ngModule`**在表单元素上**使用双向数据绑定,其本质是`[ngModel]`和`(ngModelChange)`.(在angular1.x中也有`ng-module`实现双绑).不过,
        当我们需要do something more or something different时,也可以不使用"banana in a box"语法,比如`<input>`标签可以用`value`属性和`input`事件达到同样效果,

        ```html
        <input [value]="currentHero.name"
        (input)="currentHero.name=$event.target.value" >
        ```
        该用法同时具有用法1的作用(所以也必须有`name`属性),且不用再单独声明`ngModel`.
    2. 用法3:`#xxx="ngModel"`

        在模板中获取元素的状态,要求元素上已经有用法1或用法2.下面列出几种易混淆的情况的区别并分析为什么需要该写法:
        1. 假如元素**声明了模板引用变量`#firstName`且只有该属性**,我们可以通过`firstName.value`获取该元素的值,但是不能获取它的状态;因为能获取它的值,所以本人尝试监听该模板引用变量来动态修改其他dom元素的值,结果发现相应速度很慢,不推荐这样用.
        2. 如果元素**声明了属性`name="first_name"`且只有该属性**,然后再使用`ngModel`的用法1或用法2,则`ngForm`(已绑`#f`)可以获取该元素值和状态等.本人实测获取值可以用`f.control.controls.first_name?.value`,可以感觉到该写法很麻烦,所以此时我们需要`ngModel`的用法3
        3. 用法3要求元素上必须已有用法1或者用法2,官网的解释是:
            
            >Why "ngModel"? A directive's exportAs property tells Angular how to link the reference variable to the directive. You set name to ngModel because the ngModel directive's exportAs property happens to be "ngModel".

            官网中说的name也就是此处的firstName,而要求已有用法1或用法2是因为元素上必须要声明过`ngModel`指令才能将模板引用变量firstName链接到该`ngModel`指令.
            实测即使用了用法3,依然会有一些问题,比如

            ```html
            <div *ngIf="isAdd">
                <!-- 假设first_name有个初始值10 -->
                <input name="first_name" ngModel #firstName="ngModel">
                <select *ngIf="first_name.value == '10'">
                ...
                </select>
            </div>
            ```
            在上面的例子中,`select`是在`input`的值为10的时候出现,而我们给了`input`一个初始值10,但是实测`select`并没有出现.本人觉得多半是模板表单的缺点,即需要等一个节拍才能获取`input`中的值,但此时`select`的渲染判定已经过了,所以就没有出现.所以最佳实践是将`input`的值绑定到angular组件中的值,和响应式表单混合使用.(待补充)

2. `ngForm`

    一般写法是`<form #f="ngForm" ...>`把`ngForm`的值赋值给`#f`变量,然后就可以通过`#f`变量方便的控制表单`ngForm`各元素(带`ngModel`指令和`name`属性的元素),并监听元素的属性和状态等.
    1. 属性`controls`:可以获取表单控件的验证信息.比如`f.controls.name?.errors`的值是null或undefined时，表示验证成功
3. `ngModelGroup`

    用于生成嵌套的表单对象,类似于分组,比如user对象是这样的
    ```json
    {
        "name":"xiaoming",
        "address":{
            "province":"sichuan",
            "...":"..."
        }
    }
    ```
    我在表单中想绑定了province属性,但是表单获取的出来的值没有形成嵌套,那么可以这样写使得表单获取的值是嵌套的

    ```typescript
    <div ngModelGroup="address">
        <div [(ngModel)]="user.address.province">
        ...
    </div>
    ```
3. 表单的事件和方法
    1. `(ngSubmit)="method(xxx)"`:提交表单
    2. `reset()`:重置表单

4. 关于`#`,`ngModel`和`name`
    1. `ngModel`,见前面部分
    2. `name`:单独用时作用和html中一样,和`ngModel`一起用时则可以形成模板和组件间的单双绑.
    3. `#`:在
5. 关于`f.form.value`和`ngForm.value`

    在html模板中,这两个是一样的.`(ngSubmit)="onSubmit(f)`中写的是f,但是因为f赋值给了ngForm,所以实际传的是ngForm,所以在组件中接受的ngForm,获取值时用`xxx.value`而不是`xxx.form.value`

6. 表单css状态

    |状态|为真时的 CSS 类|为假时的 CSS 类|
    |-|-|-|
    |控件被访问过。|ng-touched	|ng-untouched|
    |控件的值变化了。|ng-dirty|	ng-pristine|
    |控件的值有效。|ng-valid	|ng-invalid|

#### 响应式表单(Reactive Forms,对应的是ReactiveFormsModule模块)
1. 简介
    
    同步,使用时需导入ReactiveFormsModule模块,
2. 响应式验证器

    响应式验证器是一些简单、可组合的函数.在模板驱动表单中配置验证器有些困难，因为我们必须把验证器包装进指令中。
3. 待研究
    1. [https://www.jianshu.com/p/925adede7c60](https://www.jianshu.com/p/925adede7c60)
    2. [https://segmentfault.com/a/1190000009041192](https://segmentfault.com/a/1190000009041192)
#### 两者比较
1. 哪个更好:各有所长.可两者都用.
### 4 引导启动
### 5 NgModules
### 6 服务
几乎任何东西都可以是一个服务.典型的服务是一个类,具有明确的用途,能把一件特定的事情做好.常见的有:
- 日志服务
- 数据服务
- 消息总线
- 税款计算器
- 应用程序配置

服务没有什么特别属于Angular的特性
1. 最佳实践
    
    组件类应保持精简。组件本身不从服务器获得数据、不进行验证输入，也不直接往控制台写日志。 它们把这些任务委托给服务。
#### 依赖注入
用于提供类的实例,负责处理类所需的全部依赖,大多数依赖都是服务.
1. 过程

    1. Angular创建组件时,会首先为组件所需的服务请求一个注入器(injector)
    2. 注入器维护一个服务实例的容器，存放着以前创建的实例。 如果请求的服务实例不在容器中，注入器就会创建一个服务实例，并且添加到容器中，然后把这个服务返回给 Angular
    3. 当所有请求的服务都被解析完并返回时，Angular 会以这些服务为参数去调用组件的构造函数,这就是依赖注入。
2. angular2有统一的依赖注入接口:所有依赖注入都在组件的构造方法中完成.
### 7 HttpClient
### 8 路由与导航
### 9 测试
### 11 angular metadata

1. 使用方法

    如果用的TypeScript,angular specify the metadata with decorators(装饰器) such as @Component() and @Input().如果用的其他语言,则只能在专门定义metadata的地方定义metadata,且声明使用的字面量也不一样.如,

    ```typescript
    @Component({
        //此处专门用于定义metadata(?)
        selector: 'exe-counter',
        outputs: ['change:countChange']
    })
    export class CounterComponent {
        //ts可在此处定义
        @Output('countChange') change: EventEmitter<number> = new EventEmitter<number>();
    }
    ```
    推荐用装饰器的写法,理由如下:
    - 可使用访问修饰符
    - 易于阅读
2. 最佳实践

    目开发中尽量通过装饰器定义无状态的组件，即组件仅依赖于输入属性，这样会大大提高组件可复用性.
#### @Input('xxx')
属性装饰器之一，用来定义组件内的输入属性.其中`xxx`为可选的参数,给绑定的属性指定其他名称(一般不推荐使用,有两个名字易致混淆).在metadata或非ts语言中可写成:
```typescript
@Component({
    selector: 'exe-counter',
    template: `
      <p>当前值: {{ count }}</p>
      <button (click)="increment()"> + </button>
      <button (click)="decrement()"> - </button>
    `,
    inputs:['count:value'] //类成员属性名称:绑定的输入属性名称
})
```
1. 简介
    1. 在子组件的构造函数中，是无法获取输入属性的值，只能在`ngOnChanges()`或`ngOnInit()`钩子中获取到。
2. 相关方法
    1. setter()和getter()

        使用目的和java差不多,还可以封装业务逻辑.如,

        ```typescript
        export class CounterComponent {
            // 默认私有属性以下划线开头，不是必须也可以使用$count
            _count: number = 0; 
            biggerThanTen: boolean = false;

            @Input()
            set count (num: number) {
                this.biggerThanTen = num > 10;
                this._count = num;
            }

            get count(): number {
                return this._count;
            }
        }
        ```
    2. ngOnChanges()

        当数据绑定输入属性的值发生变化的时候，Angular会主动调用 ngOnChanges()方法。它会获得一个 SimpleChanges 对象，包含绑定属性的新值和旧值，它主要用于监测组件输入属性的变化.但手动改变输入属性的值，不会触发ngOnChanges()钩子.(?)如,

        ```typescript
        export class CounterComponent implements OnChanges{
            @Input() count: number = 0;

            ngOnChanges(changes: SimpleChanges) {
                console.dir(changes['count']);
            }
            ...
        }
        ```
#### @Output('xxx')
使用场景:子组件将信息通过事件的形式通知到父级组件.除了用装饰器,也可在metadata的outputs数组中标记出来,如
```javascript
@Component({
    inputs: ['hero'],
    outputs: ['clicks:myClick']  // propertyName:alias

})
```
#### @HostListener
绑定全局事件,会随着 component destroy 而 unbind
#### @NgModule
用于标记一个类为模块,接收一个用来描述模块属性的元数据对象.
1. 最重要的属性有：
    1. `declarations`数组:声明本模块中拥有的视图类。Angular 有三种视图类：组件、指令和管道。
    2. exports - declarations 的子集，可用于其它模块的组件模板。
    3. `imports`数组:本模块声明的组件模板需要的类所在的其它**模块**.(?)只能放NgModule类.
    4. providers - 服务的创建者，并加入到全局服务列表中，可用于应用任何部分。
    5. `bootstrap`数组:指定应用的主视图（称为根组件），它是所有其它视图的宿主。只有根模块才能设置bootstrap属性。Angular 创建它并插入index.html宿主页面.
     
#### @Component
把紧随其后的类标记成了组件类,如果不用该装饰器,则后面的类仅仅是一个普通类.该装饰器接收一个配置对象,Angular会基于这些信息创建和展示组件及其视图.
1. 配置对象的配置项
    1. `selector`:CSS选择器，它告诉 Angular 在父级 HTML 中查找<hero-list>标签，创建并插入该组件。
    2. `templateUrl`:组件 HTML 模板的模块相对地址.也可用`template`,后面跟html字面量.
    3. `providers`:组件所需服务的依赖注入提供商数组.写在这儿的是局部,写在根模块的是全局的.
    4. `styles`数组:
#### @Injectable()
Don't forget the parentheses,否则会导致一个难以诊断的错误
#### @Directive
#### @Pipe
参考自定义管道
1. 配置对象
    1. `host`:(待补充)
#### @ViewChild
## 四 其他基础知识
### 1 编译器
### 1 动画
### 2 变更检测
### 3 事件
### 5 路由器
### 6 测试
### 7 部署

## 五 经验
1. 双向绑定中某方的数据延迟取得也会生效
### 1 实际开发还需要的其他模块
- 处理表单和输入的模块
- http模块
- 强大的路由模块
- 对动画的支持的模块
- 基于material设计风格的UI组件
- 用以进行单元测试、端对端和性能测试的工具集
### 2 angular cli(angular官方脚手架)
github地址:[https://github.com/angular/angular-cli](https://github.com/angular/angular-cli)
#### 安装
prerequisites:node and npm.安装命令:`npm install -g @angular/cli`
#### 常用命令

### 3 angular4英雄教程
#### 多个组件
#### 服务
#### 路由
1. 英雄的id是数字，而路由参数的值总是字符串。 所以我们需要通过 JavaScript 的 (+) 操作符把路由参数的值转成数字。


## 六 angular第三方组件
### 1 angular material2
1. [https://github.com/angular/material2/blob/master/src/lib/dialog/dialog.md](https://github.com/angular/material2/blob/master/src/lib/dialog/dialog.md)
2. github:[https://github.com/angular/material2#feature-status](https://github.com/angular/material2#feature-status)
##### 引入
1. 安装命令`npm install --save @angular/material`
2. 待补充
## 七 问题
### 1 已解决
1. 直接修改dom会影响angular的form获取的值吗?

    实测是不会的,而且还发现一点,假如有如下代码,

    ```html
    <input #hi15>
    <span>15的值是:{{hi15?.value}}</span>
    ```

    当我在input中输入的时候,`span`中的值并没有立刻改变,只有我每次回车或是提交的时候才会改变.所以我猜测input元素**默认情况**下是只有确认输入的时候才会去调用input()事件,正在输入的时候没有去调用,当然,注册了该事件或是双绑后就不一样了.


### 2 未解决
1. 表单验证
2. 声明周期
3. npm run start \ maven install \ng server \node xxx等命令的场景和用法？
4. angular为什么重量？vue和react
5. search`webpack和ngmodule`
6. [https://material.angular.io/](https://material.angular.io/)
7. [https://segmentfault.com/a/1190000009126012](https://segmentfault.com/a/1190000009126012)
8. [https://segmentfault.com/a/1190000006222169](https://segmentfault.com/a/1190000006222169)
9. [https://github.com/angular/material2](https://github.com/angular/material2)
10. AOT与angular-cli资料整理:[https://segmentfault.com/a/1190000011812867](https://segmentfault.com/a/1190000011812867)
11. angular变更检测:[https://segmentfault.com/a/1190000010928087](https://segmentfault.com/a/1190000010928087)
12. 懒加载
13. 安全导航操作符`?.`和管道操作符`|`
    1. 优雅的一个表达式操作符?.，当遇到空值时跳出，避免应用出错。更重要的是，它非常适合多重路径的处理。
    2. 管道操作符，它可以一级一级的流动，还可以使用:添加管道条件。
14. angular实用技巧点滴:[https://www.jianshu.com/p/c2e73a09bc38](https://www.jianshu.com/p/c2e73a09bc38)
15. Angular2新人常犯的5个错误:[https://segmentfault.com/a/1190000004969541](https://segmentfault.com/a/1190000004969541)
16. 一直困惑我的:[https://segmentfault.com/a/1190000008625978](https://segmentfault.com/a/1190000008625978)
17. 怎样理解Angular2中的ViewContainerRef，ViewRef和TemplateRef？(知乎):[https://www.zhihu.com/question/54554874](https://www.zhihu.com/question/54554874)
18. blog about make your angular fast:[https://blog.thoughtram.io/angular/2017/02/02/making-your-angular-app-fast.html](https://blog.thoughtram.io/angular/2017/02/02/making-your-angular-app-fast.html)
19. zonejs:[http://www.zcfy.cc/article/how-the-hell-does-zone-js-really-work-995.html](http://www.zcfy.cc/article/how-the-hell-does-zone-js-really-work-995.html)
20. 管道: http://blog.csdn.net/qq451354/article/details/54141024
21. [掌握Angular2的依赖注入-segmentfault](https://segmentfault.com/a/1190000006672079)
22. angular4:[https://v2.angular.cn/docs/ts/latest/](https://v2.angular.cn/docs/ts/latest/)
23. angular exportAs
24. angualr正式的代码是封装过的吗?在界面上能调dom吗?
25. angularform表单的最佳实践
26. `[attr.disabled]="input.disabled ? true : null"`为什么一定要这样写.
27. 它说的`Object destructuring` (对象解构) :[https://segmentfault.com/a/1190000009037539#articleHeader11](https://segmentfault.com/a/1190000009037539#articleHeader11)

    可否用于id的排序
28. ZONES

    Angular 1中我们需要通过scope.$apply告知框架进行脏值检查。Angular 2 通过使用 Zone.js 进行脏值检查，这意味着在使用第三方库时，你再也不需要使用scope.$apply进行脏值检查了，全部交给框架就好了。Angular 2 使用 Zone.js 来获知进行同步的时间点。
    1. Brian Ford对Zone的介绍,如果你想深入了解Zone.js可以去看这个视频:[https://www.youtube.com/watch?v=3IqtmUscE_U](https://www.youtube.com/watch?v=3IqtmUscE_U)
29. 脏值检查

    Angular 2中的脏值检查,深度解析了神奇的属性绑定背后的脏值检查:[https://vsavkin.com/change-detection-in-angular-2-4f216b855d4c](https://vsavkin.com/change-detection-in-angular-2-4f216b855d4c)
30. angular-cli:[http://blog.csdn.net/crper/article/details/62884688](http://blog.csdn.net/crper/article/details/62884688)
31. 教程:[http://cw.hubwiz.com/card/c/5599d367a164dd0d75929c76/1/4/1/](http://cw.hubwiz.com/card/c/5599d367a164dd0d75929c76/1/4/1/)
### 3 思考
1. 大多数应用只有一个组件树，它们引导单一根组件

    什么情况使用多组件树?
2. angular2还可以开发react native。(自行上GitHub搜索angular2 react native).
3. youyuxi说:ng serve 对SSL的支持