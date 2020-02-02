# js6
# 一 概述
## 1 简介
该笔记主要记录es6新特性,以后可能会和js笔记合并
## 2 历史
## 3 常识
### 3.1 ECMAScript 2015(ES2015),ES6和JS6的区别
一般来讲,可以把这三个看成一个东西.

2015年6月17日，ECMA国际组织发布了 ECMAScript 的第六版，该版本正式名称为 ECMAScript 2015，但通常被称为 ECMAScript 6 或者 ES6

## 4 文档
## 5 网站
1. 阮一峰es6:[http://es6.ruanyifeng.com/](http://es6.ruanyifeng.com/)
# 三 基础
## 1 对象
### 1.1 不定参数和展开运算符
不定参数:语法是在参数前加三个点,如
```javascript
var [head, ...tail] = [1, 2, 3, 4];
console.log(tail);
// [2, 3, 4]
```

### 1.2 对象解构(Object destructuring)
ES6的解构赋值给js的语法带来了更多的现代化。它在减少了代码量的同时，增加了代码的可读性和表现力。(题外话:代码和python越来越像了.)

#### 解构赋值(Destructuring Assignment)
例子如`const { store, form, loading, errors, entity:contact } = this.props`,其中`entity`是`this.props`的属性,`contact`是新的属性名,访问的时候就可以通过新的属性名访问了.

注意:解构赋值类似Object.assign(),只是第一层深复制.(待验证)

参考:[https://segmentfault.com/a/1190000002920859](https://segmentfault.com/a/1190000002920859)

参考:[http://www.infoq.com/cn/articles/es6-in-depth-destructuring/](http://www.infoq.com/cn/articles/es6-in-depth-destructuring/)

## 2 流程控制和迭代器
### 2.2 迭代器
#### for ... of
用于遍历数组和集合等,不能用遍历普通对象

## 3 函数
### 3.1 箭头函数
我的理解是:直接声明function,则function中的this指的外层对象;而用箭头函数则this指的全局对象(如果是在组件中,则是指向组件)

匿名函数和箭头函数的`this`:两者绑定不同的this对象。匿名函数（和所有传统的Javascript函数）创建他们独有的this对象，而箭头函数则继承绑定他所在函数的this对象。这意味着在使用箭头函数时，原函数中可用的变量和常量在事件处理器中同样可用。

### 3.2 更简短定义方法的语法
对象中定义方法基本写法如下:
```JavaScript
var obj = {
  foo: function() {
    /* code */
  },
  bar: function() {
    /* code */
  }
};
```

更简短定义函数的语法如下:
```JavaScript
var obj = {
  foo() {
    /* code */
  },
  bar() {
    /* code */
  }
};
```

### 3.3 setter和getter
为什么需要setter和getter:虽然可以直接操作对象的属性,但有时我们还需要一些额外操作而不是直接获取或修改,此时可以用这两个方法.

个人感觉这两个定义上像方法,但使用时像属性.

#### 3.3.1 getter
基本使用如下
```JavaScript
var obj = {
  log: ['example','test'],
  get latest() {
    if (this.log.length == 0) return undefined;
    return this.log[this.log.length - 1];
  }
}
```

注意:getter是lazy getter,每次调用的时候才回去计算值.

#### 3.3.2 setter
基本使用如
```JavaScript
var language = {
  set current(name) {
    this.log.push(name);
  },
  log: []
}
language.current = 'EN';
language.current = 'FA';
console.log(language.log); 
// Array ["EN", "FA"]
```

## 4 js6常用对象
### 4.1 Promise对象
Promise 对象是 JavaScript 的异步操作解决方案，为异步操作提供统一接口。它起到代理作用（proxy），充当异步操作与回调函数之间的中介，使得异步操作具备同步操作的接口。Promise 可以让异步操作写起来，就像在写同步操作的流程，而不必一层层地嵌套回调函数。

就是一个容器,里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果.(本人的理解是,Promise对象只是提供了代理,实际接收的还是返回的值,而感觉不出Promise的存在)

大多数人都在使用由其他函数创建并返回的promise.promise**最直接的好处就是链式调用**。

Promise的一般形式为:
```JavaScript
new Promise(
    /* 该function称为Promise的executor执行器函数 */
    function(resolve, reject) {
        if (/* success */) {
            // ...执行代码
            resolve(xxx);
        } else { /* fail */
            // ...执行代码
            reject(xxx);
        }
    }
);
```

Promise的三种状态：
1. `pending`（初始状态,也称为未定状态）:初始化Promise后，调用executor执行器函数后的状态,表示进行中.
2. `fulfilled`（已成功）:异步操作成功，则可以调用`resolve()`来将该实例的状态置为fulfilled
3. `rejected`（已失败）:异步操作失败，则可以调用`reject()`来将该实例的状态置为rejected


Promise对象的两个特点:
1. 对象的状态不受外界影响:只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”.
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果.Promise的状态改变只有两种可能,而且都是单向的:`pending`=>`fulfilled`和`pending`=>`rejected`.改变后称为resolved（已定型）.这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。(个人疑问:什么情况下事件会错过?)

Promise的优缺点:
1. 优点:可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise 对象提供统一的接口，使得控制异步操作更加容易。
2. 缺点
    1. 无法取消,一旦建立就会立即执行
    2. 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部
    3. 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

关于stream和Promise的选择:如果某些事件不断地反复发生，一般来说，使用 Stream 模式是比部署Promise更好的选择

Promise常用方法:
1. `Promise.prototype.then(<成功调用的方法>,<失败调用的方法>)`:调用后返回一个Promise对象,意味着可以进行链式调用。then 方法将返回一个 resolved 或 rejected 状态的 Promise 对象用于链式调用，且 Promise 对象的值就是这个返回值。
  
    ```JavaScript
    const p = new Promise(function(resolve,reject){
      resolve(1);
    }).then(function(value){ // 第一个then // 1
      console.log(value);
      return value * 2;
    }).then(function(value){ // 第二个then // 2
      console.log(value);
    }).then(function(value){ // 第三个then // undefined
      console.log(value);
      return Promise.resolve('resolve');
    }).then(function(value){ // 第四个then // resolve
      console.log(value);
      return Promise.reject('reject');
    }).then(function(value){ // 第五个then //reject:reject
      console.log('resolve:' + value);
    }, function(err) {
      console.log('reject:' + err);
    });
    ```
2. `Promise.prototype.catch()`:用于处理异步操作出现的异常(所有非成功都算作异常?),返回一个Pormise对象.用了它的话就可以省略`then()`方法的第二个参数，把错误处理控制权转交给其后面的`catch()`,一般只需要在链式调用的最末尾加上一个`catch()`方法就行了.

    ```JavaScript
    var p10 = Promise.reject('手动拒绝');
    p10.then(function (data) {
        console.log(data); // 这里不会执行，因为是rejected态
    }).catch(function (err) {
        console.log(err); // 手动拒绝
    }).then(function (data) {
        // 不受上一级影响
        console.log("data:",data); // data: undefined
        console.log('状态：fulfilled'); // 状态：fulfilled
    });
    ```
3. `Promise.all(<可迭代参数>)`:接收一个可迭代参数(一般是数组),通常用来处理一些并发的异步操作，即它们的结果互不干扰，但是又需要异步执行。它最终只有两种状态：成功或者失败。全部成功才算成功.成功后返回一个数组(顺序和传入的顺序相同)
4. `Promise.race(<可迭代参数>)`:返回状态最先变化的参数的结果,如`race`的字面意思.
5. `resolve(<参数>)`:将现有对象转为 Promise 对象.`resolve()`的参数值:可以是普通的值，具有`then()`方法的对象或者Promise实例。正常情况下，它返回一个Promise对象，状态为fulfilled。但是，当解析时发生错误时，返回的Promise对象将会置为rejected状态.

    注意:不带有任何参数使用:立即(在本轮“事件循环”（event loop）的结束时，而不是在下一轮“事件循环”的开始时)返回一个resolved状态的Promise 对象.

    ```JavaScript
    //具有then()方法的对象
    var obj = {
        then: function () {
            console.log('obj 里面的then()方法');
        }
    };
    var p5 = Promise.resolve(obj);
    p5.then();//obj 里面的then()方法
    ```

## 5 类
ES2015的类,实质上是 JavaScript 现有的基于原型的继承的语法糖,也就是说本质仍然是基于原型.mdn:JavaScript 是一种基于原型而不是基于类的面向对象语言.

类声明:使用class关键字,形如,
```JavaScript
class xxx{
    constructor(...){...}
}
```

注意:js的类声明不存在提升,提前访问会抛出ReferenceError.

类表达式:分为匿名类表达式和命令类表达式
```JavaScript
/* 匿名类 */ 
let Rectangle = class {
  constructor(...) {...}
};

/* 命名的类 */ 
let A = class B {
  constructor(...) {...}
};
```

注意:没有必要专门去区分这两者,意义不大.

构造函数:一个类只能有一个构造函数,其中可以使用 super 关键字来调用一个父类的构造函数

静态方法:
1. 使用`static`关键字创建静态方法。静态方法通常用于为一个应用程序创建工具函数。
2. 在一个静态方法中调用另一个静态方法，你可以使用 this 关键字
3. 一般通过类来调用.不能通过一个类的实例调用静态方法(区别于java),但是可以将其作为构造函数的属性来调用该方法,如

    ```JavaScript
    class A{
        constructor(){
            this.constructor.say()
        }
        static say(){}
    }
    a = new A()
    a.constructor.say()
    ```

创建子类:使用`extends`关键字

### 5.1 原型链
参考:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain

遍历:
1. 访问对象的某个属性时，先在对象自身上找,然后对象的原型，该对象的原型的原型，层层搜索，直到找到一个名字匹配的属性或到达原型链的末尾。
2. 遍历对象的属性时，原型链上的每个可枚举属性都会被枚举出来。要检查对象自己定义的属性，而不是其原型链上的某个属性，必须使用所有对象从Object.prototype继承的`hasOwnProperty("xxx")`方法,该方法是js中唯一处理属性并且不会遍历原型链的方法.

性能:
1. 在原型链上查找属性比较耗时，对性能有副作用,而且试图访问不存在的属性时会遍历整个原型链。

注意:永远不要扩展原生对象的原型，除非是为了兼容新的JavaScript特性。

### 5.2 继承


# 四 高级
## 1 协议
ES6新增了两个协议：可迭代协议和迭代器协议.

### 1.1 可迭代协议
### 1.1 迭代器协议


# 六 问题
1. 对象结构带来了性能提升吗,更少资源?