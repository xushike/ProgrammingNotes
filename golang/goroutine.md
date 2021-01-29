# goroutine

# 一 概述
golang的goroutine笔记，因为内容复杂，所以单独弄一个笔记，主要是goroutine，也包括相关的内容，水平有限，整理得比较乱。。。

## 3 常识
### 3.1 linux进程分类
- 内核线程（或者叫核心进程）：
    1. 内核线程没有独立的地址空间
    2. 只在内核空间运行，从来不切换到用户空间去。内核进程和 普通进程一样，可以被调度，也可以被抢占
- 用户进程
- 用户线程

#### 协程(coroutine)（待补充）
首先要明确：协程不是进程或线程，虽然看起来很像，本质上更像函数调用。coroutine是一种运行在用户态的用户线程。go底层选择使用coroutine是因为它具有以下特点：
1. 用户空间 避免了内核态和用户态的切换导致的成本
2. 可以由语言和框架层进行调度
3. 更小的栈空间允许创建大量的实例

#### 线程

### 3.2 多线程和异步的关系
异步是目的，而多线程是实现异步的一个可选方法，不用多线程也可以实现异步。

#### 异步
异步与同步相对，当一个异步过程调用发出后，调用者在没有得到结果之前，就可以继续执行后续操作。当这个调用完成后，一般通过状态、通知和回调来通知调用者。对于异步调用，调用的返回并不受调用者控制。

对于通知调用者的三种方式，具体如下：
1. 状态：即监听被调用者的状态（轮询），调用者需要每隔一定时间检查一次，效率会很低。
2. 通知：当被调用者执行完成后，发出通知告知调用者，无需消耗太多性能。
3. 回调：与通知类似，当被调用者执行完成后，会调用调用者提供的回调函数。

异步操作的本质：所有的程序最终都会由计算机硬件来执行，所以为了更好的理解异步操作的本质，我们有必要了解一下它的硬件基础。 熟悉电脑硬件的朋友肯定对DMA这个词不陌生，硬盘、光驱的技术规格中都有明确DMA的模式指标，其实网卡、声卡、显卡也是有DMA功能的。DMA就是直 接内存访问的意思，也就是说，拥有DMA功能的硬件在和内存进行数据交换的时候可以不消耗CPU资源。只要CPU在发起数据传输时发送一个指令，硬件就开 始自己和内存交换数据，在传输完成之后硬件会触发一个中断来通知操作完成。这些无须消耗CPU时间的I/O操作正是异步操作的硬件基础。所以即使在DOS 这样的单进程（而且无线程概念）系统中也同样可以发起异步的DMA操作。

### 3.3 数据竞争
golang的赋值并不是原子操作。例如，在 32 位机器上写 int64 类型的变量是有中间状态的，它会被拆成两次写操作 MOV —— 写低 32 位和写高 32 位，如果一个线程刚写完低 32 位，还没来得及写高 32 位时，另一个线程读取了这个变量，那它得到的就是一个毫无逻辑的中间变量，比如并发读取某个动态值全为0、或者乱码...

#### 解决方案 Mutex vs Atomic
大概有两种思路：上锁（Mutex）和无锁的原子操作（Atomic）。go race detector 的作者总结了这两者的一个区别：

> Mutexes do no scale. Atomic loads do.

mutex 由操作系统实现，而 atomic 包中的原子操作则由底层硬件直接提供支持。在 CPU 实现的指令集里，有一些指令被封装进了 atomic 包，这些指令在执行的过程中是不允许中断（interrupt）的，因此原子操作可以在 lock-free 的情况下保证并发安全，并且它的性能也能做到随 CPU 个数的增多而线性扩展。

若实现相同的功能，后者通常会更有效率，并且更能利用计算机多核的优势。所以，以后当我们想并发安全的更新一些变量的时候，我们应该优先选择用 atomic 来实现。

### 3.4 数据不一致

### 3.5 内核态和用户态、用户空间和内核空间
linux中的概念（待补充）

操作系统根据资源访问权限的不同，体系架构可分为用户空间和内核空间；内核空间主要操作访问CPU资源、I/O资源、内存资源等硬件资源，为上层应用程序提供最基本的基础资源，用户空间呢就是上层应用程序的固定活动空间，用户空间不可以直接访问资源，必须通过“系统调用”、“库函数”或“Shell脚本”来调用内核空间提供的资源。

用户态和内核态的切换：
1. 用户态切换到内核态的3种方式：
   1. 系统调用
   2. 异常
   3. 外围设备的中断

### 3.6 常见并发编程模型
多线程、线程调度、异步回调（待整理）

## 4 文章
1. 15分钟读懂进程线程、同步异步、阻塞非阻塞、并发并行：https://www.cnblogs.com/mhq-martin/p/9035640.html

# 三 基础
## 1 线程的生命周期
一般有新建状态，就绪、阻塞、运行三种基本状态和死亡状态。（参考自java）
1. 新建状态：新建了一个线程
2. 就绪状态是指线程具备运行的所有条件，逻辑上可以运行，在等待处理机
3. 运行状态是指线程占有处理机正在运行；
4. 阻塞状态是指线程在等待一个事件（如某个信号量），逻辑上不可执行。
5. 死亡状态：线程方法执行结束，或异常退出。死亡的线程不可再次复用（？）。

每一个程序都至少有一个线程，在进程入口执行的第一个线程被视为这个进程的主线程，很多语言中都是以`main()`方法作为入口，当调用此方法时系统就会自动创建一个主线程。

挂起、睡眠和阻塞：挂起和睡眠是主动的，挂起恢复需要主动完成，睡眠恢复则是自动完成的，因为睡眠有一个睡眠时间，睡眠时间到则恢复到就绪态。而阻塞是被动的，是在等待某种事件或者资源的表现，一旦获得所需资源或者事件信息就自动回到就绪态。

阻塞调用和非阻塞调用：阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程。

阻塞、唤醒、执行、销毁、挂起、睡眠、休眠（待整理）

## 2 并发和锁

性能对比：
1. 互斥锁和读写锁：在读写冲突不大的的情况下，两者效率应该是接近的，互斥锁效率可能更高；在读写冲突较大的情况下，读写锁性能会更好。

### 2.1 互斥锁
### 2.2 自旋锁

CAS算法（compare and swap）： CAS算法是一种有名的无锁算法。无锁编程，即不使用锁的情况下实现多线程之间的变量同步，也就是在没有线程被阻塞的情况下实现变量的同步，所以也叫非阻塞同步（Non-blocking Synchronization）。CAS算法涉及到三个操作数：

1. 需要读写的内存值V
2. 进行比较的值A
3. 拟写入的新值B

当且仅当 V 的值等于 A时，CAS通过原子方式用新值B来更新V的值，否则不会执行任何操作（比较和替换是一个原子操作）。一般情况下是一个自旋操作，即不断的重试。


自旋锁是指当一个线程在获取锁的时候，如果锁已经被其他线程获取，那么该线程将循环等待，然后不断地判断是否能够被成功获取，知直到获取到锁才会退出循环。对于互斥锁，如果资源已经被占用，资源申请者只能进入睡眠状态。但是自旋锁不会引起调用者睡眠，如果自旋锁已经被别的执行单元保持，调用者就一直循环在那里看是否该自旋锁的保持者已经释放了锁，“自旋”一词就是因此而得名。

自旋锁等待期间，线程的状态不会改变，线程一直是用户态并且是活动的(active)。

### 2.3 读写锁

## 3 sync.WaitGroup
作用：它能够一直等到所有的goroutine执行完成，并且阻塞主线程的执行，直到所有的goroutine执行完成

## 4 信号量
对信号量有4种操作
1. 初始化（initialize），也叫做建立（create）
2. 等信号（wait），也可叫做挂起（suspend）
3. 给信号（signal）或发信号（post）
4. 清理（destroy）

## 5 死锁
死锁的规范定义：集合中的每一个进程都在等待只能由本集合中的其他进程才能引发的事件，那么该组进程是死锁的。操作系统中的定义：所有的线程或进程都在等待资源的释放。如果只有一个线程也是可以发生死锁的。例子如:
1. 线程 A 持有资源 2，线程 B 持有资源 1，他们同时都想申请对方的资源，所以这两个线程就会互相等待而进入死锁状态。
2. 。。。

java里死锁的定义：死锁是指两个或两个以上的进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外界作用下，它们都将无法进行下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程称为死锁进程。

避免死锁的方法(待整理)：

## 7 Goroutines和Channels
### 未整理
1. 网友:goroutine 并不是 “把异步回调的代码用同步的方式来写”。而是在用户空间实现了一个 M 对 N 的调度器。 
简单来讲，异步回调一般只开一个线程，有任务了之后会把让这个线程去执行这个任务，无法利用多核。 
而 goroutine 会根据机器的运行情况开 N 个操作系统级别的线程，然后把 M 个用户级别的 goroutine 调度到这 N 个线程上。 
golang 团队一直引以为傲的就是这个 M 对 N 的调度器，这种 M 对 N 调度器在业界也算是比较先进的。
2. 网友:协程不是异步回调，协程是状态的保存和切换，这种思想很容易写出异步代码，实现同样的异步功能， c++或者 java 之类的写到你想吐

### 7.1 goroutine
参考：
1. https://studygolang.com/articles/13875

是一种比线程更加轻盈、更省资源的协程.使用 4K 的栈内存就可以在堆中创建它们。因为创建非常廉价，必要的时候可以轻松创建并运行大量的协程（在同一个地址空间中 100,000 个连续的协程）。协程的栈会根据需要进行伸缩，从而动态的增加（或缩减）内存的使用，不会出现栈溢出，所以coder不用关心栈的大小；栈的管理是自动的，但不是由垃圾回收器管理的，而是在协程退出后自动释放。Go 运行时可以聪明的意识到哪些协程被阻塞了，暂时搁置它们并处理其他协程。

存在两种并发方式：确定性的（明确定义排序）和非确定性的（加锁/互斥从而未定义排序）。Go 的协程和通道理所当然的支持确定性的并发方式（例如通道具有一个 sender 和一个 receiver）

协程的底层实现(待整理): goroutine底层用的非阻塞+epoll，所以我们可以用同步的方式写出异步的程序。

创建协程：协程是通过使用关键字`go`调用（执行）一个函数或者方法（也可以是匿名或者 lambda 函数）来实现的。协程可以在程序初始化的过程中运行（在 `init()` 函数中）。`main()`函数也可以看成一个协程。
```golang
// 例子1：其中f, x, y 和 z 的求值发生在当前的 Go协程中，而 f 的执行发生在新的 Go协程中。
go f(x, y, z)
```

在一个协程中，比如它需要进行非常密集的运算，你可以在运算循环中周期的使用 `runtime.Gosched()`：这会让出处理器，允许运行其他协程；它并不会使当前协程挂起，所以它会自动恢复执行。使用 `runtime.Gosched()` 可以使计算均匀分布，使通信不至于迟迟得不到响应。

协程是独立的处理单元，一旦陆续启动一些协程，你无法确定他们是什么时候真正开始执行的。你的代码逻辑必须独立于协程调用的顺序。

`main()`退出时，`main()`中创建的协程会随着程序的结束而消亡

使用场景：
1. 比如在一个非常长的数组中查找一个元素。

常用操作：
1. 停止协程：`runtime.Goexit()`，协程可以通过调用该方法来停止，但是defer函数还会继续调用。

### 7.2 channel（管道、信道）
参考：
1. https://colobu.com/2016/04/14/Golang-Channels/

为什么需要channel：一般情况下，协程是独立的，之间没有通信，而channel就是用于协程之间的通信，它可以传输类型化数据，在任何给定时间，一个数据被设计为只有一个协程可以对其访问，所以不会发生数据竞争。 数据的所有权（可以读写数据的能力）也因此被传递。所以channel有两个作用：
1. 值的交换
2. 在没有显式的锁或竞态变量的情况下进行同步，保证了两个计算（协程）任何时候都是可知状态

channel的特点：channel只能传输一种类型（支持所有类型，甚至chan类型）的数据，它实际上是类型化消息的队列，是先进先出（FIFO）的结构，是引用类型，使用`make()`函数创建。**如果使用零值初始化创建则是nil，会一直阻塞**，推荐用`make()`函数创建。

channel的声明:分有缓冲和无缓冲两种，buffer为0或者没有时是无缓冲通道（unbuffered channel），大于0时是有缓冲通道（buffered channel）。无缓冲通道用于顺序执行、同步，缓冲通道通常用来处理异步事件，只要往里面扔就行了，缓冲使程序更具有伸缩性（scalable）。可以使用内置`cap()`函数查看缓冲容量，`len()`查看当前元素个数。为了可读性，通道的命名通常以 ch 开头或者包含 chan：
1. 无缓冲通道，只能包含一个元素，容量为0，读和写同时准备好了，channel才会开始通信，**只有读或者写，则会一直阻塞**。声明形如`var ch chan datatype`或`ch = make(chan datatype)`，如`ch1 := make(chan int)`。如果元素正在管道中流动，此时读和写也是阻塞的。
2. 有缓冲通道，写数据时，写满后再往里写的时候才会阻塞，而读则是channel为空后继续读才会阻塞。声明形如`ch := make(chan datatype, buffer)`,其中buffer是缓冲容量，即元素个数（>0），与元素类型无关。

channel的方向。默认是双向的，可以用注解来表示只发送或者只接收：
1. 只接收（只读）：`var recv_only <-chan int`
2. 只发送（只写）：`var send_only chan<- int`

关于chan类型的chan：（待补充）

channel的发送和接收。使用通信操作符`<-`。通道的发送和接收操作都是自动的，一般两个协程需要通信的话，我们是把channel作为参数传给协程。当channel被装满之后如果无协程接收，则channel的发送操作变成阻塞的，此时无法再往里面发送，同理，如果channel是空的且没有协程往里面发送，则它的接收操作是阻塞的：
1. 往channel中发送数据，此时的协程可以称为生产者：形如`ch <- int`，比如`ch1 <- 100`
2. 从channel中接收数据，有两种方式，此时的协程可以称为消费者：
    1. 接收并赋值：如`int1 := <- ch1`
    2. 直接获取通道的（下一个）值：如`<- ch`,可以不用`_`去接收，该值会被丢弃

关闭channel：
1. 关闭channel的原则：
    1. go作者说的在golang中可以不用关闭channel，channel在不被任何goroutine使用的时候，最后都会被垃圾回收机制回收，无论channel是否已经关闭。所以一般情况下不需要去关闭它，只有在当需要告诉接收者不会再提供新的值的时候，才需要关闭通道。(比如?)
    2. 不要在消费端关闭channel，不要在有多个并行的生产者时对channel执行关闭操作。也就是说正常情况下，只应该在唯一或者最后的生产者协程中关闭channel。只要坚持这个原则，就可以确保向一个已经关闭的channel发送数据的情况不可能发生。
2. 关闭channel的方法:大概有以下几种
    1. `close()`
    2. 再用一个chan专门来通知结束
    3. 从chan传过来一个特定的值来判断结束循环
3. 关闭channel的实例
    1. 一个sender，多个receiver：这是最简单的场景，sender关闭channel即可
    1. 在多个生产者端关闭
        1. 可以暴力的使用`close()`关闭，额外的需要使用recover机制来上个保险，避免程序因为panic而崩溃。
    2. 在消费者端关闭:可以较为优雅的使用sync.Once来关闭channel，这样可以确保只会关闭一次
        ```go
        // 1. 这种方式较为礼貌，但是once在多sender的情况下，还是会造成其他sender向已经关闭了的channel中塞数据，所以使用一个锁是不错的选择
        type MyChannel struct {
            C    chan interface{}
            once sync.Once
        }
        func NewMyChannel() *MyChannel {
            return &MyChannel{C: make(chan interface{})}
        }
        func (mc *MyChannel) SafeClose() {
            mc.once.Do(func() {
                close(mc.C)
            })
        }
        
        // 2. 使用锁
        type MyChannel struct {
            C      chan interface{}
            closed bool
            mutex  sync.Mutex
        }

        func NewMyChannel() *MyChannel {
            return &MyChannel{C: make(chan interface{})}
        }
        func (mc *MyChannel) SafeClose() {
            mc.mutex.Lock()
            defer mc.mutex.Unlock()
            if !mc.closed {
                close(mc.C)
                mc.closed = true
            }
        }
        func (mc *MyChannel) IsClosed() bool {
            mc.mutex.Lock()
            defer mc.mutex.Unlock()
            return mc.closed
        }
        ```
    4. 一个receiver，多个sender：可以通过关闭额外的一个channel去通知那多个sender
        ```go
        func main() {
            rand.Seed(time.Now().UnixNano())
            log.SetFlags(0)
            // ...
            const MaxRandomNumber = 100000
            const NumSenders = 1000
            wgReceivers := sync.WaitGroup{}
            wgReceivers.Add(1)
            // ...
            dataCh := make(chan int, 100)
            stopCh := make(chan struct{})
            // stopCh is an additional signal channel.
            // Its sender is the receiver of channel dataCh.
            // Its reveivers are the senders of channel dataCh.
            // senders
            for i := 0; i < NumSenders; i++ {
                go func() {
                    for {
                        // The first select is to try to exit the goroutine
                        // as early as possible. In fact, it is not essential
                        // for this specified example, so it can be omitted.
                        select {
                        case <-stopCh:
                            return
                        default:
                        }
                        // Even if stopCh is closed, the first branch in the
                        // second select may be still not selected for some
                        // loops if the send to dataCh is also unblocked.
                        // But this is acceptable for this example, so the
                        // first select block above can be omitted.
                        select {
                        case <-stopCh:
                            return
                        case dataCh <- rand.Intn(MaxRandomNumber):
                        }
                    }
                }()
            }
            // the receiver
            go func() {
                defer wgReceivers.Done()
                for value := range dataCh {
                    if value == MaxRandomNumber-1 {
                        // The receiver of the dataCh channel is
                        // also the sender of the stopCh channel.
                        // It is safe to close the stop channel here.
                        close(stopCh)
                        return
                    }
                    log.Println(value)
                }
            }()
            // ...
            wgReceivers.Wait()
        }
        ```
    5. 多个receiver，多个sender
        
        ```go
        func main() {
            rand.Seed(time.Now().UnixNano())
            log.SetFlags(0)
            // ...
            const MaxRandomNumber = 100000
            const NumReceivers = 10
            const NumSenders = 1000
            wgReceivers := sync.WaitGroup{}
            wgReceivers.Add(NumReceivers)
            // ...
            dataCh := make(chan int, 100)
            stopCh := make(chan struct{})
            // stopCh is an additional signal channel.
            // Its sender is the moderator goroutine shown below.
            // Its reveivers are all senders and receivers of dataCh.
            toStop := make(chan string, 1)
            // The channel toStop is used to notify the moderator
            // to close the additional signal channel (stopCh).
            // Its senders are any senders and receivers of dataCh.
            // Its reveiver is the moderator goroutine shown below.
            var stoppedBy string
            // moderator
            go func() {
                stoppedBy = <-toStop
                close(stopCh)
            }()
            // senders
            for i := 0; i < NumSenders; i++ {
                go func(id string) {
                    for {
                        value := rand.Intn(MaxRandomNumber)
                        if value == 0 {
                            // Here, a trick is used to notify the moderator
                            // to close the additional signal channel.
                            select {
                            case toStop <- "sender#" + id:
                            default:
                            }
                            return
                        }
                        // The first select here is to try to exit the goroutine
                        // as early as possible. This select blocks with one
                        // receive operation case and one default branches will
                        // be specially optimized as a try-receive operation by
                        // the standard Go compiler.
                        select {
                        case <-stopCh:
                            return
                        default:
                        }
                        // Even if stopCh is closed, the first branch in the
                        // second select may be still not selected for some
                        // loops (and for ever in theory) if the send to
                        // dataCh is also non-blocking.
                        // This is why the first select block above is needed.
                        select {
                        case <-stopCh:
                            return
                        case dataCh <- value:
                        }
                    }
                }(strconv.Itoa(i))
            }
            // receivers
            for i := 0; i < NumReceivers; i++ {
                go func(id string) {
                    defer wgReceivers.Done()
                    for {
                        // Same as the sender goroutine, the first select here
                        // is to try to exit the goroutine as early as possible.
                        // This select blocks with one send operation case and
                        // one default branches will be specially optimized as
                        // a try-send operation by the standard Go compiler.
                        select {
                        case <-stopCh:
                            return
                        default:
                        }
                        // Even if stopCh is closed, the first branch in the
                        // second select may be still not selected for some
                        // loops (and for ever in theory) if the receive from
                        // dataCh is also non-blocking.
                        // This is why the first select block is needed.
                        select {
                        case <-stopCh:
                            return
                        case value := <-dataCh:
                            if value == MaxRandomNumber-1 {
                                // The same trick is used to notify
                                // the moderator to close the
                                // additional signal channel.
                                select {
                                case toStop <- "receiver#" + id:
                                default:
                                }
                                return
                            }
                            log.Println(value)
                        }
                    }
                }(strconv.Itoa(i))
            }
            // ...
            wgReceivers.Wait()
            log.Println("stopped by", stoppedBy)
        }
        ```
3. 如何判断channel是否已经关闭了(待整理):
    1. `close(ch)`:如果channel已经close了，那么再调用close时就会panic。所以还要做一些额外的工作，如果`close(ch)`没有panic，那么正常关闭；如果`close(ch)`发生panic，说明它已经被关闭了，那么此时截获panic，丢弃这个panic。注意已经close的channel是不会阻塞的，所以继续读取的话还能是获取到对应类型的零值。
        ```go
        defer func() {
            if recover() != nil {
                // close(ch) panic occur
            }
        }()

        close(ch) // panic if ch is closed
        ```
    2. 使用ok判断：`v, ok := <-ch`， **ok is true if v received value，ok is false if there are no more values to receive and the channel is closed.**也就是说，ok为false的时候(todo)
    3. 在确定不会向channel写入信息的前提下，可以写一个这样的函数
        ```go
        // 因为如果channel没有关闭，<-ch将不会返回，直到chanel已经被关闭。
        func IsClosed(ch <-chan interface{}) bool {
        select {
            case <-ch:
                return true
            default:
            }
            
            return false
        }
        ```
    4. 使用`for range`来遍历通道，虽然`for range`能判断通道是否关闭，但是它不会采取任何措施，如果没有关闭且通道为空，继续取的话还是会死锁。
        ```go
        // 1. channel未关闭，继续读取
        c := make(chan int, 10)
		c <- 1
		c <- 2
		c <- 3

		for i := 0; i < 5; i++ {
			num, ok := <-c
			log.Println(num, ok)
        }
        // 输出结果:
		// 1 true
		// 2 true
		// 3 true
        // fatal error: all goroutines are asleep - deadlock!
        
        // 2. channel已经关闭，继续读取
        c := make(chan int, 10)
		c <- 1
		c <- 2
		c <- 3
		close(c)

		for i := 0; i < 5; i++ {
			num, ok := <-c
			log.Println(num, ok)
        }
        // 输出结果:
		// 1 true
		// 2 true
		// 3 true
		// 0 false
		// 0 false
        ```

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
1. 不要使用打印状态来表明通道的发送和接收顺序，因为fmt不是线程安全的，打印状态和通道实际发生读写的时间延迟会导致和真实发生的顺序不同。

    ```golang
    func main() {
        var ch chan int
        for i := 0; i < 20; i++ {
            go func(i int) {
                fmt.Println("num:", i)
            }(i)
        }
    }
    // 这种方式每个数字只会输出一次，是准确的
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

    ```go
    for i := 0; i < 20; i++ {
            go func() {
            fmt.Println("num:", i)
        }()
    }

    // 这种方式有些数字可能输出很多次，不准确
    ```

### 7.3 使用select切换通信
源码在/src/runtime/select.go

为什么需要`select`：一个channel的时候很好操作，存在多个channel的时候，我们该如何判断并在其中操作呢，通过select可以监听channel上的数据流动(或者说select就是用来监听和channel有关的IO操作)。select也称为通信开关，默认是阻塞的，只有当监听的channel中有发送或接收可以进行时才会运行，当多个channel都准备好的时候，select是随机的选择一个执行的。golang引入的select为我们提供了一种在多个channel间实现“多路复用”的一种机制。select还可用于协程的完美退出(待整理)。

`select`的语法:它是go中的一个控制结构，类似于用于通信的switch语句。每个case必须是一个通信操作，要么是发送要么是接收。如果没有case可运行，它将阻塞，直到有case可运行时，如果多个case都可执行时，select随机选一个可运行的case执行。default就是当监听的channel都没有准备好的时候，默认执行的（此时select不再阻塞等待channel）。所以它有如下特点:
1. 每个 case 都必须是一个通信
2. 所有channel表达式都会被求值、所有被发送的表达式都会被求值。
    1. 细节见例子4
3. 所有被发送的表达式都会被求值
4. 如果有多个 case 都可以运行，Select 会随机公平地选出一个执行。其他不会执行。否则：
    1. 如果有 default 子句，则执行该语句。
    2. 如果没有 default 子句，select 将阻塞，直到某个通信可以运行，Go 不会重新对 channel 或值进行求值。

```golang
// 简单使用的例子1
func fibonacci(c, quit chan int) {
	x, y := 1, 1
	for {
		select {
		case c <- x:
			x, y = y, x+y
		case <-quit:
			fmt.Println("quit")
			return
		}
	}
}

func main() {
	c := make(chan int)
	quit := make(chan int)
	go func() {
		for i := 0; i < 10; i++ {
			fmt.Println(<-c)
		}
		quit <- 0
	}()
	fibonacci(c, quit)
}

// 例子2
// 如果没有case，就单单一个select{}，会panic
func main() {
    select {} // panic
}

// 例子3
// select常配合for循环来监听channel有没有传输发生，需要注意在这个场景下，break只是退出当前select而不会退出for，需要用break break、goto或者return的方式。
ch := make(chan interface{})
go func() {
    for {
        ch <- 1
    }
}()
for {
    select {
    case i := <-ch:
        fmt.Println(i)
        break
    }
    break
}

// 例子4 
// 所有channel表达式都会被求值、所有被发送的表达式都会被求值。有两个细节
// 4.1 select开始执行时，除了赋值等号左边的表达式(比如这里的`(getAStorageArr())[0]`)，其他所有的case expression都会被求值，按语法的先后顺序
// 4.2 如果选择要执行的case是一个recv channel，那么它的赋值等号左边的表达式会被求值：如例子中当goroutine 3s后向recvchan写入一个int值后，select选择了recv channel执行，此时对=左侧的表达式
var (
    takeARecvChannel = func() chan int {
        fmt.Println("invoke takeARecvChannel")
        c := make(chan int)
        go func() {
            time.Sleep(3 * time.Second)
            c <- 1
        }()
        return c
    }
    getAStorageArr = func() *[5]int {
        fmt.Println("invoke getAStorageArr")
        var a [5]int
        return &a
    }

    takeASendChannel = func() chan int {
        fmt.Println("invoke takeASendChannel")
        return make(chan int)
    }

    getANumToChannel = func() int {
        fmt.Println("invoke getANumToChannel")
        return 2
    }
)
select {
//recv channels
case (getAStorageArr())[0] = <-takeARecvChannel():
    fmt.Println("recv something from a recv channel")
    //send channels
case takeASendChannel() <- getANumToChannel():
    fmt.Println("send something to a send channel")
}

// 运行结果:
// invoke takeARecvChannel
// invoke takeASendChannel
// invoke getANumToChannel
// invoke getAStorageArr
// recv something from a recv channel

// 例子5 
// 基于select可以实现一些有用的操作,比如超时：
select {
    case <- time.After(5 * time.Second):
    println("timeout")
}
```

## 8 基于共享变量的并发

# 四 高级
## 1 go的线程模型MPG(也有说GMP的?)
参考：
1. https://juejin.im/post/5b7678f451882533110e8948

三个核心元素支撑起了这个模型的主框架：
- M：machine的缩写。一个M代表一个内核线程，或者“工作线程”。
- P：processor的缩写。一个P代表执行一个Go代码片段所必需的资源（或称“上下文环境”）。
- G：goroutine的缩写。一个G代表一个Go代码片段。前者是对后者的一种封装。


## 1.1 go的运行时调度器(Runtime Scheduler)
goroutine使用协程，协程是在用户空间，它不依靠内核来调度（个人觉得更大层面上还是依靠的），而是协作式调度(Cooperative Scheduled)的，但最后被处理器执行的还是内核中的线程，所以需要用户线程和内核线程的调度方法。

常用的用户线程和内核线程的调度方法有：
1. N:1 多个用户线程对应一个内核线程
2. 1:1 一个用户线程对应一个内核线程
3. M:N 用户线程和内核线程是多对多的对应关系。很明显go选择的是M:N的方式

### 触发和不触发调度器的情况
调度器会在GC、“go”声明、阻塞channel操作、阻塞系统调用和lock操作后运行。它也会在非内联函数调用后执行。即如下情况会触发goroutine调度：
1. 阻塞的chan 收发
2. go声明
2. gc
2. C函数调用（本质上和syscall一样）
3. 主动调用runtime.Gosched
4. 某个goroutine的调用时间超过100ms，并且这个goroutine调用了非内联的函数

但是其他情况就不会触发调度，最简单的比如下面这个例子，因为空的for循环，会导致其他协程永远无法得到运行:
```go
runtime.GOMAXPROCS(1)
go func() {
    done = true
}()

for !done {
    // forever run 
}
```

### 中断后的恢复

## 2 go的并发模型
go的并发模型是CSP（Communicating Sequential Process，通讯顺序进程）：它是C.A.R Hoare在1978年提出的，CSP有着精确的数学模型，并实际应用在了Hoare参与设计的T9000通用计算机上。用于描述两个独立的并发实体通过共享的通讯 channel(管道)进行通信的并发模型。 CSP中channel是第一类对象，它不关注发送消息的实体，而关注与发送消息时使用的channel。它的哲学：不要通过共享内存来通信，应该通过通信来共享内存。作为Go并发编程核心的CSP理论的核心概念只有一个：同步通信。

和传统并发模型的比较：（待补充）
1. 无共享内存无锁


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