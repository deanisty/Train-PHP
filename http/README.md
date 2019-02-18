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
