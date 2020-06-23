# EMQ

# 一 概述
## 1 简介
EMQ (Erlang/Enterprise/Elastic MQTT Broker)(现名EMQX) 是基于 Erlang/OTP 平台开发的开源物联网 MQTT 消息服务器。Erlang/OTP 是出色的软实时(Soft-Realtime)、低延时(Low-Latency)、分布式(Distributed) 的语言平台。MQTT 是轻量的(Lightweight)、发布订阅模式(PubSub) 的物联网消息协议。

EMQ 项目设计目标是承载移动终端或物联网终端海量 MQTT 连接，并实现在海量物联网设备间快速低延时消息路由，有如下特点:
1. 高性能
    1. 稳定承载大规模的 MQTT 客户端连接，单服务器节点支持50万到100万连接。
    2. 分布式节点集群，快速低延时的消息路由，单集群支持1000万规模的路由。
3. 消息服务器内扩展，支持定制多种认证方式、高效存储消息到后端数据库。
4. 完整物联网协议支持，MQTT、MQTT-SN、CoAP、WebSocket 或私有协议支持。
5. 自带web管理面板

EMQX消息服务器特点：
1. 全异步架构：异步 TCP 连接处理、异步主题(Topic)订阅、异步消息发布。只有在资源负载限制部分采用同步设计，比如 TCP 连接创建和 Mnesia 数据库事务执行。
2. EMQ X 开源产品不支持服务器内部消息持久化：EMQ X 在设计上分离消息路由与消息存储职责后，数据复制容灾备份甚至应用集成，可以在数据层面灵活实现。EMQ X 企业版产品中，可以通过规则引擎或插件的方式，持久化消息到 Redis、MongoDB、Cassandra、MySQL、PostgreSQL 等数据库，以及 RabbitMQ、Kafka 等消息队列。
    1. 不支持的原因
        1. 消息路由是基于内存的，而消息存储是基于磁盘的。
3. 使用 Erlang OTP 开发，容错能力好 (电信领域久经考验的语言，曾经做出过 99.9999999% 可用性的交换机设备)
4. 官方有大量的扩展插件可供扩展。有很多认证插件，数据存储(backend)插件可供选择。可支持各种关系型数据库，NoSQL 数据库，以及常见消息队列如Kafka，RabbitMQ，Pulsar 等
5. 支持集群，支持节点水平扩展
5. 单节点支持 2000K 并发连接
6. 支持规则引擎和编解码

相关软件：
1. 客户端
    1. MQTTX(https://mqttx.app/cn/):MQTT X 的 UI 采用了聊天界面形式，简化了页面操作逻辑，用户可以快速创建连接，允许保存多个客户端，方便用户快速测试 MQTT/MQTTS 连接，及 MQTT 消息的订阅和发布。
    2. MQTT 在线测试工具（http://tools.emqx.io/）
2. 服务器
    1. EMQX

## 4 文档网址等
emqx官方文档：
1. https://docs.emqx.io/tutorial/v3/zh/
2. https://docs.emqx.io/broker/latest/en/
3. https://docs.emqx.io/broker/latest/cn/

EMQ简书账号：https://www.jianshu.com/u/9cbcdf094d33

其他文档：
1. https://www.bookstack.cn/read/emqx-v3.0/backend.md（待确认）

# 二 安装配置
## win
客户端
1. MQTT X

服务端：
1. windows zip
    1. 启动
    2. 登录地址是:http://127.0.0.1:18083

# 三 基础
## 1 插件和内置模块
### 插件
1. WebHook:WebHook 是由 emqx_web_hook 插件提供的 将 EMQ X 中的**钩子**事件通知到某个 Web 服务 的功能。
1. Delayed Publish：emqx_delayed_publish 提供了延迟发送消息的功能。当客户端使用特殊主题前缀 `$delayed/seconds/` 发布消息到 EMQ X 时，EMQ X 将在seconds秒后发布该主题消息。
    1. 参考：https://docs.emqx.io/broker/latest/cn/advanced/delay-publish.html
3. 多语言支持插件：emqx_extension_hook
4. 插件模版：emqx_plugin_template

### 内置模块
参考:https://docs.emqx.io/broker/latest/cn/advanced/internal-modules.md

1. emqx_mod_delayed 
2. 代理订阅emqx_mod_subscription：EMQ X 的代理订阅功能使得客户端在连接建立时，不需要发送额外的 SUBSCRIBE 报文，便能自动建立用户预设的订阅关系。此功能默认关闭，支持在 EMQ X Broker 运行期间动态启停。

## 2 钩子
参考：https://docs.emqx.io/broker/latest/cn/advanced/hooks.html

采用职责链设计模式(Chain-of-responsibility_pattern)

注意：
1. 尽量不要在钩子内部使用阻塞函数，这会影响系统的吞吐。

### 回调链
回调链 需要允许其上面的函数**提前终止链**和**忽略本次操作**。

### 挂载点
message.publish	MQTT 消息发布
message.deliver	MQTT 消息投递前
message.acked	MQTT 消息回执

### session
消息保存在哪儿