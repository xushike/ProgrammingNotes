# temp4study
1. 数据库索引的方式
    1. btree
1. 数学
    1. log(n)
1. js Boolean(a=b)是怎么判断的
1. 继承与原型链:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
1. js 获取命令行输入怎么获取
1. input只输入数字
1. js在不同地方引入同一个模块的时候,是引用的同一个对象还是不同的对象
2. SQL注入
2. 回归最优解
1. js date对象
1. font-size的相对单位em
2. git flow
3. apply和call
4. session和jwt
5. utf16,unicode,base64
6. JSON.stringify与JSON.parse
8. cssText
9. HTML templates（HTML模板）：<template> 和 <slot> 元素使您可以编写不在呈现页面中显示的标记模板。然后它们可以作为自定义元素结构的基础被多次重用
10. 基于回流的页面渲染,页面渲染的w3c规范和那个女人的博客
11. 事件设计模式
13. nodeValue:https://developer.mozilla.org/zh-CN/docs/Web/API/Node/nodeValue
14. innerHTML,innertext,textcontent的区别:https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent
15. https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/proto
16. DOCTYPE
17. CDATA是什么
18. 可以连续的调用Object.getPrototypeOf，直到原型链尽头
19. 扩展DOM对象的原型是非常危险的，尤其是在旧版本的Internet Explorer (6，7，8)中。:http://perfectionkills.com/whats-wrong-with-extending-the-dom/
20. 文档流顺序
21. node.parentnode和parentNOde接口有关系吗
22. Node.baseURI和document.url,element的url的区别
23. window.location.href和document的url的区别
24. hasAttributes()有参数和无参数的区别
25. angular中获取dom的比较好的做法是什么,使用querySelector呢?
26. http协议

27. html embeds是干嘛的
28. 那些节点不允许子节点?

29. properties 和 attributes
30. iframe
    参考:https://www.zhihu.com/question/20653055
    1. 会重新加载css?会有新的window对象?
    2. 完全隔离的css 和 js , 但又可以使用 contentWindow和parent 来通信. 松耦合又不失灵活 
    3. 适用环境:
        HTML规范说：The iframe element represents a nested browsing context.所以如果你需要独立的浏览上下文，那么就用 iframe，否则就不用。历史上，iframe 常被用于复用部分界面，但是多数情况下并不合适。现在，应该使用 iframe 的例子如：
            1. 沙箱隔离。2. 引用第三方内容。3. 独立的带有交互的内容，比如幻灯片。4. 需要保持独立焦点和历史管理的子窗口，如复杂的Web应用。

    4. 比较典型的应用就是网易云音乐网页版:除了播放条,其他部分全是iframe
    5. 单页面和iframe的关系
31. 未设置onclick的空button有事件监听器吗,点击时会有方法执行吗
    1. 当一个事件出现且有一个事件监听器被绑定时，消息会被随时添加。如果没有事件监听器，事件会丢失,不会被添加到队列
    2. 一个 web worker 或者一个跨域的iframe都有自己的栈，堆和消息队列。两个不同的运行时只能通过 postMessage方法进行通信。如果后者侦听到message事件，则此方法会向其他运行时添加消息。
32. requestAnimationFrame和settimeout
    1. HTML5标准规定了setTimeout()的第二个参数的最小值（最短间隔），不得低于4毫秒，如果低于这个值，就会自动增加。在此之前，老版本的浏览器都将最短间隔设为10毫秒。另外，对于那些DOM的变动（尤其是涉及页面重新渲染的部分），通常不会立即执行，而是每16毫秒执行一次。这时使用requestAnimationFrame()的效果要好于setTimeout()。

33. 深复制对原型链有什么影响?
34. 打印字符和控制字符
35. js call和apply参考:https://www.jianshu.com/p/a9990162d698
36. 页面重定向和window.location的关系
37. 浏览器跨域,iframe,跨域加载js
38. web work参考
    1. https://www.cnblogs.com/giggle/p/5350288.html
    2. https://segmentfault.com/a/1190000012528806
39. console.log()参考:https://segmentfault.com/a/1190000012957199

40. 按mdn的html元素参考重新整理html笔记:https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element
41. window和document和element

42. nodejs中如何操作dom,或者生成web页面?
43. navigator.userAgent
44. user_agent:https://developer.mozilla.org/zh-CN/docs/Glossary/User_agent
45. js的错误处理throw， try/catch
46. 时间复杂度和空间复杂度
47. fiber and goruntine
48. every day和everyday
49. css:https://www.cnblogs.com/yaohong/p/6092440.html
50. chrome及vscode等的调试
51. 抓包
52. 学习数据结构
53. 音频流和视频流
54. 数字钱包
55. linux中的vscode和chrome等可以用apt-get来更新吗
56. https://www.cnblogs.com/yaohong/p/6385228.html
57. slack一款协作办公应用
    1. qq协同excel
58. 编程之美
59. https://mp.weixin.qq.com/s/mz2QuZrE6uMXpAq8HGJe3A
60. godep那个tool的使用
61. golang给包设置多个目录,下载的包需要在多个版本间切换怎么弄比较好
62. 密钥:私钥,公钥
63. postman
64. chrome的投影
65. git log是按时间顺序排吗, 如果不是怎么弄?
66. 取数组最大最小值的算法
67. db
    1. sql中#和$的区别
    2. 各sql的变量占位符是啥
        1. note:postgresql是$
    3. 占位符防止sql注入
    4. 各sql 中 @#$%& 的区别
    5. 如何给数据库传数组等
    6. BEGIN和end if这些是存储过程用到的?普通sql中能用吗
    7. 变量和字符串拼接的结果是字符串还是?
    8. sql字符串中有特殊符号
    9. sql参数数量不确定怎么办
    10. 动态sql
    11. 临时表
    12. sql and的原理:是先计算完所有的前一个还是一个的前一个之后执行下一个and
68. gitlab
    1. 使用ssh协议,不用输入密码,使用http就需要?
69. vscode集成终端运行得很慢:https://code.visualstudio.com/docs/editor/integrated-terminal#_changing-how-the-terminal-is-rendered
70. `source xxx`只对当前窗口和新窗口生效,不对其他老窗口生效?
71. 队列,task,queue,Metric
72. 从gitlab clone需要权限吗?为什么有时候需要输入密码
73. 存储过程,队列,任务调度,时间齿轮,activeMQ
74. RESTful
75. 元祖类型和set差不多?
76. golang
    1. https://segmentfault.com/a/1190000006885571
    2. note:格式转换:【链接】Go语言string，int，int64,float转换https://www.cnblogs.com/vdvvdd/p/7211122.html
    3. go web编程:https://www.kancloud.cn/kancloud/web-application-with-golang#/comment
    4. 各种类型的转换
    5. golang有对象的概念吗,只有用结构体这些?
    6. 数组的拼接等
    7. go get时的(download)表示啥
    8. fmt的v,V,+v区别
    9. golang三个点的写法,前面三个点和后面三个点,好处是什么
        1. 项目中分开写的时候,为什么没传点, 点的长度为1
        2. note:可以用在接受单个元素的地方,比如`pois = append(pois, others...)`
    10. go get作用于github时和git pull的区别
    11. []interface{}和[]interface{}{}
    12. golang 语句中传变量是用`$1`,`$2`...?
    13. 反射
    14. 带星号和不带星号的区别
    15. 结构体实例, 类实例等
    16. golang json的意义和作用
        1. 在哪儿用别名,哪儿用本命
        2. 别名的作用是啥
    17. 多种数据的组合怎么弄,比如切片类型和map类型
    18. golang和区块链
    19. 如何配置多个 gopath,配置后会怎么样?
    20. 方法和函数的区别
        1. 参考:https://studygolang.com/articles/9945
    21. gopath和goroot的配置,立即生效参考:https://blog.csdn.net/u013256622/article/details/43703875
        1. 项目中是配置在`/etc/profile`中的(全局是这儿设置的,但是每次重新打开shell的配置是?)
            修改了/etc/profile的话,用source /etc/profile之后还是只对当前窗口生效,对新窗口不生效;似乎是因为打开新的shell调用的~/.bashrc(带验证)
            1. 最新实测,修改了/etc/profile的话,用source /etc/profile之后,还是只对当前窗口生效,对vscode的新bash shell和ubuntu的新shell都没有生效,但是重启vscode之后就变成新的了
        2. .bash_profile,.bashrc等的区别
    22. golang切片和数组的区别,`...xxx`是接收的切片还是数组
    23. type xxx func(* yyy)
    24. *和&的区别
    25. go get默认会显示是否更新,是否成功吗?
    26. exported type ICoordinate should have comment or be unexported
        1. 似乎是缺少某方法或数据
77. html 
    1. rotation

78. oracle
    1. sid是什么
79. mdn
    1. creatEvent
    2. 事件触发器
    3. 事件:https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events
80. qq
    1. 提取图片中的文字只有手机才有?

81. linux
    1. 执行source /etc/profile之后 用户名称由绿色变成白色了
    2. 递归创建目录
82. git删除远程分支后需要提交吗?其他人本地还有这个分支,操作会有什么影响?
83. to和for
84. ubuntu自带的"提取到此处"有问题?
85. 事件派发
86. OpenLayers 3 
    1. 之 动态点扩散效果:https://www.2cto.com/kf/201511/450555.html
    2. https://blog.csdn.net/qingyafan/article/details/45950125
87. git commit内容非常多之后怎么办
88. 区块链:
    1. 交易记录非常多之后怎么办
89. cpu和核心数,核心数和线程的关系
90. dom渲染顺序
91. GEOJSON等:http://www.maiziedu.com/wiki/json/geojson/
92. js获取js文件中的数据?
93. html document对象
94. canvas画图:https://www.w3cplus.com/canvas/draw-dashed-and-dotted-lines.html
95. 分辨率变化的时候矢量图会被重新渲染?
96. js
    1. 方法的声明不能在调用之后?
        什么情况下可以违背这个规则

97. 网页画图的几种方法,画矢量图用什么合适
98. 事件的几种写法
    1. 原生click和onclick的区别
99. jsDoc规范
100. 事件和观察者模式
101. json的语法和js普通对象的语法有没有什么区别
102. 什么是全拼和双拼
103. 打开csdn blog后cpu占用很高,是什么原因, 重启浏览器后打开相同的网页还是这个情况
    flash? 网页开太多了?设置了chrome的最新特性?
104. .pyc和.tmp
105. 苹果发布会的ar文件格式

106. git diff输出为空的问题
    note:默认没变应该是输出为空,如果权限变了会显示出来吗?(待测试),为什么看别人网上的可以显示出权限的变化,但是我的没看到权限的变化

107. golang
    1. `GOROOT/src/builtin/builtin.go`,这个包是干嘛的
    2. errors.New("xxx")
        1. 用该方式生成的相同的error相等吗
108. 坐标系的转换
109. webpak热部署
110. golang
    1. 通过index访问长度为0的数组和切片会报错吗,用`[0:]`呢
111. sqlite
112. sso
113. websocket
    1. 有订阅成功失败的状态吗
    2. 连接状态是返回一次还是连续不断返回?
    3. 切换页面websocket会自动断开吗

114. telnet
115. 博客:腾讯web前端coverguo
116. 自定义路书轨迹
    1. 最简单的,就是不用动画,只需要setPosition和画线就行了
    2. 参考:https://blog.csdn.net/projectno/article/details/78281689
117. js this的问题, 在func中this表示啥, 如果使用`var self = this`,此时self又表示啥,func使用箭头函数的话this又表示啥
118. 用什么数据表示三种状态比较好
119. js不存在线程安全的问题
120. js event loop
    1. 浏览器多线程和js单线程
    2. 阻塞等
        1. alert和同步xhr
            1. alert会阻塞异步代码吗,promise呢?
            2. xhr的原理
            3. 如何主动结束异步,主动实现类似alert的效果
    3. 外部js和当前js
    4. 浏览器的event loop,每遍历一个就会渲染一次?
    5. js同步和异步的优缺点和使用场景
    6. js异步编程的几种方式
        1. 哪些是可以阻塞的?哪些是可以主动停止的
        2. 异步事件加入的时间顺序是?
    7. setTimeout有最大等待时间吗;最小时间多少比较合理:30msor 50ms
        1. setTimeout的深度使用
        2. setTimeout中有多行代码的话需要再用setTimeout包裹吗,是顺序执行的吗
    8. setTimeout和setInterval的嵌套

    9. 异步的顺序不能保证?
    10. 如何主动把某个事件弄成异步的?比如路书中的`_addMarker()`方法,弄成完成后回调的那种
    11. 多个setTimeout之间的时间间隔是怎么算的?比如100ms,是前一个执行完后的一百毫秒还是跟前一个没关系?
        已解决:跟前一个执行的时间有关.如果没超出,比如前一个执行了20ms,那么再过80ms后一个就开始执行;如果前一个超出了,比如执行了200ms,那么执行完后后一个立刻执行.

121. 实现回调的几种方式
    1. 如何把普通方法弄成可以回调的?
    2. 如何修改event loop中事件的顺序?

122. angular数据异步渲染的优缺点

123. js如何一边遍历一边添加?
124. typedarray和普通array在语法上的区别
125. 网页动画的原理
    1. https://www.zhihu.com/question/20453427
    2. w3c关于动画的规范
    3. 网页动画实现的方式(不管新老):
        1. css animation
126. https://developer.mozilla.org/zh-CN/docs/Games
127. html的整个渲染流程:reflow等
128. https://www.w3cplus.com/svg/bear-animation-width-svg.html
129. 矢量图的数据比图片体积小
130. 【链接】百度地图自定义图标动画
https://blog.csdn.net/jifashihan/article/details/50460309
1. js
    1. var arr = new ArrayBuffer(16)
var typed = new Float32Array(arr)
var view = new DataView(arr)
view.setFloat32(0, 12.55)
view.setFloat32(4, 12)
console.log(arr)
console.log(typed[0])
console.log(view)
console.log(view.getFloat32(4))

为什么这里type[0]和view.getFloat32(0)不一样

1. js字符串转字符串数组,转arraybuffer
1. angular的那些奇葩写法的笔记,比如colspan要写成`[colSpan]`
1. angular mat和md
1. 重新学习sql并且认真做笔记
    1. 特别是典型的例子
1. golang json
1. ajax json
1. docker的学习:https://steamcn.com/t392743-1-1
1. 普通项目如何打包
1. vim
1. hydra安装方法
1. linux文件类型:比如d开头是目录,-是啥?
1. 百度地图精确到小数点后多少位
1. angular zone的文档
1. 要导出的js文件中使用ver,const等有没有什么影响
    1. 直接导出, 静态方法导出,实例方法导出的区别
        1. 要实现静态代码块或初始化该怎么弄?
1. linux热启动
    1. left join两次连接同一个表但字段不同会怎么样
        1. 要连一个表两次怎么弄?
1. promise走到某一步的时候退出怎么弄?
1. 廖雪峰的零基础JavaScript全栈教程:https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000
2. nginx;secureCRT;secureFX;
    1. 负载均衡:nginx后面的多个服务器
    2. 万金油高可用技术:keepalived所在的多个nginx
    3. 热备
2. shell脚本(一定要学一下)
    1. exit 0 和 1
2. vim
2. linux操作系统日志:var/log/messages
2. 哨兵
2. 各种协议
3. 通过这种方式来学习源码:自己写一个简易的springmvc,mybatis,tomcat
    1. tomcat时序图
1. angualr摇树优化
(change)和ngModelChange
    1. 网友说的是`change`写在前面则是未变的值,写在后面则是变后的值?:https://weibo.com/1880809571/E0wZXqPG2?type=comment
angular复选框的实践
arraybuffer和字符串的转换
字符串拼接效率
ftp服务器和web服务器
判断小数,正数,正整数等
css 父子 优先级
<td>中文字的换行
colspan 在第一行不生效?
页面权限
获取月初月末等时间
observeable转换为非observable
angualr 表单中:#,name等的区别

2. 那几个网站在线运行前端的例子
1. angular httpclient
    2. 使用 Angular Material 开发基于 Material Design 的应用:https://www.ibm.com/developerworks/cn/web/1506_chengfu_angularmaterial/index.html

        包含了响应式布局等很多知识,有空需要研究研究
    3. https://www.cnblogs.com/sghy/p/6951083.html
2. npx
    1. https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b
1. db
    1. add和create
    1. sql 的seq会回滚吗 
1. bootstrap为什么依赖jquery?内部实现用到js了?
1. goalng 类型转换:strconv.ParseFloat
    1. goalng模板
1. viewport做适配
1. 从package.json中删除
1. mac vscode占用内存很高
2. npm 符号链接
1. npm 创建的目录,为什么没有删除权限
1. 序列化的本质是什么,js中的 序列化又是什么
    1. 比如postMessage接受你放入它的任何对象，序列化它，将它发送给另一个web worker，
2. js
    1. 待整理:https://hacks.mozilla.org/author/lclarkmozilla-com/
2. oracle
    1. http://www.oraok.com/
    2. http://www.manongjc.com/oracle/pl-sql-tutorial.html
    3. https://my.oschina.net/u/587561/blog/96984
    4. http://www.bianceng.cn/Oracle/
2. vue
    1. https://segmentfault.com/a/1190000007825106
    2. vue ele-ui的栅格做适配很方便?
1. golang
    var buffer bytes.Buffer
	fileName := fmt.Sprintf("%s.xlsx", utility.GetGUID())
	c.commonLib.BuildXlsxData(data, header, fileName)
	f, err := os.Open(fileName)
	if err != nil {
		ctx.Errorf("打开文件失败:err:%+v", err)
		return
	}
	defer func() {
		f.Close()
		ctx.Info("删除文件：", fileName)
		os.Remove(fileName)
	}()
	buffer.ReadFrom(f)
	response.Content = buffer.String()
	response.SetHeader("Accept-Ranges", "bytes")
	response.SetHeader("Content-Type", "application/vnd.ms-excel.numberformat:@")
	response.SetHeader("Content-Disposition", "attachment;filename=卡片信息.xlsx")
	response.SetHeader("Charset", "utf-8")
	ctx.Info("返回结果")
	response.Success()

1. js判断是否是数值类型
1. blob,dataview,webgl,轮询
1. js有类型的概念吗
    1. js引擎能区分不同的基本数据类型吗

1. angular2-cookie@1.2.6 requires a peer of @angular/core@^2.0.0 but none is installed
1. SKIPPING OPTIONAL DEPENDENCY: node-sass@4.9.0
1. 从gitlab克隆的时候,如果是git协议就要输入密码(而且输入正确的密码后好像还是不对), 如果是http协议就不用,why?
1. node_modules的文件vscode 会跟追吗
1. guid的生成
1. goalng中""是null吗
1. vscode 中go怎么自动导包
1. tslint
    1. while statements must be braced (curly)
2. google chrome helper是什么,导致mac发烫
1. @next是什么版本
2. package-lock.json对跨平台有影响吗
2. npm install默认的规则是什么样的, 会默认覆盖吗还是?
2. node-sass
2. Unable to save binary /Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/node-sass/vendor/darwin-x64-57 : { Error: EACCES:permission denied, mkdir '/Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/node-sass/vendor'
    at Object.fs.mkdirSync (fs.js:885:18)
    at sync (/Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/mkdirp/index.js:71:13)
    at Function.sync (/Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/mkdirp/index.js:77:24)
    at checkAndDownloadBinary (/Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/node-sass/scripts/install.js:114:11)
    at Object.<anonymous> (/Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/node-sass/scripts/install.js:157:1)
    at Module._compile (module.js:652:30)
    at Object.Module._extensions..js (module.js:663:10)
    at Module.load (module.js:565:32)
    at tryModuleLoad (module.js:505:12)
    at Function.Module._load (module.js:497:3)
  errno: -13,
  code: 'EACCES',
  syscall: 'mkdir',
  path: '/Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/node-sass/vendor' }


2. gyp ERR! stack Error: EACCES: permission denied, mkdir '/Users/xushike/work/src/wlwk/wlwk_admin/wlwk_admin_web/node_modules/node-sass/build'




1. http://www.wutianqi.com/?p=3686
1. sql
    1. varchar2和varchar
    2. 如何查看长度单位
    4. 数据库索引是什么东西
    6. 换行符和空格会原样取出来吗
    7. 框架自动转换?
        ```golang
        map[string]interface{}{
            "count": r,
            "list":  list,
        }
        ```
    8. oracle的日期操作,比如月份的增加减少

1. npm
    1. 查看某个库的版本号
    2. 错误和警告
    3. darwin等

1. to_char和to_date

1. yyyyMM和yyyymm等
1. github博客系统

1. 项目中
    1. `DateUtility.toString`和`DateUtility.toUTCString`
    2. 使用字符串类型的枚举为什么会报错
    3. 为什么日期要转换这么多次

1. ng-template和ng-if比会增加渲染效率吗

1. overflow:auto
    1. 以及和各种scroll的关系

1. golang
    1. interface型的0和0比较的结果是啥?int型的interface和0比较呢?
    
1. 签名是什么
1. 如何把axure弄成局域网可看的
1. 学习看代码和源码
1. js == 和 ===
1. 为什么文件夹叫assets

1. vue
    1. https://www.cnblogs.com/itbainianmei/p/7826742.html
    2. https://blog.csdn.net/sinat_17775997/article/details/75950356
    3. https://blog.csdn.net/u012317188/article/details/74989692
    4. https://segmentfault.com/a/1190000009192118

2. 路由策略
2. console.log多参数的 写法
2. let's make more time
2. 日期的协议和各语言的标准
2. webpack的设置,比如打印出日期信息等
2. if else和switch在语言底层的实现
2. TMP.htm是什么
2. 如何直接打出换行符.比如在git commit - m ""中使用换行符
3. 笔记:

    //计算字符串长度(中文2，其他1)
    getStringLenth(str: string) {
        let len = 0;
        for (let ch of str) {
            if (ch.match(/[^\x00-\xff]/ig)) {
                len += 2
            } else {
                len += 1;
            }
        }
        return len;
    }
    1. https://blog.csdn.net/fengziyun/article/details/7889262

2. 路由策略
3. <meta name="viewport" content="width=device-width, initial-scale=1">
3. 富文本编辑器
3. 渐进式和函数式
2. linux 文件名带反斜杠的bug
2. 防止重复点击
3. 复制粘贴会触发onkeyup等吗

1. css
    1. 小型布局的灵活切换,比如让div变行内,让div中的元素右对齐...
    2. 哪些属性对块级元素生效,哪些对行内元素生效
    3. 宽高什么情况下是固定,什么情况下是变动的
    4. 格式化css的插件
    5. ...

        ```
        -webkit-margin-before: 0.83em;
                -webkit-margin-after: 0.83em;
                -webkit-margin-start: 0px;
                -webkit-margin-end: 0px;
        ```

2. angular
    1. http://lovepeng.gitee.io/angularbase/#/demo/index
    1. `    providers: [
        { provide: MD_PLACEHOLDER_GLOBAL_OPTIONS, useValue: { float: 'never' } }
    ]`
    2. https://blog.csdn.net/qq_24078843/article/details/78560556

1. web worker
1. 参考该页面的样式:https://www.cnblogs.com/bndong/p/6743524.html
1. encodeURIComponent和encodeURI,以及location.hash,URL中的#
    1. 参考:https://www.cnblogs.com/season-huang/p/3439277.html
    1. encodeURI方法不会对下列字符编码  ASCII字母、数字、~!@#$&*()=:/,;?+'

        encodeURIComponent方法不会对下列字符编码 ASCII字母、数字、~!*()'

1. url请求的 param 支持 哪些字符
1. 地图引擎
1. 高斯平面
1. 各种export,class和module等
1. promise并发
1. js回调地狱
1. js中实现异步编程的四种方式
1. 拦截器
1. 轮子哥:一定要把group by、partition和index的各种神奇用法搞明白
1. css怎么知道该选哪个颜色这些?
1. https://tieba.baidu.com/p/5165634082?red_tag=2983262444
1. js断点调试方法
2. c++等的析构函数
1. js的class和func的原型链 的关系
    1. `export new Api()`;
1. typescript static
1. js Date的处理:比如获取月初,月末等
1. package-lock.json
1. vue ,main.js,index.html和app.vue的关系
1. HTTP请求方法:GET，POST，HEAD等的区别
    1. w3c规范:https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html

2. HTTP访问控制(CORS):https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS

2. js线程,主线程,ajax线程,alert,Service Worker
2. js的try catch

1. ajax,promise,rxjs等的关系
1. http,file,ftp等协议的使用场景
1. golang的def是什么意思;有可选参数吗
1. virtual DOM和angular渲染的区别,如何自己实现

1. golang各种类型的转换,一定要弄明白
    1. golang类型断言
1. golang 声明了返回string,但是没有给值,会有个默认值?
1. go 双重for循环中内层的break是退出内层还是所有层
1. go如何获取map中的值
1. go interface{}和interface{}{}
1. js json相关的 研究
1. map等可以中断吗,详细研究研究
1. angular template占用什么资源?
1. color 和background-color,前者都是指的文字颜色?
1. js:如果把对象中的引用传过来并修改了,会影响对象吗
1. ajax
1. bootstrap vue
1. web worker
1. 研究下项目中Util的写法并用到vue中
1. viewport;html和css渲染;华尔街golang
1. 基于nodejs、Vue实现服务端渲染
4. go编写闭包
5. go的指针
6. go数值常量
```go
const (
	Big   = 1 << 100
	Small = Big >> 99
)
```

8. 事件冒泡

19. 获取事件的几种方法：
    1. 原生的js似乎只能遍历所有属性来判断
        1. http://blog.csdn.net/theforever/article/details/6029382
    2. google  chrome dev tools 中`getEventListeners(document.querySelector("table tbody tr td span"))`，但只能在浏览器中用
        1. https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference?hl=zh-cn
        1. http://blog.csdn.net/diquren/article/details/50543610
        2. 有没有办法在js中调用呢
        4. chrome 的开发者工具有此功能。选取元素后可以在右侧的 Event Listeners中看到绑定的事件
    3. jquery保存了事件的委托，可以获得
    4. Visual Event 2
        1. https://stackoverflow.com/questions/446892/how-to-find-event-listeners-on-a-dom-node-when-debugging-or-from-the-javascript
    5. 当时的业务场景是点击table一行的任意地方（除了超链接这些）会选中此行，后面我用event.

20. dispatchEvent 
21. web调试优化:https://segmentfault.com/a/1190000011868916
22. chrome控制台console：https://segmentfault.com/a/1190000002511877
24. https://www.cnblogs.com/yexiaochai/p/3567597.html
29. oracle日期相关操作
31. dom l3
33. https://ng.ant.design/#/docs/angular/introduce
34. https://zhidao.baidu.com/question/429999513428017812.html
35. https://material.angularjs.org/latest/demo/virtualRepeat
36. 软件设计的一些理念规则：比如开闭原则。。。
25. js事件详解:https://segmentfault.com/a/1190000005016813

38. 异步查询，动态显示搜索结果

43. restful
44. libreoffice显示目录

45. 代码生成器和项目命名规范
46. not all go tools are avaliable on the $GOPATH
48. 递归查询和插入
49. oracle的价格
50. 项目中的*号和go的星号和angular的星号
52. oracle函数：
	CREATE OR REPLACE FUNCTION wlwk_f_split(p_str       IN VARCHAR2,
                                       p_delimiter IN VARCHAR2 default (',') --分隔符，默认逗号
                                       ) RETURN split_type IS
  j        number := 0;
  i        number := 1;
  len      number := 0;
  len1     number := 0;
  str      VARCHAR2(1000);
  my_split split_type := split_type();
BEGIN
  len  := LENGTH(p_str);
  len1 := LENGTH(p_delimiter);

  WHILE j < len LOOP
    j := INSTR(p_str, p_delimiter, i);
  
    IF j = 0 THEN
      j   := len;
      str := SUBSTR(p_str, i);
      my_split.EXTEND;
      my_split(my_split.COUNT) := str;
    
      IF i >= len THEN
        EXIT;
      END IF;
    ELSE
      str := SUBSTR(p_str, i, j - i);
      i   := j + len1;
      my_split.EXTEND;
      my_split(my_split.COUNT) := str;
    END IF;
  END LOOP;

  RETURN my_split;
END;

65. oracle里我之前写那个，如果把agent_id写到里面和写到外面有什么区别？效率上来讲？先筛选再连接是不是更快?
67. js遍历对象和遍历数组等

68. 我们项目中，getFirstRow和scala和getrows等的区别，以及获取回来的值的获取方法？

72. go get显示copy状态
73. linux文件安装在什么位置比较好

76. go里的 interface{}
    1. recover()和匿名函数
    1. goinaction说的类型的状态是什么意思
    2. 将方法的接收者声明为指针有什么好处？维护接收者值的状态？
    3. vscode如何跳到上次的位置
    4. go http的默认超时时间
    5. 终端的管道语法和&&
    6. teamviewer操作
    7. angular笔记
        1. ngmodel、value等还需要熟悉
        2. 可以甲乙双绑，然后乙丙单帮或者其他吗
        3. 表单的各种类型
77. go不能调存储过程
78. plsql修改函数要这样：`CREATE OR REPLACE FUNCTION`?

84. oracle查询中如何停止
85. angular各种组件的封装
86. oracle中''和null一样？而且可以赋值给各种类型？

87. oracle 
    1. 项目里Scalar等各用于什么情况
    1. 分页的研究,为什么里面也需要排序?
    2. 普通查询需要事务吗
    1. 开发发货记录中`t.order_no = nvl(null,t.order_no)`中，如果order_no在表中的定义为可为空，那么这句就查不出东西，这是什么逻辑？
    新的写法： `&t.employee_id = @id`?
    目录是：`lib4go/db/ tpl/ tpl.analyze.go`
    2. 各种操作，比如单位转换
    3. 分组,各种函数等
    4. 日期插入和各种格式变换
    5. left join等出错时多查出数据是什么情况
    6. 如果a表有两个employee_id(意义不一样),连employee表是连几次?
    7. 什么情况下会用到右链接
    8. 左链接的时候,如何先筛选左边然后链接?
    9. 多人同时操作的时候，是怎么保证一致性的，像线程那样锁住？
    10. 同时操作多条数据，比如插入多条、修改多条
    11. plsql的sql语句中0和‘0’一样吗

89. linux如何查看某个软件的版本和所有支持的命令
90. linux蓝色的目录是什么gui

92. js的date可以直接加减而自动判断出月份?
    项目中js date的封装

94. angular中组件绑定中不能使用下划线?比如`start_time`和`startTime`
95. 切片数组的合理创建方法

100. js
    1. 中的`||`和`&&`,在判断空和true、false时的用法一样吗？多个连接的时候如何判断？
    2. ""和null
        似乎不等,但是`!""`为true
    3. js的1和“1”以及ts的1和“1”
    4. 如果删除某个对象的属性
101. ts
    1. number太大了变成e+的怎么办
        目前代码中似乎是用字符，然后正则表达式验证，而不用number类型

102. angular
    1. 组件自身可以通过`[组件名].value`来获取绑定的值，为什么其他组件不能这样获取
    3. ngmoudle和value的关系
    6. 设置某个组件只能看不能改

103. 银行卡钱不够了会怎么样
104. `||`和`&&`的多个连接是什么算的
106. linux任何管理器和强制关闭某程序，以及温柔关机
107. linux`clear`可以清空命令行,而ctrl+L不行
108. liux如何命令行中打开图片，以及像mac那样命令行和文件夹互相打开
109. go如何进入引入的包里查看代码
110. linux如何递归查询目录里是否有某个文件
111. 如何防止sql注入攻击
112. 谷歌服务很费电怎么办
113. scp可以复制到多个目录吗
114. rpc
115. 瞅字由贬义吗
116. golang for range 中除了index和element，还可以像if那样再声明其他变量吗
117. varchar2和varchar
119. `pwd`等命令会在结尾的时候加上换行符,有时候会不太方便,怎么去掉
120. 小米wifi后面的符号怎么弄的,搜狗等怎么输入滑稽符号
121. 移动基站到底是什么样的
125.  字元
126. 如何定位到光标的位置,vscode回到上一次光标的 位置
127. git新建分支和推送分支等操作
128. oracle中`''`和`num`在查询时一样吗
129. 破解接口怎么办?
130. html标签里这种`style="color:red;"`,结尾处的冒号有什么好处
131. js中新建之后没有声明类型和值,默认是string类型?
132. js forEach效率和最好的遍历
    1. js 的foreach是有序的吗
    2. 默认的变量是undefined?
    3. 默认的字符串也是undefined?
    4. js中传一个方法给另一个调用效率如何
    5. js临时环境搭建

133. `don't use underscores in Go names; var card_num should be cardNum`
145. axure
146. 图片后缀名的大写和小写会影响显示？比如代码里是jpg，但是图片实际是JPG，这样本地显示出来了，但是线上显示不出来。
147. es5的`export class StringUtility...`和`export function format`
148. linux的install.log
150. linux多个root登录会怎么样？
151. windows中按时间排序,批量修改和复制移动等等.
152. 生产者消费者和订阅的区别
154. oracle多个and和or
158. TSlint
159. x7f-xff中的￥
160. js string默认取值是什么
161. 主从高可用
162. go grpc为什么啥不用
163. 在各种语言（js等）的map()等lambda表达式中return的话只会退出lambda？
164. 没有primarykey,可以插入重复数据吗
165. go有序列化吗

167. js的map和foreach

169. 
```

    //选择运营商产品
    carrierProductChange(f) {
        let form = f.value;
        console.log("form:", form)
        if (form.up_product_id != "" && form.carrier_pool_name != undefined) {
            this.carrierProductList.forEach(pro => {
                if (pro["up_product_id"] == form.up_product_id) {
                    this.carrier_pool_name = pro["product_name"]
                    return
                }
                console.log("第三层")

            });
            console.log("第二层")
        }
        console.log("第一层层")
    }
```
并没有真正return,每次这三层都会打印,如何在return时真正退出方法?其他语言的情况?

171. angular和react中没被渲染(比如隐藏、ngif为false)的组件能被获取到吗，能修改值吗
172. angular不推荐通过dom的方式修改htmml的值?那如何修改其他ngmodel的值（不用数据绑定）
173. typescript的as感觉很有用，转换成原生js后是什么
174. js && 中可以用赋值语句吗
175. angular中number类型的input的max绑定变量没有生效是什么原因。
176. 
```javascript
	ngAfterViewInit(): void {
		if (this.isAdd) {
			this.upChannel.valueChanges.subscribe(
				res => {
					if (res) {
						this.http.post(AppSettings.apis.queryProductListByChannelID, { up_channel_id: res }).subscribe(
							res => {
								this.upProductList = res
							}
						)
					} else {
						this.upProductList = [{}]
					}
				}
			)
		}
	}
```
175. 感觉我的mac写ts还需要一些插件,明明没问题却总是报错
176. package.json的学习

178. http2.0和js模块化

    [https://zhuanlan.zhihu.com/p/26118022](https://zhuanlan.zhihu.com/p/26118022)
179. 悲观锁和乐观锁
180. angular中,如果使用了双向绑定,组件ngif消失了再出现,此时的绑定是?如何让他消失的时候绑定也清除?
181. ie的适配,angular的例子
182. google Development tools
183. js lambda从es6开始的?
184. angular2的单双绑定的写法总结
185. 换成ngAfterView和@viewchild的写法；以及formControl的onchange()方法可用否
186. upload在localhost的情况下传不上去是什么情况?但是在192.xxx就可以
187. typescript对象的属性获取要加get和()?
188. xshell
189. 工单设置完之后停留在当前页？
190. 卡片工单管理里增加按工单状态等筛选
191. 当前项目中引入的dic的服务的注解是Injectable，代表什么
192. angular construction中的参数如果是异步获取的 ，会等获取完后生成吗?比如dic
    异步方法如果写在construction里面会怎么样，会影响加载速度吗

193. 项目中的table能根据每列单独排序吗？
194. js中遍历数组是有序的吗
    java和go呢?
195. oracle to_char()   
194. 类成员不可用const关键字?
195. plsql工具的笔记
196. 为什么要用框架
197. md可以写流程图吗
198. 如果调用angular特有的onModuleChange()，那么在组件初始化的时候会触发该方法吗？

203. 这个闭包的意义是什么,不写闭包好像也可以直接执行

    以及为什么本地看不到这个百度商桥

    ```html
    <script> 
            var _hmt = _hmt || []; 
            (function() { var hm = document.createElement("script"); 
            hm.src = "https://hm.baidu.com/hm.js?af089629a31007e7e029023df7b214a0"; 
            var s = document.getElementsByTagName("script")[0]; 
            s.parentNode.insertBefore(hm, s); })();
        </script>        
    ``` 

206. 手机和电脑如何截长屏
208. 研究下项目中subscribe的写法
209. 后端go中各种fmt和返回输出，错误等的写法

211. 如何判断子组件的状态
212. 阿里云等网站是怎么做的,学习

214. 幂等的:Idempotence
215. js等的实例演示gif生成
216. [http://www.01happy.com/golang-err-is-shadowed-during-return/](http://www.01happy.com/golang-err-is-shadowed-during-return/)
217. linux vscode不显示下划线
218. plsql dev快捷键和技巧
219. js中 && 和大小与的优先级
220. oracle的模糊查询用`%`为什么没有生效

221. 额

```typescript
let val = input.card_id
        for (let index = 0; index < this.dataList.length; index++) {
            if (val == this.dataList[index].card_id) {
                //
                console.log("found item:",input)
                if (checked) {
                    this.dataList[index].checked = false
                } else {
                    this.dataList[index].checked = true
                }
            }
        }
```
当input没有card_id的时候，循环里的判断会一直成功？


222. angular textarea的cols没有生效的原因
223. oracle一直显示正在执行


227. js引入的模块没用的话会占用性能吗/
228. ngmodule单独写的作用是什么， 
229. [https://valor-software.com/ng2-file-upload/](https://valor-software.com/ng2-file-upload/)
230. 将项目表单的验证写成服务
231. 咨询公司lc牙医是否可报
234. angular在表单组件上双绑某个值和事件，那么值会先变化然后触发事件？
235. ngModel和ngvalue,以及[ngModel]几者的区别，以及name
236. app.module的和page.module的区别
237. 看看别人优秀的angular代码
238. angualr的disabled
239. 限制某些框输入的小数位数.
240. ngValue，ngGroup

242. select 有绑定值时，想绑定一个空值用。。。没有绑定值时默认是第一个。。。
243. 为什么声明了`#downCardType`还是不能在ngif中获取它的值呢？
245. 如果把ngif的值的绑定到模板引用变量，会很慢，但是绑定组件中的值则不会。。。

    还有个问题就是，如果是多层判断，那么后面的不会生效。如，
    ```
    <tr *ngIf="downCardType.value == '40'">
                    <td class="col-name">
                        <em class="required">*</em>虚拟池：</td>
                    <td>
                        <select name="is_create_virtual_pool" [ngModel]="1" #createVirtualPool="ngModel">
                            <option value="1">追加</option>
                            <option value="0">新增</option>
                        </select>
                        <span *ngIf="createVirtualPool?.value == 1">
                            <select required name="virtual_pool_id" ngModel #virtualPool="ngModel">
                                <option value="">----所有----</option>
                                <option *ngFor="let item of virtualPoolList" [ngValue]="item.virtual_pool_id">{{ item.name }}</option>
                            </select>
                            <span class="error" [innerHTML]="getErrorFor(virtualPool)"></span>
                        </span>
                    </td>
                </tr>
                <tr *ngIf="downCardType.value == '40'">
                    <span >hi{{createVirtualPool.value}}</span>
                </tr>
                ```

                246. ngModelChange何change

246. 什么样的产品可以放放同一个池子？
247. js 的any类型可以这样赋值`a.xxx=xx`，但是对象只能这样赋值`a["xxx"]=xx`？
249. 项目中的前端代码生成了新的之后发布到线下服务器不用强制刷新页面就能获取吗?我当时先启动的后端,然后生成 的前端,结果没用生效,强制刷新也没有用;然后先复制好前端再启动后端似乎就行了.(待测试)
250. ts中这样写为什么报错
```typescript
var arr = [{ name: "wang", age: 3 }, { name: "wang", age: 4 }]
for (let [i, item] of arr.entries()) {
    console.log("item:", item)
}
```

252. 局域网能访问localhost启动的服务吗
    在虚拟机里，如果开启了虚拟机的防火墙呢

253. 没有登录能访问api吗

255. 查看linux内存占用状态

260. angular表单提示，可以做成侧边那种吗

        有没有经典的现成例子

263. angular2渐进式编程.
264. 自定义指令和系统指令一样的话，默认用哪个
265. markdown流程图
266. oracle时间转换为天
267. js中各种遍历的比较：[https://www.incredible-web.com/blog/performance-of-for-loops-with-javascript/](https://www.incredible-web.com/blog/performance-of-for-loops-with-javascript/)

    结论似乎不准确,还有一点就是for of entries()方法效率似乎比较低,总之最好别用
268. 我们项目的ts编译后是es5还是什么

270. js到ts:[https://segmentfault.com/a/1190000010774159](https://segmentfault.com/a/1190000010774159)
271. 深入js的for of:[http://www.jb51.net/article/70106.htm](http://www.jb51.net/article/70106.htm)
272. linux删除后的撤销
273. es6展开运算符
274. angular json的管道怎么用
    
    在代码里用管道
275. 项目问题

    1. constructor中注入的服务比如dic,可以直接用dic,不用加this;但是在方法外面必须要加dic?
    2. 项目中的系统繁忙500错误,通过什么获取
276. 研究下word等的`1.`,`2.`
277. 熟悉下ng 时用到的js插件
278. angular transform的源代码,和项目中ydj写得的区别
    1. 项目中`{ title: "完成时间", field: "finish_time", pipes: { date: "MM-dd HH:mm",placeholder: "---" } },`这样写可以多重管道?
279. css里夫优先还是子优先?
280. 不同的指令和组件加到不同的地方,具体记录
281. ts中只定义未赋值的值是undefined,js中也是吗
283. 带_的私有变量是那个语言的语法
284. console.log多参数的写法
290. 一键部署和发布(线下)

293. 管道多参数的写法
294. oracle nvl 以及项目中的&写法,以及oracle的空不等于空的问题如何解决
    1. `u.down_order_no = nvl(@down_order_no, u.down_order_no)`和`@order_no is null or o.order_no = @order_no`
    2. 当有外链接其他表的时候不要用`&`这种写法,因为两个表可能会有相同名字的字段,这样就识别不出来了.
    3. ''和null相等吗,is null判断''呢?
    4. 连接查询的时候,把连接查询的条件放在where前面和后面有区别吗?

295. js的isNaN()对于''
296. `ng-container`和`ng-template`的区别
    1. 默认情况前者里面的内容会被渲染出来,后者不会
    2. 前者可用*指令,后者不行?
297. angular中如何层级设置样式/
298. ul中可以放div吗
299. js
    1. 一个ts中可以放多个`export class xxx`?
    2. const一定要放在`export class xxx`的外面?
    3. 0和'0'的可以直接转换吗
        1. 是不是除了0以外,其他数字和对应的字符串可以用==比较?
300. 项目后台
    1. 方法外设置了status,方法内直接返回err,会怎么样?
    2. 笔记:`err == context.ERR_DataNotExist`表示数据不存在
    3. 需要把错误信息展示给用户的临时方法是:后台把`err_msg`放在success中,`response.Success(map[string]interface{}{"err_msg": "获取代理商产品数据失败"})`
301. 最后那个项目还没看,腾讯视频搜索:TypeScript，Angular，和移动端跨平台开发
302. 公司项目
    1. 前后端api的命名和restful的关系.
        1. 根据RESTful来调整api的名称?
    2. 上有产品和下游产品,代理商的关系
    3. 虚拟池的类型是由下游卡类型决定的吗
    4. 规范所有池的命名?
    5. 不可点击时增加鼠标标志
    6. go的map返回到前端是什么?切片在js中相当于数组用?
    7. 划拨的时候卡片类型就相当于虚拟池类型?
303. js
    1. 如果js比较(比如大小的比较)两边有一边为undefined,会怎么样
    2. js for of跳出循环
        1. 用return不仅跳出,而且终止所在的方法
    3. js调试
304. 笔记
    1. 公司项目前端里,当变量实际类型是number型的时候是不能调用`match()`方法的
    2. js里string类型乘以数字会变成number类型.
305. vscode搜索类名等的快捷键
306. MDN中for of中的let和const有区别吗
307. [从 Node 到 Go：一个粗略的比较—GO平均性能比JavaScript快十几倍](http://ourjs.com/detail/59d475953506837194998ad2)
308. 如何利用git的工作流等来方便工作
309. go按字符分割切片
310. a(b())
    当b执行return()时,各种语言的表现都一样吗

311. 对于GPRS,放在类名里,用Gprs还是GPRS?用在目录名呢?
312. go

    ```golang
    type CardInfo struct {
        CardID string `json:"card_id"`
    }
    ```
    这种写法的意思?

    2. `[]model.CardInfo{}`后面这个大括号是语法要求加的吗?
    3. `[]byte(xxx)`?

313. oracle
    1. 哪些情况下inner join和left join一样??
    2. group by 表达式

314. 我们项目前端对ie的支持怎么样,能不能支持ie8以后的?

    1. 其他的框架呢?
315. 项目
    1. getStirng可以去获取number吗
    2. 自定义错误的错误码有没有大概的规则
316. 点击链接的时候光标转圈圈是自动的吗?
317. 模态和非模态
    1. [态和非模态对话框的区别](http://blog.sina.com.cn/s/blog_752af88e0100wyn1.html)
    2. [JavaFX实现一个简单的模态窗口](http://blog.csdn.net/chenweionline/article/details/5035936)

318. 大牛说的:Swift 和 Kotlin 很像
319. [【码云周刊第 58 期】打包巨慢怎么办？这些工具让你爱不释手！](https://my.oschina.net/gitosc/blog/1615755)
320. findIndex是es还是ts的方法
321. go升级到1.10
322. 杨哥说的总结 的规范是啥
323. issue如何理解
324. [使用 Sourcegraph 更好地搜索和浏览 GitHub上的代码](https://zhuanlan.zhihu.com/p/27620085)
325. 学会使用`go generate`

    go generate是一个你可以用来自动自成Go代码的命令。你可以结合例如jsonenums(一个用于为枚举类型自动生成JSON编组样板代码的类库)这样的元编程来使用go generate快速自动实现重复乏味代码的编写。在Go标准类库里面已经有大量可以用于解析AST的接口，而AST使得编写元编程工具更简单，更容易。

326. [五步让你成为GO 语言高手](http://www.jb51.net/article/62728.htm)

    开始以为是标题党,看了才发现应该不是...
327. 如何在编译器中打开go等的源码
328. go实现对gitbook文件内容的排序

    对文件做拷贝、打印、搜索、排序、统计或类似事情的程序都有一个差不多的程序结构：一个处理输入的循环，在每个元素上执行计算处理，在处理的同时或最后产生输出。

329. hash的原理到底是什么

    go语言圣经:对hash结构的遍历顺序是无法保证的(即随机的)
330. github gist
331. [github指南?](https://services.github.com/index.html)
332. linux
    1. 向标准错误流输入了东西之后如何看到?可以看到之前的吗?打印到标准错误流有什么用?

334. `ifconfig.me/all`
335. `noscript`
336. png和jpg可以直接修改后缀名转换吗?用go圣经中的转换有何不同?jpg和jepg的区别,以及mp4和mpeg4等
337. PopCount的原理和实现
338. 年龄一般是虚岁,实岁还是周岁?
339. linux什么样的文件才需要x权限?可执行二进制还是所有?
340. linux如何查看启动的进程和关闭?
    1. ps ax | grep xxx是什么
    2. 如何查看文件安装目录
    3. `status`命令是干嘛的,检查服务的状态?
    4. (所有者）×××（组用户）×××（其他用户）

        这几个的区别
        1. 如何修改文件的权限
    
341. linux中如何递归搜索文件目录
342. linux中直接执行`shutdown`会在一分钟后关机?

343. [利用K8S技术栈打造个人私有云（连载之：K8S集群搭建）](https://my.oschina.net/hansonwang99/blog/1616599)
344. innerHTML表示啥,dom结构?值还是?
345. csv和excel
346. ng-container直接包裹文字会被渲染成什么,span or 什么都没有?

347. oracle

    1. 对于`insert into xxx (...) select @xxx from c`,其中`@xxx`可以不是c的字段?此时相当于直接插入`@xxx`?其他sql语言也是这样吗/
    2. id等用varchar和number的区别

348. 扫MQ和扫数据库的区别是啥?

    直接扫数据库如何?

349. tooltip,title和hover等的区别和使用环境

    1. 项目中的mdtooltip需要引入,后面再改吧
    2. 哪种是可以复制的?可以复制的话应该更好吧
    3. [CSS3实现漂亮ToolTips效果](https://www.imooc.com/learn/331)

350. [用于提供审查、性能度量和渐进式网页应用最佳实践。](https://github.com/GoogleChrome/lighthouse)
351. Lighthouse 项目的一个分支名称为 add-a11y-tests。你认为这是一个用于特性分支的好名字吗？ （提示 - a11y 代表"accessibility"。在"accessibility" 中，a 和 y 之间有十一个字母，所以缩写为了 a11y！）
352. 如何做一个这样的博客:[大漠穷秋的github](https://damoqiongqiu.github.io/)

353. `background-color`和`background`
354. `:before`和`:after`的用法
355. `perfect-scrollbar`滚动条
356. js获取日期的前一个月?

    getDate()-30?

357. 在js or ts 中加`debugger`字段的调试方法?
358. 项目中select选中后的长度改变

    比如邮费那儿,当字段太长的时候选择出来就只能显示部分字段

359. [成都公租房租赁补贴开始申请 最高补贴100%](http://cd.qq.com/a/20180301/004785.htm)

360. zookeeper的配置是什么意思
361. go中错误的最佳实践

    如果err有很多层,怎么判断是从哪层传过来的?
362. ts里在变量名前面加`_`和后面`_`有没有什么特殊意义
363. hadra启动命令行的`-d`和`-w`等的意义
364. wlwk_merchant项目本地前端启动的特殊性
    
    必须先非本地启动的方式获取session_id然后保存为固定的,然后才能以固定的session_id本地启动

365. `link`标签是干嘛的,css放的位置
366. oracle
    
    1. `column ambiguously defined`
    2. `not a GROUP BY expression`
    3. `date format picture ends before converting entire input string`
    4. `ORA-00907`怎么看的
    3. 用`as`重命名为已有的字段名会怎么样,会不会有问题?
    2. number类型和date类型的相互转化
    3. number类型和日期类型的使用环境
    4. oracle的分页要仔细研究研究
    5. plsql中''和null相等吗

        实测是相等的
    6. group by可以用nvl,但是不能用decode
    7. 待笔记

        1. plsql中当前日期是大于当前月份的

367. 待笔记
判断输入的空字符是否为null的时候,结果为true;判断是否为'',也是true,而且直接比较`null`和`''`好像也是相等的

367. 数据库报表的设计和sql调优

    感觉这方面还需要去看不少的书和实战才行
    1. 数据库分片
    2. 如果数据量很大,每次的数据怎么生成?单独为报表做一张表?

368. vscode修改文件后的working tree是什么意思
367. 项目中go每个api的公共部分的意义吃透
368. to_char和to_date可以混用吗
369. 光标变成那种没写一个就删除右边一个的时候,按`insert`键就可以恢复?
370. 中午的时候看下销售报表
371. 项目中使用的是`https://material.angular.io/`
372. 任务调度系统,数据库的job
373. 原生css支持驼峰写法吗?比如`background-color`=>`backgroundColor`
374. 虚拟机死机如何强制唤醒
375. 学习Ajax
376. element-ui,echarts,charts;推荐前两者,文档比较完善

    [https://naver.github.io/billboard.js/](https://naver.github.io/billboard.js/)

377. js `isNaN`
378. line-height
379. 文字放在图片的右边的总结
380. svg的使用
381. 项目中的`DateUtility`等几个工具类有空研究下
382. 不知道在angular单页面应用中是否有效:[三种方法能够确定浏览器窗口的尺寸](http://www.w3school.com.cn/js/js_window.asp)
383. 项目中select中内容的排序
384. 项目中input的长度等限制
385. oracle的rownum要好好研究下
    1. 以及`rownum <= @card_count`这种写法,是不是一定要加上小于

386. 项目中css没有生效的研究

    偶尔出现的bug还是?

387. js和go的各种格式化
388. css布局
389. sum over() 不能和group by一起用?
390. ubuntu `whereis`
391. package-lock.json作用
393. 源文本中存在无法识别的标记

    @angualr/cli
394. import 后面那个带`-`,以及default是什么意思
395. saas
396. webpack的unchanged chunks是什么
397. 研究下这个`https://stackblitz.com/edit/angular-material2-year-picker?file=app%2Fapp.component.html`的实现

    https://github.com/angular/material2/issues/4853

398. bootstrap的日期控件,可只选月份:https://eonasdan.github.io/bootstrap-datetimepicker/Installing/
    1. angular2 可选:https://github.com/atais/ng2-eonasdan-datetimepicker/issues
    2. https://www.npmjs.com/package/ngx-eonasdan-datetimepicker
    3. (当前使用的):[https://github.com/vlio20/angular-datepicker](https://github.com/vlio20/angular-datepicker)
    4. 待研究:[https://musthaan.com/2017/08/28/month-picker-in-angular-2/](https://musthaan.com/2017/08/28/month-picker-in-angular-2/)
    5. 未看:[http://www.liuchungui.com/2016/10/22/bootstrap-datetimepicker%E9%9B%86%E6%88%90%E5%88%B0angular%E4%BD%BF%E7%94%A8/](http://www.liuchungui.com/2016/10/22/bootstrap-datetimepicker%E9%9B%86%E6%88%90%E5%88%B0angular%E4%BD%BF%E7%94%A8/)
    6. 未看:[http://blog.csdn.net/bluefish_flying/article/details/75244620](http://blog.csdn.net/bluefish_flying/article/details/75244620)
399. github gist
400. flex布局
    1. 似乎可以很好的跟`ng-content`配合
401. 数据库的知识要好好补一补
    1. 三表查询

402. 用来展示demo的网站:stackblitz.com/
403. 普通的sql中可以声明变量吗
404. yarn 和 angular的关系
405. angularUI库的研究:[https://segmentfault.com/q/1010000009405513]
406. 什么样的查询会使表锁住
407. windows ng serve & npm start
408. 析构函数
409. 三大运营商是怎么算短信长度的,中英文一样吗?一条短信最大长度是多少?
410. qq消息是自动同步的吗?还是不同电脑上有不同的记录?

412. plsql 的rowid和rownum区别
    1. 在sqldeveloper中,只有查出rowid才能修改

413. 现在不写存储过程了?
    1. 存储过程和sql的比较
    2. 存储过程的原理,如果有很多判断什么的,效率会低吗?
414. update可以left join吗
    1. query的时候,如果字段没有获取到会报错吗,还是返回null?

415. golang input,interface和map,slice,json,int等的转换
    
416. res的值是啥,如果操作了条返回啥
    1. 数据交换时的数据类型

417. js中有go的那种格式化打印方法吗
418. golang
    1. map[string]interface{}{}中取值只能写成`input["xxxx"]`而不能写成`input.xxx`?其他获取方法呢?
    2. go判断数据类型
    3. interface类型如何和其他类型比较?go 有类型声明吗?
    4. 项目中待研究代码
        
        ```go
        //Convert2Int 转换为int类型
        func Convert2Int(i interface{}) (int, error) {
            switch i.(type) {
            case int:
                return i.(int), nil
            case string:
                return strconv.Atoi(i.(string))
            default:
                return strconv.Atoi(fmt.Sprint(i))
            }
        }
        ```
    5. `def ...int`是什么意思
    6. 判断数据类型的方法
    7. go install的细节(比如再main同级目录还是上一层执行该命令,执行了之后默认会覆盖安装吗);可以多个src打包吗?

419. git各种版本回退的笔记,这样以后可以快速查笔记来操作
    1. git checkout会丢弃工作区的更改?
    2. 工作区等的概念

420. 项目中版权所有的那个页面怎么做的
    1. 项目中css字体等cdn的笔记,如

        ```css
        @font-face {font-family: "iconfont";

            src: url('//at.alicdn.com/t/font_481604_nhaejqxrzy9cnmi.eot?t=1511252675294'); /* IE9*/

            src: url('//at.alicdn.com/t/font_481604_nhaejqxrzy9cnmi.eot?t=1511252675294#iefix') format('embedded-opentype'), /* IE6-IE8 */

            url('data:application/x-font-woff;charset=utf-8;base64,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') format('woff'),

            url('//at.alicdn.com/t/font_481604_nhaejqxrzy9cnmi.ttf?t=1511252675294') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+*/

            url('//at.alicdn.com/t/font_481604_nhaejqxrzy9cnmi.svg?t=1511252675294#iconfont') format('svg'); /* iOS 4.1- */

        }
        ```

421. 网页怎么截长屏
423. 如何自定义项目中的错误,还是说msg返回:

    ```go
    err = fmt.Errorf("ICCID长度不对,iccid:%+v", iccid)
    msg = err.Error()
    return
    ```

424. 如何切图,给图片换颜色大小啊之类的
425. 如何系统学习css
    1. mdn的css
    2. vscode上的css插件

426. 为什么需要框架
    1. angular的特性
    2. 渐进式应用
427. 自连接用于什么样的查询?
    1. 里面的表名可以和外面一样吗
    2. 如果id是在自增的,那么按id排序和按时间排序效果是一样的,而且比较数字的话更快?

428. 项目中用户表那几个做下笔记
429. 熟练使用分支
    不然多个切换时很麻烦
    1. 本地未add,未commit,未push的在新建和切换branch下的表现

430. java isletter我源码中的`<<` 的用法
    1. go 中呢

431. 为什么要使用angular 框架
432. 把config写成一个公共的,然后其他都是引用?
433. js和angualr的import是复制吗
    1. 把项目中的commonConfig中写上`min:this.query.startTime`会怎么样?和js函数的那啥有没有关系

434. `xxx.d.ts`是什么

435.  分支没修改完,怎么添加临时存储,然后切换到另一个分支
`Your local changes to the following files would be overwritten by checkout`
    `Please, commit your changes or stash them before you can switch branches. Aborting
437. git stash之后变成九十多为啥

439. 测试普通的类可以注册为服务然后依赖注入吗

440.  insert select
441. [angular2学习使用心得](http://blog.csdn.net/liufang1991/article/details/76041161)
442. html 语义化标签,比如nav

    语义化标签有自带样式吗

443. sql的in适用于任何数据类型吗(似乎是)

    sql的""和num可以直接比较吗

445. in这种查询,可不可以传参数去表示呢

447. sftp

448. 行内css如何添加多个

449. angular的安全导航符能用到属性里吗,还是只能用到{{}}中

451. angular select中option的disabled怎么使用?
    angualr中有几种disabled

452. 前端  自定义错误码 的研究

452. 后端 错误码 相关的代码

454. 如何让组件带上版本的命名?
456. 管理系统的api如何设计比较好

457. https://www.cnblogs.com/wl0000-03/p/6050108.html


459. temp
```
 95% emitting
<--- Last few GCs --->

[85140:0x34bdd50]   162509 ms: Mark-sweep 1513.3 (1850.0) -> 1250.6 (1531.5) MB, 909.2 / 0.0 ms  allocation failure GC in old space requested
[85140:0x34bdd50]   163239 ms: Mark-sweep 1250.6 (1531.5) -> 1250.4 (1481.0) MB, 730.0 / 0.0 ms  last resort GC in old space requested
[85140:0x34bdd50]   163992 ms: Mark-sweep 1250.4 (1481.0) -> 1250.4 (1462.0) MB, 752.1 / 0.0 ms  last resort GC in old space requested


<--- JS stacktrace --->

==== JS stack trace =========================================

Security context: 0x6fbde525529 <JSObject>
    1: DoJoin(aka DoJoin) [native array.js:~94] [pc=0x11055b3354cc](this=0x2411468022d1 <undefined>,o=0x3a1cf975e389 <JSArray[13]>,p=13,D=0x241146802371 <true>,z=0x1a618cf79961 <String[2]\: \n\n>,y=0x2411468023e1 <false>)
    2: Join(aka Join) [native array.js:~119] [pc=0x11055c230ede](this=0x2411468022d1 <undefined>,o=0x3a1cf975e389 <JSArray[13]>,p=13,z=0x1a618cf79961 <String[2]\: \n\n>,y=0x2411...

FATAL ERROR: CALL_AND_RETRY_LAST Allocation failed - JavaScript heap out of memory
 1: node::Abort() [@angular/cli]
 2: 0x8cea7c [@angular/cli]
 3: v8::Utils::ReportOOMFailure(char const*, bool) [@angular/cli]
 4: v8::internal::V8::FatalProcessOutOfMemory(char const*, bool) [@angular/cli]
 5: v8::internal::Factory::NewRawTwoByteString(int, v8::internal::PretenureFlag) [@angular/cli]
 6: v8::internal::Runtime_StringBuilderJoin(int, v8::internal::Object**, v8::internal::Isolate*) [@angular/cli]
 7: 0x11055af842fd
已放弃 (核心已转储)
```

node --max_old_space_size=5048 "%~dp0/../@angular/cli/bin/ng" build --prod --no-extract-license

460. 依赖注入和import的区别是啥,为什么项目中的登录弹框用的import而不是依赖注入
    1. 以及angular的路由

        window.location.href = "/";

462. 0.0.0.0 代表什么

463. 编译hydra的命令:go install hydra

464. 变量前面加上`_`一般代表着什么

465. 如何在一个hover的时候修改其他css 的样式
    css 的hover是不是比onmouseover快?那篇加载顺序的文章

466. 项目中的`<i>`被`<a>`包围是什么意思
467. 项目中可以继续写(onclick)吗,还是只能angular的clikc?
    使用方法有什么不同

468. angular的优秀项目

469. 如何处理项目中的大数据和小数据?
468. 用好腾讯的服务器
    1. 自己搭建一个小项目,五脏俱全的那种

469. github可以给master分支设置权限吗，就是操作master需要验证的那种
470. 网友;一切异步都是流，只要是流就可以订阅？

473. angular从表单获取的默认是字符串吗

475. 项目中`ng build --prod --no-extract-license`和`ng build --prod`的区别?似乎后者不能检测出严格的错误?
    直接`ng build`能检测出错误吗?用那个language插件会不会更好?
476. git查看某个文件的历史

481. plsql中的冒号表示什么
482. dom 事件  大多数是冒泡的还是非冒泡的 

483. `this.upproductInfo = this.productInfo || {};`
    js中的||和&& 的详细笔记

484. 输入法自动插入空格
485. 如何表现select的联动呢?
486. 他们测试的那个工具挺牛逼的
487. 明明有配置有ignore,为什么拉下来代码还是有很多跟踪的变动

488. 不同环境下多css的写法

489. 项目里一格分成多格的写法

491. angular表单验证的几种方式和最佳实践

492. git文件被跟踪后再修改忽略文件,怎么才能是忽略文件立即生效呢?
    1. 如何保留文件修改而不跟踪?
    2. 本地有已跟踪但不想跟踪的,此时从远程拉下来最新的gitignore会生效吗
475. xshell 中win和linux文件互传的命令
477. plsql的占位符和通配符和标准sql中一样吗
478. google调试如何判断两个元素有没有对齐
479. 原生class的多css写法
480. margin的几种写法

481. 放弃已跟踪文件的修改
482. 商户系统npm安装的时候一直报那个miss 什么的错,一直装不上,然后 复制别人的node_modules就好了, 一定要抽空搞清楚
483. .gitignore的排除写法

484. 几种css选择器的详解

485. 项目中多行的的写法

486. js数组操作
487. 数组push的问题
    声明的数组和赋值的数组好像不一样.
488. css选择器和圆角
489. Metronic – 响应式后台管理HTML5模板-创客云
490. angular NgZone的学习
    runOutsideAngular

491. 引入类型定义的库@types
492. 
chunk    {5} inline.bundle.js, inline.bundle.js.map (inline) 0 bytes [entry]

493. 项目中引入第三方插件如echarts的写法:

494. go报错:typechecking loop involving DeviceGroupAllListQuery

495. angular三等号和两等号

495. typescript中funtion(){xxx}和()=>{xxx}写法的不同,前者似乎不能访问全局变量,后者可以访问
    因为this指针的问题?

496. 项目后台如何返回json

497. ngOnChanges
498. map可以被for循环吗

499. news about ECharts
    可视化

500. 研究material日期组件的月份写法

501. angular先渲染父组件还是子组件,html,w3c的标准呢?
    写一个实际的demo来记录下
502. 时间戳

503. angular input接受多个参数的时候,如果几个参数传的时间不一样,那么是触发几次ng changes和ng init?总结下规律

504. NgZone.runOutsideAngular
505. for of 遍历map的笔记

506. window.innerWidth

507. setTimeout是在页面渲染完之后执行吗?

508. 跳过登录的测试
509. angular引用第三方组件的方法,ydj的话
510. ajax和jquery

512. setTimeout(xxx,0)
    这个是在dom渲染完成之后才触发的吗,还是?
513. js中fn和fn()
514. Typed Array
515. 单等号和双等号的区别

516. 目前主流的几种js引擎是?
517. js instanceof  和typeof

518. 仅更新前端的 话需要重启服务吗
519. 后面要用的layui框架如何
520. git中二进制文件的历史能恢复吗

521. vscdoe无法检测大型工作区的文件变化,请访问说明..
    说明链接:https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc
    1. node_modules中的文件也会算在内吗,.gitignore会生效吗?

522. 如何取消input两边的空格
523. angular input中change,ngModelChange,input等事件的关系,onchange

524. formControlName和两种表单的关系
    form表单的valueChanges订阅事件

525. 禁用工作区和禁用

526. angular待笔记
    1. angular事件里可以使用$event
    2. 通过$event.target.value修改input的值是修改的DOM上面的值,但是通过表单里的实际值还是没变?(待研究)


527. angularhtml的事件里可以直接写js吗

528. 深入理解oracle的分页rownum等
    1. 以及最基本的增删改查
    2. 只操作一个表的创建语句需要事务吗
    3. 序列 nextval
        1. 后面的from跟什么表都可以?
        2. 在insert语句中的话可以直接`序列.nextval`,查询的话...
    4. dual

529. 项目中execute和scalar
    1. types.toint等

530. 如果有新建文件 stash似乎就不合适了?

531. oracle exists

532. 出现无法监视的时候好像代码变动的识别也会出问题

533. 查看远程分支的命令,删除本地分支后还能看到远程分支吗,还是说要提交后远程才会同步,新建的时候也是吗?

534. update会锁住数据库,锁住之后其他人只能等待,那么其他人能查询吗
535. 为什么sql查出来的金额需要FM那个转换
    1. 第一种方式getString()然后strconv..
    2. 
    3. float(xxx)

537. golang 几种类型转换方式的区别

538. 下拉框中数据很多怎么办,会导致卡顿吗
    1. angular安全导航符第一个对象为undefined会生效吗
    2. angular [htmlfor]

539. input抱在label中
540. angular 扩展的比如ng... = 后面要带引号,原生html的有些后面不带?

541. 项目中应该有拷贝之类的方法把,而不是用JSON.parse(JSON.stringify(

542. select如何适应文字长度

543. oracle查出来的0.9,返回前端的时候会变成.9,那么在go中是怎么样的呢

544. trunc

545. angular 单选框默认选中的研究
546. select的自适应，go和区块链
547. insert into () select

548. js计算中文和英文字符长度

549. select里面内容过多的优化方案

550. go判断是否中文字符的 
551. 存数据库时,对于有默认值的有哪几种生效方式

552. 创建已有商户时 的 904错误

553. git pull是拉取所有分支信息,还是仅当前分支

554. created a lockfile as package-lock.json. You should commit this file.

556. css studying :https://segmentfault.com/q/1010000000193129
557. 感觉input list值得了解一下

558. 浏览器打断点
559. jquery的使用
560. var _this = this;
561. js类的写法
562. vue每次刷新的时候是只刷新页面?

563. parseFloat的精度问题

564. chrome标签很多时的内存优化方法
566. 深入研究js func的prototype

567. git pull和git push是只影响当前分支吗?如果是影响多分支怎么办?
568. 浏览器调试js怎么弄,console.log太恼火
569. mqtt协议

16. websocket主题和队列名字???

17. 如何查看网页哪部分重新渲染了?
18. 微信的文件可以撤回吗
19. npm的教程
20. js
    1. js引擎有垃圾回收吗
    2. js func在什么情况下会变成一个类?
    3. promise,ajax,rxjs,callback等的区别
    4. 如何判断一个方法是不是异步的

22. js中0和其他的比较会怎么样
23. 防止重复点击
24. chrome如何动态修改代码,调试代码等
    1. firebug?
25. 事件派发的作用dispatch,例子参考百度测距工具
26. js精度问题

27. js math相关的方法
    1. Math.sqrt
    2. Math.pow
    3. atan 角度


28. 地图相关
    1. 墨卡托坐标等
    2. google坐标,全球坐标,百度坐标等等
    3. 高斯什么算法之类的

29. 跨域请求
    1. 浏览器同源策略
    2. 什么样的情况会出现跨域问题
        1. localhost然后请求局域网内的其他api就会出现吗?

30. 认真思考和总结目前用到的技术:为什么需要用到这些技术(比如webpack),不用的话,原始解决方案是什么
    1. 坚定之后再做深入研究

31. html的i标签代表什么

32. 单页面应用的好处和优点
33. 重现
34. websocket和心跳检测

35. js undefined == 0?
    1. 其他几个的比较原理
    1. 以及 == 和===区别


36. 什么样的情况下回出现滚动条
    1. height为100%的时候会出现滚动条

37. 项目中的Page里面的 mosq 为什么不能访问到,还有Observle对象和普通对象有什么 区别.
38. js里变量前面没有声明语句的话是默认是什么?
    1. 在方法中呢?
    2. 假如在类中有个var 声明的变量,会变成当前类的静态变量吗

39. w3c规范和mdn的关系
    1. 如何学习w3c规范

40. 自己搭建服务器,比如nginx然后发布--主要是熟悉
41. css的学习
    1. 百度地图的position: relative;

42. json和xml的优劣
43. 跨域
    1. https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434499861493e7c35be5e0864769a2c06afb4754acc6000

44. 事件委托减少DOM事件注册的数量
45. mysql的本质是什么
46. 
Worker<Void> worker = webEngine.getLoadWorker();
worker.cancel();

47. 地图协议
49. 消息队列
50. 序列化和反序列化；生产者和消费者

51. 
没有抛出异常和把异常抛到上一级有什么区别;项目中go的异常返回时什么样的
52. UEFI也提供了强大的联网功能，其他用户可以对你的主机进行可靠的远程故障诊断，而这一切并不需要进入操作系统。(远程连接帮忙装系统？)
53. 白话和粤语
54. arkit
55. star法则对简历进行修改？
56. 腾讯等企业的招聘题库
57. 删除文件的时候显示被占用，但是迅雷就可以，原理和解决办法
58. 打哈欠的时候听不到声音
59. 
20160520面试题
	StringBuffer和String;stringbuffer；不用第三个参数实现两个数交换；数组可以用泛型吗？集合内数组的排序；sql查询排序等；双色球；排序；字符操作；字符排序操作；依赖注入的实现方式；java面试题；面试官说觉得自己擅长的，问开发编程中遇到
的问题；ajax；jQuery；编码问题，各种的默认编码和编码表，字符串拆分；各种Writer的区别和使用；数据库一对多，多对多等；

60. postman的使用,现在大家都用什么?
61. go编译后的后缀名是什么,在linux和mac中?
62. js arraybuffer和java ByteBuffer
    1. 参考:
        1. https://developer.mozilla.org/en-US/docs/Web/API/ArrayBufferView
        2. https://www.cnblogs.com/copperhaze/p/6149041.html
    2. arraybuffer可以存放object吗?
    3. js 堆栈 内存的笔记,arraybuffer开辟的内存是从哪儿开辟的
    4. arraybuffer和buffer的区别
    5. buffer和缓冲区
    6. typed array

63. curl 和wget
    1. curl后面的命令跟括号还有大于小于什么意思

64. go 已经哈希操作 /usr/local/go/bin/go
    1. type的三种类型

65. zookeeper发音
66. inline-block等的深入理解和使用

67. git push dev分支的时候,说master分支本地落后了,然后master分支的推送被拒绝了

    意思是git push会推送所有分支?那么git pull呢
68. 二进制文件删了可以复原吗, 修改不能对吧?

69. 如何搜索某个文件的历史记录
70. 纸短情长为什么火了,钢琴谱,梦想三国
71. angular5 强大的响应式表单
72. 数据库索引

73. go的参数传递是不是引用传递?
74. oracle的substr 会导致不能用到索引?
    1. 效率问题

75. sql有短路原则
76. markdown的todo list
77. 项目go框架
    1. interface转int用:types.toInt()

78. sql中<>和!=的区别

79. subscrib的处理是怎么样的:有三个:res,err,和不管成功失败都进行的处理?
80. https和http2
81. 长连接和websocket
    1. 网友:长连接比WebSocket更耗服务器的资源，而且长连接也是基于HTTP的，不能全双工通信，其实对于客户端来说还是要轮询，只是不需要每次请求都要先握手

82. 动态路由
83. Web前端单元测试、自动化测试和压力测试程序的开发 
84. 如何模拟网络状况
85. async 和await
86. angular的脏检查和zone
    1. angular通过脏检查实现MVVM
87. vue lavas
88. 路由策略:RouteReuseStrategy
    1. 路由复用策略
    2. 观察者更新
    3. 几种脏值检测策略对比:https://alligator.io/angular/change-detection-strategy/ 
    4. rxjs教程

 1. SSR服务端渲染
89. 如何系统学习w3c规范
90. service worker
91. 数据库的锁
92. 单双向数据流
93. tree shaking    
94. RSS订阅
95. viewport
96. SharedArrayBuffer有线程问题吗
97. 视频音频
    1. 七牛的文件上传
98. source-map
99. 防御性编程
100. 面试：页面加载海量数据:https://juejin.im/post/5ae17a386fb9a07abc299cdd
101. PWA介绍及快速上手搭建一个PWA应用:https://juejin.im/post/5ae2f82f6fb9a07acd4d761e
102. H5之地理位置必知必会:https://juejin.im/post/5ae34306f265da0ba60f89bb

99. 从表单取出来的都是字符串吗?
100. 笔记:项目常识
    1. 前端传到后天的都是字符串类型?
    2. oracle查询和插入的时候区分字符串和数字吗?
    3. 如何去掉组件的记忆功能

101. js在导出的组件中声明var变量, 会影响其他 组件吗
102. for of不能遍历对象?
103. 腾讯区块链
104. web访问本地文件
105. pom.xml
106. left join和inner join等笛卡尔积还是要继续熟悉
107. 交叉编译