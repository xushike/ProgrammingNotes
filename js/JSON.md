# JSON

# 一 概述
json、yaml、xml等的笔记

## 1 简介
JSON的全名JavaScript Object Notation（从名字上就能看出和JavaScript的关系非常紧密），发明人是Douglas Crockford。

作者参考：https://cloud.tencent.com/developer/article/1080320

## 2 历史
### 2.2 json5
json5支持写注释了

```json5
{
    "name":"Tom"       // 你好
}
```

# 三 基础
## 2 yaml
### 2.1 嵌套
实测得知：
1. 以`-`的方式写数组的时候，外层不能有`{}`，否则出现语法错误。

# 六 问题
## 1 已解决
### 1.1 yaml：end of the stream or a document separator is expected
两个对象平行，却没有用数组的方式包裹，就出现了这个错误。

## 2 未解决
### yaml：missed comma between flow collection entries 

# 七 未整理
1. yaml的各种嵌套