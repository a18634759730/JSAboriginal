# MQTT协议

> MQTT 全称为 Message Queuing Telemetry Transport（消息队列遥测传输）是一种基于发布/订阅范式的“轻量级”消息协议，由 IBM 发布

+  MQTT 可以被解释为一种低开销，低带宽占用的即时通讯协议，可以用极少的代码和带宽的为连
接远程设备提供实时可靠的消息服务，它适用于硬件性能低下的远程设备以及网络状况糟糕的
环境下，因此 MQTT 协议在 IoT（Internet of things，物联网），小型设备应用，移动应
用等方面有较广泛的应用

+  IoT 设备要运作，就必须连接到互联网，设备才能相互协作，以及与后端服务协同工作。
而互联网的基础网络协议是 TCP/IP，MQTT 协议是基于 TCP/IP 协议栈而构建的，因此它
已经慢慢的已经成为了 IoT 通讯的标准

### 基本特点

> 1.MQTT是一种发布/订阅传输协议，基本原理和实现如下；

[my-logo.png]: https://upload-images.jianshu.io/upload_images/12653154-18bfa8f9ffd615e3.png?imageMogr2/auto-orient/ "my-logo"
![my-logo.png]

[my-logo.svg]: https://static.runoob.com/images/mix/mqtt-fidge-2.svg "my-logo"
![my-logo.svg]

MQTT 协议提供一对多的消息发布，可以解除应用程序耦合，信息冗余小。该协议需要客户端和服务
端，而协议中主要有三种身份

+  发布者（Publisher）
+  代理（Broker，服务器）
+  订阅者（Subscriber）

其中，消息的发布者和订阅者都是客户端，消息代理是服务器，而消息发布者可以同时是订阅者，
实现了生产者与消费者的脱耦。


> 2.使用 TCP/IP 提供网络连接，提供有序、无损、双向连接；

MQTT 是一种连接协议，它指定了如何组织数据字节并通过 TCP/IP 网络传输它们。设备联网，也
需要连接到互联网中，在大万维的世界中，TCP 如同汽车，有轮子就能用来运输数据，MQTT 就像是
交通规则。在网络模型中，TCP是传输层协议，而 MQTT是在应用层，在 TCP 的上层，因此MQTT 也是基于这个而构建的，提高了可靠性。

> 3.对负载内容屏蔽的消息传输

可以对消息订阅者所接受到的内容有所屏蔽。

> 4.具体有三种消息发布的服务质量：

>> + 至多一次，消息发布完全依赖底层 TCP/IP 网络。会发生消息丢失或重复。这一级别可用于如下情况，环境传感器数据，丢失一次读记录无所谓，因为不久后还会有第二次发送

>> + 至少一次，确保消息到达，但消息重复可能会发生。

>>  + 只有一次，确保消息到达一次。这一级别可用于如下情况，在计费系统中，消息重复或丢失会导致不正确的结果

> 5.小型传输，开销小，固定长度的头部是 2 字节，协议交换最小化，以降低网络流量；

整体上协议可拆分为：**固定头部**+**可变头部**+**消息体**，这就是为什么在介绍里说它非常适合"在物联网领域，传感器与服务器的通信，信息的收集"。

> 6.使用Last Will和Testament特性通知有关各方客户端异常中断的机制；

**Last Will** 即遗言机制，用于通知同一主题下的其他设备发送遗言的设备已经断开了连接。

**Testament** 遗嘱机制，功能类似于Last Will。

### 基本概念

**一、MQTT 客户端**

> 一个使用 MQTT 协议的设备、应用程序等，它总是建立到服务器的网络连接

+ 可以发布信息，其他客户端可以订阅该信息

+ 订阅其它客户端发布的消息

+ 退订或删除应用程序的消息

+ 断开与服务器连接

**二、MQTT 服务器**

> MQTT 服务器以称为 Broker（消息代理），以是一个应用程序或一台设备。它是位于消息发布者 和订阅者之间

+ 接受来自客户端的网络连接

+ 接受客户端发布的应用信息

+ 处理来自客户端的订阅和退订请求

+ 向订阅的客户转发应用程序消息

**三、主题（Topic）**

> 连接到一个应用程序消息的标签，该标签与服务器的订阅相匹配。服务器会将消息发送给订阅所匹配标签的每个客户端。

+ 要订阅的主题。一个主题可以有多个级别，级别之间用斜杠字符分隔。例如，**/world** 和 **emq/emqtt/emqx** 是有效的主题。

+ 订阅者的Topic name支持通配符#和+ ：

    + 支持一个主题内任意级别话题
    + 只匹配一个主题级别的通配符

+ 客户端成功订阅某个主题后，代理会返回一条 SUBACK 消息，其中包含一个或多个 returnCode 参数

**四、主题筛选器（Topic Filter）**

> 一个对主题名通配符筛选器，在订阅表达式中使用，表示订阅所匹配到的多个主题。

**五、QoS（消息传递的服务质量水平）**

> 服务质量，标志表明此主题范围内的消息传送到客户端所需的一致程度。

+ 值 0：不可靠，消息基本上仅传送一次，如果当时客户端不可用，则会丢失该消息。
+ 值 1：消息应传送至少 1 次。
+ 值 2：消息仅传送一次。

**六、会话（Session）**

> 每个客户端与服务器建立连接后就是一个会话，客户端和服务器之间有状态交互。会话存在于一个网络之间，也可能在客户端和服务器之间跨越多个连续的网络连接。

**七、订阅（Subscription）**

> 订阅包含主题筛选器（Topic Filter）和最大服务质量（QoS）。订阅会与一个会话（Session）关联。一个会话可以包含多个订阅。每一个会话中的每个订阅都有一个不同的主题筛选器。

+ 客户端在成功建立TCP连接之后，发送CONNECT消息，在得到服务器端授权允许建立彼此连接的CONNACK消息之后，客户端会发送SUBSCRIBE消息，订阅感兴趣的Topic主题列表（至少一个主题）
+ 订阅的主题名称采用UTF-8编码，然后紧跟着对应的QoS值

**八、发布（publish）**

> 控制报文是指从客户端向服务端或者服务端向客户端传输一个应用消息，MQTT 客户端发送消息请求，发送完成后返回应用程序线程

+ 比如安卓的推送服务，还有一些即时通信软件如微信等也是采用的推送技术。

**九、负载（Payload）**

> 消息订阅者所具体接收的内容

### 简单示例

MQTT 协议主要是根据以下情况设计的：

+ M2M（Machine to Machine），机器或设备间端到端通信，比如传感器之间的数据通讯。

+ 设备（Machine）中，例如传感器，硬件能力很弱，协议要考虑尽量小的资源消耗，比如计算能力和存储等。

根据 MQTT 的基础了解后并结合简单的架构，在这里做一个简单的示例图，可以更直观的理解MQTT协议的通信模型。MQTT Broker 就选择 EMQ 作为示范。比如有1个温度传感器（1个Machine），1个移动设备，1个电脑，一个服务器（3个Machine)，都可以得到或者显示温度传感器的温度值，需要先通过 MQTT 协议subscribe（订阅）一个比如叫 temperature 的 topic（主题）如下：

[my-logo.webp]:https://upload-images.jianshu.io/upload_images/12653154-893cd91af32d18b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/731/format/webp "my-logo"
![my-logo.webp]

图中移动设备，服务器，电脑需要先通过 EMQ subscribe 一个叫 temperature 的 topic，当温度传感器 publish 温度数据，三个设备就可以收到了。

### 进一步了解MQTT 3

MQTT 3 （当前版本3.1.1）是目前使用的最为广泛的MQTT协议标准。尽管MQTT5标准已经发布，并且带来了一些令人振奋的新特性，但是在整个应用场景上，从后台服务到消息中间件再到客户端SDK等环节上的产品升级并没有都完成，再加上既有部署的维护，业界从版本3到5的过渡可能会持续相当长一段时间，所以，对于刚加入物联网行业的生力军来说，现在来学习MQTT 3依然是一件很有意义的事情。

### MQTT协议的工作方式

前面简介中讲到，在一个QMTT协议中有三个角色会参与到整个通信过程，发布者（publisher）、代理（broker）和订阅者（subscriber）。有别于传统的客户端/服务器通讯协议，MQTT协议并不是端到端的，消息传递通过代理，包括会话（session）也不是建立在发布者和订阅者之间，而是建立在端和代理之间。代理解除了发布者和订阅者之间的耦合。
除了发布者和订阅者之间传递普通消息，代理还可以为发布者处理保留消息和遗愿消息，并可以更改服务质量（QoS）等级。

### MQTT控制报文

MQTT协议工作在TCP之上，端和代理之间通过交换预先定义的控制报文来完成通信。MQTT报文有3个部分组成，并按下表顺序出现：

|固定报头（fixed header）|可变报头（variable header）|荷载（payload）|
|:-|:-:|:-|
|所有报文都包含|部分报文包含|部分报文包含|

所有的MQTT控制报文都有一个固定报头，期格式如下：

[my-logos.webp]:https://upload-images.jianshu.io/upload_images/12653154-b0fe79c60cf65e10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/742/format/webp
![my-logos.webp]

协议版本3定义了14种MQTT报文，用于建立/断开连接、发布消息、订阅消息和维护连接。固定报头的第一字节的4-7位的值指定了报文类型，其取值如下表。0和15为系统保留值；0-3位为标志位，依照报文类型有不同的含义，事实上，除了PUBLISH报文以外，其他报文的标志位均为系统保留。如果收到报文的标志位无效，代理应断开连接。

|报文类型|值|描述|
|:-|:-|:-|
|CONNECT|1|客户端向代理发起连接请求|
|CONNACK|2|连接确认|
|PUBLISH|3|发布消息|
|PUBACK|4|发布确认|
|PUBREC|5|发布收到（QoS2）|
|PUBREL|6|发布释放（QoS2）|
|PUBCOMP|7|发布完成（QoS2）|
|SUBSCRIBE|8|客户端向代理发起订阅请求|
|SUBACK|9|订阅确认|
|UNSUBSCRIBE|10|取消订阅|
|UNSUBACK|11|取消订阅确认|
|PINGREQ|12|PING请求|
|PINGRESP|13|PING响应|
|DISCONNECT|14|断开连接

固定报头的第二字节起表示报文的剩余长度。最大4个字节，每字节可以编码至127，并含有一位继续位，如继续位非0，则下一字节依然为剩余长度。由此，理论上一个控制报文最长可以到256MB。
一些报文在固定报头和荷载之间可以有一个可变报头。可变报头的内容根据报文类型不同而不同。最常见的可变报头是报文标识符（PacketIdentifier）。
一些报文可以在最后携带一个荷载。不同的报文可以无荷载，可选荷载，或必须带有荷载。
限于篇幅，在这里我们仅以CONNECT和CONNACK为例解释一下MQTT报文的构成和报文响应行为。其他报文请查阅MQTT标准文档

### CONNECT报文

限于篇幅，在这里我们仅以CONNECT为例解释一下MQTT报文的构成。其他报文请查阅MQTT标准文档。
CONNECT是客户端连接到代理的第一个报文，如果在连接已经存在，代理收到该报文将会断开现有连接。

### CONNECT报文的固定报头

[my-mytable.webp]:https://upload-images.jianshu.io/upload_images/12653154-7b1ed63c7089add1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/720/format/webp "mytable"
![my-mytable.webp]

### CONNECT报文的可变报头

CONNECT报文的可变报头由4部分组成：

+ 协议名。协议名是UTF-8编码的大写的MQTT。
+ 协议级别。MQTT 3.1.1的协议级别为4.
+ 连接标志位。定义连接行为的参数。见下表。
+ Keep Alive。2字节，客户端和代理之间的无活动时间超过该值后，应关闭连接。如果该值置0表示客户端不要求代理启用KEEPALIVE功能。

连接标志位：
|位|7|6|5|4|3|2|1|0|
|:-|:-|:-|:-|:-|:-|:-|:-|:-|:-|
||用户名|密码|保留遗愿|遗愿QoS|遗愿QoS|遗愿|清除会话|保留（0）|

**清除会话标志位：**
这个标志位定义了如何处理会话状态。如果设置为0，客户端和代理可以恢复上一次连接时的会话状态，如果上一次连接的会话状态不存在，代理将会为客户端建立一个新的会话。如果该位设置为1，则双方将清除掉上一次连接的会话状态并建立一个新的会话。

**遗愿标志位：**
如果遗愿标志为1，则遗愿消息会被存储在代理上，当连接关闭时，代理将发布这个消息，除非在客户端断开连接时把遗愿消息清除了。

**遗愿QoS标志位：**
指定了遗愿消息的服务质量等级。

**保留遗愿消息标志位：**
指定在发布遗愿消息的时候，是否把该消息作为保留消息存储在代理。

**用户名标志位：**
如果设置为1，则用户名必须出现在荷载中，反之，用户名不允许出现在荷载中。

**密码标志位：**
如果该位为1，则密码必须出现在荷载中；如果该位为0，则密码不允许出现在荷载中。如果用户名标志位为0，则该位必须也为0。

### CONNECT报文的荷载
CONNECT报文的荷载由一个或者多个字段组成，这些字段是否出现由可变报头中的标志位决定。字段总是以长度开始。字段出现的顺序必须是：客户端标识符，遗愿主题，遗愿消息，用户名，密码。

### CONNECT报文的响应
在代理在为MQTT协议开放的端口上接收到TCP连接请求并建立连接后应该会收到CONNECT报文，如果在一定时间内代理没有收到CONNECT报文，则应该关闭这个TCP连接。
在收到CONNECT报文后，代理应该检查报文格式是否符合协议标准。如果不符合协议标准，代理应关闭连接，且不发送CONNACK报文给客户端。
代理可以检查CONNECT报文的内容并执行响应的认证和鉴权。如果这些检查没有通过，代理应该向客户端发送一个带有非0返回码的CONNACK报文。

### CONNACK报文
CONNACK是代理用来响应客户端CONNECT的报文。代理向客户端发送的第一个报文必须是CONNACT。CONNACK有一个固定报头，一个可变报头，但是不带有荷载。

### CONNACK的固定报头

[my-mytable2.webp]:https://upload-images.jianshu.io/upload_images/12653154-a73ed3e7170ff055.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp "mytable2"
![my-mytable2.webp]

CONNACT报文只有固定报头和一个2字节的可变报头，所以它的剩余长度总是2。

### CONNACK报文的可变报头

CONNACK报文的可变报头为定长2字节。第一字节的0位表示是否有会话存在。如果代理上已经有请求连接的客户端的会话，且连接请求的清除会话标识为0，则该位为1，否则该位为0。客户端可以根据这一位的值采取响应行为，比如（重新）订阅主题等。

CONNACK报文的可变报头的第二字节为返回码。如果CONNECT请求的格式正确，但是代理依然不能允许客户端连接，则返回码为一个非零值。如果连接成功，则返回0。

返回码的定义：

|值|返回码含义|
|:-|:-|:-|
|0|成功，连接请求被接受。|
|1|拒绝连接，不可接受的协议版本。|
|2|拒绝连接，不被允许的身份识别符（Client Identifier）。|
|3|拒绝连接，服务器不可用。|
|4|拒绝连接，无效的用户名和密码。|
|5|拒绝连接，客户端无授权。|
|6-255|系统保留。|

客户端接受到代理的CONNACK的返回码为0，则连接建立完成，双方可以开始通信。

### 清除会话、保留消息和QoS的组合

清除会话、保留消息等概念，在传统的客户端/服务器方式的通信中不一定会出现，这些概念有时候不太容易理解，特别是当他们被组合起来用的时候。

下面的表格汇总了当一个客户端连接上来时，它能收到消息的各种情况。

|清除会话位|保留位|订阅QoS|发布QoS|可收到的消息|
|:-|:-|:-|:-|:-|
|Y|N|0|0|N|
|Y|N|0|1|N|
|Y|N|1|0|N|
|Y|N|1|1|N|
|N|N|0|0|N|
|N|N|0|1|N|
|N|N|1|0|N|
|N|N|1|1|Y，会话全部消息|
|Y|Y|0|0|Y，最后一条消息|
|Y|Y|0|1|Y，最后一条消息|
|Y|Y|1|0|Y，最后一条消息|
|Y|Y|1|1|Y，最后一条消息|
|N|Y|0|0|Y，最后一条消息|
|N|Y|0|1|Y，最后一条消息|
|N|Y|1|0|Y，最后一条消息|
|N|Y|1|1|Y，会话全部消息|

### MQTT 5.0 协议新增介绍

MQTT 5.0 协议相比 MQTT 3.1.1 协议新增了许多内容， 比如说属性，AUTH 包，还有对一些字段做了修改，比如将 Clean Session 修改成 Clean Start 配合 Session Expiry Internal 去实现更灵活的会话控制。

这里就简单罗列一下 5.0 协议新增的内容。

### 设计目标

+ 增强了扩展性
+ 改善了错误报告的方式
+ 定型了一些通用范式，例如能力发现和请求、响应
+ 扩展机制包括用户属性(user properties)
+ 性能改善，并且添加了对小客户端（small clients） 的支持
+ 读者可以参考MQTT5.0协议规范的附录C来了解协议变更。

### 属性

为了达成新协议的设计目标，MQTT 5.0 协议中新增了许多属性，以下是新添加的属性列表。

|标识符 Identifier(十进制)|标识符 Identifier(十六进制)|名称（用法）Name(usage)|类型 Type|报文/遗嘱属性 Packet/Will Properties|
|:-|:-|:-|:-|:-|
|1|0x01|有效载荷格式指示器 Payload Format Indicator|字节|PUBLISH, 遗嘱属性 Will Properties
|2|0x02|消息到期间隔 Message Exipiry Interval|四字节整形|PUBLISH，遗嘱属性
|3|0x03|内容类型 Content Type|UTF-8 编码字符串|PUBLISH，遗嘱属性
|8|0x08|响应主题 Response Topic|UTF-8 编码字符串|PUBLISH，遗嘱属性
|9|0x09|关联数据 Correlation Data|二进制数据 Binary Data|PUBLISH，遗嘱属性
|11|0x0B|订阅标识符 Subscription Identifier|可变字节整形|PUBLISH, SUBSCRIBE
|17|0x11|会话到期间隔 Session Expiry Interval|四字节整形|CONNECT,  CONNACK, DISCONNECT
|18|0x12|已分配客户端标识符 Assigned Client Identifier|UTF-8 编码字符串|CONNACK
|19|0x13|服务器保活 Server Keep Alive|两字节整形|CONNACK
|21|0x15|认证方法 Authentication Method|UTF-8 编码字符串|CONNECT, CONNACK, AUTH
|22|0x16|认证数据 Authentication Data|二进制数据|CONNECT, CONNACK, AUTH
|23|0x17|请求响应信息 Request Response Information|字节|CONNECT
|24|0x18|遗嘱延迟间隔 Will Delay Interval|四字节整形|遗嘱属性 Will Properties
|25|0x19|请求响应信息 Request Response Information|字节|CONNECT
|26|0x1A|响应信息 Response Information|UTF-8 编码字符串|CONNACK, DISCONNECT
|28|0x1C|服务器引用 Server Reference|UTF-8 编码字符串|CONNACK, DISCONNECT
|31|0x1F|原因字符串 Reason String|UTF-8 编码字符串|CONNACK, PUBACK, PUBREC, PUBREL, PUBCOMP, SUBACK,UNSUBACK, DISCONNECT, AUTH
|33|0x21|接收最大值 Receive Maximum|两字节整形|CONNECT, CONNACK
|34|0x22|主题别名最大值 Topic Alias Maximum|两字节整形|CONNECT, CONNACK
|35|0x23|主题别名 Topic Alias|两字节整形|PUBLISH
|36|0x24|服务质量最大值 Maximum QoS|字节|CONNACK
|37|0x25|保留可用 Retain Available|字节|CONNACK
|38|0x26|用户属性 User Property|UTF-8 字符串对 UTF-8 String Pair|CONECT, CONNACK, PUBLISH, PUBACK, PUBREC, PUBREL, PUBCOMP, SUBACK, UNSUBACK,|DISCONNECT, AUTH
|39|0x27|最大报文大小 Maximum Packet Size|四字节整形|CONNECT, CONNACK
|40|0x28|可用通配符订阅 Wildcard Subscription Available|字节|CONNACK
|41|0x29|可用订阅标识符 Subscription Identifier Available|Byte|CONNACK
|42|0x2A|可用共享订阅 Shared Subscription Available|字节|CONNACK|

### 原因码

MQTT v3.1.1 只有寥寥 6 个返回码，用来表示网络连接时可能会出现的异常行为，在引入属性后的 MQTT 5.0 协议中，仅仅这 6 个返回码显然已经不足以用来描述各种异常行为，因此MQTT 5.0 协议中将返回码改成了原因码，用来实现改善错误报告的目的。 

|原因码（十进制）|原因码（十六进制）|名称|报文|
|:-|:-|:-|:-|
|0|0x00|成功 Success|CONNACK, PUBACK, PUBREC, PUBREL, PUBCOMP, UNSUBACK, AUTH
|0|0x00|正常断连 Normal disconnection|DISCONNECT
|0|0x00|准许 QoS 0  Granted QoS 0|SUBACK
|1|0x01|准许 QoS 1 Granted QoS 1|SUBACK
|2|0x02|准许 QoS 2  Granted QoS 2|SUBACK
|4|0x04|以遗嘱消息断开连接 Disconnect with Will Message|DISCONNECT
|16|0x10|没有匹配的订阅者 No matching subscribers|PUBACK, PUBREC
|17|0x11|没有订阅 No subscription existed|UNSUBACK
|24|0x18|继续认证 Continue authentication|AUTH
|25|0x19|重新认证 Re-authenticate|AUTH
|128|0x80|未指定错误 Unspecified error|CONNACK, PUBACK, PUBREC, SUBACK, UNSUBACK, DISCONNECT
|129|0x81|畸形报文 Malformed Packet|CONNACK, DISCONNECT
|130|0x82|协议错误 Protocol Error|CONNACK, DISCONNECT
|131|0x83|实现特有错误 Implementation specific error|CONNACK, PUBACK, PUBREC, SUBACK, UNSUBACK, DISCONNECT
|132|0x84|不支持的协议版本 Unsupported Protocol Version|CONNACK
|133|0x85|客户端标识符无效 Client Identifier not valid|CONNACK
|134|0x86|错误的用户名和密码 Bad User Name or Password|CONNACK
|135|0x87|未授权 Not authorized|CONNACK, PUBACK, PUBREC, SUBACK, UNSUBACK, DISCONNECT
|136|0x88|服务器不可用 Server unavailable|CONNACK
|137|0x89|服务器繁忙 Server busy|CONNACK, DISCONNECT
|138|0x8A|禁止访问 Banned|CONNACK
|139|0x8B|服务器关机中 Server shutting down|DISCONNECT
|140|0x8C|错误验证方法 Bad authentication method|CONNACK, DISCONNECT
|141|0x8D|保活超时 Keep Alive timeout|DISCONNECT
|142|0x8E|会话被接管 Session taken over|DISCONNECT
|143|0x8F|主题过滤器无效 Topic Filter invalid|SUBACK, UNSUBACK, DISCONNECT
|144|0x90|主题名无效 Topic Name invalid|CONNACK, PUBACK, PUBREC, DISCONNECT
|145|0x91|报文标识符在使用中 Packet Identifier in use|PUBACK, PUBREC, SUBACK, UNSUBACK=
|146|0x92|没有发现报文标识符 Packet Identifier not found|PUBREL, PUBCOMP
|147|0x93|超出接收最大值 Receive Maximum exceeded|DISCONNECT
|148|0x94|主题别名无效 Topic Alias invalid|DISCONNECT
|149|0x95|报文太大 Packet too large|CONNACK, DISCONNECT
|150|0x96|消息传输速率太高 Message rate too high|DISCONNECT
|151|0x97|超出限额 Quota exceeded|CONNACK, PUBACK, PUBREC, SUBACK, DISCONNECT
|152|0x98|管理行为 Administrative action|DISCONNECT
|153|0x99|有效载荷格式无效 Payload format invalid|PUBACK, PUBREC, DISCONNECT
|154|0x9A|不支持消息保留 Retain not supported|CONNACK, DISCONNECT
|155|0x9B|不支持的QoS QoS not supported|CONNACK, DISCONNECT
|156|0x9C|使用另一台服务器 Use another server|CONNACK, DISCONNECT
|157|0x9D|服务器被移除 Server moved|CONNACK, DISCONNECT
|158|0x9E|不支持的共享订阅 Shared Subscription not supported|SUBACK, DISCONNECT
|159|0x9F|超出连接速率 Connection rate exceeded|CONNACK, DISCONNECT
|160|0xA0|最大连接时间 Maximum connect time|DISCONNECT
|161|0xA1|不支持的订阅标识符 Subscription Identifiers not supported|SUBACK, DISCONNECT
|162|0xA2|不支持的通配符订阅 Wildcard Subscription not supported|SUBACK, DISCONNECT

### 实际应用

1.　由于主题别名（Topic Alias）的引入，使 MQTT PUBLISH 控制报文的体积更小，更便于在带宽和网络受限的物联网环境下传输消息。

2.　AUTH 包的引入使 MQTT 协议扩展了认证方式，增加了询问/响应式的认证方式，服务器或客户端在发送 CONNECT 与接收 CONNACK 包之间交换 AUTH 报文来完成身份验证的流程。

3.　由于很多嵌入式设备的 CPU 并没有对 AES 加密标准下的加密算法提供硬件级的支持，因此，使用 AES 加密对嵌入式设备的硬件开销是非常大的，所以 MQTT 5.0 协议提供了新的加密算法 ChaCha20 ，ChaCha20 在软件层面做加密和解密处理要比 AES 快得多。因此也算是一大进步，不过本人更希望 MQTT 下一版协议能够增加对 AEAD 加密算的支持。

总的来说，MQTT 5.0 协议的内容增加了很多，协议书的内容几乎是 MQTT 3.1.1 协议的两倍，除了本文上述提到的这些新的变化，还有很多非常细节的东西没有在这里做详细的介绍。基于 MQTT 5.0 协议现有的很多属性，在实现 MQTT 5.0 协议的时说不定还能挖掘出更多的有意思的新用法，不过这需要开发人员去多读协议的具体细节，去更深入地理解 MQTT 5.0 协议。

EMQ作为在github中最流行的MQTT中间件，开始全面支持MQTT 5.0协议，读者有兴趣的话，赶紧下载试用吧。
