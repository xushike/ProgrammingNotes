# temp4study
1. tty -s
2. 2009-11-10 23:00:00 UTC
3. studyGO放go的一些实用程序,比如反转字符
4. go编写闭包
5. go的指针
6. go数值常量
```go
const (
	Big   = 1 << 100
	Small = Big >> 99
)
```

7. Go playground 中的时间总是从 2009-11-10 23:00:00 UTC 开始， 如何校验这个值作为一个练习留给读者完成
8. 事件冒泡

14. git如何查看远程的提交记录？
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
37. 成都市城乡房屋管理局
38. 异步查询，动态显示搜索结果
39. git fetch
40. 可记为博客
	1. http://www.nowamagic.net/

41. linux新建文件以及文件类型，创建时的后缀可以变为类型吗
42. htmlelement->htmlinputelement
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

55. http状态码
58. 各种字符串和反斜杠的处理
59. ele["contend"]和ele.content和ele.()等
60. 试试在外面xshell可不可以连接到里面
62. 复制打包等命令
63.         let params = Object.assign({}, args || this.oldParams);
64. 为什么虚拟机关ubuntu经常停在黑屏
65. oracle里我之前写那个，如果把agent_id写到里面和写到外面有什么区别？效率上来讲？先筛选再连接是不是更快?
67. js遍历对象和遍历数组等

68. 我们项目中，getFirstRow和scala和getrows等的区别，以及获取回来的值的获取方法？

70. 远程如何连到局域网内的机子？
71. source 就是. ?
  [http://blog.csdn.net/codeur/article/details/54783288?utm_source=itdadao&utm_medium=referral](http://blog.csdn.net/codeur/article/details/54783288?utm_source=itdadao&utm_medium=referral)

72. go get显示copy状态
73. linux文件安装在什么位置比较好
74. 同时执行多条命令怎么搞，连接多个命令用什么
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
79. go中的变量带下划线会有警告
80. vacode跳到上一次的位置
81. 合并之后如何取消，big mistake
82. git两个人同一行下插入不同的内容的识别问题，似乎会有冲突？
83. 查看是谁修改的插件？
84. oracle查询中如何停止
85. angular各种组件的封装
86. oracle中''和null一样？而且可以赋值给各种类型？
87. git
    1. 合并之后出错的合理回滚方式？合作时别人出问题了也可以快速的恢复
    2. 如何查看远程详细的改动

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
91. git推送的时候不输入密码怎么做到的
92. js的date可以直接加减而自动判断出月份?
93. ts中某人变量默认就是any?`
94. angular中组件绑定中不能使用下划线?比如`start_time`和`startTime`
95. 切片数组的合理创建方法
96. 一生何求
97. ts的`?:`是什么写法
99. linux打包命令
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
166. 冷热启动
167. js的map和foreach
168. ubuntu永久了变卡是什么gui

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
170. js中return、continue、break
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
177. jquery现状如何,感觉不需要也可以写好项目
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
199. powershell的使用
200. win7中命令行中打开文件，前端开发，修改html，vscode相关好用插件
201. 百度商桥的原理
202. less等批量修改文本的内容

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
207. 英语中有顿号吗，否则用什么来表示顿号？
208. 研究下项目中subscribe的写法
209. 后端go中各种fmt和返回输出，错误等的写法
210. plsql如何记住尺寸
211. 如何判断子组件的状态
212. 阿里云等网站是怎么做的,学习
213. htm
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

226. 突然断电的话，vm会保存吗
227. js引入的模块没用的话会占用性能吗/
228. ngmodule单独写的作用是什么， 
229. [https://valor-software.com/ng2-file-upload/](https://valor-software.com/ng2-file-upload/)
230. 将项目表单的验证写成服务
231. 咨询李春牙医是否可报
234. angular在表单组件上双绑某个值和事件，那么值会先变化然后触发事件？
235. ngModel和ngvalue,以及[ngModel]几者的区别，以及name
236. app.module的和page.module的区别
237. 看看别人优秀的angular代码
238. angualr的disabled
239. 限制某些框输入的小数位数.
240. ngValue，ngGroup
241. Object.assign({}, this.info);的浅拷贝

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
251. stackoverflow for loop性能的文章
    1. foreach的return是不是没有用
252. 局域网能访问localhost启动的服务吗
    在虚拟机里，如果开启了虚拟机的防火墙呢
253. 没有登录能访问api吗

255. 查看linux内存占用状态
256. if else 和case switch的直观比较
257. go的{}中一定要用逗号结尾？

260. angular表单提示，可以做成侧边那种吗

        有没有经典的现成例子
261. md 的todo list;mac设置默认输入法
262. 腾讯百度等为啥自称厂
263. angular2渐进式编程.
264. 自定义指令和系统指令一样的话，默认用哪个
265. markdown流程图
266. oracle时间转换为天
267. js中各种遍历的比较：[https://www.incredible-web.com/blog/performance-of-for-loops-with-javascript/](https://www.incredible-web.com/blog/performance-of-for-loops-with-javascript/)

    结论似乎不准确,还有一点就是for of entries()方法效率似乎比较低,总之最好别用
268. 我们项目的ts编译后是es5还是什么
269. js引用传递的坑和优点.
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
285. 工单回填时的运营商池编号是干嘛的
286. shell中如何大段落的复制

288. 研究git 的flow,如何临时新建一个分支,开发部分代码然后再合并回去
289. 项目中上游渠道1000表示什么,在那儿设置的
290. 一键部署和发布(线下)

291. vscode返回光标上一次所在的位置
292. 聚合发货系统是谁写的,应该用的响应式表单
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
    `Please, commit your changes or stash them before you can switch branches. Aborting`
437. git stash之后变成九十多为啥
438. 每层目录都可以有.git
439. 测试普通的类可以注册为服务然后依赖注入吗

440.  insert select
441. [angular2学习使用心得](http://blog.csdn.net/liufang1991/article/details/76041161)
442. html 语义化标签,比如nav

    语义化标签有自带样式吗

443. sql的in适用于任何数据类型吗(似乎是)

    sql的""和num可以直接比较吗
444. 本地分支和远程分支的关联,新建之后怎么关联远程分支?

    新建分支push会怎么样?
445. in这种查询,可不可以传参数去表示呢
447. sftp
448. 行内css如何添加多个
449. angular的安全导航符能用到属性里吗,还是只能用到{{}}中
451. angular select中option的disabled怎么使用?
    angualr中有几种disabled

452. 前端  自定义错误码 的研究

452. 后端 错误码 相关的代码

453. `* [新分支]          develop2-show -> origin/develop2-show`

454. 如何让组件带上版本的命名?
456. 管理系统的api如何设计比较好

457. https://www.cnblogs.com/wl0000-03/p/6050108.html