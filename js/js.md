# JS
[TOC]
## 一 概述
1. js5是没有块级作用域的。函数是JavaScript中唯一拥有自身作用域的结构，也就是说js有函数作用域和一个全局的作用域；js6中有块级作用域
2. js对大小写敏感
3. 大多数浏览器在提及对 JavaScript 的支持情况 时，一般都以 ECMAScript 兼容性和对 DOM 的支持情况为准

### 1 简介
### 2 历史
#### js的历史
js诞生于1995年,由Netscape发明,当时的主要目的是处理以前由服务器端语言(如Perl)负责的一些输入验证操作(在之前是发送到服务端验证,当时网速不好经常等很久才能验证输入是否正确).但现在js已经不仅是验证表单输入了,而是具备了与浏览器窗口及其所有内容**交互的能力**,是一门功能全面的编程语言.
说它简单，是因为学会使用它只需片刻功夫; 而说它复杂，是因为要真正掌握它则需要数年时间。要想全面理解和掌握js,关键在于弄清楚 它的本质、历史和局限性。
(待补充)
1. js的完整实现由三个部分组成
    1. 核心(ECMAScript)
    2. 文档对象模型(DOM) 
    3. 浏览器对象模型(BOM)
2. js的名字

    只是为了蹭java的热度,除此之外可以说跟java没有关系.

js作者的采访:[https://www.youtube.com/watch?v=IPxQ9kEaF8c](https://www.youtube.com/watch?v=IPxQ9kEaF8c)

### 3 常识
#### 3.1 js的参数传递(重点)
java的参数传递是值传递，也就是传递的是原对象的副本，传递后不会对原对象有影响。而js比较特殊，对于基本类型是值传递；对于对象和数组则是共享传递，也就是说如果对形参的属性进行修改，则实参(原对象)的属性真的被修改了，如果是对形参整体赋值，则相当于把实参的地址给了形参然后形参指向了新的对象。例子如下:
```js
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

#### 3.2 深复制和浅复制(shallow copy)
深拷贝和浅拷贝主要是对于对象而言的.
- 浅拷贝:只是复制对象的地址,就是只复制一层对象的属性,不会递归复制所有层级,比如有a的浅拷贝b,修改b.x的时候,a.x也会改变
- 深拷贝:递归复制所有层级,不会出现上面a.x和b.x指向同一对象的情况.缺点是会有性能问题(上面那个只复制地址当然很快),特别是层级很多的时候.

##### 实现深拷贝的几种方式
- `Object.assign(target, ...source)`(es6)

    第一个参数target为拷贝目标，剩余参数...source是拷贝源。此方法可以将...source中的属性复制到target中，同名属性会进行覆盖，缺点是只实现了第一层属性的深拷贝,也就是说对后面的嵌套属性还是浅拷贝.

- `JSON.parse(JSON.stringify(foo))`

    实现了深拷贝,缺点是会破坏原型链,并且无法拷贝属性值为function的属性,如果只是想单纯复制一个嵌套对象,可以使用此方法.

#### 3.2 每行结尾
可用分号也可用回车,推荐分号

#### 3.3 js中实现异步编程的四种方式(待研究)
1. 回调函数
2. 事件监听
3. 发布订阅模式
4. Promise对象

#### 3.4 js的作用域,var let和const,以及变量提升
##### 作用域
js中默认只有全局作用域和函数作用域,没有块级作用域(虽然能通过一些方式实现),这点和java,go等是不一样,比如下面这个例子,在js里会输出10:

```JavaScript
for(var i =0;i<10;i++){
}
console.log(i)
```
还有一个地方需要注意，函数内部声明变量的时候，一定要使用var或let命令。如果不用的话，你实际上声明了一个全局变量,如

```JavaScript
function f1(){
　　n=999;
}
f1();
alert(n); // 999
```




##### var let和const
let和const是es5为了弥补var的不足而设计出来的。
- 使用var声明的变量，其作用域为该语句所在的函数内(没在函数则是全局的)，且存在变量提升；
- 使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升；
- 使用const声明的是常量，必须在声明时赋值,块级作用域,常量不能重新声明,也不能重新赋值。

##### 变量提升(hoisting)
函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部.但是为了代码更易理解,最佳实践是在每个作用域开始前声明这些变量.

注意:只有声明的变量会提升，初始化的不会。

#### 3.5 关于`{ [native code] }`
网上看到的解释是:浏览器内核中的js引擎是C++写的,有些js方法已经用C或C++重写了,所以显示的native code

#### 3.6 a标签中的`href="javascript:;"`和`href="javascript:void(0)"`
这两者在非IE环境下可以认为效果是一样的.

`void(<表达式>)`是js中的关键字,表示计算里面的表达式然后返回固定返回undefined,习惯上用`void(0)`来表示上面都不干,当然也可以写成`void(666)`,`void(2333)`甚至`void("fuc...")`.那么为什么不用`void(undef)`呢,因为undefined在不同环境可能被重新赋值.

那么为什么要写成`href="xxx"`这种形式呢?因为a标签里的href需要指向一个URL,但是我们不想它跳转,就给它一个伪协议(`javascript:xxx;`),表示url的内容通过javascript执行.

既然href里可以写javascript,为什么还要onclick事件呢?暂时我没搞太懂,似乎是因为写在href中有一些兼容性问题.推荐写到`onclick()`中.

#### 3.7 部分最佳实践or技巧
十进制指数:比如1000可以写成`1e3`,10000可以写成`1e4`,以此类推.(`1e0`为1)

#### 3.8 The fps that JavaScript can detect doesn't always relate to number of frames displayed

### 4 文档
### 5 相关网址
1. 廖雪峰的js标准参考教程:[http://javascript.ruanyifeng.com/](http://javascript.ruanyifeng.com/)
2. 廖雪峰的es6入门:[http://es6.ruanyifeng.com/](http://es6.ruanyifeng.com/)
3. 网友自制的:[js中文网](https://www.javascriptcn.com/)

## 二 安装配置
## 三 基础
### 0 待整理
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

### 1 变量
#### 1.1 变量的声明
弱类型:js是弱类型(loosely typed)或者说动态(dynamic)语言,意味着可以不用提前声明(declare)变量的类型,在程序运行时会被自动确定,而且同一个变量可以保存不同类型的数据.如:
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


#### 1.2 变量的类型
最新的ES标准定义了7种类型:6种原始类型(String,Number,Boolean,Null,Undefined,以及ES6的Symbol)和Object.

##### 字符串
单双引号都可以,可以根据需要包含的字符来确定:如果字符含单引号则用双引号包,如果含双引号就用单引号来包,这样不容易引起歧义.否则就要用转义字符`\`,如`var mood = 'don\'t ask';`.但最佳实践是两种引号只选其一.
1. 使用索引可访问字符串中的字符,如`var character=carname[7];`
2. 常用属性
    1. `length`:返回字符串长度,实测中文英文都是算的一个单位的长度
3. 常用方法
    1. `indexOf()`:返回字符在字符串中首次出现的位置,没有则返回-1
    2. `match()`:里面的参数可为string或RegExp,前者用于返回包含指定字符串等信息的数组,没有则返回null;更常用的是后者,用于返回正则匹配的数组,没有则返回null.
    3. `replace()`字符替换
    4. `split(string)`:字符串转数组
    5. `trim()`:去掉空格,es6新增.
    6. `test()`(待补充)

模板字符串(es6):使用反引号包裹,里面的字符默认不会被转义(意味着**会原样输出**),想转义需要在前面加反斜杠`\`;可以包含特定语法`${expression}`的占位符.
- 优点:更加优雅,不再需要考虑反斜杠来处理单引号和双引号,比如

    ```JavaScript
    console.log("Fifteen is " + (a + b) + " and\nnot " + (2 * a + b) + ".");
    ```
    可以写成
    ```JavaScript
    console.log(`Fifteen is ${a + b} and\nnot ${2 * a + b}.`);
    ```

标签函数(es6):标签函数的语法是函数名后面直接带一个模板字符串，并从模板字符串中的插值表达式中获取参数.标签函数的第一个参数是被嵌入表达式分隔的文本的数组。第二个参数开始是嵌入表达式的内容。(感觉只是语法糖,了解就行)

注意:js中直接声明的字符串和字符串对象值是一样的,但是类型是不同的(分别是string和Object)

##### 数字:即number
支持正负数和任意位的小数,如果带小数点则是浮点数.js中所有数字都是64位浮点型.
(待补充:精确度的计算)
1. 判断数值类型的常见方法是正则表达式(待补充)
2. 可用科学计数法来表示,如,

    ```javascript
    var y=123e5;    // 12300000
    var z=123e-5;   // 0.00123
    ```
3. 可用八进制和十六进制来表示,也可转换为八进制或十六进制,如

    ```javascript
    var y = 0377; 
    var z = 0xFF;
    var myNumber=128;
    myNumber.toString(16);   // 返回 80
    myNumber.toString(8);    // 返回 200
    myNumber.toString(2);    // 返回 10000000
    ```
4. 浮点运算并不100%准确,比如,

    ```javascript
    var x = 0.2+0.1; // 输出结果为 0.30000000000000004
    ```
5. `Infinity`表示无穷大的数字,可带正负.非0除以0可产生无穷大,如`2/0`
6. `NaN`表示非数字值,即指示某个值不是数字.可设置number对象为该值.全局函数`isNaN()`可判断一个值是否是NaN. 
7. `new Number(num)`生成数字对象,类似java,如,

    ```javascript
    var x = 123;              
    var y = new Number(123);
    typeof(y) // 返回 Object
    (x === y) // 为 false，因为 x 是一个数字，y 是一个对象
    ```
8. 数字常用方法
##### 布尔值
##### 对象
1. 对象的定义
    1. 关键字创建:`var obj = Object()`
    2. 花括号语法:如`{name:value,name:value}`
2. 对象的使用
    1. 访问元素:`obj.name`

#### 1.3 局部变量
#### 1.4 全局变量
1. 如果您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明

#### 1.5 变量的零值
js声明变量但是没赋初值(包括ts中声明的任意类型变量?),那么变量的值和类型都是undefined

### 2 运算符
1. `+`可以用于数字也可以用于字符串,甚至可以把字符串和数字拼接在一起(弱类型语言,所以允许这样),此时数字被自动转换为字符串

### 3 流程控制
#### 3.1 `if else`:跟java的用法一样,除了一点:
js中的if判断的是变量或表达式的布尔值而不是值,关于js的布尔值可参考[https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)

#### 3.3 比较操作符`==`和`===`
`==`并不是严格相等,而且判断的是值是否相等,而不是布尔值是否相等.js中0、""、''、null、false、undefined、NaN的**布尔值**(可通过`Boolean(xxx)`查看)都是false，其余为true(包括[]、{}、'0'、"0"、Function、Object、Infinity等).注意这儿说的布尔值而不是值.(具体的==比较待补充)

`===`严格相等.

#### 3.4 js的逻辑操作符`||`和`&&`(即短路求值,Short-circuit Evaluation)(难点)
这两个逻辑操作符判断的是js的布尔值而不是值.

短路原则:a && b中,如果a的布尔值为真,则b不会进行计算,即b被"短路";a || b中,如果a的布尔值为假,则b不会进行计算.

赋值原则:对于value=a && b && c...,如果a的布尔值为真则判断b,否则返回a的值,以此类推,直到最后一个值时返回最后一个值;对于value=a || b || c...,如果a的布尔值为假,则判断b,否则返回a,以此类推,直到最后一个值时返回最后一个值.

对于表达式(以及和浏览器控制台每句执行后的undefined的关系)

### 4 js中常用对象
#### 4.1 Array对象
js数组中的元素可以不是同一类型.

三种定义方法:略

其实还有第四种定义方法:关联数组.就是把其中的index由数字换成字符串,比如`arr["name"]="tom"`,非常不推荐使用.

array常用方法:
1. `map()`:返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值,按照原始数组元素顺序依次处理元素,不会改变原数组.语法:`array.map(function(currentValue,index,arr), thisValue)`,微软js手册的例子如下,

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

2. `splice()`

    从数组中添加/删除项目，然后返回被删除的项目.注意这个返回不是`return`,而是赋值.意味着不会中断方法的运行,用值去接收的时候才有用.
    1. `push()`:向数组的末尾添加一个或更多元素，并返回新的长度。在头部添加元素可以用:`arr.splice(0,0,xxx)`
    2. `pop()`:删除并返回数组的最后一个元素,那么删除头部的元素呢?使用`arr.splice(0,1)`.
3. `filter(callback[, thisArg])`:返回过滤后的新数组,不会改变原数组.简单使用如下

    ```javascript
    let arr = [xxx].filter((ele)=>{
        return ele > 10;
    })

    ```

array常用方法的总结:过滤用`filter()`,需要对元素进行处理用`map()`

#### 4.2 ArrayBuffer对象
用于操作二进制数据

注意:在创建之后要判断下,因为可能不会成功.
1. aa
2. bbb

#### 4.3 RegExp对象
字符模式对象,用于正则表达式
1. 两种语法如下,其中pattern表示模式,modifiers(修饰符) 用于指定全局匹配、区分大小写的匹配和多行匹配:

    ```javascript
    var patt=new RegExp(pattern,modifiers);
    //或者更简单的方式
    var patt=/pattern/modifiers;
    ```
    实际使用如下,
    ```javascript
    var re = new RegExp("\\w+");
    var re = /\w+/;
    ```
2. 常用方法
    1. `test()`:搜索字符串指定的值，根据结果返回真或假
    2. `exec()`返回字符串中检索到的指定值,没有则返回null
#### 4.4 Promise对象(es6)
简单说就是一个容器,里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果.
1. Promise对象的两个特点
    1. 对象的状态不受外界影响

        有三种状态：`pending`（进行中）、`fulfilled`（已成功）和`rejected`（已失败）.只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”.
    2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果.

        状态改变只有两种可能:从`pending`变为`fulfilled`和从`pending`变为`rejected`.改变后称为`resolved`（已定型）.这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。(个人疑问:什么情况下事件会错过?)
2. Promise的优缺点
    1. 优点
    
        可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise 对象提供统一的接口，使得控制异步操作更加容易。
    2. 缺点
        1. 无法取消,一旦建立就会立即执行
        2. 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部
        3. 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）
3. 关于stream和Promise的选择

    如果某些事件不断地反复发生，一般来说，使用 Stream 模式是比部署Promise更好的选择
4. 常用方法
    1. `resolve()`:将现有对象转为 Promise 对象
        1. 不带有任何参数使用:立即(在本轮“事件循环”（event loop）的结束时，而不是在下一轮“事件循环”的开始时)返回一个resolved状态的Promise 对象

### 5 函数
函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块(感觉形容得很精炼)

#### 5.1 定义函数(三种方法)
1. 函数声明
    (待补充)
2. 函数表达式
    1. 典型的
    2. 包含函数名称的，函数名称可以在函数内部使用，可以用来递归
3. new Function构造函数

#### 常用方法
1. `match()`方法：调用者必须是string（之前在angular表单中用number类型调用该方法会报错）

### 6 事件
### 7 模块
js中，每个文件是一个模块，文件中定义的所有对象都从属于那个模块。 通过`export`关键字，模块可以把它的某些对象声明为公共的。 其它js模块可以使用`import`语句来访问这些公共对象。

### 8 注释
有三种,前两种跟java一样
1. `//`:用于单行
2. `/**/`:用于多行
3. `<!--`:用于单行,类似html的注释但是不需要用`-->`来收尾,在编辑器里可能会有错误提示,但实际使用没问题,最佳实践应该是不用该注释.

### 9 定时器
参考网友的文章:https://www.cnblogs.com/wangying731/p/5164780.html

## 四 高级
### 1 闭包(closure)(难点)


## 五 经验
### 1 已整理
1. js匿名函数，主要作用是声明同时可以直接执行
2. 不可以用Word或写字板来编写JavaScript或HTML，因为带格式的文本保存后不是纯文本文件，无法被浏览器正常读取

## 六 问题
### 1 已解决
#### 1.1  在浏览器直接输出window.a和a，前者的值是undefined，后者是`ReferenceError`
网友的解释是，因为所有的全局变量都是window的属性，所以在window中有`var 一切=undefined`.但是只有在调用window.xxx的时候js引擎才会去声明xxx，如果没有调用window.a而是直接调用就不行了.

同理在NodeJS中输出`global.a`和`a`也是一样.

#### 1.2 数字,字符串之间的比较
纯数字与纯数字比较:以正常的数学运算方式比较

纯数字与数字字符串的比较:先将数字字符串转换为数字,然后再比较.比如"11">10,会将"11"转换为11,即比较的是11>10

纯数字与非数字字符串的比较:返回false

字符串与字符串的比较:先转换为ASCII码,然后一位一位的比较.所以会出现"10">"5"为false的情况

注意:上面的规则适用于浏览器,在NodeJS环境中规则不一样(待补充)

### 2 未解决
#### 2.1 import引入了用不到的组件,会影响性能吗?(待整理)
默认会不会本人暂时还不清楚.

如果是在Angular中,用`--prod`编译时,会自动去除掉多余的引用,所以不用担心.

#### 2.2 js中字符串是像java那样是final的吗?
用无限循环实验了下,本人猜测是内部实现是final的

#### 2.n 其他
1. js中alert输出的内容太长了怎么换行？我再dorado中输出的时候就遇到过这个问题。
2. js null和undefined的区别，两个都占用内存空间吗，用什么方法去验证呢？
3. 网友说的js的排序原理不固定,但是基本和`快速排序法`类似.
4. js闭包问题:[https://segmentfault.com/a/1190000003818163](https://segmentfault.com/a/1190000003818163)
5. 网友说:"javascript里最长的正整数长度为21位，再多就会用科学计数法进行计数"
6. 如果是弱类型,那么有什么方式分辨类型呢?还是说分辨具体类型的意义不大了?
7. js字符,数字等的相互转换的最佳实践
    1. `parseInt()`
    2. string类型的2.3转成number是?
8. const和let
9. 在字符串中使用变量的方法
10. 笔记

    1. [用JavaScript获取当月第一天和最后一天](http://ourjs.com/detail/593658adf1239006149616c1)
11. js的异常

    最开始没有,后来加入了,原因呢?效果呢?
12. 网友: js 引入了 async 和 await ，层层回调的写法，马上就要成为过去式了。

## 七 未整理
1. js模块化
    1. [https://www.zhihu.com/question/34460535](https://www.zhihu.com/question/34460535)
    2. 解决方案
        1. webpack
        2. CommonJS
        3. ES6
        4. AMD / CMD