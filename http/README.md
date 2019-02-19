### TCP/IP

TCP/IP四层协议模型：数据链路层、网络层、传输层、应用层

![TCP/IP](images/tcp-ip-networking-model.jpg)



### HTTP特性

* Hypertext Transfer Protocol (HTTP) 超文本传输协议
* HTTP是一个应用层协议
* 它被用作传输超媒体文档，例如 HTML。
* HTTP 协议基于经典的 CS 通信模式，客户端打开一个连接请求，等待服务器的响应。
* HTTP 是一个无状态协议，它不会在两次请求之间保存任何数据。


### HTTP概述

>
> 参考： https://developer.mozilla.org/en-US/docs/Web/HTTP
>

HTTP用来获取像HTML文档这样的资源，它是在互联网上交换数据的基础并且是一个客户端-服务器协议，由信息的接受者发起请求，通常来说是浏览器。一个完整的文档
由获取到的不同子文档重新组合而成，例如：文本、样式描述、图片、视频、脚本等等。

![fetch-page](images/Fetching_a_page.png)

客户端和服务器之间通过交换独立的信息进行通信（和数据流stream相对应）。客户端（通常情况下是浏览器）发送的消息被称为请求，服务器发送的消息称为响应。

HTTP在20世纪90年代被开发出来，它是一个具备良好扩展功能的协议，而且在不断的发展。它是一个应用层协议，可以基于TCP连接也可以基于TLS加密的TCP连接，
并且理论上任何可靠的传输层协议都可以被它使用。因为它的可扩展性能，它不光被用来获取超文本，而且可以用来获取图片、视频，或者post内容到服务器，
比如通过HTML的表单。HTTP也可以用来获取部分文档来按需更新局部页面。

![http-layers](images/HTTP%20%26%20layers.png)


### 基于HTTP的系统

HTTP是客户端-服务器协议：请求由一个叫 user-agent 的实体发出，或者一个代理。通常user-agent是浏览器，但是也可以是类似机器爬虫的任何东西。

任何独立的请求都会被发送到服务器，服务器会处理请求并且准备响应。在请求和响应之间还有很多实体，可能是执行特定功能的代理，比如是一个网关或者缓存，
等等。

![client-server](images/Client-server-chain.png)

真实情况下，有更多的计算机参与浏览器和服务器之间处理请求：比如路由器、调制解调器等等。正因为有分层的互联网设计，这些计算机都被隐藏在网络层传输层。
HTTP在它们之上的应用层工作。尽管在检测网络故障方面很重要，但是这些隐藏在下面的层对于解释HTTP协议来说非常的无关紧要。

#### 客户端：user-agent

user-agent 可以是能够代表用户行为的任何工具。主要是浏览器，可能也是工程师或者网站开发者为了调试应用程序而编写的程序。
浏览器发送一个获取HTML文档的请求来获取网页，然后浏览器会解析这个HTML页面，发送其他的请求获取页面上的脚本、样式信息和页面上包含的图片和视频等信息。
浏览器会将获取的这些资源组装成完整的页面。浏览器执行脚本的过程中可能会获取更多的资源，并有可能会在后续阶段更新页面。

#### Web服务器

和user-agent 相对应的另一端是 web 服务器，服务器维护着客户端请求的文档。一个服务器仅仅代表一个虚拟的机器：因为事实上它可能是服务器群、共享负载（
负载均衡）、或者是一个复杂的软件询问其他机器（就像缓存、DB、电子商务服务器...）并按需产生部分或者全部页面。

一个服务器并非只能是单独的机器，多个服务器也可以部署在同一个机器上。使用 HTTP/1.1 和主机Header参数，多个服务器甚至可以共享 IP 地址。

#### 代理

Between the Web browser and the server, numerous computers and machines relay the HTTP messages. Due to the layered structure of the Web stack, most of these operate at either the transport, network or physical levels, becoming transparent at the HTTP layer and potentially making a significant impact on performance. Those operating at the application layers are generally called proxies. These can be transparent, or not (changing requests going through them), and may perform numerous functions:
在web浏览器和服务器之间，还有许多计算机或者机器用来传递HTTP信号。因为web协议栈的分层结构，在传输层、网络层和物理层的操作对于HTTP层来说都是透明的，
但是这些操作其实对性能的影响起到关键作用。这些操作对于应用层来说通常被称作代理。它们可能是透明的（或者通过修改通过它们的请求从而变成非透明的），并
且具备很多功能：

* 缓存 - 缓存可以是公开的或者隐私的，比如浏览器缓存
* 过滤 - 比如病毒扫描、家长控制
* 负载均衡 - 允许多个服务器服务不同的请求
* 认证 - 对不同资源的访问控制
* 登录 - 允许存储历史信息

### HTTP基础特征

#### HTTP 很简单

尽管HTTP/2通过将HTTP信息封装到二进制帧中使问题变得复杂，但是通常情况下HTTP协议被设计成简单而且是人类可读的。因此HTTP信息都很容易理解，对于开发者来说
很容易测试，并且对新手来说降低了复杂程度。

#### HTTP 可扩展

HTTP/1.0开始，HTTP的 头部信息使得这个协议很容被扩展和实验。新的功能很容被添加进来，只要客户端和服务器能够对新的头部语法达成一致。

#### HTTP 是支持会话的无状态

HTTP协议本身是无状态的，也就是说即时在同一个连接上接连发起的两个请求之间也没有任何联系，如果用户试图和某个特定的网页进行连续的交互，这显然会导致问题，比如电商网站的购物车。但是尽管HTTP本身是无状态的协议，但是它允许使用cookies来使用有状态的会话。利用头部信息的可扩展性，
HTTP cookie 被添加到工作流中，并且允许在每一个HTTP请求上创建会话用来共享上下文或者状态信息。

#### HTTP 和连接

连接由传输层控制，因此基本上超出了HTTP的作用域。但HTTP并不要求传输层的协议是基于连接的，只要这个协议是可靠的，
或者不会丢失信息的至少会呈现错误的即可。TCP和UDP是两个最常见的传输层协议，TCP是可靠的，而UDP不是。
虽然连接并非是HTTP必须的，但是HTTP最终选择了TCP标准，而TCP是基于连接的协议。

在客户端和服务可以交换HTTP请求和响应之前，他们必须建立TCP连接，这个连接的建立需要一些往返的信息交换。对于HTTP/1.0来说，默认的行为是为每一个
成对的HTTP请求和响应建立一个TCP连接。但是当有多个请求在短时间内同时发送时，这种方法没有共享一个TCP连接高效。

In order to mitigate this flaw, HTTP/1.1 introduced pipelining (which proved difficult to implement) and persistent connections: the underlying TCP connection can be partially controlled using the Connection header. HTTP/2 went a step further by multiplexing messages over a single connection, helping keep the connection warm, and more efficient.

Experiments are in progress to design a better transport protocol more suited to HTTP. For example, Google is experimenting with QUIC which builds on UDP to provide a more reliable and efficient transport protocol.

