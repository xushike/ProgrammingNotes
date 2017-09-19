# markdown
[TOC]
## 一. 概述
## 二. 安装配置
## 三. 常用语法
### 1. [TOC]
    Table Of Contents (index file)，内容列表、索引，vscode自带的预览目前还不支持
### 2. 标题
    一个#表示一级标题，一直到六级标题，#后面最好跟上空格
### 3. 强调
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

~~This text will be crossed~~

_You **can** combine ~~them~~_
### 4. 链接
    前面是显示的链接，后面是实际链接，引号里是鼠标移上去的tips
[https://github.com](https://github.com "github官网")
### 5. 图片
    可以使用相对路径和绝对路径，语法和链接类似
![Image of Test](img/test.png "Image of Test")
### 6. 引用
    引用中再嵌套引用只需要多加一个>
> We're living the future so
>> the present is our past.
### 7. 列表
    分为有序和无序，有序的时候数字随便填，会自动计算的
### 8. 表格
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

### 9.转义
    不想显示Markdown标记时可以在markdown符号前面加上反斜杠或者用``包裹，比如
*This text will be bold*
    \*This text will be bold\*

### 10.上标和下标
19^th^
H~2~O
### 11. 代码块
    比如下面这个，```后面跟的java就是代码所属的语言
    ```java
    System.out.println("hello world!");
    ```
```java
System.out.println("hello world!");
```
### 12. 行内代码
    就是用``包裹，使用场景很模糊，本人觉得只要不混淆就随便用
### 13.其他
#### 13.1 缩进
1. 半角状态下，在标题下缩进了制表符之后的文字会被识别为普通文字
2. 如果想实现中文里段落开头的缩进，有两种方法（但是我尝试之后发现这个缩进对标题下的第一行无效，后面的行才有效）
    1. 输入法切换到全角，双击空格键
    2. 
        * `半方大的空白&ensp;或&#8194;`
        * `全方大的空白&emsp;或&#8195;`
        * `不断行的空白格&nbsp;或&#160;`



