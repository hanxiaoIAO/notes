[toc]

## 参考文档

[百度百科]:(https://baike.baidu.com/item/WebSocket/1953845?fr=aladdin)
[菜鸟教程]:(https://www.runoob.com/html/html5-websocket.html)
[Java实现WebSocket的两种方式]:(https://www.cnblogs.com/onlymate/p/9521327.html)
[Sring MVC 模式下使用websocket]:(https://www.jianshu.com/p/3398d0230e5f)
[java WebSocket开发入门WebSocket]:(https://www.jianshu.com/p/d79bf8174196)

## 简介

WebSocket 是一种在单个 TCP 连接上进行全双工通信的协议。WebSocket 使得客户端和服务器之间的数据交换变得简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就可以创建持久的性的连接，并进行双向数据传输。

### 背景

早期很多网站为了实现推送功能，采用轮询技术，但这种模式需要不断向服务器发送请求，浪费带宽等资源。

之后的做法是 Comet（基于 HTTP 长连接的“服务器推”技术）。这种技术虽然可以双向通信，但依然需要反复发出请求。而且普遍采用长链接，也会消耗服务器资源。

在此现状下，HTML5 定义了 WebSocket 协议，能更好的节省服务器资源和带宽，并且能更实时的进行通讯。

## 使用

### 前端/客户端

浏览器通过 JavaScript 向服务器发出建立 WebSocket 连接的请求，连接建立以后，可以通过 send() 方法向服务器发送数据，并通过 onmessage 事件来接受服务器返回的数据。

创建WebSocket对象

```javascript
var Socket = new WebSocket(url, [protocol] );
```

url：指定连接的 URL

protocal：可选的，指定可连接的子协议



Socket 对象属性

| 属性                  | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| Socket.readyState     | 只读属性 **readyState** 表示连接状态，可以是以下值： 0 - 表示连接尚未建立。 1 - 表示连接已建立，可以进行通信。 2 - 表示连接正在进行关闭。 3 - 表示连接已经关闭或者连接不能打开。 |
| Socket.bufferedAmount | 只读属性 **bufferedAmount** 已被 send() 放入正在队列中等待传输，但是还没有发出的 UTF-8 文本字节数。 |

Socket 对象事件

| 事件    | 事件处理程序     | 描述                       |
| ------- | ---------------- | -------------------------- |
| open    | Socket.onopen    | 连接建立时触发             |
| message | Socket.onmessage | 客户端接收服务端数据时触发 |
| error   | Socket.onerror   | 通信发生错误时触发         |
| close   | Socket.onclose   | 连接关闭时触发             |

Socket 对象方法

| 方法           | 描述             |
| -------------- | ---------------- |
| Socket.send()  | 使用连接发送数据 |
| Socket.close() | 关闭连接         |



Websocket 使用 ws 或 wss 的统一资源标志符，类似于 HTTPS，其中 wss 表示在 TLS 之上的 Websocket。如：

```
ws://example.com/wsapi
wss://secure.example.com/
```

Websocket 使用和 HTTP 相同的 TCP 端口，可以绕过大多数防火墙的限制。默认情况下，Websocket 协议使用 80 端口；运行在 TLS 之上时，默认使用 443 端口。

### 后端/服务端

// TODO 

## WebSocket 与 Socket 区别

软件通信有七层结构，下三层结构偏向与数据通信，上三层更偏向于数据处理，中间的传输层则是连接上三层与下三层之间的桥梁，每一层都做不同的工作，上层协议依赖与下层协议。基于这个通信结构的概念。

Socket 其实并不是一个协议，是应用层与 TCP/IP 协议族通信的中间软件抽象层，它是一组接口。当两台主机通信时，让 Socket 去组织数据，以符合指定的协议。TCP 连接则更依靠于底层的 IP 协议，IP 协议的连接则依赖于链路层等更低层次。

WebSocket 则是一个典型的应用层协议。

总的来说：Socket 是**传输控制层协议**，WebSocket 是**应用层协议**。