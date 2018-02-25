# TypeScript
[TOC]
## 一 概述
TypeScript是JavaScript的一个超集，而且本质上向这个语言添加了**可选的静态类型和基于类的面向对象**编程。是由微软开发的自由和开源的编程语言。TypeScript可以编译出纯净、简洁的JavaScript代码，并且可以运行在任何浏览器上.

### 1 简介
作者是Anders Hejlsberg,微软的架构师,超级大牛.说:TypeScript makes JavaScript scale.
- Better readability and intergratable software.
- Any browser,host,and OS.
#### TypeScript complier编译器(tsc)
- tsconfig.json:configures compliation options for JS.
- Static ytpe checking and code refactoring(重构).

Works with all the popular frameworks.
#### Typescript Adoptions
- google
- Microsoft:vscode就是用typescript写的.
- Netflix:网页播放器是用typescript写的. 
### 2 历史
### 3 常识
#### 编译错了依然会生成文件?
### 4 文档
1. [TypeScript Handbook](http://dreamapple.leanapp.cn/gitbook/typescript/index.html)

### 5 网址


## 二 安装配置
### 1 npm安装(推荐)
1. `npm install typescript -g`
2. 用`tsc -v`查看是否正确安装了typescript
### 2 配置
1. 大型项目中使用`tsconfig.json`来配置,很方便.
### 3 常用命令
1. 编译成js文件:`tsc xxx.ts...`,默认覆盖已有的
    1. 参数`--watch`:每次保存时会自动用增量编译(incremental compilation)的方式编译ts文件
## 三 基础知识
### 1 数据类型
#### 1.1 基础类型(和js几乎相同，除了是静态)
1. 数字：number
    和js一样都是浮点数，除了支持十进制和十六进制字面量，Typescript还支持ECMAScript 2015中引入的二进制和八进制字面量。如：`let hexLiteral: number = 0xf00d;`
2. 布尔值：boolean
3. 字符串：string
    和JavaScript一样，可以使用双引号（ "）或单引号（'）表示字符串。还可以使用模版字符串，它可以定义多行文本和内嵌表达式。 这种字符串是被反引号包围（ `），并且以${ expr }这种形式嵌入表达式，如：
    ```typescript
    let name: string = `Gene`;
    let age: number = 37;
    let sentence: string = `Hello, my name is ${ name }.
    I'll be ${ age + 1 } years old next month.`;
    ```
4. 数组
    1. 定义数组的两种方式：
        1. 在元素类型后面接上[]：`let list: number[] = [1, 2, 3];`
        2. 使用数组泛型，Array<元素类型>：`let list: Array<number> = [1, 2, 3];`
5. 元组Tuple
    元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 比如，
    ```typescript
    // Declare a tuple type
    let x: [string, number];
    // Initialize it
    x = ['hello', 10]; // OK
    // Initialize it incorrectly
    x = [10, 'hello']; // Error
    ```
    当访问一个越界的元素，会使用联合类型替代：
    ```typescript
    x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型
    x[6] = true; // Error, 布尔不是(string | number)类型
    ```
6. 枚举:enum
    使用枚举类型可以为一组数值赋予友好的名字.默认从0开始为元素编号，也可以手动的指定成员的数值，如，
    ```typescript
    enum Color {Red = 1, Green = 4, Blue};
    let c: Color = Color.Blue;
    ```
7. 任意值：any
    想要为那些在编程阶段还不清楚类型的变量指定一个类型,不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查，那么我们可以使用`any`类型来标记这些变量，如，
    ```typescript
    let notSure: any = 4;
    notSure = "maybe a string instead";
    notSure = false; // okay
    ```
    这样看起来和Object的作用相似，区别在于Object只允许你给它赋任意值，但是却不能够在它上面调用任意的方法，即便它真的有这些方法。如，
    ```typescript
    let notSure: any = 4;
    notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)
    let prettySure: Object = 4;
    prettySure.toFixed(); // Error
    ```
    个人觉得好像没什么用，因为最后ts要转成js，这样写ts不报错，但转后的js会报错
8. 空值:void
    void类型像是与any类型相反，它表示没有任何类型。当一个函数没有返回值时，通常会见到其返回值类型是 void，如，
    ```typescript
    function warnUser(): void {
        alert("This is my warning message");
    }
    ```
    声明一个void类型的变量没有什么大用，因为你只能为它赋予undefined和null：`let unusable: void = undefined;`
9. Null 和 Undefined
    和 void相似，它们的本身的类型用处不是很大.默认情况下null和undefined是所有类型的子类型.然而，当你指定了--strictNullChecks标记，null和undefined只能赋值给void和它们各自,这能避免很多常见的问题。
10. Never
    never类型表示的是那些永不存在的值的类型。 例如， never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是 never类型，当它们被永不为真的类型保护所约束时。(待补充)
    ```typescript
    // 返回never的函数必须存在无法达到的终点
    function error(message: string): never {
        throw new Error(message);
    }
    // 推断的返回值类型为never
    function fail() {
        return error("Something failed");
    }
    ```
#### 1.2 高级类型

### 2 变量

### 3 interfaces接口
- Interfaces describe the shape of your JS objects.
- Interface disapper during compliation to JS.
- Coercions do not add runtime checks.
1. 接口的用处

    会根据一个对象是否符合某种特定结构来进行类型检查.编译成js时接口的代码会消失,所以ts接口的唯一的目的是在开发阶段里起到辅助的作用.
    ```typescript
    interface Food {
        name: string;
        calories: number;
    }

    function speak(food: Food): void {
        console.log("Our " + food.name + " has " + food.calories + " calories.");
    }

    var ice_cream = {
        name: "ice cream",
        calories: 200
    }

    speak(ice_cream);
    ```
### 4 类
和Java,C#中的类非常相似，包括了继承，抽象类，接口实现，setters/getters 方法等
1. 类,如下

    ```typescript
    class Menu {
        items: Array<string>;  
        pages: number;       

        constructor(item_list: Array<string>, total_pages: number) {
        this.items = item_list;    
        this.pages = total_pages;
        }
    
        // Methods
        list(): void {
        console.log("Our menu for today:");
        for(var i=0; i<this.items.length; i++) {
            console.log(this.items[i]);
        }
        }
    
    } 
    
    var sundayMenu = new Menu(["pancakes","waffles","orange juice"], 1);
    
    sundayMenu.list();
    ```
2. 继承

3. 类中的静态属性和普通属性的区别

    通过转换后的ES5代码可知,类中的静态变量是属于构造函数的，而成员属性是属于实例.
    
### 5 函数
### 6 泛型
泛型（Generics）是允许同一个函数接受不同类型参数的一种模板。相比于使用 any 类型，使用泛型来创建可复用的组件要更好，因为泛型会保留参数类型。如,
```typescript
function genericFunc(argument) {
    var arrayOfT = []; // Create empty array of type T.
    arrayOfT.push(argument); // Push, now arrayOfT = [argument].
    return arrayOfT;
}
var arrayFromString = genericFunc("beep");
console.log(arrayFromString[0]); // "beep"
console.log(typeof arrayFromString[0]);
```
### 7 枚举
### 8 类型推论
### 9 高级类型
### 10 Symbols
### 11 迭代器和生成器
### 12 模块
导出和导入
### 13 命名空间
### 14 命名空间和模块
### 15 模块解析
### 16 声明合并
### 17 JSX
### 18 装饰器


### 19 Mixins
### 10 三斜线指令

## 四 高级知识
### 1 features
- Enums枚举
- Interfaces接口
- Decorators装饰器
- Protected/Private
- Union Types 
## 五 经验

## 六 问题
### 1 已解决
5. "Cannot read property 'xxx' of undefined"

    这个错经常报.可能原因有两个:
    1. 运行时xxx上确实没有xxx方法
    2. xxx可能为null或undefined,需要先判断

### 2 未解决
1. 和typings的关系  
2. 笔记:将number类型用`as`声明为string类型,然后调用match()方法会报"没有match()方法"错

    这是因为变量依然是number类型,所以不存在match()方法
3. ts中数值都是单精度?
4. 笔记:如果input组件被声明为number类型,那么在ts中,其value值也是number类型


## 七 学习
1. [http://web.jobbole.com/87535/](http://web.jobbole.com/87535/)