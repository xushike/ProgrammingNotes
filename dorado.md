# dorado
前言
零。概述  
1. dorado的api地址:[http://dorado7.bsdn.org/jsdoc/](http://dorado7.bsdn.org/jsdoc/)
1. 学习dorado最好了解：java、spring、hibernate、db、js、jquery
1. 变量名是区分大小写的。  
2. app-context.xml对应spring的配置文件  
3. 如果无法新建视图文件，应该更新dorado配置规则
4. 配置组建属性的时候，设置后最好按下回车，否则有些属性没有设置上。
5. 
>平面数据：通过键值来表达数据与数据间的关系。例如关系型数据库中的数据。每一条数据都是独立的，它们之间的关系是通过外键值指向另外一个数据的主键值。
立体数据：通过引用来表达数据与数据间的关系。例如通过Hibernate获得的领域模型数据。如我们拿到一个部门对象，部门对象内部还包含所有的雇员对象。
6. dorado7.2.3发布的时候移除了dorado-updater，推荐通过ide中的Dashboard来获取dorado的jar包更新。(目前我这个ide的版本是7.1，里面的dashboard选项不能用)

dorado5点dataset是平面的，dorado7的dataset是立体的
一。安装配置  
二。基础  
1. 基础知识
    1. dorado模型文件：  
    
    1. 关于dataset、datatype、datapath：
        >DataType我们在立体数据模型中提到过，它的目的是为了描述数据实体的各个属性的校验规则、数据类型、显示格式等等；这样我拿到一个数据之后，就可以通过DataType知道其中是一个什么样结构的数据，其中包含哪些属性，有哪些子对象等等;
        >使用的时候一般设置parent、matchType；
        >dataType可以添加propertydef子组件，DataType中propertyDef的命名一定要跟Pojo对象中保持一致，propertydef的name表示数据实体的属性名，label表示实体属性显示出来的名字。
        >dataType里可以设置reference，用el表达式可以动态加载，提高性能(在entity中通过hibernate的配置可以完成数据的全部加载，但是性能没有动态加载高)
        >dataType里可以设置defaultDisplayProperty，里面设置的就是数据实体默认展示的属性值
        >dataType可以不把对应到的属性设置完，甚至设置错了也可能没问题，因为没设置或设置错都使用的默认值

        >DataSet，就是一堆数据的集合，有一个ID，便于其他数据感知控件与其绑定，它用来封装页面的数据，任何时候，当Dataset中存在记录集时，记录指针总是指向其中某条记录。
        >使用的时候一般设置dataProvider、dataType、pageSize(每页显示的个数)

        >dataPath
        >主要使用自定义片段

    2. AutoForm  
    和datagrid一样绑定dataset之后，我点击datagrid中的行，autoform自动绑定我点击的这行，隐藏属性？
    3. action  
        1.  updateAction:
            >基于ajax的更新，一般设置id、执行中信息、执行成功信息、dataResolver(厘米是服定位表达式，对传递到后台的数据持久化)、快捷键。子组件updateItem设置dataSet就行了。execute()方法中的callback可以接受execute()执行成功后的返回值。
        
    4. 数据实体的状态
    5. 映射处理，一般有三种设置方法：
        >通过View配置mapping   
        >利用JS初始化mapping  
        >通过后台方法进行配置  

2. 组件

    1. autoform
    >autoformElement的id似乎可以随意设置，但是name却不能乱设置，name要和dataType的属性名对应

2. 一般开发步骤：
    1. 第一次要先马文hdf-parent，然后马文hex-install,然后配置vpn数据库之类的，然后就可以运行项目了  
    2. 用hibernate生成对应的bean，然后根据bean建立dorado模型文件，然后建立视图文件，然后在视图文件的model中建立继承自模型文件的datatype，在视图文件的view中建立dataset(dataset的datatype设置为前面的datatype)，(目前我的感觉是dataType是约束，dataSet是集合，这两者可以简化成一个吧？)然后在view中建立一些组件来引用dataSet
    3. 配置服务的bean：由于有前后台交互功能，需要在Spring上下文中注册一个用于提供服务的bean，对于这个bean使用Spring提供的@Component标注，如果需要使用@Component注解，需要在项目中WebContent->WEB-INF->dorado-home目录下的app-context.xml文件中增加一个配置，配置如下：
    ```xml
    <context:component-scan base-package="xxx.xxx.xxx"/>
    ```
    4. 数据库开发配置：引入依赖包->生成实体映射类->建dao文件->数据源连接配置->修改app-context.xml(具体待补充)->修改web.xml文件->准备Model
2. 调试：可以用浏览器传统的调试方法，但更推荐用dorado特有的在代码中添加debugger，相当于打了个断点，在浏览器调试的时候会自动停在这儿
3. 基于数据模型的界面开发：
4. EL表达式：分为普通和动态EL表达式；主要区别有亮点：后者求值更晚，后者可以多次计算
    1. 通过EL表达式可以获取session中对象的属性，例如${session.getAttribute('user').employeeName}即从session中的user对象中获取了中文名。

5. 注解(标记)
    1. @Expose标记：是Dorado7专门提供的标注，用于定义可暴露服务，根据这个规则Dorado7会将这个方法自动注册在 ExposedServiceManager中
    2. @Resource注解：被用来激活一个命名资源（named resource）的依赖注入，如：
    ```java
    @Resource
    private SlCompanyDao slcompanyDao;
    ```
    2. @DataProvider和@DataResolver：在运行时注册成全局的DataProvider和DataResolver放在DataProviderManager的对象中，也可以自己在model.xml文件或者view.xml的model节点下定义
    
    
三. 问题
1. project facets的java版本，jetty的jre版本，eclipse中compiler的java版本，项目中jar system library版本的关系？已蒙蔽
2. datagrid的datatype是禁用了的，不能自动生成相关的dataColumn，这个教程上没有说
3. dataType中引用前面两个全局模型文件的时候有golbal标志，我引用第三个的时候没有global标志
4. 启动jetty的时候有个bootstrap是什么东东
5. 维护员工和消息的关联关系?
6. 用动态el表达式的时候不需要异步吗？
7. arguments和context的作用
8. 出错的话怎么用浏览器调试
9. get("data:#")
10. uploadFileAction
11. hibernate和mybatis对比
12. 保存数据的时候，数据的几种状态(数据实体的系统状态)判断的原理
四. 经验
1. 在jetty中运行项目的时候，build文件夹里的class文件有时候不自动生成，refresh项目后立刻又生成了；网上说的是选中project里的build automatically；然后我实践发现我不选中这个它才会运行的时候生成，选中了反而不生成。然后我改了jdk的版本，发现不管选不选中都不生效了，于是关闭项目重启eclipse，然后再运行才有。然后我又删了class，重启项目之后突然又不生成了。最后发现antomatically选不选中应该是没有影响(也可能跟我系统有关)，但是一定要点击project里的clean，然后重新运行就有了。
现在我的jetty已经正常运行了，但是每次修改都哟重新启动jetty，这个时候选中project的build automatically就不用每次重启了。所以上面鼓捣了半天的内容只是因为系统不兼容或者jdk不兼容？？？
2. “有前后台交互功能，需要在Spring上下文中注册一个用于提供服务的bean”，我按demo的步骤在app-context.xml中配置了，结果项目根本启动不了，报的错指向配置，同时还有“Unknown ExposedService”的错，结果fhl告诉我是jdk1.8不行，要用1.7，实践后果然如此。
3. mac上没有bdf插件，于是我把windows上的bdf插件复制过去就好了 
4. 教程中部门分类的顶级分类的parent_id是null，然后下一级的parent_id就是上一层的id
5. yzp写登陆界面的时候，进入页面就报错“can't not read property ‘get’ of undefined”，代码和官方demo一样但是始终会报这个错，最后知道是dorado-core包版本的问题，从7.3换成7.4就好了。
6. 添加新的部门信息的时候报错：[Batch update returned unexpected row count from update [0]; actual row count: 0; expected: 1]()原因是：主键设置为自增长，而在我们插入记录的时候设置了ID的值