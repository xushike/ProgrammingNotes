# temp草稿
## 一.问题
1. https://angular.cn/guide/architecture
1. http://jsfiddle.net
2. http://blog.csdn.net/catwindboy/article/details/70210609
3. angular的最佳实践
4. angular自定义管道
5. Angular Material
6. https://www.cnblogs.com/Ewin/archive/2009/10/05/1578322.html
7. tealeg/xlsx
8. AngularJS 是1.x的，2.x以上统一为 Angular
9. angular2和angular4
9. http://www.bootcdn.cn/angular-material-data-table/readme/#demo
10. material-data-table和angular material是什么关系
11. https://weibo.com/segmentfault?ssl_rnd=1510906303.845&is_hot=1
12. css类选择器、css选择器
13. 配合上文click效果，只要加上一行css代码就可以实现click和hover的组合效果，此处务必使用hover伪类，并用!important来提升样式的优先级？
14. declarations和entryComponents
15. nativeElement、Renderer、等（似乎有的是只获取本身，有的是获取包括子级，需要研究研究）
16. 关于时间冒泡
17. css（参考mdn的css）
    1. css的设置有先后顺序吗
    2. css的的颜色设置为none和null有什么区别
    3. 使css无效：https://stackoverflow.com/questions/5218679/how-can-i-nullify-css-property    
    4. 计入笔记部分,比如背景色原来是红色，我修改成绿色,然后再给背景色设置某些值：
        1. auto和none：会保持绿色
        2. null：会变成红色
        3. unset(2017新增？)：会变成默认颜色，白色
        官网的说明是：CSS 关键字 unset 是 关键字 initial 和 inherit的组合。像这两个关键字一样，它允许应用任意的CSS样式，包括CSS速记 all 关键字。如果有继承父级样式，则将该属性重新设置为继承的值，如果没有继承父级样式，则将该属性重新设置为初始值。换句话说这个unset关键字会优先用inherit的样式，其次会应该用initial的样式。
        (待补充)
    5. mouseenter\mouseover
18. dom编程相关的书
19. 指令中的selector的值是css选择器,命名需要遵循驼峰式命名方式，而且可以用`button[xxx]`这样专门用于button下的xxx属性
20. ElementRef和event.target区别
21. Angualr的最佳实践
22. 在Angualr的最佳实践中推荐，
    1. 我们应该为我们定义的每一个指令，组件，服务都添加上前缀。这样做的好处在于：
   确保我们自己声明定义的这些指令，组件，服务不会与标准的HTML属性冲突，也降低与第三方指令，组件，服务冲突的可能性。   
    2. 指令的名称应该具备一定的自解释性，这样方便我们通过指令的名称就能大概知道指令的用途。
23. 指令中
    1. @input使得我们的指令，能够接受外部的输入值，根据不同的输入值表现出不同的能力，通过@Input装饰的输入声明可以确保指令的消费者只能绑定到公开的 API 中的属性，而不是其它的属性。有效的保护了指令或组件的封装性。。我的理解就是接受指令的值，也就是`[xxx]="vvv"`里的vvv，通过`ele.getAttribute("xxx")`也可以获取，但是直接声明的话封装性更好
    2. @HostListener就是监听事件然后做出动作
24. http://blog.csdn.net/shenlei19911210
25. cp的博客
26. http://blog.csdn.net/u013589443/article/details/72875875
27. 调试dom元素时的hover、focus等的查看
28. typescript implements的作用和typescript学习
29. 压缩失败了，回去多练习几次。。。
30. 爸爸去哪儿里的vipkid