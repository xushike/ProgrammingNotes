# temp4study
1. 置顶：除代码外，其他有中文的地方，用全角标点
2. 置顶：项目整体的把控
3. 置顶：对专业不能只是熟悉，最好做到清晰，言之有物。做到能
4. 置顶：坚持阅读英文资料
5. 置顶：解决问题时，先解决核心问题，不要一开始就追求所有细节，否则效率很难提升

1. psql默认输出调用的系统的什么tool？more不能翻页吗
    1. pgsql 未使用order时的默认顺序，函数的默认顺序
    4. 锁的种类级别，查询的时候会锁吗
    5. set transaction isolation level serializable
    6. exist的写法

        ```sql
        update company_skus as sku set alliances = alliances || '{"21": true}'
        where sku.company_id = 101 and sku.id in (405,404) and sku.alliances @> '{"21": false}' and exists (
            select 1 from alliance_stocks
            where alliance_id = 21 and alliance_part_id = sku.alliance_part_id
        and property = sku.property and qty > 0
        )
        ```
    7. 拍他锁、共享锁for update，for share
        1. 行级锁
    8. `update table_name t set xxx`中，即时设置了别名，xxx也不能写成`t.xxx`
    9. 视图
1. go
    2. go的嵌入：还有种区分内嵌与子类的重要手段。当内嵌一个类型时，该类型的方法会成为外部类型的方法，但当它们被调用时，该方法的接收者是内部类型，而非外部的。
        1. 上面这句话怎么理解。有相同方法时，优先调用外面的方法？方法的接收者是内部的？
        1. 和java或者c++的继承有什么区别

    3. 网友：go 的所有 io 操作（包括数据库查询， socket ，文件等）是不是没有阻塞的说法，一旦进入等待马上让出 cpu 给别的协程，等 io 的数据返回了协程调度又恢复执行了呢？
        1. 其他网友回答：文件操作至少 windows 是直接使用的系统阻塞调用，但是 go 运行时会自动再启动一个系统线程来提供给其他 go 协程，所以可以当作是。
        2. 网友2：流的操作系统也就只有 windows 可以读写文件达到也达到异步， IO 操作请使用 windows 特有的 IOCP
        3. 网友3：搞 compiler 么有搞 ai 好玩么 23333
    4. golang debug的工具链：可以通过 HTML 暴露程序内部状态，比如说一共有多少个 goroutine 在跑，他们各自的调用栈和当前的状态。
    5. go 自带的 interface+ auto generate VS 泛型
    6. string []byte 的转换是会拷贝的吗

1. git branch -r或者-a能看到被删除的分支？
    2. 如何查看合并到master的分支
1. pgsql 插入的时候如果第一个做了类型转换，后面的也会跟着做类型转换,比如这儿的jsonb？

    ```sql
    values 
    (3, '{"31":{"102":0,"110":0,"101":0}}'::jsonb, 12, '正常'),
    (4, '{"31":{"102":0,"110":0,"101":0}}', 12, '无包装'),
    ```
1. https://blog.csdn.net/erlib/article/details/52703165
1. golang查看进程号、线程号？
1. 行级锁 for udpate
1. 防御性编程指的是什么，把用户想象成恶意用户？限制各种边界条件？
    1. 什么情况下不需要防御性编程
1. 什么情况下回出现io.EOF，post请求的 时候也会出现？
1. query和form的区别
1. shell能接受最大多少的输入和输出，比如给它1G的输出，会崩掉吗
1. 高内聚低耦合的实际例子理解
1. 同时跑多个测试用例，怎么知道，几个成功，几个失败
    1. 如何查看mac是几核几CPU
1. golang里有相同底层数据类型的算是同一个数据类型吗
1. 各数据类型在各种情况下的初始值
1. url.Query()
1. 多线程，锁，自旋锁
1. golang *string
    1. *(*xxx)和xxx的区别
    1. 	defaultMaxMemory = 32 << 20 // 32 MB
1. decimal包的实现原理
1. git checkout origin会怎么样？
1. 对git的理解还是不够啊
1. 数据库的垃圾回收：
1. git如何 批量清除本地存在，但远程 已经被删了的分支
    1. git如何查看二进制文件的创建者
2. EXTRACT(epoch FROM sku.time)::bigint
1. goroutine，channel，实现通知
    1. select
    2. test中的init方法会被初始化吗
1. golang协程串行
1. golang debug日志
1. pg数据库的备份和赋值
1. pg命令行的提示为什么有时候又有时候没有
1. golagn命令行直接加上环境变量，然后os.GetEnv()可以直接
1. 死锁
1. go test显式覆盖率等git 
1. golang如何判断两个方法相等
1. golang对引用，&和值类型的修改
    1. 传指针和传引用的区别，只有细节上的不同？
1. go test的t.fail()
2. 网友：用 interface ，多态算啥～建议你读读官方的 io.Reader 模块
1. go test里加tags
2. golang错误处理：https://blog.csdn.net/u013589865/article/details/78754582
2. pg any:https://yq.aliyun.com/articles/424714
1. pg的锁，行级锁，表级锁等
2. 将go的测试用例改为example的那种形式，看下好不好用
    1. https://www.jb51.net/article/98326.htm
2. 关于代理的设置：https://www.jianshu.com/p/ff4093ed893f

# later
1. wangyin说的：然而在 Go 里面 string 类型里面每个元素都是一个 byte，所以每次你都得把它 cast 成“rune”类型才能正确的遍历每个字符，然后 cast 回去。这种把任何东西都看成 byte 的方式，就是 Unix 的思维方式，它引起过度底层和复杂的代码。
    1. 对吗

1. 增长黑客
1. xxx协议：http://www.bittorrent.org/index.html
    1. https://www.cnblogs.com/LittleHann/p/6180296.html
1. golang
    3. 大神推荐将该项目作为学习的项目，代码非常优美：github.com/golang/groupcache；然后是gin框架的代码，代码量比前者大10倍左右，不过代码不复杂，只有路由的部分比较复杂。
        1. 怎么做这样的文档：https://godoc.org/github.com/golang/groupcache
1. 2147483647
1. go编译器的学习：
    1. go tool compile -help可以查看所有我们可以传递给编译器的参数。禁用编译器优化和内联优化，你可以使用下面的参数：`go build -gcflags="-N -I"`
1. 同步锁
1. DOM编程：DOM的渲染顺序
1. rpc
1. golang远程方法调用
1. network
    1. book：计算机网络
1. vscode debug
1. 数据的锁，事务隔离级别，mvvc
    1. 排他锁，互斥锁
1. ssh
    1. mosh：断续连接
    2. 工业级代码
2. java 
    1. dump线程trace，golang可以吗
2. hash state
2. java 和kotlin:coroutine
2. mac duti
2. 无锁队列，并行，非阻塞，无栈有栈协议，上下文切换，actor ，csp这些黑话
2. make和makefile
2. golang的包管理工具：glide
    1. 如何检测golang的string里具体的内容
2. mac下什么时候需要sudo权限，访问特定文件夹的时候需要吗？
3. npm的包管理策略：如何管理不同的依赖，不同的版本等
    1. 以及npm自身各版本的区别
2. github上各种小图标和文字表示什么
    1. 比如语言，覆盖率等
2. 抢购这些是怎么做的
2. 迪杰斯特拉算法（Dijkstra）
2. 数据库拖库会怎么样
2. 二进制转成数字还是字母是用的什么协议？
2. sourcegraph
2. https://www.jianshu.com/p/ffeeb3d0efd6
2. 防盗链
2. 全文索引和分词
2. 如何ssh连接其他mac，比如连接家里的mac
2. 测试端口通不通：https://www.jb51.net/article/78082.htm
2. 将各种设置同步到一个地方，切换环境的时候直接从里面拉取就行了
2. pg: https://yq.aliyun.com/articles/174262
2. 如何查看psql函数的源码
1. 前段抓包
1. bash
    1. set -o vi
1. http 请求方式
    1. http://www.moonsec.com/post-772.html
    2. application/json
1. golang
    1. 待学习，单元和性能测试：https://blog.csdn.net/code_segment/article/details/77507491
    1. goroutine的错误处理：https://gocn.vip/question/91
1. golang中的nil
    1. https://studygolang.com/articles/9506
1. golang mutex和RWMutex
    1. how to and when use?
    1. https://studygolang.com/articles/3373
1. golang json：https://colobu.com/2017/06/21/json-tricks-in-Go/
1. golang 的性能测试例子
2. pg触发器，存储过程
1. https://gobyexample.com/
1. telnet和ping等
    1. 怎么判断接口是不是通 的
        1. https://www.jb51.net/article/78082.htm
2. sql的dump是什么
2. 将vscode的设置等用那啥同步
1. 如何生成文件的hash值
1. go的调试
    1. 断点那种，有没有自带的
1. golang http服务
1. 用go创建基于pg的缓存怎么弄
2. http协议
    1. application/json
    1. git：https://www.runoob.com/w3cnote/git-guide.html
1. 项目中
    1. fromvalue不能获取body里的内容
    2. query和form表单的内容时相似的，写在?后面，而且可以用fromvalue获取
        1. 从restful的角度讲，query是给get用的。一般参数含数组的话
    3. api中json数组和字符串逗号分隔的比较
2. golang的调度器
1. golang json转换时，结构体字段的多少会失败吗
2. 线程的睡眠，唤醒，阻塞，挂起等
    1. 做成脑图
2. illegal character U+FF08 '（'
    1. 输入了中文的（
1. golang的http相关包，比如获取参数，获取body中的某个值，获取其他等等
1. url中数组等的写法，以及各种的形式（curl，组件化），不同数据类型写法一样吗
1. go   
    1. 参数传递：引用类型和js是一样吗，通过*操作呢，也是一样吗  
        1. https://stackoverflow.com/questions/45122496/why-does-json-unmarshal-need-a-pointer-to-a-map-if-a-map-is-a-reference-type
    2. json转换时，直接传入已经是指针类型的结构体可以吗，非空的结构体可以吗？
        1. https://stackoverflow.com/questions/20478577/why-does-json-unmarshal-work-with-reference-but-not-pointer
1. 分支对比
2. git自动补全分支名的设置
2. group by和where的顺序，以及having
1. sign加密解密
1. git pull和fetch，merge的区别
    1. git rebase 的笔记
        1. git rebase -i后merge不会显示出来？别人的提交不会显示出来？
        1. 假如我的分支合并了master并修改了a文件，然后zhangsan合并master
    2. 熟悉git分支的线图
2. http router
1. 费曼学习方法：https://weibo.com/tv/v/GwHyao1TY?fid=1034:4277936765738533
2. study later : 日志
1. json化的时候有顺序吗
    1. 遍历结构体的时候有顺序吗
1. db：pg命令行输出如何设置为一行显式
    1. sql语句的增删改查是按什么顺序？
1. go
    1. os.getenv()获取的是基于哪个文件？setenv似乎没有生效
    1. os.exit()中0和1的区别，和return的区别
    1. studylater：信号处理
    1. log
        1. https://www.cnblogs.com/Goden/p/4620136.html
        2. https://studygolang.com/articles/9184
    5. path
    6. 主线程和goroutine的区别
    8. go的变量类型转换，比如int转int64
    9. http://wiki.jikexueyuan.com/project/the-way-to-go/02.7.html
2. 长轮训和socket
1. new和make的区别 
    1. 为什么var声明map不能赋值,但是make可以
        1. 双层map要make两次?
        3. 不带ok返回bool的false的技巧
    2. var声明的引用类型等于nil,但make声明的不等于nil
    2. 为什么slice用var声明后可以append来增加
1. router的group
2. linux
    1. chdir,chmod,chown，chtimes
1. go 
    1. https://medium.com/golangspec/selectors-in-go-c53a016702cf
1. go,使用`go get -u github.com/cweill/gotests/...`时提示
    git pull --ff-only
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking informati this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> master

package github.com/cweill/gotests/...: exit status 1

2. go fmt %+v出来的东西是连在一起的，如何格式化成类似jaon一样的东西，自己写？
1. localstorage
2. java中int8和int16等后面数字就表示占用的字节大小？在不同操作系统上是一样的？其他语言呢？
1. go run如何运行不含main的文件？还是只能声明包为main，这算是一个技巧吗
    1. a包里面把包声明为b，引用a包的时候用a还是b？
    1. 一个包下只能有一个main方法？那想运行其他方法的话怎么办
2. db
    1. \conninfo显式的是socket连接，难道使用psql命令的时候是通过socket连接的？
    2. 输出格式对齐和不对齐的区别，切换方法
    3. pg update连表的写法：http://qifeifei.iteye.com/blog/2211115
    4. pg学习：https://www.cnblogs.com/kungfupanda/p/4478917.html
2. golang import cycle not allowed
    1. 怎么找啊
2. don't use an underscore in package name
    1. 不允许空文件夹吗
2. 命令行翻墙
1. golang 
    1. sync add wait group，WaitGroup，Done等
        1. 简单应用，实现通知？
    2. 结构体大写小写开头的区别
    3. json化时，任意类型的空会变成什么，不加omitemty的话呢
    1. gin框架
    4. router的group
2. 数据结构和算法
    1. 前缀树比hash更快？
2. 时间戳
    1. 有毫秒形式？
    1. 小数处理
1. http协议
    1. 什么数据需要用body传，什么需要用header传，有严格要求吗，都在body里传有什么好处坏处？
    2. git fetch和pull的实战区别
    3. pull的时候，其他分支会被快速合并吗（如果有快速合并的话）
    4. post，get的使用场景和区别，什么时候可以不区分
2. MapReduce是一种编程思想
    1. 那么如何用golang实现
1. go的枚举和const
1. go的 协程和通知
1. go的面向接口编程
    1. 面向http接口呢？
    1. 接口编程的意义？
    1. go的带方法接收者的方法和普通方法的区别，
    2. 方法和interface的关系
    3. 参考：https://blog.csdn.net/sevensevensevenday/article/details/72403998
1. golang json的用法，不用结构体而用map的使用
    1. 把一个多的结构体赋值给少的结构体会发生什么？
    2. golang序列化和反序列化
    3. 返回结构体的方法，不能return nil?
1. golang
    1. 定义了三个参数，但是只使用其中两个参数，有没有什么问题
    2. 大量使用指针会不会有什么问题
2. golang later study
    1. 如何格式化golang v,+v,#v等格式的输出？自己写一个？
2. 回调接口
2. 待学习：https://colobu.com/2017/06/21/json-tricks-in-Go/
2. git自己对某个文件修改了，但是其他人删除了文件
1. http协议
2. golang的锁，死锁，互斥锁，读写锁
1. db
    1. 把条件写到on和where的区别
    1. 被连接的表的筛选条件放到on后面还是where后面好？
    2. 待笔记：）、not、and、or这四个 的优先级从左到右递减
    5. 线程，协程
        1. 一个线程里可以并行执行两个方法吗
1. postgresql
    1. case when else
    2. 函数的作用，什么情况下才用函数
1. 待研究：vscode 还有一项很强大的功能就是断点调试,结合 delve 可以很好的进行 Go 代码调试
1. git fetch
1. 测试覆盖率
2. 签名和证书
    1. https签名和其他签名
1. 测试用例，单元测试，集成测试
2. 接口设计
1. golang
    1. router里args和body
    1. golangJSON：https://blog.csdn.net/qdx411324962/article/details/48216103
    1. 取两个结构体并合并其部分
        1. 可以将一个struct放到另一个struct里
    2. []byte等的相互转换
    4. https://blog.csdn.net/liukuan73/article/details/78863731
1. 熟悉processon的使用，将笔记本上的流程图画出来
1. https协议，post，get，contentType，application/json; charset=UTF-8，请求头，请求体，返回体
    1. 如何配置ssh登录，好处和缺点
    3. 一个完整的url是怎么样的，#和？的位置等
        1. 数组的话参数是什么格式
    4. post和get在获取参数的方式上有什么区别
        1. req.URL.Query()
        2. req.FormValue
1. 静音的时候会有提醒吗？如何让pc静音但有弹出提醒
1. 签名
1. go环境变量
1. 路由
    1. 缓存
    2. 复用
1. 数据结构
    1. 堆排序,二分查找适宜用顺序表.
    1. 数据结构及其应用
    1. 如何自己实现数据结构
    1. hash，
    2. 线性表：数组，所以随机访问元素时性能较好(因为数组以一块连续的区域保存所有的元素)
    2. 链表：插入、删除时性能出色(只需改变指针地址即可)
    4. 矩阵
    5. 判断一个单向链表中是否存在环的最佳方法是快慢指针
1. 算法
    1. 常用排序算法的分类，快速排序分到哪一类？
    1. 挖坑填数，分治法
    1. 快速查找法，比如go中switch的实现
    1. hash是什么
    4. 对两个已排序数组合并后再排序
    5. 互斥，同步，死锁
    6. 动态规划
1. linux
    1. vim
        1. 大块的复制粘贴
    2. rmdir
    3. linux如何树状列出目录和文件
        1. 如何递归搜索
1. goalng
    1. golang如何比较切片，map等
        1. []int{}这种简单的可以用反射比较，但是复杂点的就不行？
    1. 空切片和nil的关系，在转json的时候不都是[]?
    1. http,server,os,runtime,path,net,context,signal，reflect,json,time(date),url，json,ioutil，sync，mutex，StructField
        1. net.Listener
        2. reflect.valueof
            1. go的反射掌握
            1. https://studygolang.com/articles/12348?fr=sidebar
            2. value.Kind(),IsValid
            3. reflect.Slice等
            4. 
                ```
                	if typ.Kind() == reflect.Ptr {
                        typ = typ.Elem()
                    }
                ```
            5. kind()
            6. typeof()
            7. reflect.Ptr是指针类型？
        3. os.Getenv
        4. context.Background()
        5. json,buffer,[]byte等的转换
        6. StructField
            1. PkgPath
    1. 平滑停机
    1. 传递切片和切片的引用有什么区别
    1. 包那么多如何学习
    1. request
        1. FormValue
    1. os.Getenv("debugTasks")
    1. path包
    2. ch := make(chan os.Signal)
        <-ch
    3. struct {
			Data interface{}
		}{data}

    4. sync.RWMutex

    1. go导入包，初始变量，初始函数，构造函数等的顺序
    1. go test
        1. https://blog.csdn.net/minghu9/article/details/53941665

    1. 注释谢单元测试只能做简单的
    1. golang中实现常见排序用什么数据结构
    1. 生产者消费者
    1. sync包
    1. channel select
    1. type声明的 为什么可以用new初始化
    1. 结构体，map，对象等的默认输出格式
    1. 结构体传入方法中被改变后，原结构体会变吗？
    1. switch中多个条件都满足时会随机选择一个？
    1. Go 语言对 protocol buffers 和 gRPC 有一流的支持

1. db
    1. 增加表字段对原有数据有什么影响
    2. 触发器
    1. postgressql ssl
    1. create table if not exists 。。。
    1. 数据库调优
    2. 缓存到go里面和缓存到redis里面的比较
    1. 定时任务
    2. 自己实现一个psql格式化的工具
1. html value等的区别
2. Pipeline流水线执行模型
1. goalng
    1. 哪种数据类型适合频繁存取
    1. 待笔记:数组（第 7 章）和结构（第 10 章）这些复合类型也是值类型
    2. 笔记:指针（第 4.9 节）属于引用类型，其它的引用类型还包括 slices（第 7 章），maps（第 8 章）和 channel（第 13 章）。被引用的变量会存储在堆中，以便进行垃圾回收，且比栈拥有更大的内存空间
    3. s := []int{1,2,3}到底是切片还是数组
2. JSON风格指南:https://github.com/darcyliu/google-styleguide/blob/master/JSONStyleGuide.md
    1. 设计更为规范的JSON（这个会森森影响到Mongo的存储，查询效率，React的性能）
1. 数据库
    1. 索引的方式
        1. btree
    2. 数据库调优
1. 数学
    1. log(n)
1. 继承与原型链:https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
1. js 获取命令行输入怎么获取
1. input只输入数字
1. js在不同地方引入同一个模块的时候,是引用的同一个对象还是不同的对象
2. 回归最优解
1. js date对象
3. apply和call
8. cssText
9. HTML templates（HTML模板）：<template> 和 <slot> 元素使您可以编写不在呈现页面中显示的标记模板。然后它们可以作为自定义元素结构的基础被多次重用
10. 基于回流的页面渲染,页面渲染的w3c规范和那个女人的博客
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
32. requestAnimationFrame和settimeout
    1. HTML5标准规定了setTimeout()的第二个参数的最小值（最短间隔），不得低于4毫秒，如果低于这个值，就会自动增加。在此之前，老版本的浏览器都将最短间隔设为10毫秒。另外，对于那些DOM的变动（尤其是涉及页面重新渲染的部分），通常不会立即执行，而是每16毫秒执行一次。这时使用requestAnimationFrame()的效果要好于setTimeout()。

33. 深复制对原型链有什么影响?
35. js call和apply参考:https://www.jianshu.com/p/a9990162d698
36. 页面重定向和window.location的关系
37. 浏览器跨域,iframe,跨域加载js
38. web work参考
    1. https://www.cnblogs.com/giggle/p/5350288.html
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
56. https://www.cnblogs.com/yaohong/p/6385228.html
58. 编程之美
59. https://mp.weixin.qq.com/s/mz2QuZrE6uMXpAq8HGJe3A
60. godep那个tool的使用
61. golang给包设置多个目录,下载的包需要在多个版本间切换怎么弄比较好
62. 密钥:私钥,公钥
64. chrome的投影
65. git log是按时间顺序排吗, 如果不是怎么弄?
66. 取数组最大最小值的算法
67. db
    1. sql中#和$的区别
    2. 各sql的变量占位符是啥
        1. note:postgresql是$
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
74. 元祖类型和set差不多?
75. golang
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
    24. go get默认会显示是否更新,是否成功吗?
    25. exported type ICoordinate should have comment or be unexported
        1. 似乎是缺少某方法或数据
76. html 
    1. rotation

77. oracle
    1. sid是什么
78. mdn
    1. creatEvent
    2. 事件触发器
    3. 事件:https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events
79. qq
    1. 提取图片中的文字只有手机才有?

80. linux
    1. 执行source /etc/profile之后 用户名称由绿色变成白色了
    2. 递归创建目录
81. git删除远程分支后需要提交吗?其他人本地还有这个分支,操作会有什么影响?
82. to和for
83. ubuntu自带的"提取到此处"有问题?
84. 事件派发
85. OpenLayers 3 
    1. 之 动态点扩散效果:https://www.2cto.com/kf/201511/450555.html
    2. https://blog.csdn.net/qingyafan/article/details/45950125
86. git commit内容非常多之后怎么办
87. 区块链:
    1. 交易记录非常多之后怎么办
88. cpu和核心数,核心数和线程的关系
89. dom渲染顺序
90. GEOJSON等:http://www.maiziedu.com/wiki/json/geojson/
91. js获取js文件中的数据?
92. html document对象
93. canvas画图:https://www.w3cplus.com/canvas/draw-dashed-and-dotted-lines.html
94. 分辨率变化的时候矢量图会被重新渲染?
95. js
    1. 方法的声明不能在调用之后?
        什么情况下可以违背这个规则

96. 网页画图的几种方法,画矢量图用什么合适
97. 事件的几种写法
    1. 原生click和onclick的区别
98. jsDoc规范
99.  事件和观察者模式
100. json的语法和js普通对象的语法有没有什么区别
101. 什么是全拼和双拼
103. .pyc和.tmp
104. 苹果发布会的ar文件格式

105. git diff输出为空的问题
    note:默认没变应该是输出为空,如果权限变了会显示出来吗?(待测试),为什么看别人网上的可以显示出权限的变化,但是我的没看到权限的变化

106. golang
    2. errors.New("xxx")
        1. 用该方式生成的相同的error相等吗
108. webpak热部署
109. golang
    3. 通过index访问长度为0的数组和切片会报错吗,用`[0:]`呢
110. sqlite
111. sso
112. websocket
    4. 有订阅成功失败的状态吗
    5. 连接状态是返回一次还是连续不断返回?
    6. 切换页面websocket会自动断开吗

113. 博客:腾讯web前端coverguo
114. 自定义路书轨迹
    7. 最简单的,就是不用动画,只需要setPosition和画线就行了
    8. 参考:https://blog.csdn.net/projectno/article/details/78281689
115. js this的问题, 在func中this表示啥, 如果使用`var self = this`,此时self又表示啥,func使用箭头函数的话this又表示啥
116. 用什么数据表示三种状态比较好
117. js不存在线程安全的问题
118. js event loop
    9. 浏览器多线程和js单线程
    10. 阻塞等
        1. alert和同步xhr
            1. alert会阻塞异步代码吗,promise呢?
            2. xhr的原理
            3. 如何主动结束异步,主动实现类似alert的效果
    11. 外部js和当前js
    12. 浏览器的event loop,每遍历一个就会渲染一次?
    13. js同步和异步的优缺点和使用场景
    14. js异步编程的几种方式
        1. 哪些是可以阻塞的?哪些是可以主动停止的
        2. 异步事件加入的时间顺序是?
    15. setTimeout有最大等待时间吗;最小时间多少比较合理:30msor 50ms
        1. setTimeout的深度使用
        2. setTimeout中有多行代码的话需要再用setTimeout包裹吗,是顺序执行的吗
    16. setTimeout和setInterval的嵌套

    17. 异步的顺序不能保证?
    18. 如何主动把某个事件弄成异步的?比如路书中的`_addMarker()`方法,弄成完成后回调的那种
    19. 多个setTimeout之间的时间间隔是怎么算的?比如100ms,是前一个执行完后的一百毫秒还是跟前一个没关系?
        已解决:跟前一个执行的时间有关.如果没超出,比如前一个执行了20ms,那么再过80ms后一个就开始执行;如果前一个超出了,比如执行了200ms,那么执行完后后一个立刻执行.

119. 实现回调的几种方式
    20. 如何把普通方法弄成可以回调的?
    21. 如何修改event loop中事件的顺序?

120. angular数据异步渲染的优缺点

121. js如何一边遍历一边添加?
122. typedarray和普通array在语法上的区别
123. 网页动画的原理
    22. https://www.zhihu.com/question/20453427
    23. w3c关于动画的规范
    24. 网页动画实现的方式(不管新老):
        1. css animation
124. https://developer.mozilla.org/zh-CN/docs/Games
125. html的整个渲染流程:reflow等
126. https://www.w3cplus.com/svg/bear-animation-width-svg.html
127. 矢量图的数据比图片体积小
128. 【链接】百度地图自定义图标动画
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
2. linux操作系统日志:var/log/messages
2. 哨兵
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
1. goalng 类型转换:strconv.ParseFloat
    1. goalng模板
1. viewport做适配
1. 从package.json中删除
1. mac vscode占用内存很高
2. npm 符号链接
1. npm 创建的目录,为什么没有删除权限
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

1. blob,dataview,
1. js有类型的概念吗
    1. js引擎能区分不同的基本数据类型吗
1. vscode 中go怎么自动导包
2. google chrome helper是什么,导致mac发烫
1. @next是什么版本
2. package-lock.json对跨平台有影响吗
2. npm install默认的规则是什么样的, 会默认覆盖吗还是?
2. node-sass

1. http://www.wutianqi.com/?p=3686
1. sql
    1. varchar2和varchar
    2. 如何查看长度单位
    6. 换行符和空格会原样取出来吗

1. npm
    1. 查看某个库的版本号
    2. 错误和警告
    3. darwin等

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
2. linux 文件名带反斜杠的bug
2. 防止重复点击
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
102. angular
    1. 组件自身可以通过`[组件名].value`来获取绑定的值，为什么其他组件不能这样获取
    3. ngmoudle和value的关系
    6. 设置某个组件只能看不能改

103. 银行卡钱不够了会怎么样
104. `||`和`&&`的多个连接是什么算的
106. linux任何管理器和强制关闭某程序，以及温柔关机
108. liux如何命令行中打开图片，以及像mac那样命令行和文件夹互相打开
109. go如何进入引入的包里查看代码
110. linux如何递归查询目录里是否有某个文件
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
159. x7f-xff中的￥
160. js string默认取值是什么
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
211. 如何判断子组件的状态
215. js等的实例演示gif生成
216. [http://www.01happy.com/golang-err-is-shadowed-during-return/](http://www.01happy.com/golang-err-is-shadowed-during-return/)
217. linux vscode不显示下划线
218. plsql dev快捷键和技巧
219. js中 && 和大小与的优先级

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
228. ngmodule单独写的作用是什么， 
229. [https://valor-software.com/ng2-file-upload/](https://valor-software.com/ng2-file-upload/)
230. 将项目表单的验证写成服务
234. angular在表单组件上双绑某个值和事件，那么值会先变化然后触发事件？
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
255. 查看linux内存占用状态
265. markdown流程图
266. oracle时间转换为天
267. js中各种遍历的比较：[https://www.incredible-web.com/blog/performance-of-for-loops-with-javascript/](https://www.incredible-web.com/blog/performance-of-for-loops-with-javascript/)

    结论似乎不准确,还有一点就是for of entries()方法效率似乎比较低,总之最好别用
270. js到ts:[https://segmentfault.com/a/1190000010774159](https://segmentfault.com/a/1190000010774159)
271. 深入js的for of:[http://www.jb51.net/article/70106.htm](http://www.jb51.net/article/70106.htm)
272. linux删除后的撤销
273. es6展开运算符
276. 研究下word等的`1.`,`2.`
279. css里夫优先还是子优先?
280. 不同的指令和组件加到不同的地方,具体记录
283. 带_的私有变量是那个语言的语法
284. console.log多参数的写法
290. 一键部署和发布(线下)

293. 管道多参数的写法
294. oracle nvl 以及项目中的&写法,以及oracle的空不等于空的问题如何解决
    1. `u.down_order_no = nvl(@down_order_no, u.down_order_no)`和`@order_no is null or o.order_no = @order_no`
    2. 当有外链接其他表的时候不要用`&`这种写法,因为两个表可能会有相同名字的字段,这样就识别不出来了.
    3. ''和null相等吗,is null判断''呢?
    4. 连接查询的时候,把连接查询的条件放在where前面和后面有区别吗?
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
361. go中错误的最佳实践

    如果err有很多层,怎么判断是从哪层传过来的?
362. ts里在变量名前面加`_`和后面`_`有没有什么特殊意义

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
378. line-height
379. 文字放在图片的右边的总结
381. 项目中的`DateUtility`等几个工具类有空研究下
382. 不知道在angular单页面应用中是否有效:[三种方法能够确定浏览器窗口的尺寸](http://www.w3school.com.cn/js/js_window.asp)
383. 项目中select中内容的排序
384. 项目中input的长度等限制
385. oracle的rownum要好好研究下
    1. 以及`rownum <= @card_count`这种写法,是不是一定要加上小于

386. 项目中css没有生效的研究

    偶尔出现的bug还是?
388. css布局
389. sum over() 不能和group by一起用?
390. ubuntu `whereis`
391. package-lock.json作用
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
406. 什么样的查询会使表锁住
408. 析构函数
409. 三大运营商是怎么算短信长度的,中英文一样吗?一条短信最大长度是多少?
413. 现在不写存储过程了?
    1. 存储过程和sql的比较
    2. 存储过程的原理,如果有很多判断什么的,效率会低吗?
414. update可以left join吗
    1. query的时候,如果字段没有获取到会报错吗,还是返回null?

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
    6. 判断数据类型的方法
    7. go install的细节(比如再main同级目录还是上一层执行该命令,执行了之后默认会覆盖安装吗);可以多个src打包吗?

419. git各种版本回退的笔记,这样以后可以快速查笔记来操作
    1. git checkout会丢弃工作区的更改?
    2. 工作区等的概念


420. 网页怎么截长屏
421. 如何自定义项目中的错误,还是说msg返回:

    ```go
    err = fmt.Errorf("ICCID长度不对,iccid:%+v", iccid)
    msg = err.Error()
    return
    ```

422. 如何切图,给图片换颜色大小啊之类的
423. 如何系统学习css
    1. mdn的css
    2. vscode上的css插件
425. 自连接用于什么样的查询?
    5. 里面的表名可以和外面一样吗
    6. 如果id是在自增的,那么按id排序和按时间排序效果是一样的,而且比较数字的话更快?

426. 项目中用户表那几个做下笔记
427. 熟练使用分支
    不然多个切换时很麻烦
    1. 本地未add,未commit,未push的在新建和切换branch下的表现

428. java isletter我源码中的`<<` 的用法
    2. go 中呢

429. 为什么要使用angular 框架
430. 把config写成一个公共的,然后其他都是引用?
431. js和angualr的import是复制吗
    3. 把项目中的commonConfig中写上`min:this.query.startTime`会怎么样?和js函数的那啥有没有关系

432. `xxx.d.ts`是什么

433.  分支没修改完,怎么添加临时存储,然后切换到另一个分支
`Your local changes to the following files would be overwritten by checkout`
    `Please, commit your changes or stash them before you can switch branches. Aborting

3.    insert select
4.   [angular2学习使用心得](http://blog.csdn.net/liufang1991/article/details/76041161)
5.   html 语义化标签,比如nav

    语义化标签有自带样式吗

6.   sql的in适用于任何数据类型吗(似乎是)

    sql的""和num可以直接比较吗

7.   in这种查询,可不可以传参数去表示呢

8.   sftp

9.   行内css如何添加多个

10.  angular的安全导航符能用到属性里吗,还是只能用到{{}}中

11.  angular select中option的disabled怎么使用?
    angualr中有几种disabled

12.  前端  自定义错误码 的研究

13.  后端 错误码 相关的代码

14.  如何让组件带上版本的命名?
15.  管理系统的api如何设计比较好

16.  https://www.cnblogs.com/wl0000-03/p/6050108.html
2.   0.0.0.0 代表什么

3.   编译hydra的命令:go install hydra

4.   变量前面加上`_`一般代表着什么

5.   如何在一个hover的时候修改其他css 的样式
    css 的hover是不是比onmouseover快?那篇加载顺序的文章

6.   项目中的`<i>`被`<a>`包围是什么意思
7.   项目中可以继续写(onclick)吗,还是只能angular的clikc?
    使用方法有什么不同

8.   angular的优秀项目

9.   如何处理项目中的大数据和小数据?
10.  用好腾讯的服务器
    1. 自己搭建一个小项目,五脏俱全的那种

11.  github可以给master分支设置权限吗，就是操作master需要验证的那种
12.  网友;一切异步都是流，只要是流就可以订阅？

13.  angular从表单获取的默认是字符串吗

14.  项目中`ng build --prod --no-extract-license`和`ng build --prod`的区别?似乎后者不能检测出严格的错误?
    直接`ng build`能检测出错误吗?用那个language插件会不会更好?
15.  git查看某个文件的历史

16.  plsql中的冒号表示什么
17.  dom 事件  大多数是冒泡的还是非冒泡的 

18.  `this.upproductInfo = this.productInfo || {};`
    js中的||和&& 的详细笔记

19.  输入法自动插入空格
20.  如何表现select的联动呢?
21.  他们测试的那个工具挺牛逼的
22.  明明有配置有ignore,为什么拉下来代码还是有很多跟踪的变动

23.  不同环境下多css的写法

24.  项目里一格分成多格的写法

25.  angular表单验证的几种方式和最佳实践

26.  git文件被跟踪后再修改忽略文件,怎么才能是忽略文件立即生效呢?
    1. 如何保留文件修改而不跟踪?
    2. 本地有已跟踪但不想跟踪的,此时从远程拉下来最新的gitignore会生效吗
27.  xshell 中win和linux文件互传的命令
28.  plsql的占位符和通配符和标准sql中一样吗
29.  google调试如何判断两个元素有没有对齐
30.  原生class的多css写法
31.  margin的几种写法

32.  放弃已跟踪文件的修改
33.  商户系统npm安装的时候一直报那个miss 什么的错,一直装不上,然后 复制别人的node_modules就好了, 一定要抽空搞清楚
34.  .gitignore的排除写法

35.  几种css选择器的详解

36.  项目中多行的的写法

37.  js数组操作
38.  数组push的问题
    声明的数组和赋值的数组好像不一样.
39.  css选择器和圆角
40.  Metronic – 响应式后台管理HTML5模板-创客云
42.  引入类型定义的库@types
43.  
chunk    {5} inline.bundle.js, inline.bundle.js.map (inline) 0 bytes [entry]

1.   项目中引入第三方插件如echarts的写法:

2.   go报错:typechecking loop involving DeviceGroupAllListQuery

3.   angular三等号和两等号

4.   typescript中funtion(){xxx}和()=>{xxx}写法的不同,前者似乎不能访问全局变量,后者可以访问
    因为this指针的问题?
10.  angular先渲染父组件还是子组件,html,w3c的标准呢?
    写一个实际的demo来记录下
15.  window.innerWidth

16.  setTimeout是在页面渲染完之后执行吗?

17.  跳过登录的测试
18.  angular引用第三方组件的方法,ydj的话
19.  ajax和jquery

20.  setTimeout(xxx,0)
    这个是在dom渲染完成之后才触发的吗,还是?
21.  js中fn和fn()
22.  Typed Array
23.  单等号和双等号的区别

24.  目前主流的几种js引擎是?
25.  js instanceof  和typeof

26.  仅更新前端的 话需要重启服务吗
27.  后面要用的layui框架如何
28.  git中二进制文件的历史能恢复吗

29.  vscdoe无法检测大型工作区的文件变化,请访问说明..
    说明链接:https://code.visualstudio.com/docs/setup/linux#_visual-studio-code-is-unable-to-watch-for-file-changes-in-this-large-workspace-error-enospc
    1. node_modules中的文件也会算在内吗,.gitignore会生效吗?

30.  如何取消input两边的空格
31.  angular input中change,ngModelChange,input等事件的关系,onchange

32.  formControlName和两种表单的关系
    form表单的valueChanges订阅事件

33.  禁用工作区和禁用

34.  angular待笔记
    1. angular事件里可以使用$event
    2. 通过$event.target.value修改input的值是修改的DOM上面的值,但是通过表单里的实际值还是没变?(待研究)


35.  angularhtml的事件里可以直接写js吗

36.  深入理解oracle的分页rownum等
    3. 以及最基本的增删改查
    4. 只操作一个表的创建语句需要事务吗
    5. 序列 nextval
        1. 后面的from跟什么表都可以?
        2. 在insert语句中的话可以直接`序列.nextval`,查询的话...
    6. dual

37.  项目中execute和scalar
    7. types.toint等

38.  如果有新建文件 stash似乎就不合适了?

39.  oracle exists

40.  出现无法监视的时候好像代码变动的识别也会出问题

41.  查看远程分支的命令,删除本地分支后还能看到远程分支吗,还是说要提交后远程才会同步,新建的时候也是吗?

42.  update会锁住数据库,锁住之后其他人只能等待,那么其他人能查询吗
43.  为什么sql查出来的金额需要FM那个转换
    8. 第一种方式getString()然后strconv..
    9. 
    10. float(xxx)

44.  golang 几种类型转换方式的区别

45.  下拉框中数据很多怎么办,会导致卡顿吗
    11. angular安全导航符第一个对象为undefined会生效吗
    12. angular [htmlfor]

46.  input抱在label中
47.  angular 扩展的比如ng... = 后面要带引号,原生html的有些后面不带?

49.  select如何适应文字长度

50.  oracle查出来的0.9,返回前端的时候会变成.9,那么在go中是怎么样的呢

51.  trunc

52.  angular 单选框默认选中的研究
53.  select的自适应，go和区块链
54.  insert into () select

55.  js计算中文和英文字符长度
57.  go判断是否中文字符的 
58.  存数据库时,对于有默认值的有哪几种生效方式
60.  git pull是拉取所有分支信息,还是仅当前分支
61.  created a lockfile as package-lock.json. You should commit this file.

62.  css studying :https://segmentfault.com/q/1010000000193129
63.  感觉input list值得了解一下

64.  浏览器打断点
67.  js类的写法
68.  vue每次刷新的时候是只刷新页面?

69.  parseFloat的精度问题

70.  chrome标签很多时的内存优化方法
71.  深入研究js func的prototype
74.  mqtt协议

75. websocket主题和队列名字???

76. 如何查看网页哪部分重新渲染了?
77. 微信的文件可以撤回吗
78. npm的教程
79. js
    1. js引擎有垃圾回收吗
    2. js func在什么情况下会变成一个类?
    3. promise,ajax,rxjs,callback等的区别
    4. 如何判断一个方法是不是异步的

80. js中0和其他的比较会怎么样
81. 防止重复点击
82. chrome如何动态修改代码,调试代码等
    1. firebug?
83. 事件派发的作用dispatch,例子参考百度测距工具
84. js精度问题

85. js math相关的方法
    1. Math.sqrt
    2. Math.pow
    3. atan 角度


86. 地图相关
    1. 墨卡托坐标等
    2. google坐标,全球坐标,百度坐标等等
    3. 高斯什么算法之类的

87. 跨域请求
    1. 浏览器同源策略
    2. 什么样的情况会出现跨域问题
        1. localhost然后请求局域网内的其他api就会出现吗?

88. 认真思考和总结目前用到的技术:为什么需要用到这些技术(比如webpack),不用的话,原始解决方案是什么
    1. 坚定之后再做深入研究

89. html的i标签代表什么

90. 单页面应用的好处和优点
91. 重现
92. websocket和心跳检测

93. js undefined == 0?
    1. 其他几个的比较原理
    2. 以及 == 和===区别


94. 什么样的情况下回出现滚动条
    1. height为100%的时候会出现滚动条

95. 项目中的Page里面的 mosq 为什么不能访问到,还有Observle对象和普通对象有什么 区别.
96. js里变量前面没有声明语句的话是默认是什么?
    1. 在方法中呢?
    2. 假如在类中有个var 声明的变量,会变成当前类的静态变量吗

97. w3c规范和mdn的关系
    1. 如何学习w3c规范

98. 自己搭建服务器,比如nginx然后发布--主要是熟悉
100. json和xml的优劣
101. 跨域
    2. https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434499861493e7c35be5e0864769a2c06afb4754acc6000

102. 事件委托减少DOM事件注册的数量
103. mysql的本质是什么
104. 
Worker<Void> worker = webEngine.getLoadWorker();
worker.cancel();

47. 地图协议
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
的问题；ajax;编码问题，各种的默认编码和编码表，字符串拆分；各种Writer的区别和使用；数据库一对多，多对多等；

61. go编译后的后缀名是什么,在linux和mac中?
62. js arraybuffer和java ByteBuffer
    1. 参考:
        1. https://developer.mozilla.org/en-US/docs/Web/API/ArrayBufferView
        2. https://www.cnblogs.com/copperhaze/p/6149041.html
    2. arraybuffer可以存放object吗?
    3. js 堆栈 内存的笔记,arraybuffer开辟的内存是从哪儿开辟的
    4. arraybuffer和buffer的区别
    6. typed array

63. curl 和wget
    1. curl后面的命令跟括号还有大于小于什么意思
66. inline-block等的深入理解和使用

67. git push dev分支的时候,说master分支本地落后了,然后master分支的推送被拒绝了

    意思是git push会推送所有分支?那么git pull呢
68. 二进制文件删了可以复原吗, 修改不能对吧?

69. 如何搜索某个文件的历史记录
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
98. source-map
99. 防御性编程
100. 面试：页面加载海量数据:https://juejin.im/post/5ae17a386fb9a07abc299cdd
101. PWA介绍及快速上手搭建一个PWA应用:https://juejin.im/post/5ae2f82f6fb9a07acd4d761e
102. H5之地理位置必知必会:https://juejin.im/post/5ae34306f265da0ba60f89bb

99. 从表单取出来的都是字符串吗?
101. js在导出的组件中声明var变量, 会影响其他 组件吗
102. for of不能遍历对象?
103. 腾讯区块链
104. web访问本地文件
105. pom.xml
106. left join和inner join等笛卡尔积还是要继续熟悉
107. 交叉编译
108. study later:elasticsearch
109. IO多路复用
110. 服务编排
    1. apache camel

# problem but ignore
1. 用mac的默认shell切换到分支下的某个目录，然后切换分支再切换回来，这个时候ls显示为空，但是目录下是有文件的，而且其他命令可以访问到目录下的文件。然后用`cd ../current_path`切换到当前目录，ls又能显示里面的文件了。
    1. 怀疑ls有缓存之类的东西，应该跟它的实现原理有关,how it works?

2. 逆向三件套：capstone engine, unicorn engine, keystone engine
3. CPU架构（如：X86 、X86_64 、ARM 、ARM 64、MIPS、SPARC）
4. go cloud项目
5. k8s
6. 区块链
7. 各种语言的转换工具：java,kotlin,js...

# projects
1. mit开源的Scratch

# job requires
1. 深入理解和使用 JSON and RESTful Web Services、RPC 通信接口开发
2. 熟悉消息组件，Kafka、Mongodb、Redis 的使用；