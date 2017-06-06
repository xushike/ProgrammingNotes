# dorado
前言
零。概述  
1. 变量名是区分大小写的。  
2. app-context.xml对应spring的配置文件  
3. 如果无法新建视图文件，应该更新dorado配置规则
一。安装配置  
二。使用  
1. 
2. 调试：可以用浏览器传统的调试方法，但更推荐用dorado特有的在代码中添加debugger，相当于打了个断点，在浏览器调试的时候会自动停在这儿
三. 问题
1. project facets的java版本，jetty的jre版本，eclipse中compiler的java版本，项目中jar system library版本的关系？已蒙蔽
四. 经验
1. 在jetty中运行项目的时候，build文件夹里的class文件有时候不自动生成，refresh项目后立刻又生成了；网上说的是选中project里的build automatically；然后我实践发现我不选中这个它才会运行的时候生成，选中了反而不生成。然后我改了jdk的版本，发现不管选不选中都不生效了，于是关闭项目重启eclipse，然后再运行才有。然后我又删了class，重启项目之后突然又不生成了。最后发现antomatically选不选中应该是没有影响(也可能跟我系统有关)，但是一定要点击project里的clean，然后重新运行就有了。
现在我的jetty已经正常运行了，但是每次修改都哟重新启动jetty，这个时候选中project的build automatically就不用每次重启了。所以上面鼓捣了半天的内容只是因为系统不兼容或者jdk不兼容？？？
2. “有前后台交互功能，需要在Spring上下文中注册一个用于提供服务的bean”，我按demo的步骤在app-context.xml中配置了，结果项目根本启动不了，报的错指向配置，同时还有“Unknown ExposedService”的错，结果fhl告诉我是jdk1.8不行，要用1.7，实践后果然如此。
3. mac上没有bdf插件，于是我把windows上的bdf插件复制过去就好了 
