# python
# 一 概述
## 1 简介
大小写敏感

### 优点
1. 动态语言，灵活、简单、强大、简洁,专注于解决问题,拥有丰富的资源,无需浪费时间造轮子
2. 在网络爬虫、数据分析、数据挖掘、AI、机器学习、Web开发、金融、运维、测试等多个领域都有不俗的表现
3. Python 强有力的数据处理能力能够将繁琐凌乱的数据轻松转换为结构化数据，以至于成为了最受欢迎的语言。
4. 喜欢Python的原因很简单，因为它确确实实给开发者带来了愉悦的编程体验。

### 缺点
1. 网友:由于历史的原因，Python 的部署工具生态相当混乱
2. stream.io创始人Thierry Schellenbach：
    1. Python 非常棒，但是其在序列化/去序列化、排序和聚合中表现欠佳。我们经常会遇到这样的问题：Cassandra 用时 1ms 检索了数据，Python 却需要 10ms 将其转化成对象。

### 他人评价
朋友:
1. 最优雅的语言

网友:
1. 库很强大
2. 创业公司多，python出活快，雇程序员可以少一些;应用面广;简单易学

## 2 历史
Python有两个版本，一个是2.x版，一个是3.x版，这两个版本是不兼容的。但是3.x版会越来越普及

### python是怎么火起来的

## 3 常识
### 3.1 吉祥物蟒蛇
python(意思是蟒蛇)，因为作者喜欢一个叫MontyPython的喜剧团体

### 3.2 Pythonic
Pythonic 就是很 Python 的 Python 代码，一般用来形容python特有的代码(明显区别于其他语言的写法)

## 4 文档等
1. 官方
    1. https://docs.python.org/3/library/
1. 《python核心编程》：了解python的工作机制--包括数据对象和内存管理之间的关系--你将成功一名更高效的python程序员
2. 阮一峰python教程:https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000
3. Google Colab：练习python的好地方，直接云端跑代码。似乎连国外的老师都推荐。
   1. 参考：https://sspai.com/post/52980
4. 《The Zen of Python》(python的禅宗)
    1. Beautiful is better than ugly.（美丽胜于丑陋）
    2. Explicit is better than implicit.（明了胜于晦涩）
    3. 。。。

# 二 安装配置
## 3 mac

# 三 基础
## 0 架构

### 包的导入
使用：
1. 导入内置包`import package_name`比如`import math`
2. 导入本地包的函数：如果`my_abs()`的函数定义保存到了`abstest.py`文件了，那么，可以在该文件的当前目录下用`from abstest import my_abs`来导入`my_abs()`函数

## 1 工具生态
### python
使用：有两种用法
1. python命令行交互：命令行模式下输入`python`回车，就进入到Python交互模式，它的提示符是`>>>`
2. `python example.py`运行指定的`.py`文件

### pip and pip3
使用：
1. 查看已安装package的信息`pip show package_name`
    1. `location`本地安装位置

## 3 数据类型

使用：
1. 检查数据类型：使用内置的`isinstance()`

    ```python
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    ```

### 字符串
python3的字符串默认使用Unicode编码。

## 4 流程控制
### 4.1 if else
使用：
1. python的if可以后置

    ```py
    return a if a>b else b
    ```

## 5 函数
参考：
1. https://docs.python.org/3/library/functions.html


使用：
1. 定义函数:使用关键字`def`

    ```python
    # 定义空函数
    def func_name():
        # pass可以看做占位符，用于打桩，可以先提前写好，保证代码的运行
        # 缺少了pass则会报语法错误
        pass 
    ```
2. 函数的返回值：是`tuple`类型
2. 调用函数：调用函数时如果参数个数不对，则会抛出`TypeError`错误

## 6 面向对象
使用：
1. 定义类

    ```python
    class Student(object): # class关键字用于定义类

        # 特殊方法__init__，类似于其他语言的new()
        # 注意它前后分别有两个下划线
        # 第一个参数必须是self，self就指向创建的实例本身
        def __init__(self, name, score): 
            self.name = name
            self.score = score

        def print_score(self):
            print('%s: %s' % (self.name, self.score))

    # 创建实例
    student = Student("tom",99)
    ```

# 四 高级
# 五 经验
## 2 库
1. 科学计算领域的NumPy和SciPy
2. 网页开发的Django
3. 机器学习领域鼎鼎大名的scikit-learn
4. 自然语言处理的nltk
5. json处理：dumps和loads

### 输入输出
#### 输入
获取输入:`input()`

#### 输出
输出的格式化有几种方式：
1. 占位符：python占位符的格式化方式和C语言一样

    ```python
    'Age: %s. Gender: %s' % (25, True)
    'Age: 25. Gender: True'
    ```

2. 字符串的`format()`方法：写起来比较繁琐
3. `f-string`:类似于js的模板字符串。以`f`开头的字符串

    ```python
    r = 2.5
    s = 3.14 * r ** 2
    print(f'The area of a circle with radius {r} is {s:.2f}')
    The area of a circle with radius 2.5 is 19.62
    ```

### requests
`requests.get()`等方法是短连接，而`requests.Session().get()`是长连接

```py
import requests

r = requests.get('https://github.com/Ranxf')       # 最基本的不带参数的get请求
r1 = requests.get(url='http://dict.baidu.com/s', params={'wd': 'python'})      # 带参数的get请求
```

# 六 问题
1. pip是啥
2. interpreter是啥,IDLE是啥

## 1 已解决
### 1.1 更新pip和pip3
mac正确更新pip3的方法`sudo python3 -m pip install --upgrade pip`

#### 提示 SSL: TLSV1_ALERT_PROTOCOL_VERSION
出现这个错误的原因是python.org已经不支持TLSv1.0和TLSv1.1了。更新pip可以解决这个问题。但是如果使用传统的`python -m pip install --upgrade pip`的方式，还是会出现那个问题。这是一个鸡和蛋的问题，你因为TLS证书的问题需要去升级pip，升pip的时候又因为TLS证书的原因不能下载最新版本的pip。最后只能手动的去升级pip：`curl https://bootstrap.pypa.io/pip/2.7/get-pip.py | python`
1. 如果是在mac，可能提示使用`/Library/Frameworks/Python.framework/Versions/2.7/Resources/Python.app/Contents/MacOS/Python -m pip install --upgrade pip`这个命令来切换到最新的pip

todo

# 七 待整理
## 1 已整理
### 元组(tuple)
元组（tuple）是关系数据库中的基本概念，关系是一张表，表中的每行（即数据库中的每条记录）就是一个元组，每列就是一个属性。 在二维表里，元组也称为行。在python中,元组和列表十分类似，只不过元组和字符串一样是不可变的，即你不能修改元组。元组通过圆括号中用逗号分割的项目定义。(待补充)

1. 布尔型为True、False，注意大小写
2. 缩紧规则：具有相同缩进的代码被视为代码块
>缩进请严格按照Python的习惯写法：4个空格，不要使用Tab，更不要混合Tab和空格，否则很容易造成因为缩进引起的语法错误。

3. dict的第一个特点是查找速度快，无论dict有10个元素还是10万个元素，查找速度都一样。而list的查找速度随着元素增加而逐渐下降。  
第二个特点：无序；第三个特定：key不可变(比如Python的基本类型如字符串、整数、浮点数都是不可变的)

## 2 未整理
1. awesome-python
2. python的timeit时间监控模块
3. search "学了Python后,我走哪里都可以连WIFI!为什么?反正就是这么强!"
4. Django框架
5. https://www.zhihu.com/pub/book/19550511
6. 关于爬虫，这里有一份《中国焦虑图鉴》：http://developer.51cto.com/art/201807/579966.htm###
7. 数据清洗
8. 数据可视化
    1. 词云图