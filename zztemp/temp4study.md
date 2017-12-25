# temp4study
1. console.log参数的写法和文档的看法
1. http的笔记
2. 知乎live：https://www.zhihu.com/lives/，可以回看吗
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
9. go的blank identifier
10. angular@ViewChild
11. querySelector的用法终于搞懂了，但是似乎并没有什么用
12. element和node的区别
13. 必须在两天内激活windows才能继续使用？
14. git如何查看远程的提交记录？
15. 发文字被转码怎么办
16. 我们项目中用到了jquery了吗
17. developers.google.com
18. querySelector笔记
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
23. console对象
24. https://www.cnblogs.com/yexiaochai/p/3567597.html
26. 根据事件传递的状态来判断是否是从已点击的按钮传过来的？
27. go的三个作者的中英文名
29. oracle日期相关操作
31. dom l3
32. `ctrl+a  ctrl+k`
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
47. oracle的两条竖线
48. 递归查询和插入
49. oracle的价格
50. 项目中的*号和go的星号和angular的星号
51. 如果有两个db怎么办，框架里db的逻辑是怎么样的
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
56. 类型转换难道用as？
57. 如何在有程序运行的情况下清shell屏
58. 各种字符串和反斜杠的处理
59. ele["contend"]和ele.content和ele.()等
60. 试试在外面xshell可不可以连接到里面
61. 内置的内置的make函数
62. 复制打包等命令
63.         let params = Object.assign({}, args || this.oldParams);
64. 为什么虚拟机关ubuntu经常停在黑屏
65. oracle里我之前写那个，如果把agent_id写到里面和写到外面有什么区别？效率上来讲？先筛选再连接是不是更快?
66. 四川500个机场的新闻
67. js遍历对象和遍历数组等

68. 我们项目中，getFirstRow和scala和getrows等的区别，以及获取回来的值的获取方法？
69. analys tool missing
70. 远程如何连到局域网内的机子？
71. source 就是. ?
  [http://blog.csdn.net/codeur/article/details/54783288?utm_source=itdadao&utm_medium=referral](http://blog.csdn.net/codeur/article/details/54783288?utm_source=itdadao&utm_medium=referral)

72. go get显示copy状态
73. linux文件安装在什么位置比较好
74. 同时执行多条命令怎么搞，连接多个命令用什么
75. 公司项目中组件名字用`-`不要用`.`？
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

88. ngOnInit（）和construct
89. linux如何查看某个软件的版本和所有支持的命令
90. linux蓝色的目录是什么gui
91. git推送的时候不输入密码怎么做到的
92. js的date可以直接加减而自动判断出月份?
93. ts中某人变量默认就是any?`
94. angular中组件绑定中不能使用下划线?比如`start_time`和`startTime`
95. 切片数组的合理创建方法
96. 一生何求
97. ts的`?:`是什么写法
98. 如何修改vscode里`tab`键的格数
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
101. ngfor的顺序是什么样的
102. angular
    1. 组件自身可以通过`[组件名].value`来获取绑定的值，为什么其他组件不能这样获取
    2. #showSaleDiscountBlock的笔记
    3. ngmoudle和value的关系
    4. 双向绑定的select，修改value值，会自动选中吗？如果修改为""呢？
    5. name和`#`的关系是什么
    6. 设置某个组件只能看不能改

103. 银行卡钱不够了会怎么样
104. `||`和`&&`的多个连接是什么算的
105. vscode翻页
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
144. vscode移到行首行位快捷键
145. axure
146. 图片后缀名的大写和小写会影响显示？比如代码里是jpg，但是图片实际是JPG，这样本地显示出来了，但是线上显示不出来。
147. es5的`export class StringUtility...`和`export function format`
148. linux的install.log
149. 网页当页内跳转如何回到前一个位置
150. linux多个root登录会怎么样？
151. windows中按时间排序,批量修改和复制移动等等.
152. 生产者消费者和订阅的区别
153. oracle外面的join后可以不跟条件吗
154. oracle多个and和or
156. angular的Input()和ViewChild()
157. constructor和ngoninit、ngAfterViewInit\FormControl
158. TSlint
159. x7f-xff中的￥
