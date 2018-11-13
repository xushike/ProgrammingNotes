# go-crawler

# 三 基础
普通退出：`server.Close()`
HTTP Server优雅退出(gracefullly exit)：`http.Server.Shutdown()`

自动实现接口的缺点：自动实现接口乍一看似乎很有用，但这样会让事情变得复杂，特别是在大型应用中，如果有几个接口拥有相同的方法，那么就会点让人摸不着头脑。开发者实际想要实现哪个接口？或许他们应该在代码的注释中写清楚！有一个解决方案用于确保一个类型实现了一个接口，就像 Java 的implements关键字一样，这实在是太简单了：
```golang
type MyStruct struct{} 
func (m MyStruct) Sort(other Sortable){} 
var _ Sortable = MyStruct{} 
var _ Sortable = (*MyStruct)(nil) 
```

Go官网的server是32位的

Golang 标准包布局：https://www.jianshu.com/p/022ba2dd9239

# 六 问题
## 1 已解决
### 1.1 复用http.request.body的方法
requset.body默认是readcloser

方法一：取出来之后再用`ioutil.NopCloser()`设置进去
```go
// 把request的内容读取出来
var bodyBytes []byte
if c.Request.Body != nil {
 bodyBytes, _ = ioutil.ReadAll(c.Request.Body)
}
// 把刚刚读出来的再写进去
c.Request.Body = ioutil.NopCloser(bytes.NewBuffer(bodyBytes))
```

# 七 未整理
1. https://blog.csdn.net/kenkao/article/details/55505742
2. 参考：https://blog.csdn.net/superwebmaster/article/details/80319502