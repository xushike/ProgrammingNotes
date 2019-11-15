# frontEnd前端
# 一 概述
## 2 历史
## 3 常识
### 3.1 HTML attribute 与 DOM property 的对比(待整理)
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

### 3.2 各浏览器的激进版
- 黄色的Chrome([Chrome Canary](https://www.google.com/chrome/browser/canary.html)):可与chrome同时运行.
- 紫色的Safari技术预览版([Safari Technology Preview](https://developer.apple.com/safari/technology-preview/))
- 深蓝色的Firefox([Firefox Nightly](https://www.mozilla.org/en-US/firefox/nightly/all/))：更新最快、新功能最多，也是最不稳定的一个版本，每天更新的 所以叫nightly。另外还有Aurora，Beta、Release和esr版本。
- Firefox开发者版本：https://www.mozilla.org/zh-CN/firefox/developer/
- 改头换面的IE([Microsoft Edge](https://www.microsoft.com/en-us/windows/microsoft-edge))

### 3.3 UI库和CSS框架
感觉可以把这两个概念当做同一个概念俩看待,UI库也是对html和css的封装

### 3.4 收藏夹图标(Favicon)

### 3.5 单页面应用(SinglePage Web Application，SPA）和多页面应用（MultiPage Application，MPA）
SPA:只有一张Web页面的应用，是一种从Web服务器加载的富客户端，单页面跳转仅刷新局部资源 ，公共资源(js、css等)仅需加载一次，常用于PC端官网、购物等网站

MPA:多页面跳转刷新所有资源，每个公共资源(js、css等)需选择性重新加载，常用于 app 或 客户端等

参考:https://juejin.im/post/5a0ea4ec6fb9a0450407725c

### 3.6 怪异模式(Quirks Mode)
现代浏览器通常会尝试根据W3C标准呈现HTML内容。 但是，为了提供与旧网页的兼容性，所有浏览器都支持另一种模式--怪异模式.怪异模式不是W3C标准,最好不要使用.

当没有DOCTYPE声明或声明不正确时,会呈现怪异模式.

### 3.7 如何优雅的选择默认字体(font-family)
参考：https://www.imooc.com/article/11261

## 4 文档
1. 如何设计「拖放」功能:[https://zhuanlan.zhihu.com/p/33243404](https://zhuanlan.zhihu.com/p/33243404)

## 5 网站
### 5.1 js工具网站
1. 10 款优秀的在线 JavaScript 工具推荐:[http://www.iteye.com/news/25351](http://www.iteye.com/news/25351)
2. 在线编辑工具——由HTML编辑器、CSS编辑器、JavaScript编辑器和输出界面4个部分组成，你可以方便地进行代码测试:[jsfiddle.net](https://jsfiddle.net/)
3. http://jsbin.com/
4. https://codepen.io/
5. https://stackblitz.com

### 5.2 图标网站
1. 阿里:[http://www.iconfont.cn/](http://www.iconfont.cn/)

### 5.3 设计
1. 追波网,有趣的设计交流平台,听说很出名:[http://dribbble.com/](http://dribbble.com/)
2. codepen:一个展示html,css,js的在线社区
3. artstation:ArtStation is the showcase platform for games, film, media & entertainment artists.个人感觉里面的插画质量很高

### 5.4 博客
1. [http://yunkus.com/](http://yunkus.com/)
2. 张鑫旭:http://www.zhangxinxu.com/

### 5.5 学习网站
1. scriptoj,刷js题的网站:http://scriptoj.mangojuice.top/

### 5.6 其他
1. [稳定、快速、免费的前端开源项目 CDN 加速服务](http://www.bootcdn.cn/)

# 三 基础
## 1 热更新


## 2 渐进式框架
渐进式：主张最少。它给你提供足够的optional，但并不主张很多required，也不多做职责之外的事！这就是渐进式。通俗讲就是“给你一个空屋，至于你需要什么自己一件件添，而不是那种家居家电全齐，自己不喜欢再一件件的扔了”。比如Vue，在不依赖全家桶的情况下，单凭一个 Vue 就可以跑起来整个 App。如果觉得 Model 共享数据不方便，可以接入 Vuex，如果觉得路由不方便，可以接入 Vue-Router，所以 Vue 可以渐进地用社区提供的周边方案配一套全家桶。

## 3 响应式和自适应布局
自适应：是为了解决如何才能在不同大小的设备上呈现同样的网页。自适应有一个问题，如果屏幕太小，即使网页能够根据屏幕大小进行适配，但是会感觉在小屏幕上查看，内容过于拥挤，响应式正是为了解决这个问题而衍生出来的概念。

响应式：它可以自动识别屏幕宽度、并做出相应调整的网页设计，布局和展示的内容可能会有所变动。

渐进增强和优雅降级：举一个例子，gmail 和 qqmail。 他俩的宽度都是 100%，都是自适应。但是： qqmail 就是 css hack 的完美体现，你用任何一个浏览器，几乎可以看到同一个样子的邮箱，腾讯的前端工程师们用各种 css hack 技术来展示邮箱页面，为的是统一的用户体验。 而 gmail 使用了渐进增强，你的浏览器越强，你看到的效果就越好，用户体验就越好。 

实现响应式的方案有:
1. flex-layout

# 四 高级
## 1 已整理
1. 知乎张克军

    参考链接:[https://www.w3ctech.com/topic/983](https://www.w3ctech.com/topic/983)
    前端工程师是所有工程师角色中最有也最需要“工匠精神”的。前端工程师的基本职责就是还原设计，把一个躺在设计图上的死的设计变成可以用的活的设计。所谓“工匠精神”体现在这个“活”字上。可视方面，一个动画的过程是否顺畅，一个交互动作全部状态是否都做到位，适配上是否足够灵活。代码方面，一段通用代码是否足够通用，代码冗余是否最小，性能是否足够快等等。简单的实现是最低要求，剩下的部分产品经理、项目经理不会要求，那是优秀的前端工程师发挥的空间。前端工程师的成长就是一个修炼的过程，修炼的开始就是在学会了那些书本上可以学到的编程知识后。在前端工程师的素质中，我认为应用能力是最重要的。这种应用能力可看成是一种产品的塑造能力，前提要有产品思维和设计思维，能自主发现并弥补产品、设计的空白和不合理环节，可以很好的控制代码的复杂度，高效高质量的完成开发需求。提升这种能力，纸上谈兵不行，只能在各种项目中摸爬滚打，如同医生不断积累临床经验一样。如果公司项目不能满足，就自己找项目做。我在刚毕业的时候，接过不少私活，通常这类项目发挥空间大。
2. 除了PC端和移动端,还有面向未来的AR、VR端

    1. 网友:它们的特性就不同于二维平面的移动端，掌握 VR、AR 端的开发就需要新学习很多三维图形图像以及图像识别领域的东西。
3. 关于三大框架

    Angular 约束多，擅长复杂中后台场景和多人协作。Vue 灵活，适用于简单业务快速迭代（当然也有 Vue 做中后台的）。React 组件化设计的好，可以实现比较好的组件生态进行复用。对于这些框架，你只需要基于现有的业务体系和开发者经验，做好最佳的技术方案选型即可。在某些场景下甚至 jQuery 反而是更好的技术选型。

## 2 前端的常见概念
### 2.1 前端工程化体系
### 2.2 前端组件化
### 2.3 异步加载
### 2.4 样式预处理器
### 2.5 代码自动review工具
### 2.6 热更新
给BS架构的页面加载提速的终极方案就是CDN,而CS架构不存在加载压力,但是更新不灵活,所以需要前端热更新

### 2.7 懒加载(Lazy loading)

### 2.8 面包屑导航
来自于一个故事(略).面包屑导航的作用是告诉访问者他们目前在网站中的位置以及如何返回.在许多关于网站用户使用体验的调查报告中也得出，如果超过3次点击，访客还没有找到需要的信息，那么有大约80%的访客会离开网站。

## 3 浏览器开发者工具


# 五 经验
## 1 已整理
网友:
1. 我想奉劝所有人，学前端一定要 JS/CSS 两手抓 ... 是真有 JavaScript 工程师这个岗位的，有的比较高大上，可能是搞搞游戏，玩玩 3D...

## 1 前端提速

## 2 前端趋势
[2018 年最值得关注的 JavaScript 趋势](http://36kr.com/p/5110763.html)

### 2.1 WebAssembly
知乎:[如何评论浏览器最新的 WebAssembly 字节码技术？](https://www.zhihu.com/question/31415286)

### 2.2 server-side rendering
服务端渲染
1. 网友的评价
    1. This allowed for single page applications to be search engine friendly.

### 2.3 PWA
PWA的特点:
1. 利用Service Worker在网络不确定的情况下即时加载：Service Worker是独立的JS线程，与文档无关的生命周期，离线更新资源的能力--通过预缓存关键资源，可以消除对网络的依赖，确保为用户提供即时可靠的体验。
2. 快速：据统计，如果站点加载时间超过 3s，53% 的用户会放弃等待
3. Reliable : SW Cache、Fetch、Push、Navigation Preload、Background Fetch、Background Synchronization、   CompositorWorker

PWA带来的影响:
1. 逐步给前端开放浏览器内核基础能力，甚至是操作系统能力，比如缓存、推送、添加桌面图标、下载、图片解码、渲染等等
2. 前端正变得无所不能，很多事情都可在Web实现，比如SW、WebGL、WebRTC、WebAR/VR等等

## 3 跨站点脚本（XSS）
除了`<script>`标签,还有其他dom元素和属性允许执行代码,比如`<img onerror="...">`和`<a href="javascript:...">`

## 4 种子库seed
有一种核心种子库,其他项目都根据这个种子库来创建衍生库.只要种子库保持更新，其他库可以同步保持更新.
种子库没有业务逻辑的代码,主要是平时开发时所需要的所有脚本，以及npm的一些基本依赖。另外一些共用组件，共用逻辑代码（例如登录验证等等）


## 5 性能测量(待实践)
[Chrome 开发工具的网络性能页](https://developers.google.com/web/tools/chrome-devtools/network-performance/understanding-resource-timing)是开始学习度量性能的好地方。

[WebPageTest工具](https://www.webpagetest.org/)是另一个不错的选择，它能帮你验证你的部署是否成功了。

# 六 问题
## 1 已解决
### 1.1 浏览器未响应
原因可能有很多,但是最先应该考虑的是js代码:在浏览器环境中，一些代价高昂的计算会导致糟糕的用户体验，因为一个页面的用户界面无响应多数是由于在运行js代码.

### 1.2 chrome的控制台执行console.log没有打印输出，只有undefined
因为开了多个网页，怀疑是某个页面把console赋值了。

## 2 未解决
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

16. 伪类不能放进内联样式表?
17. 也可换行?

    ```css
    span 
    { 
    display : table;
    }
    ```

18. https://www.moocbaba.com/product-tag/99

# 七 待整理
1. (不是那么重要):https://lzw.me/a/fed-file-download.html
    1. https://lzw.me/a/pwa-service-worker.html

2. mozilla工程师Lin Clark的文章:https://hacks.mozilla.org/author/lclarkmozilla-com/
3. https://medium.com/@moz2000tw/2017%E5%B9%B4%E5%9B%9E%E9%A1%A7-%E7%82%BA%E4%BA%86%E9%96%8B%E7%99%BC%E8%80%85-mozilla-%E6%8A%8A-web-%E8%AE%8A%E5%BE%97%E6%9B%B4%E5%A5%BD%E4%BA%86-a735d4914775

4. https://developer.mozilla.org/zh-CN/docs/Web
5. 浏览器的工作原理：新式网络浏览器幕后揭秘:https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/
6. 四种防止表单重复提交的方法
:http://www.aazzp.com/2017/10/30/%E5%9B%9B%E7%A7%8D%E9%98%B2%E6%AD%A2%E8%A1%A8%E5%8D%95%E9%87%8D%E5%A4%8D%E6%8F%90%E4%BA%A4%E7%9A%84%E6%96%B9%E6%B3%95/
7. 你不知道的 DOMContentLoaded:https://zhuanlan.zhihu.com/p/25876048

8. 前端性能调优:
    1. firebug,目前已集成到新版firefox中
    2. yslow
    3. YUI compressor