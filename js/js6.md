# js6
# 一 概述
## 1 简介
该笔记主要记录es6新特性,以后可能会和js笔记合并
## 2 历史
## 3 常识
### 3.1 ECMAScript 2015(ES2015),ES6和JS6的区别
一般来讲,可以把这三个看成一个东西.

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
#### for ... in
遍历目标的键(所以返回的似乎是字符串),可以用于任何数据类型,但本职工作是用于遍历对象,如果遍历数组和集合,则可能出问题(待补充).

写法是`for (<修饰符> <变量名> in <要操作的对象>){...}`,比如有对象`obj = { a: [], b: [1, 2] }`,则`for (let x in obj){...}`,其中x返回的是对象的属性名,而且是字符串,那么要访问对象的属性值,则可以`obj[x]`

#### for ... of
用于遍历数组和集合等,不能用遍历普通对象

## 3 函数
### 3.1 箭头函数
我的理解是:直接声明function,则function中的this指的外层对象;而用箭头函数则this指的全局对象(如果是在组件中,则是指向组件)

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
2. `fulfilled`（已成功）:异步操作成功，则可以调用resolve()来将该实例的状态置为fulfilled
3. `rejected`（已失败）:异步操作失败，则可以调用reject()来将该实例的状态置为rejected


Promise对象的两个特点:
1. 对象的状态不受外界影响:.只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”.
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果.Promise的状态改变只有两种可能,而且都是单向的:`pending`=>`fulfilled`和`pending`=>`rejected`.改变后称为resolved（已定型）.这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。(个人疑问:什么情况下事件会错过?)

Promise的优缺点:
1. 优点:可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise 对象提供统一的接口，使得控制异步操作更加容易。
2. 缺点
    1. 无法取消,一旦建立就会立即执行
    2. 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部
    3. 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

关于stream和Promise的选择:如果某些事件不断地反复发生，一般来说，使用 Stream 模式是比部署Promise更好的选择

Promise常用方法:
1. `Promise.prototype.then(<成功调用的方法>,<失败调用的方法>)`:调用后返回一个Promise对象,意味着可以进行链式调用.
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



# 四 高级
## 1 import
导入模块的导出,有几种写法:
- 导入某模块的所有导出:`import * as [name] from ...`:可以用别名`[name]`来使用模块(如果模块里有多个导出,用了星号后能不能直接使用这些导出的名字呢?)
- 导入单个导出:`import {xxx} from ...`:也可以使用别名
- 导出多个导出;`import {foo, bar} from ...`:也可以使用别名
- 仅为副作用而导入一个模块:`import ...`
- 导入默认值:`import myDefault from ...`:导入单个或多个时导出时,需要知道导出的名字,很不方便,所以js允许设置一个默认的导出,形如`export default xxx`,这样导入的时候就可以随意去一个名字,而且不用大括号包裹来表示默认的导出.

# 六 问题
1. 对象结构带来了性能提升吗,更少资源?