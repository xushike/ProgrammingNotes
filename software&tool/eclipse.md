# eclipse
## 一. 概述
1. 版本的特点
    1. 3.5之前的安装插件很麻烦，
## 一. 安装配置
1. 配置git
2. 配置maven,主要设置两点
    1. installations：maven的安装目录
    2. user settings：settings.xml的目录
    3. maven的默认依赖是1.5，在eclipse中显示的时候可能会比较别扭，可以去settings文件中修改profile，将其改为其他版本的jdk，这样默认显示就不会那么别扭了
## 二. 基础
1. 关于work space和work set
    1. space必须设置，每次eclipse启动就会把space的项目加载进来，一个space只能同时被一个eclipse打开
    2. set相当于项目的分类，比如有公司的，有学习的，有其他人的，就可以用set来分类
    3. 个人觉得space可以看做书，set看做目录

## 三. 使用
1. 关于git moudle：import的时候选择projects from folder or archive，切换分支的时候要注意，如果分支里的模块没有引入，是会报错的，所以切换之后第一次要引入  
报的错是：Non-resolvable parent POM...
    >注：老版eclipse上没有这个选项，我还要试试下面两种方式行不行得通  
    1.将的module外面那层目录删掉  
    2.弄清moudule的原理，修改module？
## 四.问题
1. 克隆仓库的时候失败，报错：packfile is truncated.  
2. 点击team里只有Apply Patch、Share Project.  
原因：可能是断电导致的某些信息没有被识别到，也可能是我切换了eclipse的版本  
解决办法：点击share project重新选择到项目git所在目录