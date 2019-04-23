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
```
//websocket请求头实例
GET /chat HTTP/1.1   //必需。
Host: server.example.com  // 必需。WebSocket服务器主机名
Upgrade: websocket // 必需。并且值为" websocket"。有个空格
Connection: Upgrade // 必需。并且值为" Upgrade"。有个空格
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ== // 必需。其值采用base64编码的随机16字节长的字符序列。
Origin: http://example.com //浏览器必填。头域（RFC6454）用于保护WebSocket服务器不被未授权的运行在浏览器的脚本跨源使用WebSocket API。
Sec-WebSocket-Protocol: chat, superchat //选填。可用选项有子协议选择器。
Sec-WebSocket-Version: 13 //必需。版本。
```
需要注意的是这是一个get请求
2. 服务端握手响应
为防止攻击者通过精心构造的包来欺骗服务器，服务器把两块信息合并开形成响应。第一块是客户端请求头的Sec-WebSocket-Key，
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==，服务器通过取该头域的值以字符串的形式拼接全局唯一的标识（258EAFA5-E914-47DA-95CA-C5AB0DC85B11），
此值不大可能被不明白WebSocket协议的网络终端使用，然后使用SHA-1 hash编码，在进行base64编码，将结果作为服务器的Sec-WebSocket-Accept头域返回。具体如下
```
请求头：Sec-WebSocket-Key:dGhlIHNhbXBsZSBub25jZQ==
取值，字符串拼接后得到："dGhlIHNhbXBsZSBub25jZQ==258EAFA5-E914-47DA-95CA-C5AB0DC85B11";
SHA-1后得到： 0xb3 0x7a 0x4f 0x2c 0xc0 0x62 0x4f 0x16 0x90 0xf6 0x46 0x06 0xcf 0x38 0x59 0x45 0xb20xbe 0xc4 0xea
Base64后得到： s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
最后的结果值作为响应头Sec-WebSocket-Accept的值
```
最红形成WebSocket服务器端的握手响应
```
HTTP/1.1 101 Switching Protocols   //必需。响应头。状态码为101。任何非101的响应都为握手未完成。但是HTTP语义是存在的。
Upgrade: websocket  // 必需。升级类型。
Connection: Upgrade //必需。本次连接类型为升级。
Sec-WebSocket-Accept:s3pPLMBiTxaQ9kYGzzhZRbK+xOo=  //必需。表明服务器是否愿意接受连接。如果接受，值就必须是通过上面算法得到的值。
```
3. 握手关闭
关闭握手可使用TCP直接关闭连接的方法来关闭握手。但是TCP关闭握手不总是端到端可靠的，比如出现拦截代理和其他中间设施。
也可以任何一段发送呆有执行控制序号（比如状态码1002，协议错误）的数据的帧来开始关闭握手，当另一方接受到这个关闭帧，就必须关闭连接。
## 基础
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