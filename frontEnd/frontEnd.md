# frontEnd前端
## 一 概述
### 1 历史
### 2 常识
#### HTML attribute 与 DOM property 的对比(待整理)
```
attribute 是由 HTML 定义的。property 是由 DOM (Document Object Model) 定义的。

Attributes are defined by HTML. Properties are defined by the DOM (Document Object Model).

少量 HTML attribute 和 property 之间有着 1:1 的映射，如id。

有些 HTML attribute 和 property名字不一样，如colspan对应colSpan,for对应htmlFor.

有些 DOM property 没有对应的 attribute，如textContent,innerHTML.

大量 HTML attribute看起来映射到了property…… 但却不像我们想的那样！

最后一类尤其让人困惑…… 除非我们能理解这个普遍原则：

attribute 初始化 DOM property，然后它们的任务就完成了。property 的值可以改变；attribute 的值不能改变。

例如，当浏览器渲染<input type="text" value="Bob">时，它将创建相应 DOM 节点， 其value property 被初始化为 “Bob”。

当用户在输入框中输入 “Sally” 时，DOM 元素的value property 变成了 “Sally”。 但是这个 HTML value attribute 保持不变。如果我们读取 input 元素的 attribute，就会发现确实没变： input.getAttribute('value') // 返回 "Bob"。

HTML attribute value指定了初始值；DOM value property 是当前值。

disabled attribute 是另一个古怪的例子。按钮的disabled property 是false，因为默认情况下按钮是可用的。 当我们添加disabled attribute 时，只要它出现了按钮的disabled property 就初始化为true，于是按钮就被禁用了。

添加或删除disabled attribute会禁用或启用这个按钮。但 attribute 的值无关紧要，这就是我们为什么没法通过 <button disabled="false">仍被禁用</button>这种写法来启用按钮。

设置按钮的disabled property（如，通过 Angular 绑定）可以禁用或启用这个按钮。 这就是 property 的价值。

就算名字相同，HTML attribute 和 DOM property 也不是同一样东西。
```

1. 参考stackoverflow的回答,大意是html的attribute渲染时会转换成dom的property,而且attribute的值会随property一起变化等等:[What is the difference between attribute and property?](https://stackoverflow.com/questions/258469/what-is-the-difference-between-attribute-and-property)
2. 本人简单测了下(待补充),普通的html对attribute和property两种写法都是支持的,比如`label`标签的`for`和`htmlFor`;而且chrome inspector shows both attributes and properties.
3. 关于文中说的**property的值可以改变；attribute的值不能改变**,我简单测了下,其中好像只有`value`符合,而`href`,`for`和`htmlFor`都是attribute跟着property一起变化.(其他的测试待补充),所以文中的这个说法很可能只是针对angular的.
### 3 网址
1. 追波网,有趣的设计交流平台,听说很出名:[http://dribbble.com/](http://dribbble.com/)
### 4 书籍
## 三 基础
### 1 热更新
## 四 经验
1. 知乎张克军

    参考链接:[https://www.w3ctech.com/topic/983](https://www.w3ctech.com/topic/983)
    前端工程师是所有工程师角色中最有也最需要“工匠精神”的。前端工程师的基本职责就是还原设计，把一个躺在设计图上的死的设计变成可以用的活的设计。所谓“工匠精神”体现在这个“活”字上。可视方面，一个动画的过程是否顺畅，一个交互动作全部状态是否都做到位，适配上是否足够灵活。代码方面，一段通用代码是否足够通用，代码冗余是否最小，性能是否足够快等等。简单的实现是最低要求，剩下的部分产品经理、项目经理不会要求，那是优秀的前端工程师发挥的空间。前端工程师的成长就是一个修炼的过程，修炼的开始就是在学会了那些书本上可以学到的编程知识后。在前端工程师的素质中，我认为应用能力是最重要的。这种应用能力可看成是一种产品的塑造能力，前提要有产品思维和设计思维，能自主发现并弥补产品、设计的空白和不合理环节，可以很好的控制代码的复杂度，高效高质量的完成开发需求。提升这种能力，纸上谈兵不行，只能在各种项目中摸爬滚打，如同医生不断积累临床经验一样。如果公司项目不能满足，就自己找项目做。我在刚毕业的时候，接过不少私活，通常这类项目发挥空间大。
## 五 问题
1. [http://www.uisdc.com/material-motion-design-guideline-2](http://www.uisdc.com/material-motion-design-guideline-2)
2. [https://baike.baidu.com/item/SPA/17536313#viewPageContent](https://baike.baidu.com/item/SPA/17536313#viewPageContent)
3. 异步事件
    1. 击键