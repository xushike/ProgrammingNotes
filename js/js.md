# JS
[TOC]
## 一. 概述
1. js5是没有块级作用域的。函数是JavaScript中唯一拥有自身作用域的结构，也就是说js有函数作用域和一个全局的作用域；js6中有块级作用域
2. js对大小写敏感
3. 大多数浏览器在提及对 JavaScript 的支持情况 时，一般都以 ECMAScript 兼容性和对 DOM 的支持情况为准
### 1. js的一些常识
#### 1.1 js的历史
js诞生于1995年,当时的主要目的是处理以前由服务器端语言(如Perl)负责的一些输入验证操作(在之前是发送到服务端验证).说它简单，是因为学会使用它只需片刻功夫; 而说它复杂，是因为要真正掌握它则需要数年时间。要想全面理解和掌握 JavaScript，关键在于弄清楚 它的本质、历史和局限性。
(待补充)
1. js的完整实现由三个部分组成
    1. 核心(ECMAScript)
    2. 文档对象模型(DOM) 
    3. 浏览器对象模型(BOM)
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
#### 1.3 关于html的脚本加载
HTML 应用程序，通常建议把所有的脚本都放置在 `<body> `元素的最底部。这会提高网页加载速度，因为 HTML 加载不受制于脚本加载。而对于库(比如`xxx.js`)，只要放在对应的脚本前面就行了(因为某些脚本的调用只能在库加载之后进行？)。
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
### 2 变量
#### 2.1 局部变量
#### 2.2 全局变量
### 3 函数
函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块(感觉形容得很精炼)
1. 定义函数(三种方法)
    1. 函数声明
    2. 函数表达式
        1. 典型的
        2. 包含函数名称的，函数名称可以在函数内部使用，可以用来递归
    3. new Function构造函数
2. 
5. match()方法：调用者必须是string（之前在angular表单中用number类型调用该方法会报错）
### 4 对象
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
#### 4.2 Array
### 5 事件

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
