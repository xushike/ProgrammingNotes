# android
[TOC]
## 一 概述
### 1 简介
Android系统是由Andy Rubin创建的，后来被Google收购了.有趣的是Android系统的命名都是以点心来命名的.

### 3 常识
#### xml文件开头的声明
形如`xmlns:xxx="..."`:因为XML文件不仅仅用于Android,还可以用于很多地方,所以这句声明表示该XML文件用于Android的开发和布局(这也就是所有属性前都加了`android:`的原因),也可以理解为命名空间(?)
1. 而且,所有的布局文件中都需要加入xmlns开头的两个声明,否则不能正确运行.
2. 更多信息(待研究):[What does “xmlns” in XML mean?](https://stackoverflow.com/questions/1181888/what-does-xmlns-in-xml-mean)
3. 还可以使用tools命名空间,帮助很大 

    比如`tools:text`,相当于占位符,在预览的时候不会显示,而是用于动态展示.

#### 代码的`@`
一般表示指定某种资源

- 指定id:`android:id = " @+id/ben_text_view"`

    指定id时,值以字母开头,不能有空格和特殊符号;其中的"+"号只有在第一次声明id的时候用到
- 指定图片路径:`android:src = " @drawable/[pic_name]"`,不需要图片的扩展名
- 指定颜色
    1. 值`@android:color/[color_name]`:指定Android标准颜色,比较有限
    2. 十六进制,支持所有颜色

#### Android Go
谷歌推出的专为低配手机用的系统,相当于Android8的精简版

#### Android Instant Apps和微信小程序
两者都是免安装的应用.只不过 Instant Apps 是基于 Android 操作系统的，微信小程序是基于微信 App 生态的，但本质上还是不一样的，Instant Apps 本质上还是原生 App，只不过允许你在下载安装之前，先体验下 App 部分模块的功能，觉得不错，适合你，那么你可以再下载安装，而微信小程序本质上不是原生应用，他是基于一种类似 React Native 的框架来达到原生的体验，而且只能在微信内部运行。
Instant Apps 体验更好，功能更强大，可以独立运行在手机上，而微信小程序没法独立运行，是基于微信生态下的应用，而且技术上也有一些限制。
1. Instant Apps的缺点
    1. Instant Apps 深度链接的识别需要依赖 Google Play(但是国内需要梯子)
    2. 只支持 Android 平台，iOS 不支持

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
    6. 关于文本和设备边缘的间隔:16dp最佳;文件之间的间隔:8dp最佳.
    7. 最好不要有启动动画

3. 某机构收集的android学习资料:[Android 学习资料收集](https://github.com/Freelander/Android_Data)


## 二 安装配置
### 1 win
### 2 mac
#### 新建项目
1. Company Domain:应用的唯一标识符,看起来像一个网址,一般填入的是`[my_name].com`,这个值反转后就是应用发布后的包名(package name)(google app和手机会根据这个来识别你的应用?),所以必须是在全世界发布的app中都是唯一的才行.
3. project location:AS会创建一个默认位置,一般用它就好.
4. 选择设备和版本

    设备有手机和平板,TV,Wear,Glass等选项.选版本时选"help me choose"会出现不同版本的使用情况

5. 选择模板

    blank activity和empty activity

6. 创建后的文件结构查看方式:推荐用Android
7. 在手机上运行
    大神推荐Nexus 5
    1. 开启开发者选项和USB调试
        
        第一次需要点击版本号好几次(?),然后设置里就有开发者选项了.
    2. usb连接
    3. install derver(windows only):因为mac下默认是允许连接的
    4. install apo

8. 在模拟器上运行

    第一次运行模拟器的时候可能会不正常,大部分问题都可以解决,但更推荐使用真机.

## 三 基础
### 1 未整理
1. Android应用的界面使用布局（ViewGroup 对象）和微件（View 对象）层次结构构建。布局是一种不可见的容器，用于控制其子视图在屏幕上的位置。微件是界面组件，例如按钮和文本框。
2. 嵌套布局会增加绘制界面所需的时间。
3. 您还可以使用顶部或底部边缘创建水平对齐，不过，按钮在其图像周围包含内边距，因此如果您按照这种方式对齐这些视图，视觉对齐将是错误的。
4. 关于接口,抽象类和具体类
    接口是完全没有实现,抽象类是部分实现,具体类是完全实现;编写代码的时候具体用哪个要看情况.

### 2 文件结构
#### 2.1 android视图模式
该视图模式也是google官方推荐的模式,app目录里的文件大概如下
1. mainfests
    - AndroidManifest.xml

        视图主文件,包含:
        1. 包名(package name)
        2. 应用组件:如activity name,intents,通知权限,最低api等
2. java
3. res:包含应用外观的所有内容
    1. drawable:放置图片
    1. layout:包含app设计和布局的xml
    2. menu
    3. mipmap:放置应用图标
    4. values

### 3 Intent
分为隐式和显式Intent,显式就是指定具体的Intent,隐式就是不知道具体的,比如打开一个网页,不管哪个浏览器app,只要能打开网页就行.
#### 3.1 隐式Intent
可以设置更具体的一些信息,同时还要对没有可选的情况进行处理

### 4 布局
#### 4.1 ViewGroups
类似于视图的容器,分类如下

- 线性布局（LinearLayout）
    1. 位置权重

        类似于比例布局
        1. 如果权重为0,则宽高会使用设置的值

- 相对布局（RelativeLayout）

    其中的子元素不设置的话默认会放在左上角.
    1. 子元素布局

        用`layout_xxx`来设置,比如相对于某个兄弟元素的左边可以用`layout_toLeftOf`,较某兄弟元素下面用`layout_below`,和父元素的右对齐可以用`layout_alignParentRight`

- 约束布局(ConstraintLayout)

    Android Studio默认使用约束布局

### 5 日志
根据日志的严重情况分为五个类别,分别是xxx,都接受两个参数,第一个是消息来自何处,一般填类名,第二个参数就是消息内容.

### 6 可回收的视图
#### 6.1 ListView
1. 视图回收
3. ArrayAdapter

#### GridView
#### RecyclcerView

### 7 Activity


## 四 高级
### 1 真机调试
[http://expelliarmus923.github.io/2017/03/31/%E7%9C%9F%E6%9C%BA%E8%B0%83%E8%AF%95%E5%90%84%E7%A7%8D%E6%96%B9%E6%B3%95/](http://expelliarmus923.github.io/2017/03/31/%E7%9C%9F%E6%9C%BA%E8%B0%83%E8%AF%95%E5%90%84%E7%A7%8D%E6%96%B9%E6%B3%95/)

### 2 Udacity的google Android课程
整个纳米学位免费的课程如下
- Android 基础：用户界面
- Android 基础：用户输入
- Android 基础：多屏应用
- Android 基础：网络
- Android 基础：数据存储

#### 课程1 入门课程
##### 课程1A:视图VIEWS
使用大驼峰写法
1. 显示文字的叫TextView

    1. 默认背景颜色是透明色
    2. 宽高参数值`wrap_content`:根据文字的长度自动调整宽高
    3. 属性`textStyle`:指定文字是粗体或斜体
    4. 属性`textAlignment`:文字在视图中对齐的方式
    5. 属性`textSize`:文字大小,推荐使用sp
    6. 属性`fontFamily`:设置字体
    7. 属性`textColor`:文字颜色

2. 图片=>ImageView
    1. 属性`scaleType`:图片的对齐方式
        1. `center`:居中,不会对图片大小做修改
        2. `centerCrop`:居中,同时自动调整图片大小填充满整个屏幕(保持原有的纵横比?)
    2. 
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

##### 宽度和高度
"子视图的高宽和位置是由父视图决定的"这句话如何理解
##### 内外边距
内外边距可用于所有视图,padding和margin的默认值是0;设置了margin之后就像在视图的周围有一道防护,阻止其他元素进入.
##### 课程1C:课程实践
#### 课程2 用户输入
##### 课程2A:制作一款交互性应用
##### 课程3B:面向对象编程
###### intent
android框架的重点之一,调用其他应用.comment intents.


### 3 Android官网的培训
[https://developer.android.com/training](https://developer.android.com/training)

### 4 ARCore 
### 5 Google Lens
能实时识别用智能手机相机所拍摄的物品并提供与之相关的内容，都是通过利用强大的计算机视觉算法实现的

## 五 经验
### 1 app推荐
洋葱数学

### 2 各机型的一些笔记
#### 2.1 魅族
SmartBar

#### 2.2 小米



## 六 问题
### 2 未解决
1. android framwork和anfroid sdk
2. 统一推送联盟
3. Hybrid App（混合模式移动应用）是指介于web-app、native-app这两者之间的app，兼具“Native App良好用户交互体验的优势”和“Web App跨平台开发的优势”。

    其他信息可先参考百度百科.
4. android的c++开发包叫做ndk,就是native开发包
5. Android上页面推荐使用rem单位?
6. [Listview与Adapter的关系和简单应用](http://blog.sina.com.cn/s/blog_a364999b01014kzl.html)

7. ViewGroup中设置的属性是干嘛的
8. dimens文件
9. `layout_padding`和`margin`的区别,我怎么感觉两者差不多呢?
10. 不同视图的id可以相同?
11. logcat
12. 如何给xml中的属性注释

## 七 待整理
1. [去哪儿查找android资料](https://classroom.udacity.com/courses/ud836/lessons/4329970891/concepts/43237591300923)
2. 导入项目的几种方式
3. ADB
4. [Android 性能优达学城课程，其中也介绍了Memory Monitor](https://classroom.udacity.com/courses/ud825/lessons/3846748822/concepts/37868186490923)

5. 微信公众平台接口测试帐号申请 
6. JuiceSSH

7.  12 栏响应式栅格布局?