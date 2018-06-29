# JS
[TOC]

# 一 概述

## 1 简介
js为什么是单线程:与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？所以，为了避免复杂性，从一诞生，JavaScript就是单线程，这已经成了这门语言的核心特征，将来也不会改变。

### 1.1 未整理
1. js5是没有块级作用域的。函数是JavaScript中唯一拥有自身作用域的结构，也就是说js有函数作用域和一个全局的作用域；js6中有块级作用域
2. js对大小写敏感
3. 大多数浏览器在提及对 JavaScript 的支持情况 时，一般都以 ECMAScript 兼容性和对 DOM 的支持情况为准

### 1.4 缺点
1. JavaScript支持异步，但本质是单线程环境,即使采用Ajax也只能局部更新，只是“看上去有了响应，但总体时间还是不变，甚至会变慢”.

## 2 历史
### js的历史
js诞生于1995年,由Netscape发明,当时的主要目的是处理以前由服务器端语言(如Perl)负责的一些输入验证操作(在之前是发送到服务端验证,当时网速不好经常等很久才能验证输入是否正确).但现在js已经不仅是验证表单输入了,而是具备了与浏览器窗口及其所有内容**交互的能力**,是一门功能全面的编程语言.
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

#### 3.2.1 实现深拷贝的几种方式
- `Object.assign(target, ...source)`(es6)

    第一个参数target为拷贝目标，剩余参数...source是拷贝源。此方法可以将...source中的属性复制到target中,然后返回target.同名属性会进行覆盖，缺点是只实现了第一层属性的深拷贝,也就是说对后面的嵌套属性还是浅拷贝.

- `JSON.parse(JSON.stringify(foo))`

    实现了深拷贝,缺点是会破坏原型链,并且无法拷贝属性值为function的属性,如果只是想单纯复制一个嵌套对象,可以使用此方法.

### 3.2 每行结尾
可用分号也可用回车,推荐分号

### 3.3 js中实现异步编程的四种方式(待研究)
1. 回调函数
2. 事件监听
3. 发布订阅模式
4. Promise对象

### 3.4 js的作用域,var let和const,以及变量提升
#### 3.4.1 作用域
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




#### 3.4.2 var let和const
let和const是es5为了弥补var的不足而设计出来的。
- 使用var声明的变量，其作用域为该语句所在的函数内(没在函数则是全局的)，且存在变量提升；
- 使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升；
- 使用const声明的是常量，必须在声明时赋值,块级作用域,常量不能重新声明,也不能重新赋值。

#### 3.4.3 变量提升(hoisting)
函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部.但是为了代码更易理解,最佳实践是在每个作用域开始前声明这些变量.

注意:只有声明的变量会提升，初始化的不会。

### 3.5 关于`{ [native code] }`
网上看到的解释是:浏览器内核中的js引擎是C++写的,有些js方法已经用C或C++重写了,所以显示的native code

### 3.6 a标签中的`href="javascript:;"`和`href="javascript:void(0)"`
这两者在非IE环境下可以认为效果是一样的.

`void(<表达式>)`是js中的关键字,表示计算里面的表达式然后返回固定返回undefined,习惯上用`void(0)`来表示上面都不干,当然也可以写成`void(666)`,`void(2333)`甚至`void("fuc...")`.那么为什么不用`void(undef)`呢,因为undefined在不同环境可能被重新赋值.

那么为什么要写成`href="xxx"`这种形式呢?因为a标签里的href需要指向一个URL,但是我们不想它跳转,就给它一个伪协议(`javascript:xxx;`),表示url的内容通过javascript执行.

既然href里可以写javascript,为什么还要onclick事件呢?暂时我没搞太懂,似乎是因为写在href中有一些兼容性问题.推荐写到`onclick()`中.

### 3.7 部分最佳实践or技巧
十进制指数:比如1000可以写成`1e3`,10000可以写成`1e4`,以此类推.(`1e0`为1)

### 3.8 The fps that JavaScript can detect doesn't always relate to number of frames displayed
(待验证)

### 3.9 Spread Operator和rest操作符
rest操作符:主要用于获得传递给函数的参数列表.如,

```javascript
function countArguments(...args) {  
　　return args.length;
}
countArguments('welcome', 'to', 'Earth'); // 3  
```

有两个作用:
1. 语法糖
2. 表示箭头函数中的arguments.具体参考:https://segmentfault.com/q/1010000008720963?_ea=1724154

spread操作符:主要用于数组构造和解构，在调用时将数组填入函数参数.如

```javascript
//数组构造
const odd = [1, 3, 5 ];
const nums = [2, ...odd, 4 , 6]; // [2,1,3,5,4,6]
//解构数组
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

### 3.10 js的宿主对象,本地对象和内置对象
#### 3.10.1 宿主,宿主环境和宿主对象
在浏览器中:宿主和宿主环境就是浏览器.浏览器通过

## 4 文档
## 5 相关网址
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

## 1 数据类型
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
最新的ES标准定义了7种类型:6种原始类型(String,Number,Boolean,Null,Undefined,以及ES6的Symbol)和Objects.

Objects包含:
1. 标准对象("Normal" objects)
2. 函数(functions)
3. 有续集(Indexed collections):Arrays和typed Arrays
4. 键集(Keyed collections):Maps, Sets, WeakMaps, WeakSets
5. 结构化数据(Structured data):JSON
6. java标准库的內建对象,如日期(Dates),字符串(String),Math等

判断数据的类型用`typeof xxx`or`typeof (xxx)`,返回字符串,内容是xxx的类型,一般有一下几种类型:
1. 对这些基本类型就是对应的类型:string,number,boolean,undefined,symbol
2. 对于null,是object.意味着`typeof null === "object"`,注意这其实是一个错误,但是一直没有修复.参考:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof
3. 对于函数是function
4. 对于宿主对象（由JS环境提供）,是Implementation-dependent
5. 对于任何其他对象是object

注意:`typeof Number(1)`是number,但是`typeof new Number(1)`是object,这两种写法都不推荐使用,String,Boolean也一样.

#### 1.2.1 字符串
单双引号都可以,可以根据需要包含的字符来确定:如果字符含单引号则用双引号包,如果含双引号就用单引号来包,这样不容易引起歧义.否则就要用转义字符`\`,如`var mood = 'don\'t ask';`.但最佳实践是两种引号只选其一.

使用索引可访问字符串中的字符,如`var character=carname[7];`

常用属性:
1. `length`:返回字符串长度,实测中文英文都是算的一个单位的长度

常用方法:
1. `indexOf()`:返回字符在字符串中首次出现的位置,没有则返回-1
2. `match()`:里面的参数可为string或RegExp,前者用于返回包含指定字符串等信息的数组,没有则返回null;更常用的是后者,用于返回正则匹配的数组,没有则返回null.
3. `replace()`字符替换
4. `split(string)`:字符串转数组
5. `trim()`:去掉首尾空格,es6新增.
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

注意:
1. js中直接声明的字符串和字符串对象值是一样的,但是类型是不同的(分别是string和Object)
2. 打印模板字符串中的Object对象默认会输出成形如`[object Object]`,可以用`JSON.stringify(obj)`打印具体内容.

js去除字符串中空格的几种方法(待补充):
1. `replace(/\s/g, "")`

js判断字符串是否全部为数字的几种方法(待补充):
1. `isNaN(Number(xxx))`

#### 1.2.2 数字number
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
#### 1.2.3 布尔值
#### 1.2.4 对象
标准对象的定义:
1. 关键字创建:`var obj = Object()`
2. 花括号语法:如`{name:value,name:value}`

对象的使用:
1. 访问元素:`obj.name`

### 1.3 局部变量
### 1.4 全局变量
1. 如果您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明

### 1.5 变量的零值
js声明变量但是没赋初值(包括ts中声明的任意类型变量?),那么变量的值和类型都是undefined

## 2 运算符,比较符,逻辑操作符
### 2.1 运算符+
可以用于数字也可以用于字符串,甚至可以把字符串和数字拼接在一起(弱类型语言,所以允许这样),此时数字被自动转换为字符串

### 2.2 delete
delete 操作符用于删除对象的某个属性.只能删除自身的属性(区别于原型链的属性);var, let以及const创建的不可设置的属性不能被delete操作删除;

一般情况都会返回true(属性不存在也返回true),除非属性是自己不可设置的值,比如`Math.PI`

删除数组元素:删除的元素不属于该数组,数组长度不受影响.两个例子如下
```JavaScript
var trees = ["redwood","bay","cedar","oak","maple"];
delete trees[3];
if (3 in trees) {
   // 这里不会执行
}
console.log(trees) //["redwood","bay","cedar",,"maple"]
console.log(trees.length)//5
```

```JavaScript
var trees = ["redwood","bay","cedar","oak","maple"];
trees[3] = undefined;
if (3 in trees) {
   // 这里会执行
}
console.log(trees) //["redwood","bay","cedar",,"maple"]
console.log(trees.length)//5
```


### 2.3 比较操作符`==`和`===`
`==`并不是严格相等,而且判断的是值是否相等,而不是布尔值是否相等.js中0、""、''、null、false、undefined、NaN的**布尔值**(可通过`Boolean(xxx)`查看)都是false，其余为true(包括[]、{}、'0'、"0"、Function、Object、Infinity等).注意这儿说的布尔值而不是值.(具体的==比较待补充)

`===`严格相等.

### 2.4 js的逻辑操作符`||`和`&&`(即短路求值,Short-circuit Evaluation)(难点)
这两个逻辑操作符判断的是js的布尔值而不是值.

短路原则:a && b中,如果a的布尔值为真,则b不会进行计算,即b被"短路";a || b中,如果a的布尔值为假,则b不会进行计算.

赋值原则:对于value=a && b && c...,如果a的布尔值为真则判断b,否则返回a的值,以此类推,直到最后一个值时返回最后一个值;对于value=a || b || c...,如果a的布尔值为假,则判断b,否则返回a,以此类推,直到最后一个值时返回最后一个值.

对于表达式(以及和浏览器控制台每句执行后的undefined的关系)

## 3 流程控制和循环
### 3.1 if else
跟java的用法一样,除了一点:js中的if判断的是变量或表达式的布尔值而不是值,关于js的布尔值可参考[https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy)

### 3.2 switch case default

### 3.3 while和do ... while

### 3.4 for ... in
可以遍历任何数据类型,但最适合的是遍历对象的属性,默认以字符串的形式遍历出对象的所有属性.

如何遍历Array对象,循环的是数组的索引,而且也是字符串类型,不是数值.

关于遍历的顺序:遍历顺序依赖于环境,所以该方法并不能保证顺序.但是约定成俗的顺序应该是:先遍历属性名是数值的(从0升序),然后属性名不是数值的则是按定义时的顺序遍历.

属性和方法:
1. `object.hasOwnProperty() boolean`:判断是否是对象自身的属性,如果是继承的属性则返回false.

注意:
1. 该方法遍历时最好不要动态修改属性,因为不能保证后面的遍历是否能访问到.

### 3.5 forEach((ele,index,array)=>{...})
对于array的遍历,一般情况下`forEach()`比`for ... of`更好用.

## 4 js中常用对象
### 4.1 Array对象
优点:存储的对象能动态增多和减少，并且可以存储任何类型的JavaScript值

定义方法:三种普通创建方法,以及通过函数(`split`,`match`等)创建
1. `new Array(length)`
    
    创建指定长度的空数组
    1. 注意是空数组,而不是值为undefined的数组,虽然打印其中的值时为undefined.
    2. 如果想创建值为单个数字的数组呢?可用js6新增的`Array.of(element...)`,element可以是任意类型
2. `new Array(element0, element1, ..., elementN)`
3. `[element0, element1, ..., elementN]`

还有一种额外的但不推荐的定义方法:关联数组.就是把其中的index由数字换成字符串,比如`arr["name"]="tom"`.(但是非常不推荐使用)

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

    从原数组中添加/删除项目，然后返回被删除的项目,该方法会改变原数组.注意这个返回不是`return`,而是赋值.意味着不会中断方法的运行,用值去接收的时候才有用.
    1. `push()`:向数组的末尾添加一个或更多元素，并返回新的长度。在头部添加元素可以用:`arr.splice(0,0,xxx)`
    2. `pop()`:删除并返回数组的最后一个元素,那么删除头部的元素呢?使用`arr.splice(0,1)`.

3. `filter(callback[, thisArg])`:返回过滤后的新数组,不会改变原数组.简单使用如下

    ```javascript
    let arr = [xxx].filter((ele)=>{
        return ele > 10;
    })

    ```

4. `find()`:返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined
5. `array.slice(start?,end?)`:从数组中切割出新数组,该方法不会改变原数组.如果不带参数,则是整个复制.start和index一样从0开始算,如果是复数,则表示倒数,-1表示倒数第一个元素,以此类推.

array常用方法的总结:过滤用`filter()`,需要对元素进行处理用`map()`

### 4.3 RegExp对象
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

## 5 函数
函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块(感觉形容得很精炼)

### 5.1 定义函数(三种方法)
1. 函数声明
    (待补充)
2. 函数表达式
    1. 典型的
    2. 包含函数名称的，函数名称可以在函数内部使用，可以用来递归
3. new Function构造函数

### 常用方法
1. `match()`方法：调用者必须是string（之前在angular表单中用number类型调用该方法会报错）

## 6 事件
## 7 模块
js中，每个文件是一个模块，文件中定义的所有对象都从属于那个模块。 通过`export`关键字，模块可以把它的某些对象声明为公共的。 其它js模块可以使用`import`语句来访问这些公共对象。

## 8 注释
有三种,前两种跟java一样
1. `//`:用于单行
2. `/**/`:用于多行
3. `<!--`:用于单行,类似html的注释但是不需要用`-->`来收尾,在编辑器里可能会有错误提示,但实际使用没问题,最佳实践应该是不用该注释.

## 9 定时器(难点)
参考网友的文章:https://www.cnblogs.com/wangying731/p/5164780.html

详见DOM笔记的window部分.

# 四 高级
## 1 闭包(closure)(难点)

## 2 按位操作符(Bitwise Operator)
### 2.2 双位操作符(Double Bitwise NOT)
可以用来替代`Math.floor()`,快得多.例如
```javascript
Math.floor(4.9) === 4  //true
~~4.9 === 4  //true
```

## 3 ArrayBuffers,SharedArrayBuffers,ArrayBuffer视图
### 3.1 ArrayBuffers
为什么我们需要这两个:在js中创建一个变量的时候,引擎会去猜测变量的类型以及如何在内存中表示,会导致分配的内存是实际需要的2~8倍,可能会导致大量的内存浪费.ArrayBuffer用来表示通用的、固定长度的原始二进制数据缓冲区(基本上就像原始内存一样,它模仿了C语言中的直接内存访问),是值类型,不是引用类型.

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

#### 类型数组视图(Typed array views)
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

#### 数据视图(DataView)
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
首先要弄清楚为什么js需要模块化:开发中,我们需要引入其他软件,新旧代码之间就会存在依赖关系,由于这些软件需要一起工作,因此它们之间不存在冲突是非常重要的.封装可以防止模块之间相互冲突,这也是C语言库中元素通常带有前缀的原因之一.
随着js越来越复杂,依赖管理可能会变得麻烦,重构也受到影响:如何维护加载链的正确顺序?

主流的几个方案:
1. webpack
2. CommonJS
3. ES6
4. AMD / CMD

### 4.1 webpack

### 4.2 CommonJS
CommonJS是用于开发服务器端的JS项目.同步加载模块.NodeJS采用的CommonJS规范.

优点:简单,支持循环依赖

缺点:
1. 没有模块的构造函数
2. 模块是单一文件.

引入是`require('module-name')`,导出是`exports`


### 4.3 ES2015
import和export指令的静态特性允许静态分析器在不运行代码的情况下构建完整的依赖关系树。

优点:
1. 支持同步和异步加载。
2. 语法简单。
3. 支持静态分析工具。

#### 导入import
引入模块的几种写法,其中`module-name`一般是模块js文件的路径,一般不包含`.js`扩展名,用单引号或双引号包裹:
1. 导入整个模块:形如`import {export} from "module-name"`,也可以使用别名`import { export as alias } from "module-name"`
2. 导入里面的多个子模块:形如`import {foo, bar} from "module-name"`:也可以使用别名`import { export1 , export2 as alias2 , ["module-name"] } from "module-name"`
3. 导入成默认值:形如`import myDefault from "module-name"`:导入单个或多个时导出时,需要知道导出的名字,很不方便,所以js允许设置一个默认的导出,形如`export default xxx`,这样导入的时候就可以随意取一个名字,而且不用大括号包裹来表示默认的导出.
4. 仅为副作用而导入一个模块:`import "module-name"`
5. 导入某模块的所有导出:`import * as xxx from "module-name"`:可以用别名`xxx`来使用模块.此时如果模块里有多个导出,就可以使用xxx.yyy来使用对应的导出.

#### 导出export
1. 命名导出:形如`export { myFunction }`(存在名为myFunction的方法)或者直接写在方法方法上`export function diag(xxx) {...}`,还可以导出成常量`export const foo = Math.sqrt(2)`

    命名导出对导出多个值很有用。在导入时,必须使用相同名称。
2. 默认导出:导出函数`export default function() {}`,导出类`export default class {}`

    对于默认导出,在导入的时候可以使用任意名字接收,如`import abc from 'module-name'`


### 4.4 AMD / CMD
支持异步加载模块,意味着启动更快.兼容`require`,`exports`和`define`

优点:
1. 支持构造函数
2. 模块可拆分成多个文件
3. 支持构造函数

缺点:
1. 语法更加复杂

目前最流行的AMD实现是:require.js和Dojo

## 5 event loop(重点和难点)
js是单线程,也就意味着所有任务需要排队.event loop是js运行时概念,所有任务可以分为两种:同步和异步.同步任务在主线程上执行,所有同步任务形成一个执行栈,前一个执行完才会执行后一个;异步任务不进入主线程,而是进入任务队列中

执行过程:
1. 所有同步任务形成一个执行栈,在主线程上依次执行
2. 异步任务进入任务队列,等待执行.
3. "执行栈"中的所有同步任务执行完毕后，系统就会读取任务队列,使其进入执行栈,开始执行
    1. 如果使用了定时器,那么会先判断是否到了执行时间,如果没到则不管,到了或者过时了才会进入主线程
4. 不断重复上面的步骤,所以才叫event loop

优点:永不阻塞.例外是alert或者同步 XHR.

多个运行时相互通信:一个 web worker 或者一个跨域的iframe都有自己的栈，堆和消息队列。两个不同的运行时只能通过`postMessage()`方法进行通信。如果后者侦听到message事件，则此方法会向其他运行时添加消息。

### 5.1 任务队列(task queue)
先进先出,它是事件的队列,这个事件包括IO事件和用户产生的事件,比如点击,页面滚动.

### 5.2 定时器


# 五 经验
## 1 已整理
1. js匿名函数，主要作用是声明同时可以直接执行
2. 不可以用Word或写字板来编写JavaScript或HTML，因为带格式的文本保存后不是纯文本文件，无法被浏览器正常读取

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
网友的解释是，因为所有的全局变量都是window的属性，所以在window中有`var 一切=undefined`.但是只有在调用window.xxx的时候js引擎才会去声明xxx，如果没有调用window.a而是直接调用就不行了.

同理在NodeJS中输出`global.a`和`a`也是一样.

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

# 七 未整理
