# goroutine

# 一 概述
golang的goroutine笔记，因为内容复杂，所以单独弄一个笔记，主要是goroutine，也包括相关的内容。

## 3 常识
### 3.1 linux进程分类
- 内核线程（或者叫核心进程）：
    1. 内核线程没有独立的地址空间
    2. 只在内核空间运行，从来不切换到用户空间去。内核进程和 普通进程一样，可以被调度，也可以被抢占
- 用户进程
- 用户线程

### 3.2 多线程和异步的关系
异步是目的，而多线程是实现异步的一个可选方法，不用多线程也可以实现异步。

#### 异步
异步与同步相对，当一个异步过程调用发出后，调用者在没有得到结果之前，就可以继续执行后续操作。当这个调用完成后，一般通过状态、通知和回调来通知调用者。对于异步调用，调用的返回并不受调用者控制。

对于通知调用者的三种方式，具体如下：
1. 状态：即监听被调用者的状态（轮询），调用者需要每隔一定时间检查一次，效率会很低。
2. 通知：当被调用者执行完成后，发出通知告知调用者，无需消耗太多性能。
3. 回调：与通知类似，当被调用者执行完成后，会调用调用者提供的回调函数。

异步操作的本质：所有的程序最终都会由计算机硬件来执行，所以为了更好的理解异步操作的本质，我们有必要了解一下它的硬件基础。 熟悉电脑硬件的朋友肯定对DMA这个词不陌生，硬盘、光驱的技术规格中都有明确DMA的模式指标，其实网卡、声卡、显卡也是有DMA功能的。DMA就是直 接内存访问的意思，也就是说，拥有DMA功能的硬件在和内存进行数据交换的时候可以不消耗CPU资源。只要CPU在发起数据传输时发送一个指令，硬件就开 始自己和内存交换数据，在传输完成之后硬件会触发一个中断来通知操作完成。这些无须消耗CPU时间的I/O操作正是异步操作的硬件基础。所以即使在DOS 这样的单进程（而且无线程概念）系统中也同样可以发起异步的DMA操作。

## 4 文章
1. 15分钟读懂进程线程、同步异步、阻塞非阻塞、并发并行：https://www.cnblogs.com/mhq-martin/p/9035640.html

# 三 基础
## 1 线程的状态
线程也有就绪、阻塞和运行三种基本状态和死亡状态。就绪状态是指线程具备运行的所有条件，逻辑上可以运行，在等待处理机；运行状态是指线程占有处理机正在运行；阻塞状态是指线程在等待一个事件（如某个信号量），逻辑上不可执行。每一个程序都至少有一个线程，在进程入口执行的第一个线程被视为这个进程的主线程，很多语言中都是以`main()`方法作为入口，当调用此方法时系统就会自动创建一个主线程。

挂起、睡眠和阻塞：挂起和睡眠是主动的，挂起恢复需要主动完成，睡眠恢复则是自动完成的，因为睡眠有一个睡眠时间，睡眠时间到则恢复到就绪态。而阻塞是被动的，是在等待某种事件或者资源的表现，一旦获得所需资源或者事件信息就自动回到就绪态。

阻塞调用和非阻塞调用：阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程。

阻塞、唤醒、执行、销毁、挂起、睡眠、休眠（待整理）

## 3 sync.WaitGroup
作用：它能够一直等到所有的goroutine执行完成，并且阻塞主线程的执行，直到所有的goroutine执行完成

## 4 信号量
对信号量有4种操作
1. 初始化（initialize），也叫做建立（create）
2. 等信号（wait），也可叫做挂起（suspend）
3. 给信号（signal）或发信号（post）
4. 清理（destroy）

## 5 死锁
死锁的规范定义：集合中的每一个进程都在等待只能由本集合中的其他进程才能引发的事件，那么该组进程是死锁的。操作系统中的定义：所有的线程或进程都在等待资源的释放。如果只有一个线程也是可以发生死锁的。

## 7 Goroutines和Channels
### 未整理
1. 网友:goroutine 并不是 “把异步回调的代码用同步的方式来写”。而是在用户空间实现了一个 M 对 N 的调度器。 
简单来讲，异步回调一般只开一个线程，有任务了之后会把让这个线程去执行这个任务，无法利用多核。 
而 goroutine 会根据机器的运行情况开 N 个操作系统级别的线程，然后把 M 个用户级别的 goroutine 调度到这 N 个线程上。 
golang 团队一直引以为傲的就是这个 M 对 N 的调度器，这种 M 对 N 调度器在业界也算是比较先进的。
2. 网友:协程不是异步回调，协程是状态的保存和切换，这种思想很容易写出异步代码，实现同样的异步功能， c++或者 java 之类的写到你想吐

### 7.1 goroutine
是一种比线程更加轻盈、更省资源的协程.使用 4K 的栈内存就可以在堆中创建它们。因为创建非常廉价，必要的时候可以轻松创建并运行大量的协程（在同一个地址空间中 100,000 个连续的协程）。协程的栈会根据需要进行伸缩，从而动态的增加（或缩减）内存的使用，不会出现栈溢出，所以coder不用关心栈的大小；栈的管理是自动的，但不是由垃圾回收器管理的，而是在协程退出后自动释放。Go 运行时可以聪明的意识到哪些协程被阻塞了，暂时搁置它们并处理其他协程。

存在两种并发方式：确定性的（明确定义排序）和非确定性的（加锁/互斥从而未定义排序）。Go 的协程和通道理所当然的支持确定性的并发方式（例如通道具有一个 sender 和一个 receiver）

实现方式：协程是通过使用关键字 go 调用（执行）一个函数或者方法来实现的（也可以是匿名或者 lambda 函数。协程可以在程序初始化的过程中运行（在 `init()` 函数中）。`main（）`函数也可以看成一个协程。

在一个协程中，比如它需要进行非常密集的运算，你可以在运算循环中周期的使用 runtime.Gosched()：这会让出处理器，允许运行其他协程；它并不会使当前协程挂起，所以它会自动恢复执行。使用 Gosched() 可以使计算均匀分布，使通信不至于迟迟得不到响应。

协程是独立的处理单元，一旦陆续启动一些协程，你无法确定他们是什么时候真正开始执行的。你的代码逻辑必须独立于协程调用的顺序。

`main() `退出时，main()中创建的协程会随着程序的结束而消亡

使用场景：
1. 比如在一个非常长的数组中查找一个元素。

常用操作：
1. 停止协程：`runtime.Goexit()`，协程可以通过调用该方法来停止，尽管这样做几乎没有必要。

### 7.2 channel
为什么需要channel：一般情况下，协程是独立的，之间没有通信，而channel就是用于协程之间的通信，它可以传输类型化数据，在任何给定时间，一个数据被设计为只有一个协程可以对其访问，所以不会发生数据竞争。 数据的所有权（可以读写数据的能力）也因此被传递。所以channel有两个作用：
1. 值的交换
2. 默认是同步的，保证了两个计算（协程）任何时候都是可知状态

channel的特点：channel只能传输一种类型（支持所有类型，甚至chan类型）的数据，它实际上是类型化消息的队列，是先进先出（FIFO）的结构，是引用类型，使用`make()`函数创建。如果使用零值初始化创建则是nil，会一直阻塞，推荐用`make()`函数创建。

channel的声明:分有缓冲和无缓冲两种，buffer为0或者没有时是无缓冲通道（unbuffered channel），大于0时是有缓冲通道（buffered channel）。无缓冲通道用于顺序执行、同步，缓冲通道通常用来处理异步事件，只要往里面扔就行了，缓冲使程序更具有伸缩性（scalable）。可以使用内置`cap()`函数查看缓冲容量，`len()`查看当前元素个数。为了可读性，通道的命名通常以 ch 开头或者包含 chan：
1. 无缓冲通道，只能包含一个元素，容量为0，读和写同时准备好了，channel才会开始通信，只有读或者写，则会一直阻塞。声明形如`var ch chan datatype`或`ch = make(chan datatype)`，如`ch1 := make(chan int)`。如果元素正在管道中流动，此时读和写也是阻塞的。
2. 有缓冲通道，写数据时，写满后再往里写的时候才会阻塞，而读则是channel为空后继续读才会阻塞。声明形如`ch := make(chan datatype, buffer)`,其中buffer是缓冲容量，即元素个数（>0），与元素类型无关。

channel的方向。默认是双向的，可以用注解来表示只发送或者只接收：
1. 只接收：`var recv_only <-chan int`
2. 只发送：`var send_only chan<- int`

关于chan类型的chan：（待补充）

channel的发送和接收。使用通信操作符`<-`。通道的发送和接收操作都是自动的，一般两个协程需要通信的话，我们是把channel作为参数传给协程。当channel被装满之后如果无协程接收，则channel的发送操作变成阻塞的，此时无法再往里面发送，同理，如果channel是空的且没有协程往里面发送，则它的接收操作是阻塞的：
1. 往channel中发送数据，此时的协程可以称为生产者：形如`ch <- int`，比如`ch1 <- 100`
2. 从channel中接收数据，有两种方式，此时的协程可以称为消费者：
    1. 接收并赋值：如`int1 := <- ch1`
    2. 直接获取通道的（下一个）值：如`<- ch`,可以不用`_`去接收，该值会被丢弃

关闭channel。只有在当需要告诉接收者不会再提供新的值的时候，才需要关闭通道。关闭方法有以下几种：（待补充）
1. 直接使用`close(ch)`或者加上defer语句：`defer close(ch)`
2. 使用ok判断：`v, ok := <-ch   // ok is true if v received value`
3. 可以使用`for range`来遍历通道，它会自动判断通道是否关闭，如果没有关闭且通道为空，继续取的话还是会死锁。

信号量模式：（待补充）

关于main协程和其他协程共同操作channel的死锁错误，分接收和发送两种情况，稍微有点复杂，重在理解：
1. 如果main协程要从channel中接收值，执行到这一步时main协程会判断之前声明的协程里是否有等次数的往channel中发送值的方法（这里等次数的意思是，如果接收了n（n>0）次值，那么发送值的次数要>=n），如果有则程序继续执行，如果没有则会在第n次接收前抛出如下错误：

    ```
    fatal error: all goroutines are asleep - deadlock!
    chan receive (nil chan)...
    ```
2. 如果main协程要往channel中发送值，执行到这一步时，会判断之前声明的协程里是否有等次数的从channel中接收值的方法（这里等次数的意思是，如果发送了n（n>0）次值，那么接收值的次数要>=n），如果有，则程序继续运行，如果没有则会在第n次发送前抛出如下错误，

    ```golang
    fatal error: all goroutines are asleep - deadlock!
    .. [chan send]:
    ```

注意：
1. 如果移除操作channel的协程的go关键字，程序无法运行，运行时会抛出死锁错误，似乎和main中操作channel的死锁错误差不错。
2. 不要使用打印状态来表明通道的发送和接收顺序，因为fmt不是线程安全的，打印状态和通道实际发生读写的时间延迟会导致和真实发生的顺序不同。

    ```golang
    func main() {
        var ch chan int
        for i := 0; i < 20; i++ {
            go func(i int) {
                fmt.Println("num:", i)
            }(i)
        }
    }
    //输出结果
    num: 6
    num: 7
    num: 12
    num: 9
    num: 10
    num: 11
    Beginning shortWait()
    num: 1
    num: 16
    num: 13
    ```

#### 7.2.1 使用select切换协程
语法和switch非常相似，也称为通信开关。

为什么需要它：它监听进入通道的数据，也可以是用通道发送值(?)

注意：
1. 如果多个条件都满足，那么会随机执行其中一个。

## 8 基于共享变量的并发

# 四 高级
## 1 go的线程模型
三个核心元素支撑起了这个模型的主框架：
- M：machine的缩写。一个M代表一个内核线程，或者“工作线程”。
- P：processor的缩写。一个P代表执行一个Go代码片段所必需的资源（或称“上下文环境”）。
- G：goroutine的缩写。一个G代表一个Go代码片段。前者是对后者的一种封装。

## 2 go的CSP并发模型
CSP模型：是上个世纪七十年代提出的，用于描述两个独立的并发实体通过共享的通讯 channel(管道)进行通信的并发模型。 CSP中channel是第一类对象，它不关注发送消息的实体，而关注与发送消息时使用的channel

CSP

哲学：不要通过共享内存来通信， 应该通过通信来共享内存。

# 六 问题

# 七 未整理
1. 死锁，活锁，优先级反转
2. 基于内存共享和基于消息共享内存的对比
3. 网友：goroutine 并不是 “把异步回调的代码用同步的方式来写”。而是在用户空间实现了一个 M 对 N 的调度器。

    简单来讲，异步回调一般只开一个线程，有任务了之后会把让这个线程去执行这个任务，无法利用多核。

    而 goroutine 会根据机器的运行情况开 N 个操作系统级别的线程，然后把 M 个用户级别的 goroutine 调度到这 N 个线程上。

    golang 团队一直引以为傲的就是这个 M 对 N 的调度器，这种 M 对 N 调度器在业界也算是比较先进的。

    1. 网友2：其实就是用户态线程
    2. 网友3：goroutine 是个很神奇的东西，他的调度能在行级，不是简单的 yield 一下就做到的。这种特性可以保证某个线程不会被拿不到资源被饿死。我也不相信 java 用线程模型造出来的东西性能可以好到哪里。
    3. 网友4：golang 对内部所有可能的阻塞系统调用都做了封装, 当遇到可能发生阻塞的系统调用自动切换, 关于这方面可以浏览相关 goroutine 切换原理.

4. 内核和用户态
5. 多线程的应用场景：
    1.服务器中的文件管理或通信控制
    2.前后台处理
    3.异步处理

6. 守护线程、幽灵线程
7. 线程or进程状态在linux中的字母表示