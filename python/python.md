# python
# 一 概述
## 1 简介
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
### python是怎么火起来的

## 3 常识
### 3.1 吉祥物蟒蛇
python(意思是蟒蛇)，因为作者喜欢一个叫MontyPython的喜剧团体

### 3.2 Pythonic
Pythonic 就是很 Python 的 Python 代码，一般用来形容python特有的代码(明显区别于其他语言的写法)

## 4 文档等
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
## 1 内置数据类型

## 2 正则表达式

# 四 高级
## 1 库
1. 科学计算领域的NumPy和SciPy
2. 网页开发的Django
3. 机器学习领域鼎鼎大名的scikit-learn
4. 自然语言处理的nltk

## 2 json处理
dumps和loads

# 六 问题
1. pip是啥
2. interpreter是啥,IDLE是啥

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