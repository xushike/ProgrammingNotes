# MQTT

# 一 概述
## 1 简介
MQTT（Message Queuing Telemetry Transport，消息队列遥测传输）是IBM开发的一个即时通讯协议，使用发布/订阅的方式提供互相之间的通讯。MQTT是为在计算能力有限，且工作在低带宽、不可靠的网络的远程传感器和控制设备通讯而设计的协议。它的设计思想是轻巧、开放、简单、易于实现。这些特点使得它对很多场景来说都是很好的选择，特别是对于受限的环境如机器与机器的通信（M2M）以及物联网环境（IoT）。它具有以下主要的几项特性：
1. 该协议支持所有平台，几乎可以把所有联网物品和外部连接起来
2. 有三种消息发布服务质量
    - “至多一次”，消息发布完全依赖底层 TCP/IP 网络。会发生消息丢失或重复。这一级别可用于如下情况，环境传感器数据，丢失一次读记录无所谓，因为不久后还会有第二次发送。
    - “至少一次”，确保消息到达，但消息重复可能会发生。
    - “只有一次”，确保消息到达一次。这一级别可用于如下情况，在计费系统中，消息重复或丢失会导致不正确的结果。
3. 小型传输，开销很小（固定长度的头部是 2 字节），协议交换最小化，以降低网络流量；
4. 使用 TCP/IP 提供网络连接,基于 TCP/IP 协议，提供两者之间的一个有序的、无损的、基于字节流的双向传输
5. 事实的 IoT 通讯的标准协议
4. 有许多为物联网优化的特性，比如适应不同网络的QoS、层级主题、遗言等等
    1. 遗言：使用 Last Will 和 Testament 特性通知有关各方客户端异常中断的机制
    2. MQTT 协议提供了 3 种（QoS）服务质量用于消息传输，适应不同的物联网数据传输场景
        1. QoS 0：最多一次传送 (只负责传送，发送过后就不管数据的传送情况)，<=1。 是一种 "fire and forget" 的消息发送模式：Sender (可能是 Publisher 或者 Broker) 发送一条消息之后，就不再关心它有没有发送到对方，也不设置任何重发机制。
        2. QoS 1：至少一次传送 (确认数据交付),>=1
            1. 对于发送方来说，当它发送一个pub报文时，它会一直等待着来自对方(接收方)的消息确认报文pubAck。只有收到pubAck报文之后，它才认为该pub报文已经发送成功，否则，就会执行重试。 如果接收方已经收到了pub报文，而且它也把pubAck报文发送出去了，但是由于网络状况太差或者其他原因，导致了这个pubAck报文丢失了，发送方接收不到来自接收方的pubAck确认报文。于是，发送方就会对此pub报文进行二次重发，这样的话，接收方就又收到了一条和原来一模一样的pub报文。可见，导致重复消息的原因就是： pubAck报文在网络传输中丢失造成的。
        3. QoS 2：正好一次传送 (保证数据交付成功),=1
            1. Qos2是最高的服务质量等级，消息丢失和重复都是不可接收的。但是使用这个服务质量等级会有额外的开销。Qos2的pub报文的接收者使用一个两步确认过程来确认收到。实现较为复杂:https://docs.emqx.io/broker/v3/en/protocol.html#qos2-message-publish-and-subscribe
        4. QoS 降级：因为 QoS 分为**发送到 Broker的 QoS** 和 **从 Broker 接收的 QoS** 两部分，所以最终收到的 QoS 等级跟这两部分都有关系：如果发送者发送了一个 QoS2 的消息，但是接收者订阅时使用的是QoS1，那么接收到的消息等级就是 QoS1。这个叫做 QoS 降级。
        4. 选择：QoS 级别越高，流程越复杂，系统资源消耗越大。应用程序可以根据自己的网络场景和业务需求，选择合适的 QoS 级别，比如在同一个子网内部的服务间的消息交互往往选用 QoS 0；而通过互联网的实时消息通信往往选用 QoS 1；QoS 2 使用的场景相对少一些，适合一些支付请求之类的要求较高的场景。
    3. 保留消息：MQTT客户端向服务器发布(PUBLISH)消息时，可以设置保留消息(Retained Message)标志。保留消息(Retained Message)会驻留在消息服务器，后来的订阅者订阅主题时仍可以接收该消息。
    4. ACL鉴权：实际场景,我们需要监听每一台设备的链接和断开事件等EMQ的系统行为,这样的事件当然不是任何一个连接到服务器的终端,这样的限制就是ACL鉴权

除了MQTT的协议特性外还有一些客观原因:
1. 对语言友好主流语言的客户端都有
2. 大部分硬件方案天生支持
3. 数十个MQTT服务器端程序可供选择
4. 社区成熟解决方案被广泛运用遇到问题方便寻求帮助

MQTT 协议标准，服务器提供三种连接方式，
1. TCP：默认端口为 1883
2. TLS：默认端口为 8883
3. WebSocket：默认端口为 8083

MQTT传输的消息分为：主题（Topic）和负载（payload）两部分：
1. Topic，可以理解为消息的类型，订阅者订阅（Subscribe）后，就会收到该主题的消息内容（payload）；
2. payload，可以理解为消息的内容，是指订阅者具体要使用的内容。

发布订阅模式是传统 Client/Server 模式的一种解耦方案。发布者通过 Broker 与消费者之间通信，Broker 的作用是将受到的消息通过某种过滤规则，正确地发送给消费者。发布/订阅模式 相对于 客户端/服务器模式 的好处在于：
1. 发布者和消费者之间不必预先知道对方的存在，比如不需要预先沟通对方的 IP Address 和 Port
2. 发布者和消费者之间不必同时运行。因为 Broker 是一直运行的。

## 2 历史
MQTT was created by Andy Stanford-Clark of IBM, and Arlen Nipper (then of Arcom Systems, later CTO of Eurotech)

据 Arlen Nipper 在一 IBM Podcast 上的自述，MQTT 原名是 MQ TT， 注意 MQ 与 TT之间的空格，其全称为: MQ Telemetry Transport，是九十年代早期，他在参与 Conoco Phillips 公司的一个原油管道数据采集监控系统(pipeline SCADA system)时，开发的一个实时数据传输协议。它的目的在于让传感器通过带宽有限的 VSAT ，与 IBM 的 MQ Integrator 通信。由于 Nipper 是遥感和数据采集监控专业出身，所以按业内惯例给了个 MQ TT 的名字。

## 3 常识
### 1 Broker和Server
对于MQTT来说两者是一个意思：MQTT服务器是发布者和订阅者之间通信的代理（因此中文也有将 MQTT 服务器翻译为 MQTT 代理）

到目前为止，比较流行的开源 MQTT Broker 有几个：
1. Eclipse Mosquitto: https://github.com/eclipse/mosquitto，使用 C 语言实现的 MQTT Broker。Eclipse 组织还还包含了大量的 MQTT 客户端项目：https://www.eclipse.org/paho/#
2. EMQX: https://github.com/emqx/emqx：使用 Erlang 语言开发的 MQTT Broker，支持许多其他 IoT 协议比如 CoAP、LwM2M 等
3. Mosca: https://github.com/mcollina/mosca：使用 Node.JS 开发的 MQTT Broker，简单易用。
4. VerneMQ: https://github.com/vernemq/vernemq：同样使用 Erlang 开发的 MQTT Broker
5. HiveMQ：https://www.hivemq.com/

从支持 MQTT5.0、稳定性、扩展性、集群能力等方面考虑，EMQX 的表现应该是最好的

### 2 协议
`mqtt://`，如果是 SSL/TLS 认证连接的话，需要修改为 `mqtts://`

## 4 文档网址等
1. MQTT官方 : https://github.com/mqtt/mqtt.github.io
2. 服务中间件列表: https://github.com/mqtt/mqtt.github.io/wiki/servers
3. 客户端列表: https://github.com/mqtt/mqtt.github.io/wiki/libraries
4. oasis:https://docs.oasis-open.org/mqtt

# 三 基础
## 0 架构
## 1 工具生态
### mqttx
https://github.com/emqx/MQTTX/blob/main/README-CN.md

## 协议
MQTT协议中有三种身份：发布者（Publish）、代理（Broker）（服务器）、订阅者（Subscribe）。其中，消息的发布者和订阅者都是客户端，消息代理是服务器，消息发布者可以同时是订阅者。

当应用数据通过MQTT网络发送时，MQTT会把与之相关的服务质量（QoS）和主题名（Topic）相关连。

## 会话（Session）
每个客户端与服务器建立连接后就是一个会话，客户端和服务器之间有状态交互。会话存在于一个网络之间，也可能在客户端和服务器之间跨越多个连续的网络连接

## 主题
主题是一个UTF-8字符串。MQTT的主题是不要预先创建的，发布者发送消息到某个主题、或者订阅者订阅某个主题的时候，Broker 就自动创建了这个主题。

### 主题过滤器(TopicFilter)
主题过滤器:含有通配符的主题，目的是让客户端同时订阅多个主题。

使用：
1. 所有的主题名和主题过滤器必须至少包含一个字符
2. 主题名或主题过滤器以前置或后置斜杠`/`区分
3. 只包含斜杠`/`的主题名或主题过滤器是合法的
4. 主题名和主题过滤器是 UTF-8 编码字符串， 它们不能超过 65535 字节
5. 主题名和主题过滤器是区分大小写的

### 主题层级
MQTT 的 Topic 有层级结构，主题层级分隔符使得主题名结构化。如果存在分隔符，它将主题名分割为多个主题层级。

层级分隔符(即`/`,`U+002F`)：
1. 位置：可以出现在主题名称的任何位置
    1. 比如`/topic`、`topic/`、`to/pic`
1. 不带层级分隔符(待整理)：表示模糊匹配？
    1. 所以`/topic`和`topic`是两个不同的主题。
    2. 和`topic/`比呢

通配符：
1. 种类：mqtt支持的通配符有`+`、`#`和`$`，`+`和`#`可以一起使用
    1. `+`是单层通配符。
        1. 位置：在主题过滤器的任意层级都可以使用单层通配符，包括第一个和最后一个层级。然而它必须占据过滤器的整个层级 。可以在主题过滤器中的多个层级中使用它
        2. 例子
            1. `news/+`可以匹配`news/sports`，`news/society`，但是不能匹配`news/`和`news/sports/basketball`
            2. `news/+/basketball`可匹配`news/sports/basketball`，`news/shopping/basketball`
            3. `china/+/+/zhongshanlu`能匹配`china/guangzhou/tianhe/zhongshanlu`和`china/shenzhen/nanshan/zhongshanlu`
    2. `#`是多层(1~n)通配符，匹配它的父级和任意数量的子层级。
        1. 位置：多层通配符必须位于它自己的层级或者跟在主题层级分隔符后面，且必须是主题过滤器的最后一个字符 
        2. 例子
            1. `#`匹配所有
            2. `news/#`可以匹配 `news`、`news/sports`、`news/sports/basketball` 以及 `news/sports/basketball/x` 等等。
            3. `school/teacher#`、`school/teacher/#/lever`是无效的
    3. `$`有两种用法，由它的位置决定
        1. 位置:
            1. 如果放在主题开头，表示这些主题被保留为MQTT代理服务器的内部特性。一般情况下客户端是不能向这些主题发布消息的(只能订阅)。目前，broker所发布的主题格式还没有明确的的官方标准。一般的做法是用`$SYS/`开头表示系统主题。
                1. 特殊情况比如开了延迟发布模块就可以发送`$delayed/...`
            2. 只要不是放在主题的最开头，就表示匹配任意一个字符
        2. 例子
            1. 
2. 通配符只能在订阅主题时使用，并且在发布消息时不允许使用。

推荐设计：
1. 不在最前面加`/`,比如`/news/sports/basketball`, 等于在最前面有一个空字符串层级,浪费了一层，可以使用`news/sports/basketball`
2. 尽量不用特殊字符，就用英文加数字就行
3. 使用特定主题，而不是一般主题
    1. 比如`myhome/livingroom/temperature`, `myhome/livingroom/brightness`,`myhome/livingroom/humidity`多个主题，而不是用`myhome/livingroom`单个主题来获取全部信息

## 发布订阅
定阅与发布必须要有主题，只有当定阅了某个主题后，才能收到相应主题的payload,才能进行通信。

### 消息发布服务质量
1. “至多一次”，消息发布完全依赖底层TCP/IP网络。会发生消息丢失或重复。这一级别可用于如下情况，环境传感器数据，丢失一次读记录无所谓，因为不久后还会有第二次发送。这一种方式主要普通APP的推送，倘若你的智能设备在消息推送时未联网，推送过去没收到，再次联网也就收不到了。
2. “至少一次”，确保消息到达，但消息重复可能会发生。
3. “只有一次”，确保消息到达一次。在一些要求比较严格的计费系统中，可以使用此级别。在计费系统中，消息重复或丢失会导致不正确的结果。这种最高质量的消息发布服务还可以用于即时通讯类的APP的推送，确保用户收到且只会收到一次。

## 遗言(Last Will)和遗嘱(Testament)
Last Will：即遗言机制，用于通知同一主题下的其他设备发送遗言的设备已经断开了连接。

Testament：遗嘱机制，功能类似于Last Will。

### Will Flag

定义了客户端（没有主动发送DISCONNECT消息）出现网络异常导致连接中断的情况下，服务器需要做的一些措施。

简而言之，就是客户端预先定义好，在自己异常断开的情况下，所留下的最后遗愿（Last Will），也称之为遗嘱（Testament）。 这个遗嘱就是一个由客户端预先定义好的主题和对应消息，附加在CONNECT的可变头部中，在客户端连接出现异常的情况下，由服务器主动发布此消息。

只有在Will Flag位为1时，Will Qos和Will Retain才会被读取，此时消息体payload中要出现Will Topic和Will Message具体内容，否则，Will QoS和Will Retain值会被忽略掉。