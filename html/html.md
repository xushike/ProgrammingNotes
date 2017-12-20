# html
## 一 概述
1. html5正快速被前端人员采用,所以以后的开发建议都遵循h5的标准
### 1 关于html的一些常识
#### 1.1 关于Dhtml
DHTML是Dynamic HTML的简称，就是动态的html（标准通用标记语言下的一个应用），是相对传统的静态的html而言的一种制作网页的概念。所谓动态HTML（Dynamic HTML，简称DHTML），其实并不是一门新的语言，它只是HTML、CSS和客户端脚本的一种集成，即一个页面中包括html+css+javascript（或其它客户端脚本），其中css和客户端脚本是直接在页面上写而不是链接上相关文件。DHTML不是一种技术、标准或规范，只是一种将目前已有的网页技术、语言标准整合运用，制作出能在下载后仍然能实时变换页面元素效果的网页设计概念。
#### 1.2 什么是现代浏览器
现代浏览器（指 IE6-IE8 除外的浏览器，包括 IE9+、FireFox、Safari、Chrome 和 Opera 等）
#### 1.3 关于预留字符和字符实体
(待补充)
参考:[http://www.w3school.com.cn/html/html_entities.asp](http://www.w3school.com.cn/html/html_entities.asp)
## 二 安装配置
## 三 HTML基础
### 1 在html中使用脚本
在当初开发 JavaScript 的时候，Netscape 要解决的一个重要问题就是如何做到让 JavaScript 既能与 HTML 页面共存，又不影响那些页面在其他浏览器中的呈现效果。经过尝试、纠错和争论，最终的决定就是:为 Web 增加统一的脚本支持。
#### 1.1 `<script>`元素
向 HTML 页面中插入 JavaScript 的主要方法，就是使用`<script>`元素。这个元素由 Netscape 创造 并在 Netscape Navigator 2 中首先实现。后来，这个元素被加入到正式的 HTML 规范中。
1. 使用该标签
    使用`<script>`有两种方式:接在页面中嵌入 JavaScript 代码和包含外部 JavaScript 文件。
    1. 嵌入:只需指定其type属性,然后将js代码放在元素内部即可,如
        ```html
        <script type="text/javascript">
            function sayHi(){
                alert("Hi!");
            }
        </script>
        ```
        会被从上到下依次解释

    2. 包含外部js文件:src属性是必需的,这个属性的值是一个指向外部js文件的链接，如
        ```html
        <script type="text/javascript" src="example.js"></script>
        ```
        与解析嵌入式js代码一样， 在解析外部js文件(包括下载该文件)时，页面的处理也会暂时停止。
        如果是在 XHTML 文档 中，也可以省略前面示例代码中结束的</script>标签，如:
        ```html
        <script type="text/javascript" src="example.js" />
        ```
        但是，不能在 HTML 文档使用这种语法。原因是这种语法不符合 HTML 规范，而且也得不到某些 浏览器(尤其是 IE)的正确解析。
        带有src属性的`<script>`元素不应该在其`<script>`和`</script>`标签之间再包含js代码,否则,嵌入的代码会被忽略。
        使用包含外部这种方式有如下三个优点:
        1. 可维护性
        2. 可缓存:如果有两个页面使用同一个js...
        3. 适应未来:就不必麻烦的使用同时支持HTML和XHTML的hack方式了.
2. 该标签属性
    HTML 4.01 为 `<script>`定义了下列 6 个属性。
    1. `async`(异步脚本):可选。表示应该立即执行脚本，但不应妨碍页面中的其他操作，比如下载其他资源或等待加载其他脚本。只对外部脚本文件有效.所以最佳实践是异步脚本不要在加载期间修改DOM.
    如果有多个脚本都指定了该属性,不保证顺序,所以多个脚本之间不要有依赖.异步脚本一定会在页面的 load 事件前执行，但可能会在 DOMContentLoaded 事件触发之前或之 后执行。
    一般用法是`async`,在XHTML中是`async="async"`
    2. charset:可选。表示通过 src 属性指定的代码的字符集。由于大多数浏览器会忽略它的值， 因此这个属性很少有人用。
    3. `defer`(延迟脚本):可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有效。IE4~IE7对嵌入脚本也支持这个属性。
    由此可见将js放在`<body>`底部是最佳实践.
    一般用法是`defer="defer"`(?)
    HTML5 规范要求脚本按照它们出现的先后顺序执行，因此第一 个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于 DOMContentLoaded 事件执行。在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoaded 事件触发 前执行，因此最好只包含一个延迟脚本。
    4. language:已废弃。原来用于表示编写代码使用的脚本语言(如 JavaScript、JavaScript1.2 或 VBScript)。大多数浏览器会忽略这个属性，因此也没有必要再用了。
    5. src:可选。表示包含要执行代码的外部文件。
    6. type:可选。可以看成是 language 的替代属性;表示编写代码使用的脚本语言的内容类型(也称为 MIME 类型)。虽然 text/javascript 和 text/ecmascript 都已经不被推荐使用，但人 们一直以来使用的都还是 text/javascript。实际上，服务器在传送 JavaScript 文件时使用的 MIME 类型通常是 application/x–javascript，但在 type 中设置这个值却可能导致脚本被 忽略。另外，在非 IE 浏览器中还可以使用以下值:application/javascript 和application/ecmascript。考虑到约定俗成和最大限度的浏览器兼容性，目前 type 属性的值依旧还是 text/javascript。不过，这个属性并不是必需的，如果没有指定这个属性，则其默认值仍为 text/javascript。
3. 该标签位置

    之前是放在`<head>`中,浏览器在遇到`<body>`标签时才开始呈现内容,js多了会出现明显的延迟，而延迟期间的浏览器窗口中将是一片空白。于是放在`<body>`元素中页面内容的后面.
    (Android应用的快速启动是不是也是类似原理?)
## 四 XHTML基础
### 1 关于xhtml
简介参考笔记的dom目录.

### 2 在XHTML中使用`<script>`
xhtml更严格,如,
```html
<script type="text/javascript">
        function compare(a, b) {
            if (a < b) {
                alert("A is less than B");
            } else if (a > b) {
                alert("A is greater than B");
            } else {
                alert("A is equal to B");
} }
</script>
```
在HTML中没毛病,但是在XHTML中,这儿的小于号会被当做新标签的开始,从而导致错误.
解决办法有两个:
1.  使用HTML实体
    
    比如使用(`&lt;`)替换小于号,但是该方法会导致代码不好理解.
2. 使用`CData`片段来包含js代码

    CData 片段是文档中的一个特殊区域，这个区域中可以包含不需要解析的任意格式的文本内容。如,
    ```html
    <script type="text/javascript"><![CDATA[
        function compare(a, b) {
            if (a < b) {
                alert("A is less than B");
            }  else {
                ...
            }
        }            
    ]]></script>
    ```
3. 最佳实践

    因为XHTML不是所有浏览器都支持,所以可以用hack的方法,如
    ```html
    <script type="text/javascript">
    //<![CDATA[
        function compare(a, b) {
            if (a < b) {
                alert("A is less than B");
            }  else {
                ...
            }
        }
    //]]>
    </script>
    ```
    这样,所有现代浏览器都可以支持了.
## 五 问题

