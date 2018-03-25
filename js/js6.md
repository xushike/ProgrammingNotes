# js6
## 一 概述
### 1 简介
该笔记主要记录es6新特性,以后可能会和js笔记合并
### 2 历史
### 3 常识
### 4 文档
### 5 网站
1. 阮一峰es6:[http://es6.ruanyifeng.com/](http://es6.ruanyifeng.com/)
## 三 基础
### 1 对象
#### 不定参数和展开运算符
1. 不定参数

    语法是在参数前加三个点
    ```javascript
    var [head, ...tail] = [1, 2, 3, 4];
    console.log(tail);
    // [2, 3, 4]
    ```

#### 对象解构(Object destructuring)
ES6的解构赋值给js的语法带来了更多的现代化。它在减少了代码量的同时，增加了代码的可读性和表现力。代码和python越来越像了.
参考:[https://segmentfault.com/a/1190000002920859](https://segmentfault.com/a/1190000002920859)
参考:[http://www.infoq.com/cn/articles/es6-in-depth-destructuring/](http://www.infoq.com/cn/articles/es6-in-depth-destructuring/)


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