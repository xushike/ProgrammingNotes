# maven
## 一. 概述
1. 和maven同级别的还有ant、gradle
## 一. 安装配置
1. 安装环境要求：  
Maven 3.0/3.1 需要 JDK 1.5 或以上, 而Maven 3.2 要求 JDK 1.6 或以上版本
2. 安装步骤
    1. 下载zip解压
    2. 新建系统变量：M2_HOME，添加%M2_HOME%\bin到path中
3. maven安装目录说明
    * bin：maven的mvn运行脚本
    * boot：包含一个类加载器的框架，mvn用它来加载自己的类库
    * conf：配置文件
        * settings.xml：很多的配置（镜像仓库、默认仓库位置）
    * lib：类库

## 二. 基础
1. maven项目目录说明
    * src
        * main
            * java
                * package
        * test
            * java
                * package
        * resources：资源文件
    * target
        * classes：class文件
        * surefire-reports：测试报告

2. pom.xml
    * modelVersion：代表mvn的版本，固定4.0.0?
    * groupId：项目的包名
    * artifactId：模块名
    * packaging：默认是jar，还有war、zip、pom等
    * name：项目描述名
    * url：项目地址
    * description：项目描述
    * licenses：许可信息
    * organization：组织信息
    * dependencies
        * scope：依赖范围，比如写成test，则只在测试的时候有效。有6种可选，默认compile
        * optional：设置依赖是否可选，默认false
        * exclusions：排除依赖传递列表
            * 
    * dependencyManagement：依赖的管理
    * build
        * plugins：插件列表
    * parent：
    * modules：用来聚合模块
    * properties：定义属性，可用类似el表达式的方式引用

3. 命令，其实maven的命令也是调用的它的插件
    * mvn 
        1. clean：删除target
        2. install：安装jar包到本地仓库
        3. 
        4. compile：编译
4. maven生命周期
    1. clean
        1. pre-clean清理前的工作
        2. clean清理上一次构建生成的所有文件
        3. post-clean执行清理后的文件
    2. default（最核心）
        1. compile
        2. 
    3. site生成站点
        1. 

5. 依赖
    1. 依赖冲突  
    依赖冲突的有两个原则：短路优先、路径相同时则先声明的优先
6. 聚合，当项目中有多个模块需要install的时候，如果一个一个打包太麻烦，这时候就可以用聚合  
需要打包成pom和用到`<module>`
7. 继承，如果有好几个模块都要用到同一个jar，这个时候可以声明一个模块专门来管理公用的包  
需要用到`dependencyManagement`和`parent`
## 三. 使用
1. 用archetype创建目录骨架  
archetype是maven的一个插件
    1. mvn archetype:generate
        * groupId:组织名,一般是公司网址的反写加项目名
        * artifact:一般是项目名-模块名
        * version：版本号（snapshot快照、alpha内部测试、beta公测、release稳定、GA正式发布）
        * package：代码所在的包
2. 使用镜像仓库
## 四. 经验

## 五. 问题
1. settings移到新仓库地址下意义？
2. 本地找不到会去远程找，没网的时候怎么办？
3. 在依赖中引入jetty和直接安装jetty的插件有什么区别？
4. clean的时候不会删除依赖吧？
5. install的时候只是install？