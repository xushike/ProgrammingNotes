# java
零. 概述
1. ide(eclipse)中，设置里的compiler版本是jdk的编译版本，而installed JREs是jre(运行环境)的版本，前者不应该比后者高，否则编译出来会出问题，大概就是：  
>JDK1.5编译的程序在JRE1.6中能不能运行？可以。
>JDK1.6编译的程序在JRE1.5中能不能运行？一定不可以。  

比如我前者是1.7，后者是1.6，当我代码打包后放到用1.7去运行应该没问题，但是用1.6去运行就可能出问题。
在eclipse中每个项目可以单独设置自己的compiler版本(即jdk的版本)，但是jre的版本是和eclipse的设置通用的。
还有运行时服务器需要的jdk or jre版本我还没研究，因为目前我都是在jetty容器中测试的，而上面的可能只是针对项目，跟容器可能不一样，所以上面的结论可能都是错的(虽然网友也是上面的结论)。
再加一条网友的结论吧：
>Java Compiler选择的版本必须和'Project Facets'中指定的java版本一致。
>否则eclipse会抛异常：Java compiler level does not match the version of the installe

2. 关于project facets，相当于针对语言或者框架的首选项，比如里面的java设置了1.6，那么我新建一个项目，某人的jdk应该是1.6(当然我还要测试一下这个设置和项目以及ide设置的优先级才能确定)

一. 安装配置
1. mac上安装之后查看java路径：/usr/libexec/java_home，一般显示结果是：/Library/Java/JavaVirtualMachines/jdk1.8.0.jdk/Contents/Home
