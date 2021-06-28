# JS
[TOC]

# 一 概述
## 1 简介
js为什么是单线程:与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？所以，为了避免复杂性，从一诞生，JavaScript就是单线程，这已经成了这门语言的核心特征，将来也不会改变。

为什么js在前端这么火：
1. 历史原因（个人感觉）
2. 事件机制（？）
3. nodejs

### 1.1 未整理
1. js5是没有块级作用域的。函数是JavaScript中唯一拥有自身作用域的结构，也就是说js有函数作用域和一个全局的作用域；js6中有块级作用域
2. js对大小写敏感
3. 大多数浏览器在提及对 JavaScript 的支持情况 时，一般都以 ECMAScript 兼容性和对 DOM 的支持情况为准

### 1.4 缺点
1. JavaScript支持异步，但本质是单线程环境,即使采用Ajax也只能局部更新，只是“看上去有了响应，但总体时间还是不变，甚至会变慢”.

## 2 历史
TC39 委员会每年都发布一个语言的新版本

### js的历史
js在1995年由Netscape的一位名为Brendan Eich的工程师创立,当时的主要目的是处理以前由服务器端语言(如Perl)负责的一些输入验证操作(在之前是发送到服务端验证,当时网速不好经常等很久才能验证输入是否正确).但现在js已经不仅是验证表单输入了,而是具备了与浏览器窗口及其所有内容**交互的能力**,是一门功能全面的编程语言.
说它简单，是因为学会使用它只需片刻功夫; 而说它复杂，是因为要真正掌握它则需要数年时间。要想全面理解和掌握js,关键在于弄清楚 它的本质、历史和局限性。
(待补充)

js的完整实现由三个部分组成:
1. 核心(ECMAScript)
2. 文档对象模型(DOM) 
3. 浏览器对象模型(BOM)

js的名字:只是为了蹭java的热度,除此之外可以说跟java没有关系.

js作者的采访:[https://www.youtube.com/watch?v=IPxQ9kEaF8c](https://www.youtube.com/watch?v=IPxQ9kEaF8c)

## 3 常识
### 3.1 js的参数传递(重点)
三种传递方式的区别：
- 按值传递（call-by-value，pass-by-value）：
- 按引用传递（call-by-reference，pass-by-reference）：
- 共享传递（call-by-sharing，pass—by-sharing）：对于传递到函数参数的对象类型，如果直接改变了拷贝的引用，那是不会影响到原来的那个对象；如果是通过拷贝的引用，去进行内部的值的操作，那么就会改变到原来的对象的。

js所有函数的参数都是按值传递的，不过不同数据类型具体有所不同：如果参数是值类型则复制值,如果是引用类型则复制引用(也叫共享传递).本人实测java似乎也是这样。例子如下:

```javascript
var obj = {x : 1};
function foo(o) {
o.x = 3;
}
foo(obj);
console.log(obj.x); // 3, 被修改了! 

var obj = {x : 1};
function foo(o) {
o = 100;
}
foo(obj);
console.log(obj.x); // 仍然是1, obj并未被修改为100.
```

### 3.2 深复制和浅复制(shallow copy)
为什么会有深浅复制:因为栈中的数据要求大小固定,所以js的基本类型是放在栈中的,而引用类型(对象和数组等)因为大小不固定所以放在堆中,但是我们可以把引用类型的地址写在栈中供我们访问.这样当我们操作基本类型的时候,操作的是值,而操作引用类型的时候,操作的是它的地址.所以有如下例子,

例子1:
```JavaScript
var a = 1;
var b = a;//复制
a = 2;//此时a为2,但是b为1
```

例子2:
```JavaScript
var color1 = ['red','green'];
var color2 = color1;//复制
console.log(color2)//['red','green'];
color1.push('black') ;//改变color1的值
console.log(color2)//['red','green','black'] 因为操作的是地址,也就是说操作的是同一个数组
```

也就是说简单的赋值没有办法复制引用类型,所以需要深复制和浅复制.

深拷贝和浅拷贝主要是对于引用类型而言的.
- 浅拷贝:只是复制引用类型的地址,就是只复制一层引用类型的属性,不会递归复制所有层级,比如有a的浅拷贝b,修改b.x的时候,a.x也会改变
- 深拷贝:递归复制所有层级,不会出现上面a.x和b.x指向同一引用类型的情况.缺点是会有性能问题(上面那个只复制地址当然很快),特别是层级很多的时候.

#### 实现深拷贝的几种方式
- `Object.assign(target, ...source)`(es6):第一个参数target为拷贝目标，剩余参数...source是拷贝源。此方法可以将...source中的属性复制到target中,然后返回target.同名属性会进行覆盖，缺点是只实现了第一层属性的深拷贝,也就是说对后面的嵌套属性还是浅拷贝.
    
    ```js
    // 深拷贝
    function changeName (obj) {
    let copy = Object.assign({}, obj)
    copy.name = "marry"
    }
    var a = { name: "tom" }
    changeName(a)
    console.log(a); // tom
    
    // 浅拷贝
    function changeName (obj) {
    let copy = Object.assign(obj)
    copy.name = "marry"
    }
    var a = { name: "tom" }
    changeName(a)
    console.log(a); // marry
    ```

- `JSON.parse(JSON.stringify(foo))`

    实现了深拷贝,缺点是会破坏原型链,并且无法拷贝属性值为function的属性,如果只是想单纯复制一个嵌套对象,可以使用此方法.

### 3.2 每行结尾
可用分号也可用回车,推荐分号

### 3.3 js中实现异步编程的四种方式(待研究)
1. 回调函数
2. 事件监听
3. 发布订阅模式
4. Promise对象

### 3.4 js的作用域(scope,action scope),var let和const,变量提升，以及TDZ
#### 3.4.1 作用域
js中默认只有全局作用域和函数作用域,没有块级作用域(虽然能通过一些方式实现),这点和java,go等是不一样,比如下面这个例子,在js里会输出10:

```JavaScript
for(var i =0;i<10;i++){
}
console.log(i) // 10
```
还有一个地方需要注意，函数内部声明变量的时候，一定要使用var或let命令。如果不用的话，你实际上声明了一个全局变量,如

```JavaScript
function f1(){
　　n=999;
}
f1();
alert(n); // 999
```

#### 3.4.2 var let和const
let和const是es5为了弥补var的不足而设计出来的。
- 使用var声明的变量，其作用域为该语句所在的函数内(没在函数则是全局的)，且存在变量提升；
- 使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升；
- 使用const声明的是常量，必须在声明时赋值,块级作用域,常量不能重新声明,也不能重新赋值。
    1. 如果变量是引用类型的话,引用地址(指针)不能改变,但是引用对象是可以改变的.意味着const声明对象的话,对象的属性是可以改变的,这个时候需要用到`Object.freeze()`方法(或者ts里面的`readonly`).

#### 3.4.3 变量提升(hoisting)
函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部.但是为了代码更易理解,最佳实践是在每个作用域开始前声明这些变量.

注意:只有声明的变量会提升，初始化的不会。

#### 3.4.4 TDZ
暂死区


### 3.5 关于`{ [native code] }`
网上看到的解释是:打印自定义的对象，会显示出源码，但是打印全局对象，因为这些全局对象是程序自带的，是二进制编译的（c\c++），所以无法显示出来源代码，只能显示的native code

### 3.6 a标签中的`href="javascript:;"`和`href="javascript:void(0)"`
这两者在非IE环境下可以认为效果是一样的.

`void(<表达式>)`是js中的关键字,表示计算里面的表达式然后返回固定返回undefined,习惯上用`void(0)`来表示上面都不干,当然也可以写成`void(666)`,`void(2333)`甚至`void("fuc...")`.那么为什么不用`void(undef)`呢,因为undefined在不同环境可能被重新赋值.

那么为什么要写成`href="xxx"`这种形式呢?因为a标签里的href需要指向一个URL,但是我们不想它跳转,就给它一个伪协议(`javascript:xxx;`),表示url的内容通过javascript执行.

既然href里可以写javascript,为什么还要onclick事件呢?暂时我没搞太懂,似乎是因为写在href中有一些兼容性问题.推荐写到`onclick()`中.

### 3.7 部分最佳实践or技巧
十进制指数:比如1000可以写成`1e3`,10000可以写成`1e4`,以此类推.(`1e0`为1)

### 3.8 The fps that JavaScript can detect doesn't always relate to number of frames displayed
(待验证)

### 3.9 Spread syntax（展开语法）和Rest syntax(剩余语法)
参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax
（待整理）
rest operator（rest操作符）:主要用于获得传递给函数的参数列表.如,

```javascript
function countArguments(...args) {  
　　return args.length;
}
countArguments('welcome', 'to', 'Earth'); // 3  
```

有两个作用:
1. 语法糖
2. 表示箭头函数中的arguments.具体参考:https://segmentfault.com/q/1010000008720963?_ea=1724154

spread operator（spread操作符）:主要用于数组构造和解构，在调用时将数组填入函数参数。展开语法和 Object.assign() 行为一致, 执行的都是浅拷贝(只遍历一层)。

```javascript
// 例子
// 数组构造
const odd = [1, 3, 5 ];
const nums = [2, ...odd, 4 , 6]; // [2,1,3,5,4,6]
// 解构数组
[a,...otherArr] = nums; // otherArr的值是[1,3,5,4,6]
```
有几个作用:
1. JS的函数只能返回一个值，如果返回多个值就需要用到数组或对象。展开运算符提供了一种处理这种返回值的有效方法
2. 替换push方法.push方法的参数不能是数组，所以只好通过apply方法变通使用push方法。有了展开运算符，就可以像下面直接将数组传入push方法,
    
    ```javascript
    var arr1 = [0, 1, 2], arr2 = [3, 4, 5];
    //Array.prototype.push.apply(arr1, arr2);
    arr1.push(...arr2);
    ```

注意:任何实现了Iterator接口的对象，都可以用展开运算符转为真正的数组.其他的似乎不行.

### 3.10 宿主对象（host objects）、本地对象（native objects）、内置对象（Build-in objects）和全局对象(global object)
宿主环境:与大多数编程语言不相同的，JavaScript 语言并没有输入/输出的概念。它被设计成在一个宿主环境下运行的脚本语言，它帮助给宿主环境提供与外界交流的机制。宿主环境有浏览器、Nodejs、操作系统等.

宿主对象（host objects）:由ECMAScript实现的宿主环境提供的对象。包含两大类，一个是宿主提供，一个是自定义类对象，ECMAScript官方未定义的对象都属于宿主对象,**所有非本地对象都是宿主对象**。宿主提供对象原理--->由宿主框架通过某种机制注册到ECscript引擎中的对象。比如宿主浏览器（以远景为参考）会向ECscript注入window对象，构建其实现javascript。同理还有浏览器提供的所有的BOM和DOM都是宿主对象。

本地对象（native objects）:独立于宿主环境的 ECMAScript 实现提供的对象。比如Object、Function、Array、String、Boolean、Number、Date、RegExp、Error等。可以简单理解为本地对象就是ECMAScript定义的类（引用类型），在运行过程中动态创建的对象，需要new。

内置对象（Build-in objects）:又称内部对象、标准内置对象(standard built-in objects)，由 ECMAScript 实现提供的、独立于宿主环境的所有对象。内置对象在 ECMAScript 程序开始执行时就被创建，即在引擎初始化阶段就被创建好的对象。这意味着开发者不必明确实例化内置对象，它已被实例化了。每个内置对象都是本地对象。ECMA-262 只定义了两个内置对象：`Global`和`Math`。`Math`对象我们经常用到，但`Global`对象很特别，它实际上根本不存在(无法直接访问)，在ECMAScript中，不存在独立的函数，所有函数都必须是某个对象的方法，任何不属于其他对象的方法和属性都是`Global`这个对象的方法和属性，所以事实上并不存在什么全局属性和全局函数，因为一切全局的函数和属性都是这个Global对象的方法和属性。比如`isNaN()`、`parseInt()`和`parseFloat()`方法等，看起来都是函数，而实际上，它们都是Global对象的方法。并且ECMAScript也没有定义怎样定义和调用这个对象，故所有`Global.`属性和`Global.()`都是无效的，但是在WEB浏览器中中把Global对象作为window对象的一部分实现了，故一切的所谓的全局属性和方法都是window对象的方法和属性。
```JavaScript
// 所以在web浏览器中，以下几种写法效果是一样的(假设this指向全局对象)
window.parseFloat("2.3");
this.window.parseFloat("2.3")
this.parseFloat("2.3") 
parseFloat("2.3")
// 以及
this == this.window // true
this === this.window // true
```

全局对象：包含两种理解，一是宿主对象里的全局对象和根据ECMAScript语法自定义的全局对象，比如`var objA = xxx`，在非严格模式下能通过`this.objA`来访问；二就是上面的本地对象或者宿主环境提供的全局对象，比如浏览器里面的window、Node.js的global，参考:[Standard built-in objects
](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)。两种理解都是可以的，两种都是在全局作用域下，全局作用域包含了全局对象的属性，包括继承来的属性，这个属性包含值属性(Value properties)和方法属性(Function properties)。

### 3.11 VanillaJS
使用VanillaJS意味着使用纯JavaScript而不使用jQuery之类的任何其他库。人们以此为笑话来提醒其他开发人员，如今无需其他JavaScript库即可完成许多工作，提醒世人并不是所有的网页都需要框架，第三方框架的大量引入是网页性能江河日下的罪魁祸首。所以它其实是"PlainJS"--原生JS。

### 3.12 naming convention 命名规范
最开始的时候方法名比较混乱，有驼峰比如`getClass()`、`toString()`，也有非驼峰比如`fontsize()`、`fontsize()`等，不过后面的版本已经被规范了，其中`fontsize()`、`fontsize()`等已经被Deprecated。

推荐命名规范：
- 构造函数和类名是大写开头驼峰式命名，如Array, Object, Number, String。
- 变量名、全局函数和类方法是小写开头驼峰式命名，如Array.prototype.findIndex()，String.prototype.fromCharCode()
- 常数是全大写+下划线命名，如Number.MAX_SAFE_INTEGER

### 3.13 严格模式
```JavaScript
'use strict';
```

### 3.14 falsy和truthy
js中**只有0、""、''、null、false、undefined、NaN这七个的布尔值(可通过`Boolean(xxx)`查看)是false**，其余为true(包括[]、{}、'0'、"0"、Function、Object、Infinity等).注意这儿说的布尔值而不是值.

### 3.15 shim和sham
参考：
1. https://github.com/es-shims/es5-shim

shim指能用旧js引擎完美模拟新ES中的方法，而不能完美模拟的就变成了sham，sham只是尽力模拟(as close as possible)，只承诺代码不会崩溃，不保证能起作用。比如
1. 在VUE中，`Object.defineProperty`这个特性是无法使用低级浏览器中的方法来实现的，所以Vue的响应式不支持IE8以及更低版本的浏览器(待确认)

## 4 文档网址等
1. 廖雪峰的js标准参考教程:[http://javascript.ruanyifeng.com/](http://javascript.ruanyifeng.com/)
2. 廖雪峰的es6入门:[http://es6.ruanyifeng.com/](http://es6.ruanyifeng.com/)
3. 网友自制的:[js中文网](https://www.javascriptcn.com/)

# 二 安装配置
# 三 基础
## 0 待整理
1. this的四种情况：
    1. 当在全部范围内使用 this，它将会指向全局对象。
    2. 函数调用时，这里 this 也会指向全局对象。
    3. 方法调用 test.foo(); 这个例子中，this 指向 test 对象。
    4. 调用构造函数 new foo(); 如果函数倾向于和 new 关键词一块使用，则我们称这个函数是构造函数。在函数内部，this 指向新创建的对象。 
2. 变量
    1. 没加修饰符声明的变量默认全局
2. **变量提升**，javascript的变量声明具有hoisting机制，JavaScript引擎在执行的时候，会把所有变量的声明都提升到`当前作用域`的最前面。
    1. 此处引用sf上某个大神的定义，我觉得定义得比较合适：定义变量分为三个阶段
        1. create（创建，相当于一般人说的声明）
        2. init（初始化，相当于一般人说的分配内存空间，此时的值是undefined）
        3. assign（赋值，也就是一般人说的赋值或者初始化）
    2. 大神总结的提升
        1. const和let只提升create，此时还没分配空间，称为`暂时死区`，所以只是在提升之后取值的话会报错`ReferenceError`
            1. 如果let x=xxx（xxx是任何一个不存在的变量），那么后面永远都用不了x了，因为x永远处于created状态，即`永远的暂时死区`
        2. var提升create和init
        4. 函数表达式（Function Expression）提升create和init，此时`函数表达式`的值是undefined，`函数表达式`此时还不能调用，否则会报错`TypeError`；如果是包含名称的函数表达式，比如
        ```
        var a=function b(){}
        ```
        使用b的话，则函数的值和调用函数都会报错`ReferenceError`
        3. 函数声明（Function Declaration）提升提升create、init、assign

## 1 变量和数据类型
### 1.1 变量的声明
弱类型(动态类型):js是弱类型(loosely typed)或者说动态(dynamic)语言,意味着可以不用提前声明(declare)变量的类型,在程序运行时会被自动确定,而且同一个变量可以保存不同类型的数据.如:
```javascript
var age=3;
age="hello";
```

强类型:有些语言要求声明变量的同时声明变量的类型,这种做法称为**类型声明**(typing),所对应的语言称为*强类型*(strongly typed)语言.

变量提升:具体见var,let,const和变量提升笔记.最佳实践还是提前声明变量.

关于变量命名:js变量名允许包含字母、数字、美元符号和下划线,但不能以数字开头.跟java一样

简单使用:
- 声明单个:`var age`
- 声明多个:`var age,mood`
- 声明并赋值:`var age=1,mood="sad"`

### 1.2 数据的类型
最新的ES标准定义了7种类型:6种原始类型(也称为基本数据类型)(String,Number,Boolean,null,undefined,以及ES6的Symbol)和Object(也称为引用数据类型)（这个Object是广义的，指代除了基本数据类型以外的所有其他类型）.

Object包含:
1. 标准对象("Normal" objects)
2. 函数(functions)
3. 有续集(Indexed collections):Arrays和typed Arrays
4. 键集(Keyed collections):Maps, Sets, WeakMaps, WeakSets
5. 结构化数据(Structured data):JSON
6. java标准库的內建对象,如日期(Dates),字符串(String),Math，正则表达式(RegExp)等

基本数据类型和Object的区别：
1. 基本数据类型：
    1. 存放在栈中
        1. 原始类型放在栈中是因为：原始类型占据空间是固定的，可以将他们存在较小的内存--栈中，这样便于迅速查询变量的值
    2. 数据大小确定
    3. 它们是直接按值存放的，访问也是直接按值访问
    4. 传递的时候是按值传递(call by value,pass by value)
2. 引用数据类型：
    1. 值存放在堆中，但是变量保存在栈中，变量保存的是堆内存中的引用地址
        1. 引用类型的值放在堆中是因为：引用类型的值的大小会改变，放在栈中的话会降低变量查询的速度，而把它的变量放在栈中的话，变量里指针地址的大小是固定的，所以把它的变量存储在栈中对性能无任何负面影响，所以它的值放在堆中，变量放在栈中
    2. 数据大小不固定
    3. 直接通过变量(引入)来访问值，不能直接访问值
    4. 传递的时候也是共享传递(call-by-sharing，pass—by-sharing)
        1. 是因为：对于复杂类型，按值传递性能较低

判断数据的类型用`typeof xxx`or`typeof (xxx)`,返回字符串,内容是xxx的类型,一般有一下几种类型:
1. 对这些基本类型就是对应的类型:string,number,boolean,undefined,symbol,除了null。对于null,是object.意味着`typeof null === "object"`,注意这其实是一个错误,因为历史一直没有修复.参考[typeof MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof).所以判断变量是不是对象的时候一般会排除它为null的情况,如`typeof foo == 'object' && foo !== null`

    ```js
     // 1. typeof()
    console.log(typeof (null)); // object
    console.log(typeof (undefined)); // undefined
    console.log(typeof ("abc"));// string
    console.log(typeof (123));// number
    console.log(typeof (true));// boolean
    // 2. 用Object.prototype.toString
    console.log(Object.prototype.toString.call(null)); // [object Null]
    console.log(Object.prototype.toString.call(undefined)); // [object Undefined]
    console.log(Object.prototype.toString.call("abc"));// [object String]
    console.log(Object.prototype.toString.call(123));// [object Number]
    console.log(Object.prototype.toString.call(true));// [object Boolean]
    ```
2. 对于函数是function
3. 对于宿主对象（由JS环境提供）,是`Implementation-dependent`
4. **对于任何其他对象(Object、Array、Function等)是object**，此时可以使用`Object.prototype.toString.call()`，如

    ```js
    ```

注意:`typeof Number(1)`是number,但是`typeof new Number(1)`是object,这两种写法都不推荐使用,String,Boolean也一样.

primitive values(原始值):除 Object 以外的所有类型都是不可变的（值本身无法被改变）。与 C 语言不同，JavaScript 中字符串是不可变的。JavaScript 中对字符串的操作一定返回了一个新字符串，原始字符串并没有被改变。我们称这些类型的值为“原始值”。

#### 1.2.1 字符串和String对象
单双引号都可以,可以根据需要包含的字符来确定:如果字符含单引号则用双引号包,如果含双引号就用单引号来包,这样不容易引起歧义.否则就要用转义字符`\`,如`var mood = 'don\'t ask';`。最佳实践是两种引号只选其一

使用索引可访问字符串中的字符,如`var character=carname[7];`

属性:
1. 字符串长度：`length`，返回字符串长度。实测中文英文都是算的一个单位的长度，所以它返回的其实是字符数而不是字节数。

方法:
1. 位置:下标从0开始，每个单位表示一个字符，不是字节。
    1. 根据下标访问字符：`charAt(idx)`:返回idx位置的字符.
    2. 子字符串在字符串中首次出现的位置：`indexOf(string[,fromIndex])`，返回字符在字符串中首次出现的位置,没有则返回-1
        1. `fromIndex`:可选,表示字符串中开始查找的位置.
2. `match()`:里面的参数可为string或RegExp,前者用于返回包含指定字符串等信息的数组,没有则返回null;更常用的是后者,用于返回正则匹配的数组,没有则返回null.
3. 截取字符串
    1. `stirng.slice(fromIndex[,endIndex])`，左闭右开，不改变原字符串。
    2. `substr(start[,length])`：ES未标准化该方法，暂不推荐使用
    2. `substring(start[,stop])`：左闭右开
3. 字符替换：`replace(regexp|substr, newSubStr|function)`，不改变原字符串。接收两个参数，第一个参数称为模式（pattern），表示所有将要被替换的字符串，可以字符串字面量或者正则表达式；第二个参数称为替换值（replacement），可以是字符串字面量或者函数。第二个参数还有更多细节，具体参考：[replace MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)
    1. 如果第一个参数是字符串字面量，则仅仅是第一个匹配的会被替换。
    2. 如果第二个参数是函数，则函数的返回值作为替换值，多个匹配值则函数执行多次。

4. `split(string)`:字符串转数组,string参数可以是正则表达式
5. `trim()`:去掉首尾空格,es6新增.
6. `test()`(待补充)
7. 转换大小写：`toUpperCase()`和`toLowerCase()`

模板字符串(es6):使用反引号包裹,里面的字符默认不会被转义(意味着**会原样输出**),想转义需要在前面加反斜杠`\`.可以包含特定语法`${expression}`的占位符.
1. 优点:更加优雅,不再需要考虑反斜杠来处理单引号和双引号。例子如

    ```JavaScript
    console.log("Fifteen is " + (a + b) + " and\nnot " + (2 * a + b) + ".");
    ```
    可以写成
    ```JavaScript
    console.log(`Fifteen is ${a + b} and\nnot ${2 * a + b}.`);
    ```

标签函数(tag function,es6):标签函数的语法是函数名后面直接带一个模板字符串，并从模板字符串中的插值表达式中获取参数.标签函数的第一个参数是被嵌入表达式分隔的文本的数组。第二个参数开始是嵌入表达式的内容。（感觉没有广泛的使用场景，仅了解就行了）

注意:
1. js中直接声明的字符串和字符串对象值是一样的,但是类型是不同的(分别是string和Object)
2. 打印模板字符串中的Object对象默认会输出成形如`[object Object]`,可以用`JSON.stringify(obj)`打印具体内容.

js去除字符串中空格的几种方法(待补充):
1. `replace(/\s/g, "")`

js判断字符串是否全部为数字的几种方法(待补充):
1. `isNaN(Number(xxx))`

#### 1.2.2 数值number
支持正负数和任意位的小数,js中不存在整数,所有数字都是64位浮点型.
(待补充:精确度的计算)
使用：
1. 声明
    1. 可用科学计数法来表示,如,

        ```javascript
        var y=123e5;    // 12300000
        var z=123e-5;   // 0.00123
        ```
    2. 可用八进制和十六进制来表示,也可转换为八进制或十六进制,如

        ```javascript
        var y = 0377; 
        var z = 0xFF;
        var myNumber=128;
        myNumber.toString(16);   // 返回 80
        myNumber.toString(8);    // 返回 200
        myNumber.toString(2);    // 返回 10000000
        ```
    5. `Infinity`表示无穷大的数字,可带正负.非0除以0可产生无穷大,如`2/0`。注意不能用小写开头，会变成普通字符串
        
        ```js
        console.log("3" < "Infinity"); // true
        console.log("3" < Infinity); // true
        console.log(3+Infinity); // Infinity
        ```
    6. `NaN`表示非数字值,即指示某个值不是数字.可设置number对象为该值,但NaN是不好(toxic)的,把它传给任何一个数学操作，结果都会返回一个NaN.全局函数`isNaN()`可判断一个值是否是NaN.
    7. `new Number(num)`生成数字对象,类似java,如,

        ```javascript
        var x = 123;              
        var y = new Number(123);
        typeof(y) // 返回 Object
        (x === y) // 为 false，因为 x 是一个数字，y 是一个对象
        ```
2. 绝对值
    1. `Math.abs(numberA)`
1. 判断数值类型的常见方法是正则表达式(待补充)
4. 浮点运算
    1. 自带的浮点运算并不100%准确,比如,

        ```javascript
        var x = 0.2+0.1; // 输出结果为 0.30000000000000004
        ```
    2. 所以可以引入第三方包，比如decimal.js
5. 数值和字符串类型的数值
    
    ```js
    // 加运算符和其他运算符不一样
    console.log("2" + 1); // 21
    console.log(1 + "2"); // 12
    console.log("2" * 3); // 6
    console.log(8/"2"); // 4
    ```

#### 1.2.3 Date
采用系统时区，基本是各语言的默认行为，但js并没有这样做，它默认使用UTC时区。

使用：
1. 初始化：创建一个新Date对象的唯一方法是通过new 操作符，例如`let now = new Date()`，若将它作为常规函数调用（即不加 new 操作符），将返回一个字符串，而非 Date 对象。 

    ```js
    let d = new Date();
    console.log(d); // 2020-10-09T08:24:32.145Z
    console.log(Date()); // Fri Oct 09 2020 16:24:32 GMT+0800 (GMT+08:00)
    ```
3. 获取时间戳
    1. `Date.now()`序列化从1970年1月1日0点0分0秒(UTC)到现在的毫秒数，它也有几个缺点：
        1. 它的精度会随user agent的不同而不同，比如在Firefox 59 中，默认被取整至 20 微秒；从Firefox 60开始，则被取整至 2 毫秒。`performance.now()`提供了精确到亚毫秒（sub-millisecond）的时间戳(也是不准确的)。
        2. 它取决于系统时钟，这不仅意味着它不够精确，而且还不总是递增。WebKit工程师（Tony Gentilcore）的解释如下：基于系统时间的日期可能不太会被采用，对于实际的用户监视也不是理想的选择。 大多数系统运行一个守护程序，该守护程序定期同步时间。 通常每15至20分钟将时钟调整几毫秒。 以该速率，大约10秒间隔的1％将是不准确的。
    2. `(*Date).getTime()`:获取毫秒的时间戳
2. 字符串和日期的转换：`Date.toISOString()`能够将日期类型转成ISO格式的字符串，`Date.parse(dateString)`方法能够将ISO格式的日期字符串转成日期。
3. 获取相对时间
    1. 略
    2. 如果想获取常见的“昨天”，“20秒前”或“1个月”之类的短语，而不是完整日期和时间戳，可以使用`Intl.RelativeTimeFormat`

#### 1.2.4 对象
标准对象的定义:
1. 关键字创建:`var obj = Object()`
2. 花括号语法:如`{name:value,name:value}`

对象的使用:
1. 访问元素:`obj.name`

#### 1.2.5 null和undefined
参考:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null

最开始只有null,undefined是作为补充设计出来的.要理解两者的区别,最好理解两者语义上的不同.

`null`是js基本类型之一，同时也是字面量，它表示一个值被定义了，只不过是定义为“空值”。出现场景:
1. 作为函数的参数，表示该函数的参数不是对象。
2. 作为对象原型链的终点。

例子如下:
```javascript
Object.getPrototypeOf(Object.prototype)
// null
```

`undefined`表示没有定义(就是此处应该有一个值，但是还没有定义).出现场景有:
1. 变量被声明了，但没有赋值时，就等于undefined。
2. 调用函数时，应该提供的参数没有提供，该参数等于undefined。
3. 对象没有赋值的属性，该属性的值为undefined。
4. 函数没有返回值时，默认返回undefined。
    
    ```js
     Math.random = function () {
        console.log("hello")
    }
    console.log(Math.random());
    // hello
    // undefined
    ```

例子如下:
```javascript
var i;
i // undefined

function f(x){console.log(x)}
f() // undefined

var  o = new Object();
o.p // undefined

var x = f();
x // undefined
```

两者区别:
1. 所以设置一个值为 null 是合理的，如`objA.valueA = null;`,但设置一个值为 undefined 是不合理的
2. null是字面量,而undefined是全局对象的属性
3. 其他

    ```javascript
    null === undefined // false
    null  == undefined // true
    ```

判断一个值是否为null或者是否为undefined：同时判断是否属于两者之一比较简单，方法较多，单独判断的方法如下。
```js
// 判断一个值是否为null：稍微有些复杂，一般不会用到，因为很少会有需要单独判断null的场景
!exp && typeof(exp)!="undefined" && exp!=0

// 判断一个值是否为undefined
typeof(xxx) == "undefined"
```

#### 1.2.6 二进制
##### 二进制读写
使用内置的`ArrayBuffer`和`DataView`等来进行二进制读写。使用场景有:
1. canvas 图像处理。
2. WebGL 与显卡通信。
3. 文件操作
4. Ajax响应

##### 二进制运算
js共支持5种二进制操作：
1. `&`与 ：同是高位则返回高位，否则返回低位
2. `|`或：有一方是高位，则返回高位
3. `!`非：按位取反
4. `^`异或：同位相同则返回低位，相反则返回高位
5. `->>`：按位左移或右移，每移动一位代表乘以或除以2

```js
// 例子1 获取某个整数对应的二进制形式中含有1的个数
// 方法一
n.toString(2).split("0").join("").length 

// 方法二 用二进制运算更高效
function countBits (n) {
    for (c = 0; n; n >>= 1) { // 只要n不为0就继续右移，想象碎纸机就好理解了
        c += n & 1 // 存储统计结果
    }
    return c;
}

console.log(countBits(1234)) // 5
```

### 1.3 类型转换(Type conversion)
js的类型转换包含Type conversion和Type coercion(类型强制转换)，两者的区别是：前者可以是隐式的也可以是显式的，后者是隐式的。

1. number to string
    1. `toString()`
    2. 加上空字符串

### 1.4 局部变量
### 1.5 全局变量
1. 如果您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明

### 1.6 变量的零值
js声明变量但是没赋初值(包括ts中声明的任意类型变量?),那么变量的值和类型都是undefined

## 2 运算符,比较符,逻辑操作符
### 2.1 加减乘除运算符
#### 2.1.1 加
可以用于数字也可以用于字符串,甚至可以把字符串和数字拼接在一起(弱类型语言,所以允许这样),此时数字被自动转换为字符串.例子如下,
```javascript
> "3" + 4 + 5
345
> 3 + 4 + "5"
75
```

#### 2.1.2 乘
JS中浮点数乘法精度问题:java和JavaScript中计算小数运算时，都会先将十进制的小数换算到对应的二进制，一部分小数并不能完整的换算为二进制，这里就出现了第一次的误差。待小数都换算为二进制后，再进行二进制间的运算，得到二进制结果。然后再将二进制结果换算为十进制，这里通常会出现第二次的误差。要避免这种情况呢，通常可以将小数同时扩大相同10的整倍数，完成计算后，在去掉之前添加的整倍数.

例子:
```javascript
39.2*3
// 117.60000000000001

39.2*10*3/10
// 117.6
```

### 2.2 delete
delete 操作符用于删除对象中不是继承而来的属性(区别于原型链的属性).var, let以及const创建的不可设置的属性不能被delete操作删除;

一般情况都会返回true(属性不存在也返回true),除非属性是自己不可设置的值,比如`Math.PI`

使用场景:
1. 删除数组元素:删除的元素不再属于该数组,数组长度不受影响.两个例子如下

    ```JavaScript
    var trees = ["redwood","bay","cedar","oak","maple"];
    delete trees[3];
    if (3 in trees) {
    // 这里不会执行
    }
    console.log(trees) //["redwood","bay","cedar",,"maple"]
    console.log(trees[3]) // undefined
    console.log(trees.length)//5
    ```

    ```JavaScript
    var trees = ["redwood","bay","cedar","oak","maple"];
    trees[3] = undefined;
    if (3 in trees) {
    // 这里会执行
    }
    console.log(trees) //["redwood","bay","cedar",,"maple"]
    console.log(trees[3]) // undefined
    console.log(trees.length)//5
    ```

2. 删除`setter`和`getter`设置的属性

### 2.3 比较操作符==(也称标准相等操作符)、===(Identity/ strict/triple equality)、!=(Inequality)、>(Greater than operator)
`==`并不是严格相等，会先转换成相同类型，然后判断值是否相等，而不是布尔值是否相等.(具体的==比较待补充)

`!=`:如果两操作数不是同一类型，JavaScript会尝试将其**转为一个合适的类型，然后进行比较**。
```js
1 !=   2     // true
1 !=  "1"    // false
1 !=  '1'    // false
1 !=  true   // false
0 !=  false  // false
```

`===`严格相等，不会做type conversion(类型转换)

`==`和`===`的区别和总结（待补充）：
1. `==`比较的时候会**先转换成相同类型再比较**，当两个操作数都是对象时，JavaScript会比较其内部引用，当且仅当他们的引用指向内存中的相同对象（区域）时才相等，即他们在栈内存中的引用地址相同。而`===`在类型不同时直接返回false
2. 当需要明确操作数的类型和值的时候，或者操作数的确切类型非常重要时，应使用严格相等操作符。否则，当你允许操作数在比较前进行类型转换时，可以使用标准相等操作符来比较。

### 2.4 js的逻辑操作符`||`和`&&`(即短路求值,Short-circuit Evaluation)(难点)
这两个逻辑操作符判断的是布尔值而不是值.

短路原则:a && b中,如果a的布尔值为真,则b不会进行计算,即b被"短路";a || b中,如果a的布尔值为假,则b不会进行计算.

赋值原则:对于value=a && b && c...,如果a的布尔值为真则判断b,否则返回a的值,以此类推,直到最后一个值时返回最后一个值;对于value=a || b || c...,如果a的布尔值为假,则判断b,否则返回a,以此类推,直到最后一个值时返回最后一个值.

对于表达式(以及和浏览器控制台每句执行后的undefined的关系)

### 2.5 按位操作符(Bitwise Operator)
#### 2.5.1 双位操作符(Double Bitwise NOT)
可以用来替代`Math.floor()`,快得多.例如
```javascript
Math.floor(4.9) === 4  //true
~~4.9 === 4  //true
```

## 3 流程控制和循环
### 3.1 if else
跟java的用法基本一样,除了一点:js中的if判断的是变量或表达式的布尔值而不是值,关于js的布尔值可参考[https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)



### 3.2 switch case default

### 3.3 while和do ... while

### 3.4 for循环
可以使用`break`和`continue`，意思和java中一样

#### 3.4.1 普通for循环
这里有个MDN上的有趣的优化写法,很简练,但是注意只有确定数组中不包含“falsy”值(即`a[i]`的值不是falsy)时才可以使用,总之不用最好:
```javascript
for (var i = 0, item; item = a[i]; i++) {
    // Do something with item
}
```

#### 3.4.2 for in
可以遍历任何数据类型，但最适合的是遍历对象的属性，如果是对象，该方法依次访问这个对象及其原型链中所有可枚举的属性，默认以字符串的形式遍历出对象的所有属性.

如果遍历Array对象,循环的是数组的索引,而且也是字符串类型,不是数值.

关于遍历的顺序:遍历顺序依赖于环境,所以该方法并不能保证顺序.但是约定成俗的顺序应该是:先遍历属性名是数值的(从0升序),然后属性名不是数值的则是按定义时的顺序遍历.

注意:
1. 该方法遍历时最好不要动态修改属性,因为不能保证后面的遍历是否能访问到.

#### 3.4.3 forEach((ele,index,array)=>{...})
对于array的遍历,一般情况下`forEach()`比`for ... of`更好用.

### 3.5 三目（三元）运算符

## 4 JS本地对象
参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects

### 4.1 Global
包含值属性和方法属性

#### 值属性
有以下值属性，它们都是simple value, 它们have no properties or methods。也称为全局变量。
- Infinity：是一个数值，表示无穷大。初始值是Number.POSITIVE_INFINITY。
- NaN:全局属性 NaN 的值表示不是一个数字（Not-A-Number），和`Number.NaN`相同。编码中很少直接使用到 NaN。通常都是在计算失败时，作为 Math 的某个方法的返回值出现的（例如：Math.sqrt(-1)）或者尝试将一个字符串解析成数字但失败了的时候（例如：parseInt("blabla")）。**NaN自身永不相等于自身**
- undefined
- null literal
- globalThis

#### 方法属性
##### decodeURI(),encodeURI(),decodeURIComponent()和encodeURIComponent()
根据HTTP的规范(URL允许的字符集是ISO-8859-1、以及一些其他要求)，所以有效的URI中不能包含空格、中文等。而这些URI编码方法就可以对URI进行编码或解码，它们用特殊的UTF-8编码（也称为转义序列，本质是把UTF8的每个字节转换成百分号加上对应的16进制，比如"张三"会被替换成`%E5%BC%A0%E4%B8%89`，空格会被转换为`%20`）替换所有无效的字符，从而让浏览器能够接受和理解。大家通俗地叫这几个方法为`urlencode`(url编码)方法

```JavaScript
var uriStr = "http://www.baidu.com?name=张三&num=001 zs"; 
var uriec = encodeURI(uriStr); 
document.write("编码后的" + uriec); 
// 编码后的http://www.baidu.com?name=%E5%BC%A0%E4%B8%89&num=001%20zs 
var uridc = decodeURI(uriec); 
document.write("解码后的" + uridc); 
// 解码后的http://www.baidu.com?name=张三&num=001 zs
```

两者的区别:
1. `encodeURIComponent()`和`decodeURIComponent()`:转义除了字母、数字、`(`、`)`、`.`、`!`、`~`、`*`、`'`、`-`和`_`（共71个）之外的所有字符。可知它不适合用于对整个URI进行编码，因为冒号、正斜杠、问号和井字号也会被编码，所以它主要用于对URI中的某一段(比如URI里的查询字符串)进行编码。
2. `encodeURI()`和`decodeURI()`:不能转义的字符比上面两个方法多，除了上面的两个方法不能转义的，还包括`;`、`/`、`?`、`:`、`@`、`&`、`=`、`+`、`$`和`#`（共82个）。可知它不会对本身属于URI的特殊字符进行编码，例如冒号、正斜杠、问号和井字号，所以`encodeURI()`主要用于整个URI的编码。

##### 其他
`parseInt()`:将字符串转换为整型,第二个参数表示数值的进制，可选填。（待整理）例子如,
```javascript
parseInt("123", 10) // 123
parseInt("010", 10) // 10
parseInt("010") // 此处未指定进制,该函数根据开头的0来决定将那个字符串转换为八进制数字,所以结果是8
```

`isNaN`:NaN不能通过相等操作符（== 和 ===）来判断 ，因为 NaN == NaN 和 NaN === NaN 都会返回 false。 因此，isNaN()就很有必要了。该方法还是有瑕疵的，所以更推荐用ES6的`Number.isNaN()`，后者更可靠。

`eval()`（不推荐使用）:函数会将传入的字符串当做js代码执行，然后返回结果，类似于一个js解析器。它只接受一个参数，多余的参数会被忽略。如果传入的字符串是表达式，它会对表达式求值；如果...在`eval(`)中创建的任何变量以及函数都不会被提升，只有执行到`eval()`时才创建
```JavaScript
// 1. 传入的字符串是表达式
console.log(eval('2 + 2')); // 4
// 2. 传入的参数不是字符串
console.log(eval(new String('2 + 2'))); // 输出：2 + 2，eval()返回了包含"2 + 2"的字符串对象
```

### 4.2 Math
操作：
1. 取近似值
    1. 四舍五入：`Math.round()`，返回一个数字四舍五入后最接近的整数。但是在对小数部分的0.5处理上该方法和其他语言不同，其他语言一般是舍入到远离0的方向，但是该方法是上舍入。比如`Math.round(3.5)`是4，但`Math.round(-3.5)`是-3.
    2. 向下舍入：`Math.floor()`
    3. 向上取整：`Math.ceil()`
2. 取最大值`Math.max()`:如果没有参数，则结果为`-Infinity`,如果给定的参数中至少有一个参数无法被转换成数字，则会返回 NaN。
3. 生成随机数`Math.random()`：生成0~1的pseudorandom number。
    1. 缺点:非密码学安全，其实现是与宿主对象相关，并且不能保证加密使用的安全性(why?)。
        
        ```js
        // 生成UUID，缺点是重复率较高
        'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
            var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
            return v.toString(16);
        })
        ```
    2. 如果在浏览器环境下，更推荐使用加密安全的`window.crypto.getRandomValues()`

### 4.3 Object
**几乎所有的 JavaScript 对象都是 Object 的实例**

#### 4.3.1 值
1. `Object.prototype`:表示Object的原型对象
2. `Object.prototype.constructor`:对象的构造函数

#### 4.3.2 方法
1. `Object.toString(numA)`：每个对象都有一个`toString(numA)`方法，当该对象被表示为一个文本值时，或者一个对象以预期的字符串方式引用时自动调用（和其他语言类似）。默认情况下，`toString(numA)` 方法被每个 Object 对象继承。如果此方法在自定义对象中未被覆盖，`toString(numA)`返回 "[object obj_type]"，特别的`toString(numA)`调用 null 返回[object Null]，undefined 返回 [object Undefined]。`numA`是可选的，表示进制,接收区间`[2,36]`中的任意整数作为可选参数。
    ```JavaScript
    var o = new Object();
    o.toString(); // [object Object]
    (1234).toString(2) // "10011010010"
    ```
2. `Object.assign(targetA, sourceA...)`:对象合并。将源对象的所有可枚举属性，复制到目标对象，它只有第一层的深拷贝。如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。
    1. `Object.assign`拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（enumerable: false）。
    
    ```js
    // 如果只有一个参数，Object.assign会直接返回该参数。
    const obj = {a: 1};
    Object.assign(obj) === obj // true
    
    // 如果该参数不是对象，则会先转成对象，然后返回
    typeof Object.assign(2) // object
    // 由于undefined和null无法转成对象，所以如果它们作为参数，就会报错。
    Object.assign(undefined) // 报错
    Object.assign(null) // 报错
    ```
3. `Object.getPrototypeOf()`
3. `Object.setPrototypeOf(objA, objB)`：设置一个指定对象的原型到另一个对象。该方法性能较差，更推荐用`Object.create()创建新对象的方式代替`它是ES6新增的方法，有个旧方法是`Object.prototype.__proto__`。
    
    ```js
    // Polyfill
    // 仅适用于Chrome和FireFox，在IE中不工作：
    Object.setPrototypeOf = Object.setPrototypeOf || function (obj, proto) {
    obj.__proto__ = proto;
    return obj; 
    }
    ```

4. `Object.defineProperty(obj, prop, descriptor)`:方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回这个对象。该方法是数据双向绑定实现的基石.

    ```JavaScript
    // 1.
    // 这个例子展示使用getter和setter方法扩展 Date原型
    var d = Date.prototype;
    Object.defineProperty(d, "year", {
        get: function () { return this.getFullYear() },
        set: function (y) { this.setFullYear(y) }
    });
    var now = new Date();
    console.log(now.year);  // 2000
    now.year = 2001; 
    console.log(now); // 987617605170
    // Wed Apr 18 11:13:25 GMT-0700 (Pacific Daylight Time) 2001
    // 2.
    var o = { a:0 }
    Object.defineProperties(o, {
        "b": { get: function () { return this.a + 1; } },
        "c": { set: function (x) { this.a = x / 2; } }
    });
    ```
5. `Object.getOwnPropertyNames()`:该方法返回一个数组，它包含了对象 o 所有拥有的属性（无论是否可枚举）的名称。
6. 判断对象是否包含某个(字段)属性
    1. 使用`in`,属性名称需要用字符串
        
        ```js
        var obj = {name:'jack'};
        console.log(('name' in obj)); // --> true
        console.log(('toString' in obj)); // --> true
        console.log((toString in obj)); // --> false
        console.log(('toString2' in obj)); // --> false     
        ```
    2. 和`undefined`作比较来判断是否是非`undefined`的字段，但是本身值是undefined的属性没法判断
        
        ```js
        var o = { x: 1, y: undefined };
        console.log(o.x !== undefined); //true
        console.log(o.z !== undefined); //false
        console.log(o.toString !== undefined);//true
        console.log(o.toString2 !== undefined);//false

        console.log(o.y !== undefined); //false, 本身值是undefined的就没法判断了
        console.log("y" in o); // true
        console.log(o.hasOwnProperty("y")); // true
        ```
    3. 使用`object.hasOwnProperty() boolean`判断是否是对象自身的属性,如果是继承的属性则返回false.
    
        ```js
        var obj = {name:'jack'};
        obj.hasOwnProperty('name'); // --> true
        obj.hasOwnProperty(name); // --> ReferenceError
        obj.hasOwnProperty('toString'); // --> false
        ```
7. `Object.freeze()`:冻结对象，使其不能被修改。使用场景一般是const声明对象时会用到（还可以使用ts的readonly）。当然这里面有很多细节需要注意，具体参考：[Object.freeze() MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
    1. 该操作不可逆
    2. 该方法只影响对象本身的属性,不影响原型属性
8. `Object.keys(o)`:该方法返回一个对象 o 自身包含（不包括原型中）的所有属性的名称的数组。
    
#### 4.3.x 原型链
一个实例的`__proto__`属性，指向它的原型对象

### 4.4 Array
特点:
1. 无类型：可以存储任何类型的JavaScript值。
    1. 扒开V8里数组的C++源码可以看到，数组JSArray继承自JSObject，也就是说，数组是一个特殊的对象，既然是对象，内部也是key-value的存储形式，所以可以存放不同的数据类型。从注释上还可以看到数组有fast和slow两种模式。
        1. fast数组：底层结构是FixedArray，是一种线性的存储方式。新创建的空数组，默认的存储方式是快数组，快数组长度是可变的，可以根据元素的增加和删除来动态调整存储空间大小，内部是通过扩容和收缩机制实现。
            1. 扩容策略:根据最大的索引值来扩容
                1. 扩容后的新容量 = 旧容量的1.5倍 + 16
                2. 扩容后会将数组拷贝到新的内存空间中
            2. 收缩策略：也是根据最大的索引值来判断
                1.  如果容量 >= length的2倍 + 16，则进行收缩容量调整，否则用holes对象（空洞对象，指的是数组中分配了空间，但是没有存放元素的位置，被访问时会得到undefined）填充未被初始化的位置
                2. 收缩的大小`elements_to_trim`，根据 length + 1 和 old_length 进行判断，是将空出的空间全部收缩掉还是只收缩二分之一。
        1. slow数组：底层结构是HashTable，不用开辟大块连续的存储空间，节省了内存，但是由于需要维护这样一个 HashTable，其效率会比快数组低。
        3. 两种模式的比较：快数组就是以空间换时间的方式，申请了大块连续内存，提高效率。 慢数组以时间换空间，不必申请连续的空间，节省了内存，但需要付出效率变差的代价。
        4. 两种模式的转换
            1. 快 -> 慢:当对数组赋值时使用远超当前数组的容量+ 1024时（这样出现了大于等于 1024 个空洞，这时候要对数组分配大量空间则将可能造成存储空间的浪费，为了空间的优化，会转化为慢数组。
            2. 慢 -> 快: 当慢数组的元素可存放在快数组中且长度在 smi 之间且仅节省了50%的空间,则会转变为快数组(待整理)
2. 动态：可根据需要增长或缩减
3. 可能是稀疏的：数组元素的索引不一定是连续的，意味着稀疏数组length属性值大于元素的个数

有以下几种创建方法：
1. `new Array(length)`：创建指定长度的空数组(可以理解为只有length，没有值和索引)
    1. **注意是空数组,而不是值为undefined的数组**,虽然打印其中的值时可能为undefined.
    2. 如果想创建值为单个数字的数组呢?可用js6新增的`Array.of(element...)`,element可以是任意类型
2. `Array()`:等同于`new Array()`。
2. `new Array(element0, element1, ..., elementN)`
3. literal syntax(字面量):`[element0, element1, ..., elementN]`
4. 通过函数`split()`,`match()`等创建

还有一种额外的但不推荐的定义方法:关联数组.就是把其中的index由数字换成字符串,比如`arr["name"]="tom"`.(但是非常不推荐使用)

几种创建方法的对比：
1. 在初始化大数组的时候，`new Array()`(以及`Array()`)性能更好。（待验证）

#### 4.4.1 属性
1. 长度`length`

#### 4.4.2 方法
1. 读取：
    1. 下标，JS数组的下标是字符串类型的，所以以下几种方法都可以获得对应的数据，是因为Javascript自动将数字转化为字符串。
        ```js
        let arr = [100, 12.3, "red", "blue", "green"];
        arr[arr.length] = "black";
        console.log(arr.length);    // 6
        console.log(arr[5]);  //black
        console.log(arr['5']);  //black
        console.log(arr["5"]);  //black
        ```
1. 数组和字符串的转换
    1. `string1.split(string2)`
    2. `array.join(string)`
2. `splice()`：从原数组中添加/删除项目，然后返回被删除的项目,该方法会改变原数组.注意这个返回不是`return`,而是赋值.意味着不会中断方法的运行,用值去接收的时候才有用.
    1. 在头部添加元素可以用:`arr.splice(0,0,xxx)`；删除头部的元素可以使用`arr.splice(0,1)`等等
3. 在数组头/末尾添加或删除项目
    1. 这两个方法使它表现得像栈一样
        1. `push()`:向数组的末尾添加一个或更多元素，并返回新的长度。
        2. `pop()`:删除并返回数组的最后一个元素。
    2. 这两个方法使它表现得像队列一样
        1. `unshift()`：头部添加
        2. `shift()`：头部删除
4. `map()`:返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值,按照原始数组元素顺序依次处理元素,不会改变原数组.语法:`array.map(function(currentValue,index,arr), thisValue)`,微软js手册的例子如下,

    ```JavaScript
    obj = {divisor: 10}
    remainder = function (value) {
        return value % this.divisor;
    }
    numbers = [6, 12, 25, 30];
    result = numbers.map(remainder, obj);
    console.log(result);
    ```

    如果把方法写在map的callback()里面,

    ```JavaScript
    result = numbers.map((ele)=>{
        return ele % this.divisor;    
    }, obj);
    ```
    则`this`会变成`{}`,目前还不清楚为啥.
    参考:"回调中所用的 ES2015 箭头函数 比等价的函数表达式更加简洁，能优雅的处理 this 指针。"

3. `filter(callback[, thisArg])`:返回过滤后的新数组,不会改变原数组.简单使用如下

    ```javascript
    let arr = [xxx].filter((ele)=>{
        return ele > 10;
    })

    ```
4. `find(func)`:返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined
5. `Array.prototype.slice([begin[,end]])`:从数组或类数组中拷贝出新的数组，这个拷贝是对原数组元素的浅拷贝，该方法不会改变原数组。如果不带参数,则是整个复制。begin和index一样从0开始算,如果是复数,则表示倒数,-1表示倒数第一个元素,以此类推.
6. 排序`sort(sortby)`：对数组进行排序，然后返回对数组的引用。排序是在原数组上进行，不生成副本。sortby参数是可选的，如果没提供，则默认按字符编码的顺序进行排序，如果提供了，则必须是函数。V8版本7.0开始使用Timsort实现。
    
    ```js
    // 例子1 提供了sortby
    function sortNumber(a,b){
        return a - b
    }
    arr.sort(sortNumber)
    ```

array常用操作总结
1. 过滤用`filter()`,需要对元素进行处理用`map()`
2. 判断数组为空(待补充):

    ```js
    arr.length == 0
    ```

注意：
1. 查看`map()`方法的文档发现：callbackfn is called only for elements of the array which actually exist; it is not called for missing elements of the array。可知js数组的undefined元素和空插槽(empty item，不存在任何元素，但是算入了数组长度。类似于golang`make([]int64,0,xxx)`的容量)是不同的，在进行`map()`、`every()`、`filter()`、`forEach()`、`some()`等遍历方法时，是不会对不存在的元素执行回调函数，但是会对undefined元素执行。例子见studyJS项目。
2. 如何获取数组的容量(capacity):目前js似乎没提供相关的方法来获取

#### 4.4.3 类数组（Like Array、Array-Like)
**只要有一个 length 属性和(0..length-1)范围的整数属性都认为是类数组对象**。比如宿主浏览器提供的HTMLCollection类型、NodeList对象，`{'length': 2, '0': 'eat', '1': 'bananas'}`，方法实例的arguments等。

### 4.5 RegExp对象及正则表达式
参考：
1. http://ecma-international.org/ecma-262/5.1/#sec-15.10

字符模式对象,用于正则表达式

使用：
1. 声明语法：有两种，如下,其中pattern表示模式,是正则表达式的主体；modifiers(修饰符)是可选的，用于指定全局匹配、区分大小写、多行匹配等:

    ```javascript
    var patt=new RegExp(pattern,modifiers); // 写法一
    var patt=/pattern/modifiers;  // 写法二：更简洁
  
    // 比如
    var re = new RegExp("\\w+");
    var re = /\w+/;
    var re = /hello/i; // i是修饰符，表示不区分大小写，所以整句的意思是不区分大小写地搜索hello字符串
    ```
2. 常用方法
    1. 在字符串上使用
        1. `stringA.search(pattern)`, 其中的pattern可以是正则也可以是普通字符串，所以它的作用是检索与正则表达式/字符串相匹配的子字符串，并返回子串的起始位置
        2. `stringA.replace(pattern, target)`，其中的pattern可以是正则也可以是普通字符串，所以它的作用是在字符串中用target替换另一些字符
    2. 在正则对象上使用
        1. `regExpA.test(stringA)`:检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false
            
            ```js
            // 写法一
            var patt = /e/;
            patt.test("The best things in life are free!");
            
            // 写法二：更简洁
            /e/.test("The best things in life are free!")
            ```
        2. `regExpA.exec(stringA)`检索字符串中的正则表达式的匹配,该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为 null
            1. 注意返回的数组和普通数组稍有不同，参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array
3. 详细语法
    1. modifiers(修饰符)
        1. `i`执行对大小写不敏感的匹配。
        2. `g`执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。reg对象有个lastIndex属性，只有搭配`g`修饰符一起使用才会生效，在每次匹配成功后更新lastIndex的值为当前成功匹配的下一个位置，下次匹配就从这个位置开始，即使换了stringA对象也是这样。
        3. `m`执行多行匹配。
    2. 正则主体
        1. 分组
        2. 环视(Look around)，即前瞻后顾(见studyJS笔记)
            1. 环视匹配的是特定位置，不匹配任何字符，也就是并不会“占用”字符。这一点与单词分界符`\b`，锚点`^`和`$`相似，但是环视更加通用。
        3. 反向引用
4. 问题
    1. 如何一次获取字符串中所有匹配项？目前好像没提供类似的方法，可以使用`g`修饰符和for循环来实现
        
        ```js
         // 1. 查找成对的字母
        let str = "aabbbbgbddesddfiid"
        let re = /(\w)(\1)/g
        let res;
        while ((res = re.exec(str)) !== null) {
            console.log(res[0]);
        }
        ```
        

### 4.6 Function
参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function

#### 4.6.1 属性
1. `Function.length`:函数签名中入参(形参)的数量。

#### 4.6.2 方法
1. `Function.prototype.bind()`：该方法创建一个新的函数(称为Bound Function,BF)，在新函数被调用时，这个新函数的 this 被指定为 bind() 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。
2. `Function.prototype.call(thisArg, arg1, arg2, ...)`：该方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。简单概括它的作用就是允许其他对象调用某个对象的函数/方法，并且能被继承。
    1. `thisArg`:在非严格模式下，如果没有指定`thisArg`或者指定为 null 或 undefined 时会自动替换为指向全局对象，原始值会被包装；在严格模式下，不指定`thisArg`则`this`的值是undefined
    
    ```js
    // 例子
    // 1. 
    Math.max.call(null, ...[1,2]])
    Math.max.call(...[1,2]])
    // 2. 在web浏览器中
    var forEach = Array.prototype.forEach;
    var divs = document.getElementsByTagName( 'div' );
    var firstDiv = divs[ 0 ];
    forEach.call(firstDiv.childNodes, function( divChild ){ // 将某个宿主对象 （如 NodeList） 作为 this 传递给原生方法 （如 forEach） 不能保证在所有浏览器中工作，已知在一些浏览器中会失败
        divChild.parentNode.style.color = '#0F0';
    });
    ```
3. `Function.prototype.apply(thisArg, [argsArray])`:该方法调用一个指定的this值，以及一个数组（或类似数组对象（比如数组字面量或Function.arguments））提供的参数。该方法和`call`只有一个区别。

    ```JavaScript
    // 例子
    // 1. 可以使用arguments对象作为argsArray来把所有的参数传递给被调用对象，这样在使用apply函数的时候就不需要知道被调用对象的所有参数。
    ...
    // 2. 
    Array.prototype.slice.apply([1,2]) /
    Math.max.apply(null, [1,2]) // 对于静态方法，thisArgs需要指定为null，因为没有对象去调用
    Array.apply(null, Array(2))
    ```
`call()`和`apply()`异同：
1. 相同之处：两个函数的作用是相同的。
2. 不同之处：
    1. thisArg后面的参数不同：`call()`方法的接受的是多个参数，而`apply()`方法接受的是一个包含多个参数的数组。

#### 4.6.3 arguments
见arguments部分

### 4.7 Number
JavaScript的Number类型为双精度IEEE 754 64位浮点类型。

#### 4.7.1 属性
1. `Number.POSITIVE_INFINITY`:正无穷大
2. `Number.NEGATIVE_INFINITY`:负无穷大
3. `Number.NaN`:

### 4.8 JSON
包含两个方法: 用于解析 JavaScript Object Notation  (JSON) 的`parse()`方法，以及将对象/值转换为 JSON字符串的 `stringify()`方法。除了这两个方法, JSON这个对象本身并没有其他作用，也不能被调用或者作为构造函数调用。

```js
var a = {
  "data": "{\"code\":\"200\",\"message\":\"接口掉用成功\",\"success\":true}",
}
c = JSON.parse(a.data)
console.log(c); // { code: '200', message: '接口掉用成功', success: true }
```

更多关于JSON的其他知识参考JSON笔记

#### 4.8.1 方法
1. `JSON.stringify(value[, replacer [, space]]) string`:replacer可以是函数、数组、null或省略，space用于指定缩进的字符串，用于美化输出（pretty-print）

### 4.9 ArrayBuffer
见arraybuffer部分笔记

### 4.10 Proxy
参考：
2. https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy

### 4.11 Symbol
为什么需要Symbol:ES5对象属性名等都是字符串，如果使用了别人提供的对象，想给这个对象加上新的方法(mixin模式)，而新方法名字可能和原方法相同，很容易冲突。所以ES6引入Symbol来解决这个问题。

什么是Symbol:ES6新引入的原始数据类型，表示一个独一无二的值。

Symbol的使用
1. 创建:通过`Symbol(descriptionA)`函数生成，不能用`new`命令，因为Symbol是原始类型，不是对象
    ```js
    // 1. 字面量创建:descriptionA是描述性的字符串，不影响Symbol的唯一性
    let s1 = Symbol('foo');
    let s2 = Symbol('foo');
    s1.toString() // "Symbol(foo)"
    s1 === s2 // false
    // 2. Symbol.for(descriptionA):从已经登记到全局的Symbol中搜索是否已经有该descriptionA的Symbol，如果有就返回该Symbol，否则就创建一个，并将其登记到全局。注意这个登记是全局环境的，不管有没有在全局环境运行，意味着在不同的iframe或 service worker中可以取到同一个值
    let s1 = Symbol.for('foo');
    let s2 = Symbol.for('foo');
    s1 === s2 // true
    ```

2. 关于descriptionA参数:descriptionA是描述性的字符串，主要是方便我们区分Symbol。
3. 类型:`typeof symbolA`是"symbol"，所以可以理解Symbol是一个独一无二的类似字符串的一个东西。
4. 运算：Symbol 值不能与其他类型的值进行运算，会报错。但是可以显式转为字符串(`symbolA.toString()`)和布尔值(默认为true)
5. 主要使用场景
    1. 用作对象的属性名
        1. 注意写法，应该永远用方括号，不能使用点运算符，如果使用了点运算符，因为点运算符后面只能跟字符串，此时用的就是字符串，而不是这个Symbol。
            ```js
            // 下面三种写法作用一样
            let mySymbol = Symbol();
            // 第一种写法
            let a = {};
            a[mySymbol] = 'Hello!';
            // 第二种写法
            let a = {
            [mySymbol]: 'Hello!'
            };
            // 第三种写法
            let a = {};
            Object.defineProperty(a, mySymbol, { value: 'Hello!' });
            ```
            
            ```js
            // 点运算符的例子
            const mySymbol = Symbol();
            const a = {};
            
            a.name = 'Tom';
            a.mySymbol = 'foo'; // 这里点运算符后的mySymbol是一个字符串，和Symbol类型的mySymbol没有关系
            a[mySymbol] = 'bar'; // 正确写法
            console.log(a.mySymbol, a['mySymbol'] == a.mySymbol); // foo true
            console.log(a[mySymbol]); // bar
            console.log(a); // { name: 'Tom', mySymbol: 'foo', [Symbol()]: 'bar' }
            ```
        2. Symbol作为属性名时，该属性是公开属性，不是私有属性
        3. 遍历对象的Symbol属性:遍历对象的时候，Symbol属性不会被`for...in`、`for...of`、`Object.keys()`、`Object.getOwnPropertyNames()`、`JSON.stringify()`这些常规方法遍历到，可以通过`Object.getOwnPropertySymbols()`和`Reflect.ownKeys()`方法遍历到。利用这个特性，可以用Symbol定义一些只用于内部的方法。
            1. `Object.getOwnPropertySymbols()`方法，可以获取指定对象的所有 Symbol 属性名。该方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。
            2. 新的API`Reflect.ownKeys()`方法可以返回所有类型的键名，包括常规键名和 Symbol 键名。
    2. 用作常量:可以用来定义一组常量，保证这组常量的值都是不相等的。

Symbol的属性:
1. `description`(ES2019)

Symbol的方法:
1. `Symbol.keyFor(symbolA)`:方法返回一个已登记的Symbol类型的key(即descriptionA)。如果Symbol没有被登记，返回undefined

### 4.12 Intl
它提供了精确的字符串对比、数字格式化，和日期时间格式化(Collator，NumberFormat 和 DateTimeFormat等)，都是language-sensitive(语言敏感的)(或者说本地化)的

参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl

使用：
1. 大部分都有`formatToParts()`方法
1. `RelativeTimeFormat()`:可以输出短语化的相对时间
    
    ```js
    // 英文相对时间
    rtf = new Intl.RelativeTimeFormat('en');
    // output :: 15 minutes ago
    console.log(rtf.format(-15, 'minute'));
    // output :: in 8 hours
    console.log(rtf.format(8, 'hour'));

    // 中文相对时间
    rtf = new Intl.RelativeTimeFormat('zh-Hans');
    // output :: 15分钟前
    console.log(rtf.format(-15, 'minute'));
    // output :: 8小时后
    console.log(rtf.format(8, 'hour'));
    // 1天前
    console.log(rtf.format(-1, 'day'));
    // 昨天
    const rtf = new Intl.RelativeTimeFormat('zh-Hans', {
        numeric: 'auto', // other values: 'always'
    });
    console.log(rtf.format(-1, 'day'));
    ```

## 5 函数
函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块(感觉形容得很精炼).实际上,JS的所有函数都是Function对象,只不过它比较特殊,能够被调用.

个人感觉js的函数可以分为普通函数和生成器函数,一般讨论的都是普通函数.

注意:函数体`{}`内不使用var定义的变量是全局变量(待测试)


### 5.1 定义普通函数(三种方法)
1. 函数声明(function declaration),函数声明有提升.语法是以`function`开头,如

    ```JavaScript
    hoisted(); // "foo"

    function hoisted() {
        console.log("foo"); 
    }
    ```
    1. 函数生成器声明 (function* 语句)和函数生成器表达式 (function*表达式):返回Generator对象(该对象主要用于迭代?),没遇到过,待补充
2. 函数表达式(function expression),语法是不以`function`开头
    1. 函数表达式没有提升,所以不能在定义之前调用,如

        ```JavaScript
        notHoisted(); // TypeError: notHoisted is not a function

        var notHoisted = function() {
        console.log("bar");
        };
        ```

    2. 命名函数表达式:包含函数名称的，函数名称可以在函数内部使用.使用场景一般是你想在函数体内部引用当前函数(可以用来递归).而且也推荐使用函数名的方法在函数体内部调用当前函数.如

        ```JavaScript
        var math = {
            'factorial': function factorial(n) {
                if (n <= 1)
                return 1;
                return n * factorial(n - 1);
            }
        };
        ```

    3. 匿名函数（anonymous）:函数表达式省略函数名后就变成了匿名函数,匿名函数的的`this`指向调用它的对象(?).
        1. 即时调用的函数表达式(IIFE,Immediately Invokable Function Expressions):当函数只使用一次时可以使用该语法.如

            ```JavaScript
            (function() {
                statements
            })();

            (function foo() {
                statements
            })()
            ```

            它有两个好处:
            1. 不仅避免了外界访问此 IIFE 中的变量，而且又不会污染全局作用域
            2. IIFE中定义的任何变量和函数，都会在执行结束时被销毁。这种做法可以减少闭包占用的内存问题
    4. 箭头函数(arrow functions)(重点):更适用于那些本来需要匿名函数的地方.引入箭头函数有两个方面的作用：更简短的函数并且不绑定this.
        1. 需要返回对象字面量时,要写成这样:

            ```JavaScript
            参数=> ({foo: bar})
            ```
        2. 支持剩余参数和默认参数:如,

            ```JavaScript
            (参数1, 参数2, ...rest) => {函数声明}
            (参数1 = 默认值1,参数2, …, 参数N = 默认值N) => {函数声明}
            ```
        3. 支持参数列表解构
        4. 参数括号内定义的变量是局部变量;函数体{}内不使用var定义的变量是全局变量,用var定义的变量是局部变量
        5. 不绑定this:在箭头函数出现之前，每个新定义的函数都有它自己的 this值（在构造函数的情况下是一个新对象，在严格模式的函数调用中为 undefined，如果该函数被称为“对象方法”则为基础对象等）.而箭头函数不会创建自己的this,它只会从自己的作用域链的上一层继承this.
        6. 不绑定Arguments 对象:在大多数情况下，使用剩余参数是相较使用arguments对象的更好选择,如

            ```JavaScript
            function foo() { 
            var f = (...args) => args[0]; 
            return f(2); 
            }

            foo(1); 
            // 2
            ```
    
3. `new Function()`构造函数.使用Function构造器生成的Function对象是在函数创建时解析的,而上面几种方法是跟其他代码一起解析的,所以`new Function()`是调用效率最低的.

    ```JavaScript
    var sum = new Function('a', 'b', 'return a + b');

    console.log(sum(2, 6));
    // expected output: 8
    ```

### 5.2 函数的this(难点)
MDN上说的似乎只针对浏览器环境,然后本人在NodeJS环境中测试的结果和浏览器环境差异很大,所以以下结论只针对浏览器环境.

1. 对于非箭头函数,每个新定义的函数都有它自己的 this值,然后又分以下几种情况:
    1. 如果函数属于类,则this是该类的对象
    2. 如果函数是某个对象的属性,则this是该对象
    3. 如果函数属于某个方法(函数的外层是某个方法),则this是全局对象(即Window)
        1. 此时想使用外层方法的this,可以在外层将this赋值给一个变量,然后在函数中使用该变量,如

            ```JavaScript
            function Person() {
                var that = this;
                that.age = 0;

                setInterval(function growUp() {
                    //  回调引用的是that变量, 其值是预期的对象. 
                    that.age++;
                }, 1000);
            }
            ```
    
    可以看出,这个结论和"匿名函数的的`this`指向调用它的对象"似乎有点冲突.暂时以结论为准吧.
2. 对于箭头函数:不会创建自己的this,只会从自己的作用域链的上一层继承this,如,

    ```JavaScript
    function Person(){
        this.age = 0;

        setInterval(() => {
            this.age++; // this正确地指向person 对象
        }, 1000);
        }

        var p = new Person();
    ```

### 5.3 默认参数
### 5.4 arguments
arguments 是一个函数的局部变量，它表示被调用对象的所有未指定的参数。arguments对象不是一个 Array 。它类似于Array，但除了length属性和索引元素之外没有任何Array属性。例如，它没有 pop 方法。但是它可以被转换为一个真正的Array：
```js
var args = Array.prototype.slice.call(arguments);
var args = [].slice.call(arguments);
// ES2015
const args = Array.from(arguments);
const args = [...arguments];
 ```

属性：
1. `arguments.length`:实际传递给函数参数的个数，区别于`Function.length`。

### 5.5 剩余参数(rest parameters)
剩余参数和 arguments对象之间的区别主要有三个：
1. 剩余参数只包含那些没有对应形参的实参，而 arguments 对象包含了传给函数的所有实参。
2. arguments对象不是一个真正的数组，而剩余参数是真正的 Array实例，也就是说你能够在它上面直接使用所有的数组方法，比如 sort，map，forEach或pop。
3. arguments对象还有一些附加的属性 （如callee属性）

### 5.6 生成器函数(generator function)(js6)
区别于普通函数,生成器函数返回一个Generator对象(符合可迭代协议和迭代器协议的对象,可以简单理解为iterator对象),它是js对协程的不完全实现,生成器函数在执行时能暂停，后面又能从暂停处继续执行.生成器函数不能当构造器使用.一般使用场景是状态机,流程控制.

两种定义方法(第一种更常用):
1. 在函数声明的`function`后面加上`*`,如
    
    ```JavaScript
    function* gen(){
        var index = arguments[0] || 0;
        while(true)
            yield index++;
    }

    ```

2. 使用`GeneratorFunction`.注意`GeneratorFunction`是js内置对象,但不是全局对象,它可以通过`Object.getPrototypeOf(function*(){}).constructor`来获取.例子如,

    ```JavaScript
    var GeneratorFunction = Object.getPrototypeOf(function*(){}).constructor
    var g = new GeneratorFunction("a", "yield a * 2");
    var iterator = g(10);
    console.log(iterator.next().value); // 20
    ```

生成器函数的执行流程:调用一个生成器函数并不会马上执行它里面的语句，而是返回它的迭代器 （iterator ）对象。当这个迭代器的 `next()`方法被首次调用时，其内的语句会执行到第一个出现`yield`的位置暂停,`yield`后紧跟迭代器要返回的值.如果用的是 `yield*`（多了个星号），则表示将执行权移交给另一个生成器函数（当前生成器暂停执行,当另一个生成器函数执行后才继续）.`next()`方法返回一个对象，这个对象包含两个属性：value 和 done，value 属性表示本次 yield 表达式的返回值，done为布尔类型，表示生成器后续是否还有 yield 语句，即生成器函数是否已经执行完毕并返回。继续调用`next()`则往下一个`yield`执行.在生成器函数中显式`return`时，会导致生成器立即变为完成状态，即调用 next() 方法返回的对象的 done 为 true。如果 return 后面跟了一个值，那么这个值会作为当前调用 next() 方法返回的 value 值。

调用`next()`方法时，如果传入了参数，那么首先这个参数会作为生成器函数上一条执行语句的返回值,然后再执行当前执行语句.典例如下,
```JavaScript
function *gen(){
    yield 10;
    y=yield 'foo';
    yield y;
}

var gen_obj=gen();
console.log(gen_obj.next());// 执行 yield 10，返回 10
console.log(gen_obj.next());// 执行 yield 'foo'，返回 'foo'
console.log(gen_obj.next(10));// 将 10 赋给上一条 yield 'foo' 的左值，即执行 y=10，返回 10
console.log(gen_obj.next());// 执行完毕，value 为 undefined，done 为 true
```

## 6 事件


## 9 定时器(难点)
参考网友的文章:https://www.cnblogs.com/wangying731/p/5164780.html

详见DOM笔记的window部分.

## 13 错误/异常处理

## 15 注释
有两种，跟java一样：
1. `//`:单行注释
2. `/**/`:多行注释，多行注释书写在字符串 `/*` 和 `*/` 之间，如，

    ```javascript
    /*
        I am also
        a comment
    */
    ```

# 四 高级
## 1 闭包(closure)
闭包，指的是词法表示包括不被计算的变量的函数，也就是说，嵌套的函数可以访问在其外部声明的变量,同时也意味着函数内的引用的外部变量,是在运行时才计算的.JS的闭包很有用,它主要有以下几个作用:
1. 嵌套的函数可以访问在其外部声明的变量,意味着变量被引用着所以不会被回收，因此可以用来封装私有变量和方法,带来了许多与面向对象编程相关的好处,比如我可以保存一个变量,函数运行完后该变量会被保存,待需要的时候调用.但这是优点也是缺点，不必要的闭包只会徒增内存消耗.

参考:
1. https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures
2. 1分钟理解js闭包:[http://www.jb51.net/article/83524.htm](http://www.jb51.net/article/83524.htm)

## 2 web worker
参考：
1. http://www.ruanyifeng.com/blog/2018/07/web-worker.html

包含普通线程和共享线程(SharedWorker):
2. 共享线程：共享线程是为了避免线程的重复创建和销毁过程，降低了系统性能的消耗，共享线程SharedWorker可以同时有多个页面的线程链接。

使用场景：
1. cpu密集型计算、边缘计算
2. 在不受第三方脚本影响的上下文中运行脚本，有两种方法：iframe 和 Web Worker。相比之下 Web Workers 更好用，因为它们实例化更快，毕竟它们仅创建新的 JavaScript 执行上下文，而不是完整的 DOM。这里不受影响指的是web worker不受主线程里脚本的影响，比如在主线程中重新定义了`Math.random`，但是在web worker的脚本中不受影响。具体见studyJS项目

问题：
1. Uncaught DOMException: Failed to construct 'Worker': Script at 'file:///.../worker.js' cannot be accessed from origin 'null'.
    1. 有些浏览器禁止通过本地文件访问使用Web Worker，有以下几种方法解决
        1. about:config
            1. 设置security.fileuri.strict_origin_policy为false
        2. 把文件放到服务器

## 3 ArrayBuffers,SharedArrayBuffers,ArrayBuffer视图
### 3.1 ArrayBuffers
为什么我们需要这两个:在js中创建一个变量的时候,引擎会去猜测变量的类型以及如何在内存中表示,会导致分配的内存是实际需要的2~8倍,比如普通数组，可能变成快数组或者满数组，最终可能会导致大量的内存浪费。而ArrayBuffer用来表示通用的、固定长度的原始二进制数据缓冲区(基本上就像原始内存一样,它模仿了C语言中的直接内存访问),它里面每个元素是值类型,不是引用类型(区别于普通数组可以存引用类型).

我们不能直接操作ArrayBuffer,而是通过类型数组对象(typed array objects)或者数据视图(DataView)对象来操作.那么为什么不让程序员直接访问内存,而是添加这个抽象层:直接访问内存会带来一些安全漏洞.

使用场景:与普通数组相比,ArrayBuffer占用小,性能高,主要用于音频视频编辑，访问WebSockets,WebAudio,Ajax等,可以快速方便地通过类型化数组来操作原始的二进制数据,适合处理大数据和提高性能.

构造:
1. `new ArrayBuffer(num)`:num的单位为字节,该ArrayBuffer的内容被初始化为0

静态属性和方法:
1. `length`:构造函数的length属性,值为1.(意义是?)
2. `[Symbol.species]`:返回构造器
3. `ArrayBuffer.isView(arg)`:arg是否是ArrayBuffer的视图实例(例如 类型数组对象 或 DataView)

属性和方法:
1. `byteLength`:数组缓冲区的字节大小,不可变.
2. `slice(beginIndex[,endIndex])`


### 3.2 ArrayBuffer视图
简单介绍:ArrayBuffer视图就是对ArrayBuffer增加了一层抽象,它可以是类型数组视图或者数据视图,通过它,我们可以读写ArrayBuffer中的内容.
```js
// bf申请了1kb的内存区域。但是并不能对bf直接操作，需要将它赋给一个类型数组对象或者视图对象来操作
var bf = new ArrayBuffer(1024); 
// 创建了有符号的32位的整数数组b，每个数占4字节，长度也就是 1024 / 4 = 256 个，通过它就可以操作这块内存区域了
var b = new Int32Array(bf);
b[3]=1;
```

#### 3.2.1 类型数组视图(Typed array views)
形如Int8Array，Uint32Array，Float64Array等以及特殊的Uint8ClampedArray.(其中Uint8ClampedArray很擅长Canvas数据处理)

创建类型数组视图:
1. 形如`new Int8Array(arg)`:arg可以是数字、array或者arraybuffer.如果是arraybuffer,则arraybuffer的字节数是BYTES_PER_ELEMENT的整数倍才会创建成功,所以接着要判断是否创建成功.同一个arraybuffer可以创建多个视图
2. 形如`new Int8Array(arg,byteOffset?,byteLength?)`:byteLength是类型数组的字节大小.

属性和方法:
1. `BYTES_PER_ELEMENT`:每个元素所占的字节数,比如Int8Array是1.可以通过类型数组类名中的数字来记忆,8就是8位,对应1字节,以此类推.
2. `byteLength`
3. `byteOffset`:返回视图在它ArrayBuffer中占用内存区域的起点位置.(和index一样从0开始)
3. `length`:元素个数
4. `name`:构造器的名称,如"Int8Array"
4. 转换为普通数组:`Array.from()`或者`Array.prototype.slice.call(typedArray)`

#### 3.2.2 数据视图(DataView)
和类型数组视图比,更加灵活,不用考虑平台字节序问题.

那么什么是平台字节序:"Endian"(字节序) 和 "endianness"(字节顺序) (或者 "byte-order") 描述计算机如何组织字节生成对应数字的.主要有三种:
1. little-endian(小字节序、低字节序):  如0x78 0x56 0x34 0x12,即低位字节排放在内存的低地址端，高位字节排放在内存的高地址端,在所有的英特尔处理器上使用.
2. big-endian(大字节序、高字节序): 0x12 0x34 0x56 0x78,通常被叫做"网络字节顺序"("network byte order"),因为互联网标准通常要求数据使用big-endian存储, 从标准Unix套接字层开始一直到标准化网络的二进制数据结构
3. mixed-endian (混合字节序,historic and very rare): 0x34 0x12 0x78 0x56

创建:`new DataView(buffer [, byteOffset [, byteLength]])`

使用:
1. 赋值:形如`dataView.setInt8(12, 42)`
2. 取值:形如`dataView.getInt8(12)`

注意赋值和取值中的byteOffset(也就是例子中的12)是对于arraybuffer的,不是对于dataView的.

### 3.3 SharedArrayBuffers
与 ArrayBuffer 不同的是,SharedArrayBuffers不能被分离.但是因为安全漏洞,SharedArrayBuffers将会被禁用,所以简单了解就行了.

## 4 js模块化
为什么需要模块化:开发中,我们需要引入其他软件,新旧代码之间就会存在依赖关系,由于这些软件需要一起工作,因此它们之间不存在冲突是非常重要的.封装可以防止模块之间相互冲突,这也是C语言库中元素通常带有前缀的原因之一。所以可以归纳以下几个：
1. 防止全局污染
2. 依赖管理

随着js越来越复杂,依赖管理可能会变得麻烦,重构也受到影响:如何维护加载链的正确顺序?

主流的几个方案: 
1. 方案
    1. 社区方案
        1. webpack
        2. CommonJS
        4. AMD/CMD/UMD
    2. 官方方案
        3. ES6
2. 对比：
    1. 编译时和运行时：
        1. CommonJS和AMD/CMD/UMD在运行时确定模块的依赖关系，因为它是通过查找对象属性来判断
        2. ES Modules是在编译时确定模块的依赖关系。
    

### 4.1 webpack

### 4.2 CommonJS
CommonJS是用于开发服务器端的JS项目.同步加载模块.NodeJS采用的CommonJS规范.

使用：
1. 原理：require 命令第一次加载该脚本时就会执行整个脚本，然后在内存中生成一个对象（模块可以多次加载，但是在第一次加载时才会运行，结果被缓存），这个结果长成这样：
    
    ```js
    {
        id: '...',
        exports: { ... },
        loaded: true,
        ...
    }
    ```
1. 优缺点
    1. 优点:
        1. 简单
        2. 所有代码都运行在模块作用域，不会污染全局作用域
        3. 支持循环依赖
    2. 缺点:
        1. 没有模块的构造函数
        2. 模块是单一文件
        2. 因为是同步加载，所以不适合浏览器环境
3. 细节
    1. 模块加载的顺序，按照其在代码中出现的顺序

```js
// 把方法定义到模块的属性上
module.exports.sayHello = function() {
    console.log('Hello ');
};
var myModule = require('module');
myModule.sayHello();

// 把模块定义为方法
module.exports = sayHello;
// 调用则需要改为
var sayHello = require('module');
sayHello();
```

### 4.3 ES2015
`import`和`export`指令的静态特性允许静态分析器在不运行代码的情况下构建完整的依赖关系树。注意它会自动采用严格模式，且 `import` 命令具有提升效果，会提升到整个模块的头部，首先执行

优点:
1. 支持同步和异步加载。
2. 语法简单。
3. 支持静态分析工具。

```js
// 导出模块:方法一 命名导出。命名导出对导出多个值很有用。（一个模块可以有任意个命名导出）
export var firstName = 'Michael'; // 导出成变量
var firstName = 'Michael'; 
var lastName = 'Jackson';
export { firstName, lastName }; // 导出多个变量
export { firstName as aliasA, lastName as aliasB }; // 使用别名导出多个变量
export function diag(xxx) {...}  // 导出成方法
export { myFunction } // 导出成方法，存在名为myFunction的方法
export const foo = Math.sqrt(2) // 导出成常量
export default class {} // 导出类

// 导出模块:方法二 默认导出。命令用于指定模块的默认输出（一个模块只能有一个默认输出）。如果使用了 export default 语法，在 import 时则可以任意命名
export default 121 // 默认导出变量 121
export default function myLogger() {} // 默认导出方法

// 导出使用总结：模块的默认导出通常是用在你期望该从模块中获取到任何想要的内容；而命名导出则是用于一些有用的公共方法，但是这些方法并不总是必要的。

// 导入模块：一般使用模块js文件的路径来导入，一般不包含".js"扩展名,用单引号或双引号包裹，导入的方式很多，如下
import { firstName } from 'module'; // 导入整个模块
import { firstName as alias } from 'module'; // 使用别名导入整个模块
import { firstName, lastName, year } from 'module'; // 导入里面的多个子模块
import { firstName, lastName, year as alias1, alias2, alias3} from 'module'; // 使用别名导入里面的多个子模块
import alias from 'module'; // 导入单个或多个时,需要知道导出的名字,很不方便,所以js允许设置一个默认的导出。对于使用默认导出的模块，可以使用随意的名字来接收，而且不用大括号包裹
import "module"  // 仅为副作用而导入
import * as moduleA from 'module'; // 导入某模块的所有导出,可以用别名`moduleA`模块.此时如果模块里有多个导出,就可以使用moduleA.partA来使用对应的导出.(注意和默认导入不一样)
import A, { myA, Something } from './A' // 默认导入和命名导入结合使用
```

### 4.4 AMD/CMD/UMD
AMD(Asynchronous Module Definition),支持异步加载模块,意味着启动更快(更适合浏览器环境)，兼容`require`,`exports`和`define`；CMD(Common Module Definition)，是 Sea.js 所推广的一个模块化方案的输出；UMD，全称 Universal Module Definition，即通用模块规范。既然 CommonJs 和 AMD 风格一样流行，那么需要一个可以统一浏览器端以及非浏览器端的模块化方案的规范。

优点:
1. 支持构造函数
2. 模块可拆分成多个文件
3. 支持构造函数

缺点:
1. 语法更加复杂

目前最流行的AMD实现是:require.js和Dojo

## 5 event loop(重点和难点)
首先说说异步，异步准确的说应该叫浏览器的event loops或者说是javaScript运行环境的event loops，因为ECMAScript中没有event loops，event loops是在[HTML Standard](https://html.spec.whatwg.org/#event-loops)定义的。

js是单线程,也就意味着所有任务需要排队.event loop是js运行时概念,所有任务可以分为两种:同步和异步.同步任务在主线程上执行,所有同步任务形成一个执行栈,前一个执行完才会执行后一个;异步任务不进入主线程,而是进入任务队列中

执行过程:
1. 所有同步任务形成一个执行栈,在主线程上依次执行
2. 异步任务进入任务队列,等待执行.
3. "执行栈"中的所有同步任务执行完毕后，系统就会读取任务队列,使其进入执行栈,开始执行
    1. 如果使用了定时器,那么会先判断是否到了执行时间,如果没到则不管,到了或者过时了才会进入主线程
4. 不断重复上面的步骤,所以才叫event loop

优点:js的优点是永不阻塞(永不阻塞这个说法可能不太准确，因为`alert()`或者同步XHR是会导致阻塞的)，因为它处理I/O通常是通过事件和回调来执行，所以当一个应用正等待一个 IndexedDB 查询返回或者一个异步XHR请求返回时，它仍然可以处理其它事情，比如用户输入。

多个运行时相互通信:一个 web worker 或者一个跨域的iframe都有自己的栈，堆和消息队列。两个不同的运行时只能通过`postMessage()`方法进行通信。如果后者侦听到message事件，则此方法会向其他运行时添加消息。

### 5.1 任务队列(task queue)
先进先出,它是事件的队列,这个事件包括IO事件和用户产生的事件,比如点击,页面滚动.

### 5.2 定时器

## 6 js引擎
SpiderMonkey：https://developer.mozilla.org/zh-CN/docs/Mozilla/Projects/SpiderMonkey

## 7 编译时和运行时
函数编译时按顺序发生的事情：
1. 创建AO对象（Activation Object(执行期上下文)）
2. 变量声明提升：找形参和变量声明，将变量和形参名作为AO属性名，值为undefined
3. 将实参值与形参相统一
4. 函数声明整体提升：在函数中找函数声明，作为属性名，值为函数体

```js
// 例子1 
function test (a, b) {
  console.log("a:", a);
  console.log("b:", b);
  c = 0;
  var c;
  a = 3;
  b = 2;
  console.log("b:", b);
  function b () { }
  function d () { }
  console.log("b:", b);
}
test(1)
// output:
// a: 1
// b: function b () { }
// b: 2
// b: 2
```

# 五 经验
## 1 已整理
1. 不可以用Word或写字板来编写JavaScript或HTML，因为带格式的文本保存后不是纯文本文件，无法被浏览器正常读取
2. 要理解javaScrip,最核心的就是要理解对象和函数两个部分

## 2 即时编译器JIT(Just in time compiling)
为什么需要JIT:
首先要了解编程两种翻译机器语言的方法:解释器或编译器.他们有各自的优点和缺点.
- 解释器:不用经历整个编译步骤,简单说就是一边翻译一边运行.优点是可以快速开始运行代码,缺点是遇到重复代码每次都会去翻译.
- 编译器:一开始先把整个翻译完,然后再运行,重复代码就不用每次都翻译.

而JIT结合了两者的优点,一边翻译一边运行,同时有个监视器(or分析器),记录代码运行的次数和类型,如果某行代码经常运行,就会保存一个编译过的版本,然后下次运行的时候直接用编译后的版本.通常优化编译器会使代码更快，但有时它们可​​能会导致意外的性能问题.



JIT的引入导致js的性能比之前快了10倍,使得js能做更多的东西,b如NodeJS的服务端编程.

### 2.1 V8中的JIT
缺点:
1. JIT 基于运行期分析编译，而 Javascript 是一个没有类型的语言，于是， 大部分时间，JIT 编译器其实是在猜测 Javascript 中的类型

### 2.2 AOT(Ahead of time)

# 六 问题
## 1 已解决
### 1.1  在浏览器直接输出window.a和a，前者的值是undefined，后者是`ReferenceError`
网友的解释是，因为所有的全局变量都是window的属性，所以在window中有`var 一切=undefined`.但是只有在调用window.xxx的时候js引擎才会去声明xxx，如果没有调用window.a而是直接调用就不行了。同理在NodeJS中输出`global.a`和`a`也是一样。

从mdn官网可知，如果xxx没有被定义过且没有初始化过,就会出现`ReferenceError: xxx is not defined`这个错误。而调用`window.xxx`的时候，js会去声明xxx，所以不会抛出这个错误。

### 1.2 数字,字符串之间的比较
纯数字与纯数字比较:以正常的数学运算方式比较

纯数字与数字字符串的比较:先将数字字符串转换为数字,然后再比较.比如"11">10,会将"11"转换为11,即比较的是11>10

纯数字与非数字字符串的比较:返回false

字符串与字符串的比较:先转换为ASCII码,然后一位一位的比较.所以会出现"10">"5"为false的情况

注意:上面的规则适用于浏览器,在NodeJS环境中规则不一样(待补充)

### 1.3 func和func()的区别
前者是函数的引用,表示传递函数;后者是调用函数

## 2 未解决
### 2.1 import引入了用不到的组件,会影响性能吗?(待整理)
默认会不会本人暂时还不清楚.

如果是在Angular中,用`--prod`编译时,会自动去除掉多余的引用,所以不用担心.

### 2.2 js中字符串是像java那样是final的吗?
用无限循环实验了下,本人猜测是内部实现是final的

### 2.n 其他
1. js中alert输出的内容太长了怎么换行？我再dorado中输出的时候就遇到过这个问题。
3. 网友说的js的排序原理不固定,但是基本和`快速排序法`类似.
4. js闭包问题:[https://segmentfault.com/a/1190000003818163](https://segmentfault.com/a/1190000003818163)
5. 网友说:"javascript里最长的正整数长度为21位，再多就会用科学计数法进行计数"
6. 如果是弱类型,那么有什么方式分辨类型呢?还是说分辨具体类型的意义不大了?
7. js字符,数字等的相互转换的最佳实践
    1. `parseInt()`
    2. string类型的2.3转成number是?
10. 笔记

    1. [用JavaScript获取当月第一天和最后一天](http://ourjs.com/detail/593658adf1239006149616c1)
11. js的异常

    最开始没有,后来加入了,原因呢?效果呢?

# 七 未整理
1. this关键字:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this
2. https://developer.mozilla.org/zh-CN/docs/a_re-introduction_to_javascript?redirect=no
3. https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/JavaScript_technologies_overview
4. https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide
5. es模块默认导入是静态的。这个静态是什么意思？
6. js代码格式化的选择：Prettier 和 StandardJS