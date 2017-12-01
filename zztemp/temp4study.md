# temp4study
1. http的笔记
2. 知乎live：https://www.zhihu.com/lives/，可以回看吗
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
26. 根据事件传递的状态来判断是否是从已点击的按钮传过来的？
27. go的三个作者的中英文名
29. oracle日期相关操作
31. dom l3
32. `ctrl+a  ctrl+k`
33. https://ng.ant.design/#/docs/angular/introduce
34. https://zhidao.baidu.com/question/429999513428017812.html
35. https://material.angularjs.org/latest/demo/virtualRepeat
36. 软件设计的一些理念规则：比如开闭原则。。。
25. js事件详解:https://segmentfault.com/a/1190000005016813
37. 成都市城乡房屋管理局
38. 异步查询，动态显示搜索结果
39. git fetch
40. 可记为博客
	1. http://www.nowamagic.net/

41. linux新建文件以及文件类型，创建时的后缀可以变为类型吗
42. htmlelement->htmlinputelement
43. restful
44. libreoffice显示目录
45. 代码生成器和项目命名规范
46. not all go tools are avaliable on the $GOPATH
47. oracle的两条竖线
48. 递归查询和插入
49. oracle的价格
50. 项目中的*号和go的星号和angular的星号
51. 如果有两个db怎么办，框架里db的逻辑是怎么样的
52. oracle函数：
	CREATE OR REPLACE FUNCTION wlwk_f_split(p_str       IN VARCHAR2,
                                       p_delimiter IN VARCHAR2 default (',') --分隔符，默认逗号
                                       ) RETURN split_type IS
  j        number := 0;
  i        number := 1;
  len      number := 0;
  len1     number := 0;
  str      VARCHAR2(1000);
  my_split split_type := split_type();
BEGIN
  len  := LENGTH(p_str);
  len1 := LENGTH(p_delimiter);

  WHILE j < len LOOP
    j := INSTR(p_str, p_delimiter, i);
  
    IF j = 0 THEN
      j   := len;
      str := SUBSTR(p_str, i);
      my_split.EXTEND;
      my_split(my_split.COUNT) := str;
    
      IF i >= len THEN
        EXIT;
      END IF;
    ELSE
      str := SUBSTR(p_str, i, j - i);
      i   := j + len1;
      my_split.EXTEND;
      my_split(my_split.COUNT) := str;
    END IF;
  END LOOP;

  RETURN my_split;
END;

55. http状态码
56. 类型转换难道用as？
57. 如何在有程序运行的情况下清shell屏
58. 各种字符串和反斜杠的处理
59. ele["contend"]和ele.content和ele.()等
60. 试试在外面xshell可不可以连接到里面
61. 内置的内置的make函数
62. 复制打包等命令
63.         let params = Object.assign({}, args || this.oldParams);
64. 为什么虚拟机关ubuntu经常停在黑屏
65. oracle里我之前写那个，如果把agent_id写到里面和写到外面有什么区别？效率上来讲？先筛选再连接是不是更快?
66. 四川500个机场的新闻
67. js遍历对象和遍历数组等

68. 我们项目中，getFirstRow和scala和getrows等的区别，以及获取回来的值的获取方法？
69. analys tool missing
70. 远程如何连到局域网内的机子？
71. source 就是. ?
  [http://blog.csdn.net/codeur/article/details/54783288?utm_source=itdadao&utm_medium=referral](http://blog.csdn.net/codeur/article/details/54783288?utm_source=itdadao&utm_medium=referral)

72. go get显示copy状态
73. linux文件安装在什么位置比较好
74. 同时执行多条命令怎么搞，连接多个命令用什么
75. 公司项目中组件名字用`-`不要用`.`？
76. r interface{}