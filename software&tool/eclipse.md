# eclipse
一. 安装配置
1. 配置git
二. 基础

三. 使用
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
