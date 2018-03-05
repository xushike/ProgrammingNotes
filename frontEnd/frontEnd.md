# frontEnd前端
## 一 概述
### 2 历史
### 3 常识
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

#### 各浏览器的激进版
- 黄色的Chrome([Chrome Canary](https://www.google.com/chrome/browser/canary.html)):可与chrome同时运行.
- 紫色的Safari([Safari Technology Preview](https://developer.apple.com/safari/technology-preview/))
- 深蓝色的Firefox([Firefox Nightly](https://www.mozilla.org/en-US/firefox/nightly/all/))
- 改头换面的IE([Microsoft Edge](https://www.microsoft.com/en-us/windows/microsoft-edge))

### 5 网址
1. 追波网,有趣的设计交流平台,听说很出名:[http://dribbble.com/](http://dribbble.com/)

### 4 文档
1. 如何设计「拖放」功能:[https://zhuanlan.zhihu.com/p/33243404](https://zhuanlan.zhihu.com/p/33243404)

### 6 js工具网站
1. 10 款优秀的在线 JavaScript 工具推荐:[http://www.iteye.com/news/25351](http://www.iteye.com/news/25351)
1. 在线编辑工具——由HTML编辑器、CSS编辑器、JavaScript编辑器和输出界面4个部分组成，你可以方便地进行代码测试:[jsfiddle.net](https://jsfiddle.net/)

## 三 基础
### 1 热更新

## 四 经验
1. 知乎张克军

    参考链接:[https://www.w3ctech.com/topic/983](https://www.w3ctech.com/topic/983)
    前端工程师是所有工程师角色中最有也最需要“工匠精神”的。前端工程师的基本职责就是还原设计，把一个躺在设计图上的死的设计变成可以用的活的设计。所谓“工匠精神”体现在这个“活”字上。可视方面，一个动画的过程是否顺畅，一个交互动作全部状态是否都做到位，适配上是否足够灵活。代码方面，一段通用代码是否足够通用，代码冗余是否最小，性能是否足够快等等。简单的实现是最低要求，剩下的部分产品经理、项目经理不会要求，那是优秀的前端工程师发挥的空间。前端工程师的成长就是一个修炼的过程，修炼的开始就是在学会了那些书本上可以学到的编程知识后。在前端工程师的素质中，我认为应用能力是最重要的。这种应用能力可看成是一种产品的塑造能力，前提要有产品思维和设计思维，能自主发现并弥补产品、设计的空白和不合理环节，可以很好的控制代码的复杂度，高效高质量的完成开发需求。提升这种能力，纸上谈兵不行，只能在各种项目中摸爬滚打，如同医生不断积累临床经验一样。如果公司项目不能满足，就自己找项目做。我在刚毕业的时候，接过不少私活，通常这类项目发挥空间大。
2. 除了PC端和移动端,还有面向未来的AR、VR端

    1. 网友:它们的特性就不同于二维平面的移动端，掌握 VR、AR 端的开发就需要新学习很多三维图形图像以及图像识别领域的东西。
3. 关于三大框架

    Angular 约束多，擅长复杂中后台场景和多人协作。Vue 灵活，适用于简单业务快速迭代（当然也有 Vue 做中后台的）。React 组件化设计的好，可以实现比较好的组件生态进行复用。对于这些框架，你只需要基于现有的业务体系和开发者经验，做好最佳的技术方案选型即可。在某些场景下甚至 jQuery 反而是更好的技术选型。

### 1 前端UI框架
#### angular
ng-bootstrap、OnsenUI 和 material2 等

#### vue
bootstrap-vue、vue-material、Element UI、Mint UI 等

#### 中立UI框架
Bulma

### 2 前端的常见概念

#### 前端工程化体系
#### 前端组件化
#### 异步加载
#### 样式预处理器
#### 代码自动review工具
#### 热更新
给BS架构的页面加载提速的终极方案就是CDN,而CS架构不存在加载压力,但是更新不灵活,所以需要前端热更新

#### 懒加载

#### 面包屑导航
来自于一个故事(略).面包屑导航的作用是告诉访问者他们目前在网站中的位置以及如何返回.在许多关于网站用户使用体验的调查报告中也得出，如果超过3次点击，访客还没有找到需要的信息，那么有大约80%的访客会离开网站。

## 五 经验
### 1 前端提速

### 1 前端趋势
[2018 年最值得关注的 JavaScript 趋势](http://36kr.com/p/5110763.html)

#### WebAssembly
知乎:[如何评论浏览器最新的 WebAssembly 字节码技术？](https://www.zhihu.com/question/31415286)

#### server-side rendering
服务端渲染
1. 网友的评价
    1. This allowed for single page applications to be search engine friendly.

### 2 跨站点脚本（XSS）
除了`<script>`标签,还有其他dom元素和属性允许执行代码,比如`<img onerror="...">`和`<a href="javascript:...">`

## 六 问题
1. [http://www.uisdc.com/material-motion-design-guideline-2](http://www.uisdc.com/material-motion-design-guideline-2)
2. [https://baike.baidu.com/item/SPA/17536313#viewPageContent](https://baike.baidu.com/item/SPA/17536313#viewPageContent)
3. 异步事件,哪些事件是异步的
    1. 击键
4. 防止表单重复提交以及一些常见的问题
5. 如何使用Firebug, Developer Tools来扒前端代码
6. 专业美工是怎么切图的
7. [https://segmentfault.com/a/1190000009485047](https://segmentfault.com/a/1190000009485047)
8. 蚂蚁前端玉伯的博客
9. 有价值的问题

    针对无线页面跨页面跳转的状态本地存储方案、多页面无刷新的单页面路由方案等等。
10. UI,UE,UX等

    知乎:[https://www.zhihu.com/question/27928975](https://www.zhihu.com/question/27928975)
11. [在 React、Vue项目中使用 SVG](http://mp.weixin.qq.com/s/Lez6iRkfaHCjGV1m2PMQ_Q)
12. 这个界面感觉很不错:[https://research.hackerrank.com/developer-skills/2018/](https://research.hackerrank.com/developer-skills/2018/)

13. web端=>桌面端

    1. node-webkit
14. 优达学院
    1. 可以使用 Photoshop、Paint、Preview 或 GIMP 等软件或在线工具更改图片的大小
    2. 可以使用手机的摄像头应用或以下在线录制工具：
        - CamStudio (Windows)
        - Quicktime (Mac 10.x)
        - Jing (Windows/Mac)

15. 锚文本和超链接的区别?

16. 伪类不能放进内联样式表?