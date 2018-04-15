# js6
## 一 概述
### 1 简介
该笔记主要记录es6新特性,以后可能会和js笔记合并
### 2 历史
### 3 常识
#### 3.1 ECMAScript 2015(ES2015),ES6和JS6的区别
一般来讲,可以把这三个看成一个东西.

### 4 文档
### 5 网站
1. 阮一峰es6:[http://es6.ruanyifeng.com/](http://es6.ruanyifeng.com/)
## 三 基础
### 1 对象
#### 1.1 不定参数和展开运算符
1. 不定参数

    语法是在参数前加三个点
    ```javascript
    var [head, ...tail] = [1, 2, 3, 4];
    console.log(tail);
    // [2, 3, 4]
    ```

#### 1.2 对象解构(Object destructuring)
ES6的解构赋值给js的语法带来了更多的现代化。它在减少了代码量的同时，增加了代码的可读性和表现力。代码和python越来越像了.
参考:[https://segmentfault.com/a/1190000002920859](https://segmentfault.com/a/1190000002920859)
参考:[http://www.infoq.com/cn/articles/es6-in-depth-destructuring/](http://www.infoq.com/cn/articles/es6-in-depth-destructuring/)

### 2 流程控制和迭代器
#### 2.2 迭代器
##### for ... in
遍历目标的键(所以返回的似乎是字符串),可以用于任何数据类型,但本职工作是用于遍历对象,如果遍历数组和集合,则可能出问题(待补充).

写法是`for (<修饰符> <变量名> in <要操作的对象>){...}`,比如有对象`obj = { a: [], b: [1, 2] }`,则`for (let x in obj){...}`,其中x返回的是对象的属性名,而且是字符串,那么要访问对象的属性值,则可以`obj[x]`

##### for ... of
用于遍历数组和集合等,不能用遍历普通对象

### 3 函数
#### 3.1 箭头函数
我的理解是:直接声明function,则function中的this指的外层对象;而用箭头函数则this指的全局对象(如果是在组件中,则是指向组件)

## 四 高级
### 1 import
导入模块的导出,有几种写法:
- 导入某模块的所有导出:`import * as [name] from ...`:可以用别名`[name]`来使用模块(如果模块里有多个导出,用了星号后能不能直接使用这些导出的名字呢?)
- 导入单个导出:`import {xxx} from ...`:也可以使用别名
- 导出多个导出;`import {foo, bar} from ...`:也可以使用别名
- 仅为副作用而导入一个模块:`import ...`
- 导入默认值:`import myDefault from ...`:导入单个或多个时导出时,需要知道导出的名字,很不方便,所以js允许设置一个默认的导出,形如`export default xxx`,这样导入的时候就可以随意去一个名字,而且不用大括号包裹来表示默认的导出.

## 六 问题
1. 对象结构带来了性能提升吗,更少资源?