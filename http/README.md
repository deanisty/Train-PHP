### TCP/IP






### Hypertext Transfer Protocol (HTTP) 超文本传输协议

>
> 参考： https://developer.mozilla.org/en-US/docs/Web/HTTP
>
Hypertext Transfer Protocol (HTTP) is an application-layer protocol for transmitting hypermedia documents, such as HTML. 
HTTP是一个应用层协议，它被用作传输超媒体文档，例如 HTML。
It was designed for communication between web browsers and web servers, but it can also be used for other purposes. 
设计 HTTP 的目的是是为了在浏览器和服务器之间通信，但是它也可以用于其他用途。
HTTP follows a classical client-server model, with a client opening a connection to make a request, 
HTTP 协议基于经典的 CS 通信模式，客户端打开一个连接请求，等待服务器的响应。
then waiting until it receives a response. 
HTTP is a stateless protocol, meaning that the server does not keep any data (state) between two requests. 
HTTP 是一个无状态协议，它不会在两次请求之间保存任何数据。
Though often based on a TCP/IP layer, it can be used on any reliable transport layer; 
HTTP 底层通常基于 TCP/IP 协议栈，它可以被用作任何可靠传输层之上，
that is, a protocol that doesn't lose messages silently, such as UDP.

