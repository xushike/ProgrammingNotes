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
### 5 angular第三方组件简介
### 6 网站
1. Angular2资源大全,感觉比较全面:[https://github.com/lightningtgc/awesome-ng2](https://github.com/lightningtgc/awesome-ng2)
### 7 文档
## 二 安装配置
### 1 win
1. 
### 3 mac
1. 需要先安装node和npm
## 三. 基础
### 1 架构
1. 当应用启动时，Angular 会从根组件开始启动，并解析整棵组件树，数据由上而下流下下一级子组件。
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
        2. 属性绑定(`[property]="expression"`):如`<img [src]="heroImageUrl">`,且右边可用三目运算符(?).
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

            事件对象有两种形态,取决于目标事件:
            1. 如果目标事件是原生DOM元素事件,`$event`就是DOM事件对象,有target和target.value这样的属性。
            2. 如果事件属于指令(指`@Output`声明的事件属性),`$event`则是`emit(xxx)`的`xxx`.
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
        1. `ngModule`指令

            我们希望能在像`<input>`和`<select>`这样的HTML元素上使用双向数据绑定,但是原生HTML不支持.所以Angular提供了`ngModule`**在表单元素上**使用双向数据绑定,其本质是`[ngModel]`和`(ngModelChange)`.(在angular1.x中也有`ng-module`实现双绑).不过,使用该指令之前必须导入FormsModule并把它添加到Angular模块的imports列表中。
            当我们需要do something more or something different时,可以不使用"banana in a box"语法,比如`<input>`标签可以用`value`属性和`input`事件达到同样效果,

            ```html
            <input [value]="currentHero.name"
            (input)="currentHero.name=$event.target.value" >
            ```


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
angular1.x包含了超过70个内置指令,实际上不需要那么多,angular2.x开始,用绑定就能达到原来的效果.
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

            这个`*`其实是语法糖(其他几个结构指令也是如此),Angular把`*ngIf`属性翻译成一个`<ng-template>`元素并用它来包裹宿主元素,其中`NgIf`是类名,`ngIf`是属性名.如,

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

        3. 关于模板输入变量和模板引用变量
            1. 模板输入变量:上例的`let hero`是模板输入变量,不同于模板引用变量.
            2. 模板引用变量:变量名加#来声明(比如`#elseBlock`),引用的是它所附着到的元素、组件或指令,可以在整个模板的任意位置访问.
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
3. 组件
#### 管道
#### 动画
### 3 表单
### 4 引导启动
### 5 NgModules
### 6 依赖注入
#### 1
#### x 参考
1. [掌握Angular2的依赖注入-segmentfault](https://segmentfault.com/a/1190000006672079)
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
#### @Output
使用场景:子组件将信息通过事件的形式通知到父级组件.
#### @HostListener
绑定全局事件,会随着 component destroy 而 unbind







### 2 模块
1. 模块定义了一个应用程序，模块控制器通常属于一个应用程序。
2. 模块的好处：JavaScript 中应避免使用全局函数。因为他们很容易被其他脚本文件覆盖。AngularJS 模块让所有函数的作用域在该模块下，避免了该问题。
2. 创建模块的方法：
```javascript
<script>
var app = angular.module("myApp", []); 
</script>
```
### 4 管道
1. http://blog.csdn.net/qq451354/article/details/54141024
## 四. 经验
1. 双向绑定中某方的数据延迟取得也会生效
## 五 angular material2
1. [https://github.com/angular/material2/blob/master/src/lib/dialog/dialog.md](https://github.com/angular/material2/blob/master/src/lib/dialog/dialog.md)
## 六. 问题
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