# websocket
## 介绍
WebSocket一种建立在单个TCP连接上进行全双工通讯的协议。
WebSocket让浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输
## 原理
简略版
1. 客户端浏览器向服务器发起一个附加头信息（比如Update:WebSocket，Connection:Update表明这是一个申请协议升级的http请求）http请求
2. 服务端解析附加头信息产生应答信息返回给客户端
3. 客户端收到应答信息建立WebSocket连接
4. 客户端或服务端关闭连接，双方关闭连接
详细版
1. 客户端握手请求

## 基本使用
### 创建
```var socket = new Websocket(url , [protocol]);```
参数url使用ws://协议（或者类似于https://用于安全链接的wss://协议）指向要连接的主机   
参数protocol是一个字符串数组，指定了可协商的子协议   
### 属性
#### 常量属性
socket.readyState：(只读)表示连接状态
> 0-WebSocket.CONNETING-连接未建立
> 1-WebSocket.OPEN-连接已建立，可进行通信
> 2-WebSocket.CLOSING-连接正在进行关闭
> 3-WebSocket.CLOSED-连接已关闭或连接不能打开
#### Other
属性名|值类型|描述
:--|:-:|:--
binaryType|String|表示连接传输的二进制数据类型的字符串。默认为"blob"
bufferedAmount|Number|(只读)表示被send()放入队列中等待传输但还未发出的UTF-8文本字节数
protocol|String/Array|连接建立前为空，连接建立后为客户端和服务端确定下来的协议名称
readyState|String|(只读)连接当前状态，这些状态是与常量相对应的。
extenstions|String|服务器选择的扩展
### 事件
事件|事件处理程序|描述
:--|:--|:--
open|socket.onopen|连接建立时触发
message|socket.onmessage|客户端接受服务端数据时触发
error|socket.onerror|通信发生错误时触发
close|socket.onclose|连接关闭或失败时触发
### 方法
方法|描述
:--|:--
socket.send(data)|使用连接发送数据data，可以试String/Blob/ArrayBuffer/ByteBuffer等
socket.close()|关闭连接
## ajax轮询和long poll
在WebSocket之前，一般可采用ajax和long poll来实现实时信息传递    
ajax轮询：让隔几秒发送一次请求询问服务器是否有新信息
long poll：发送请求询问服务器后等待有消息后才返回，客户端接受信息后才会再次建立连接
## socket
socket不是协议，它是程序层面上对传输层协议（例如TCP）的接口封装

参考链接：[https://www.cnblogs.com/fuqiang88/p/5956363.html](https://www.cnblogs.com/fuqiang88/p/5956363.html)