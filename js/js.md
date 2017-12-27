# JS
[TOC]
## 一. 概述
1. js5是没有块级作用域的。函数是JavaScript中唯一拥有自身作用域的结构，也就是说js有函数作用域和一个全局的作用域；js6中有块级作用域
2. js对大小写敏感
3. 大多数浏览器在提及对 JavaScript 的支持情况 时，一般都以 ECMAScript 兼容性和对 DOM 的支持情况为准
### 1. js的一些常识
#### 1.1 js的历史
js诞生于1995年,当时的主要目的是处理以前由服务器端语言(如Perl)负责的一些输入验证操作(在之前是发送到服务端验证,当时网速不好经常等很久才能验证输入是否正确).但现在js已经不仅是验证表单输入了,而是具备了与浏览器窗口及其所有内容**交互的能力**,是一门功能全面的编程语言.
说它简单，是因为学会使用它只需片刻功夫; 而说它复杂，是因为要真正掌握它则需要数年时间。要想全面理解和掌握js,关键在于弄清楚 它的本质、历史和局限性。
(待补充)
1. js的完整实现由三个部分组成
    1. 核心(ECMAScript)
    2. 文档对象模型(DOM) 
    3. 浏览器对象模型(BOM)
2. js的名字

    只是为了蹭java的热度,除此之外可以说跟java没有关系.
#### 1.2 js的参数传递
java的参数传递是值传递，也就是传递的是原对象的副本，传递后不会对原对象有影响。而js比较特殊，对于基本类型是值传递；对于对象则是共享传递，也就是说如果对形参的属性进行修改，则实参(原对象)的属性真的被修改了，如果是对形参整体赋值，则相当于把实参的地址给了形参然后形参指向了新的对象。例子如下:
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
#### 1.3 每行结尾
可用分号也可用回车,推荐分号
## 二. 安装配置

## 三. 基础
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
1. 关于是否事先声明:js允许直接对变量赋值而无需事先声明(declare),这点与很多编程语言不同.推荐还是提前声明变量.
2. 关于命令:js变量名允许包含字母、数字、美元符号和下划线,但不能以数字开头.跟java一样
1. 声明单个:`var age`
2. 声明多个:`var age,mood`
3. 声明并赋值:`var age=1,mood="sad"`
#### 1.2 变量的类型
有些语言要求声明变量的同时声明变量的类型,这种做法称为*类型声明*(typing),所对应的语言称为*强类型*(strongly typed)语言,但js不需要类型声明,所以是弱类型语言.这意味着可任意改变数据的类型.如
```javascript
var age=3;
age="hello";
```
1. 字符串

    单双引号都可以,可以根据需要包含的字符来确定:如果字符含单引号则用双引号包,如果含双引号就用单引号来包,这样不容易引起歧义.否则就要用转义字符`\`,如`var mood = 'don\'t ask';`.但最佳实践是两种引号只选其一.
    1. 使用索引可访问字符串中的字符,如`var character=carname[7];`
    2. 常用属性
        1. `length`:返回字符串长度
    3. 常用方法
        1. `indexOf()`:返回字符在字符串中首次出现的位置,没有则返回-1
        2. `match()`:里面的参数可为string或RegExp,前者用于返回包含指定字符串等信息的数组,没有则返回null;更常用的是后者,用于返回正则匹配的数组,没有则返回null.
        3. `replace()`字符替换
        4. `split(string)`:字符串转数组
        5. `trim()`:去掉空格,es6新增.
    4. 模板字符串(es6)
2. 数字:即number对象

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
3. 布尔值
4. 对象
    1. 对象的定义
        1. 关键字创建:`var obj = Object()`
        2. 花括号语法:如`{name:value,name:value}`
    2. 对象的使用
        1. 访问元素:`obj.name`
#### 1.4 局部变量
#### 1.5 全局变量
### 2 运算符
1. `+`可以用于数字也可以用于字符串,甚至可以把字符串和数字拼接在一起(弱类型语言,所以允许这样),此时数字被自动转换为字符串
### 3 流程控制
1. `if else`:跟java的用法一样,除了一点:
    js中的if判断的是变量或表达式的布尔值而不是值
2. 比较操作符`==`和`===`
    1. `==`并不是严格相等,而且判断的是值是否相等,而不是布尔值是否相等.js中0、""、''、null、false、undefined、NaN的**布尔值**(可通过`Boolean(xxx)`查看)都是false，其余为true(包括[]、{}、'0'、"0"、Function、Object、Infinity等).注意这儿说的布尔值而不是值.(具体的==比较待补充)
    2. `===`严格相等.
3. js的逻辑操作符`||`和`&&`(难点)
    1. 短路原则:a && b中,如果a的布尔值为真,则b不会进行计算,即b被"短路";a || b中,如果a的布尔值为假,则b不会进行计算.
    2. 赋值原则:对于value=a && b && c...,如果a的布尔值为真则判断b,否则返回a的值,以此类推,直到最后一个值时返回最后一个值;对于value=a || b || c...,如果a的布尔值为假,则判断b,否则返回a,以此类推,直到最后一个值时返回最后一个值.
    3. 对于表达式(以及和浏览器控制台每句执行后的undefined的关系)

### 4 js中常用对象
#### 4.1 window
所有浏览器都支持 window对象。它表示浏览器窗口。
所有js全局对象、函数以及变量都是window对象的成员。甚至HTML DOM的document 也是window对象的属性之一
1. 关于Window和window

    官网的说法是windowh和self是对Window本身的引用,但知乎网友的回答应该准确:Window是接口，window是实例而且是单实例，全局变量是window的属性。
1. 关于window尺寸

    浏览器窗口的尺寸不包括工具栏和滚动条.有三种方法可以获取:
    1. 对于IE9和其他大部分browser:
        - window.innerHeight - 浏览器窗口的内部高度
        - window.innerWidth - 浏览器窗口的内部宽度
    2. 对于Internet Explorer 8、7、6、5：
        - document.documentElement.clientHeight
        - document.documentElement.clientWidth
    3. 其他:
        - document.body.clientHeight
        - document.body.clientWidth
    4. 所有最佳实践如下,
        ```JavaScript
        var w=window.innerWidth
        || document.documentElement.clientWidth
        || document.body.clientWidth;
        ```
3. 常用属性
    1. console

        用于向浏览器控制台输出,它的方法应该主要用于调试, 而不是显示给用户.打印单个对象时,直接输出对象的字符形式;打印多个对象时类似c的printf风格.也接受字符串拼接.google develop tools中可以打印样式甚至图片.常用方法如下,
        1. log()
        2. info()
        3. warn()
        4. error()
        5. time()和timeEnd():一般都是两个一起使用,前者启动计时器,后者以毫秒为单位输出计时器经过的时间.
        想为打印的输出增加样式,使用`console.log("%c需要输出的信息 ", "css 代码")`,如
        ```javascript
        console.log("%cMy stylish message", "color: red; font-style: italic");
        ```
2. 常用方法
    1. window.open() - 打开新窗口
    2. window.close() - 关闭当前窗口
    3. window.moveTo() - 移动当前窗口
    4. window.resizeTo() - 调整当前窗口的尺寸

3. 关于window.location和window.open：前者可以当字符串使用，
#### 4.2 Array对象
1. 三种定义方法:略

    1. js数组中的元素可以不是同一类型.
    2. 其实还有第四种定义方法:关联数组.就是把其中的index由数字换成字符串,比如`arr["name"]="tom"`,非常不推荐使用.
2. 

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
### 5 函数
函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块(感觉形容得很精炼)
1. 定义函数(三种方法)
    1. 函数声明
    2. 函数表达式
        1. 典型的
        2. 包含函数名称的，函数名称可以在函数内部使用，可以用来递归
    3. new Function构造函数
2. 
5. match()方法：调用者必须是string（之前在angular表单中用number类型调用该方法会报错）
### 6 事件
### 7 注释
有三种,前两种跟java一样
1. `//`:用于单行
2. `/**/`:用于多行
3. `<!--`:用于单行,类似html的注释但是不需要用`-->`来收尾,在编辑器里可能会有错误提示,但实际使用没问题,最佳实践应该是不用该注释.
## 四. 使用
## 五. 经验
1. js匿名函数，主要作用是声明同时可以直接执行
2. 关于直接输出window.a和a，前者的值是undefined，后者是`ReferenceErroe`，网友的解释是，因为所有的全局变量都是window的属性，所以在window中有
```
var 一切=undefined；
```
但是只有在调用window.xxx的时候js引擎才会去声明xxx，如果没有调用window.a而是直接调用就不行了
## 五. 问题
1. js中alert输出的内容太长了怎么换行？我再dorado中输出的时候就遇到过这个问题。
2. js null和undefined的区别，两个都占用内存空间吗，用什么方法去验证呢？
