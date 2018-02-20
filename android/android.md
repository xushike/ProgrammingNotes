# android
[TOC]
## 一 概述
### 1 简介
Android系统是由Andy Rubin创建的，后来被Google收购了.有趣的是Android系统的命名都是以点心来命名的.

### 3 常识
1. `xmlns:xxx="..."`:表示命名空间

### 4 文档
### 5 网站
1. 菜鸟教程for Android:[Android 基础入门教程](http://www.runoob.com/w3cnote/android-tutorial-android-studio.html)
2. 关于设计规范(排版,文字大小,颜色,布局等),可以参考google的:[Material Design](https://material.io/guidelines/style/typography.html#)

    值得好好研究,特别是没有产品经理的时候.

    1. 大量使用无边框图片
    2. 元素间最好留一些空隙
    3. 不建议使用太多的风格和字体,一般3到4种即可
    4. 颜色也不要太多,特别是材料(倾向于使用大片的饱和色)
    5. 对于重要元素可以使用浮动,高亮等

## 三 基础
### 1 未整理
1. Android应用的界面使用布局（ViewGroup 对象）和微件（View 对象）层次结构构建。布局是一种不可见的容器，用于控制其子视图在屏幕上的位置。微件是界面组件，例如按钮和文本框。
2. 嵌套布局会增加绘制界面所需的时间。
3. 您还可以使用顶部或底部边缘创建水平对齐，不过，按钮在其图像周围包含内边距，因此如果您按照这种方式对齐这些视图，视觉对齐将是错误的。


### 2 ...


## 四 高级
### 1 真机调试
[http://expelliarmus923.github.io/2017/03/31/%E7%9C%9F%E6%9C%BA%E8%B0%83%E8%AF%95%E5%90%84%E7%A7%8D%E6%96%B9%E6%B3%95/](http://expelliarmus923.github.io/2017/03/31/%E7%9C%9F%E6%9C%BA%E8%B0%83%E8%AF%95%E5%90%84%E7%A7%8D%E6%96%B9%E6%B3%95/)

### 2 Udacity的google Android课程
#### 入门课程
##### 课程1A:视图VIEWS
使用大驼峰写法
1. 显示文字的叫TextView

    1. 默认背景颜色是透明色
    2. 宽高参数值`wrap_content`:根据文字的长度自动调整宽高
    3. 值前面的`@`表示要引用资源,比如引用图片,自带的颜色等.

2. 图片=>ImageView
    1. 对齐属性`scaleType`
        1. `center`:居中,不会对图片大小做修改
        2. `centerCrop`:居中,同时自动调整图片大小(保持原有的纵横比?)
3. 按钮=>Button
4. others
##### XML语法
1. 一般这样写:`<xxx ... />`;有子元素的时候,这样写阅读体验更好:`<xxx ... > /xxx>`
2. 属性

    因为是XML,所以属性要用引号(双引号)包裹

3. [XML可视化工具链接](http://labs.udacity.com/android-visualizer/#/android/xml-syntax-errors)
##### 更改TextView
1. 推荐使用dp单位,这样在不同分辨率的手机上看到的大小是一样的;如果用px就不一样.
2. 推荐所有可触摸的目标,比如button的宽高最少为48dp
3. 关于文字外观(待阅读):[Text appearance and theme attributes on Android](http://discussions.youdaxue.com/t/text-appearance-and-theme-attributes-on-android/6947)
4. 修改颜色

    Android自带的颜色是一个有限集,比如`blue`就没有,但是支持十六进制的所有颜色(Hex color).写法是`#xxxxxx`

##### 解决错误
1. [常见视图备忘单](http://cn-static.udacity.com/nd801/Common_Android_Views_Cheat_Sheet.pdf)

#### 课程1B:打造布局
一些概念如下
- 视图组（ViewGroups）
- 根视图（Root View）
- 父（Parent）
- 子（Child）
- 兄弟姐妹（Sibling）

##### ViewGroups
类似于视图的容器,分类如下

- 线性布局（LinearLayout）
    1. 位置权重

        类似于比例布局
        1. 如果权重为0,则宽高会使用设置的值

- 相对布局（RelativeLayout）

##### 宽度和高度
"子视图的高宽和位置是由父视图决定的"这句话如何理解

### 3 Android官网的培训
[https://developer.android.com/training](https://developer.android.com/training)

## 五 经验
### 1 app推荐
洋葱数学

## 六 问题
### 2 未解决
1. android framwork和anfroid sdk
2. 统一推送联盟
3. Hybrid App（混合模式移动应用）是指介于web-app、native-app这两者之间的app，兼具“Native App良好用户交互体验的优势”和“Web App跨平台开发的优势”。

    其他信息可先参考百度百科.
4. android的c++开发包叫做ndk,就是native开发包
5. Android上页面推荐使用rem单位?
6. [Listview与Adapter的关系和简单应用](http://blog.sina.com.cn/s/blog_a364999b01014kzl.html)