# temp4study
1. tty -s
2. 2009-11-10 23:00:00 UTC
3. studyGO放go的一些实用程序,比如反转字符
4. go编写闭包
5. go的指针
6. go数值常量
```go
const (
	Big   = 1 << 100
	Small = Big >> 99
)
```

7. Go playground 中的时间总是从 2009-11-10 23:00:00 UTC 开始， 如何校验这个值作为一个练习留给读者完成
8. 事件冒泡
9. go的blank identifier
10. angular@ViewChild
11. querySelector的用法终于搞懂了，但是似乎并没有什么用
12. element和node的区别
13. 必须在两天内激活windows才能继续使用？
14. git如何查看远程的提交记录？
15. 发文字被转码怎么办
16. 我们项目中用到了jquery了吗
17. developers.google.com
18. querySelector笔记
19. 获取事件的几种方法：
	1. 原生的js似乎只能遍历所有属性来判断
		1. http://blog.csdn.net/theforever/article/details/6029382
	2. google  chrome dev tools 中`getEventListeners(document.querySelector("table tbody tr td span"))`，但只能在浏览器中用
		1. https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference?hl=zh-cn
		1. http://blog.csdn.net/diquren/article/details/50543610
		2. 有没有办法在js中调用呢
		4. chrome 的开发者工具有此功能。选取元素后可以在右侧的 Event Listeners中看到绑定的事件
	3. jquery保存了事件的委托，可以获得
	4. Visual Event 2
		1. https://stackoverflow.com/questions/446892/how-to-find-event-listeners-on-a-dom-node-when-debugging-or-from-the-javascript

20. dispatchEvent 
21. web调试优化:https://segmentfault.com/a/1190000011868916
22. chrome控制台console：https://segmentfault.com/a/1190000002511877
23. console对象
24. https://www.cnblogs.com/yexiaochai/p/3567597.html
25. js事件详解:https://segmentfault.com/a/1190000005016813
26. 根据事件传递的状态来判断是否是从已点击的按钮传过来的？
27. go的三个作者的中英文名
28. 修改ubuntu锁屏时间
29. oracle日期相关操作
30. 区分点击和拖选
	1.  input type ="radio"的内部实现原理，为什么我小范围拖动鼠标会被判断为点击，而选中一个单词就不会触发点击
31. dom l3
32. `ctrl+a  ctrl+k`
33. https://ng.ant.design/#/docs/angular/introduce
34. https://zhidao.baidu.com/question/429999513428017812.html
35. https://material.angularjs.org/latest/demo/virtualRepeat
36. 如何关闭某个应用的一个实例(比如同时打开两个vscode，如何关闭其中一个，快捷键)