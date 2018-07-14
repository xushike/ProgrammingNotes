# server服务器相关

# 一 概述
主要记录web server相关的知识

## 1 简介
虽然每个网页服务器程序有很多不同，但有一些共同的特点：每一个网页服务器程序都需要从网络接受HTTP请求，然后提供HTTP回复给请求者。HTTP回复一般包含一个HTML文件，有时也可以包含纯文本文件、图像或其他类型的文件。

一般来说这些文件都存储在网页服务器的本地文件系统里，而URL和本地档名都有一个阶级组织结构的，服务器会简单的把URL对照到本地文件系统中。当正确安装和设置好网页服务器软件，服务器管理员会从服务器软件放置文件的地方指定一个本地路径名为根目录。

例如，在“example.funnycorp.com”服务器上设置了服务器软件，并把服务器软件的根目录设置为“/home/public/web/”，当一个浏览者输入URL “http://example.funnycorp.com/lips/raspberry.html”，“example.funnycorp.com”上的服务器软件就会读取“/home/public/web/lips/raspberry.html”这个文件。

现在市面上普遍的网页（HTTP）服务器有：
- Apache软件基金会的Apache HTTP服务器
- Microsoft的Internet Information Server（IIS）
- Google的Google Web Server
- Nginx公司的nginx
    - 淘宝从nginx改良的Tengine
- lighttpd公司的lighttpd
- Cherokee_(Web服务器)
- Microsoft的FrontPage


# 三 基础
