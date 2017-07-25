# HappyChat
基于Netty实现的WebSocket聊天室，实现的功能如下：
<br>
1. 支持昵称登录；<br>
2. 支持多人同时在线；<br>
3. 同步显示在线人数；<br>
4. 支持文字和表情的内容；<br>
5. 浏览器与服务器保持长连接，定时心跳检测；
<br><br>
## 服务器
服务器端使用Netty作为通信框架，支持客户端通过WebSocket通信。服务器会检测链路是否处于空闲，如果60秒内没有收到客户端的任何消息，那么服务器会主动关闭该链路。<br><br>
为保证链路的可用性，服务器会定时发送Ping消息给客户端，客户端收到Ping消息后，必须回一个Pong消息响应，避免链路由于空闲而被关闭。<br><br>
客户端连接服务器之后，需要提供昵称给服务器，服务器保存每一个用户的昵称和相关的链路信息，用于后续的聊天显示。<br><br>
客户端发送聊天消息到服务器之后，服务器不会存储聊天消息，而是直接转发给其它的客户端。
<br><br>
## 客户端
由于是通过WebSocket协议来接入，所以浏览器作为客户端的话，必须支持WebSocket协议，现在项目中已经提供了Html页面的客户端，访问地址如下：<br>
<br>
在项目的doc文件夹下包含了客户端的HTML源码，有兴趣的童鞋可以参考一下。
<br>
<br>
## 协议
协议比较简单，所有的消息都一个Json字符串，格式如下：<br>
`head | body | extend`<br>

* head作为头部，用int类型存储，4个字节；
* body 消息的有效载体，用string类型存储，长度无限度；
* extend 协议的扩展字段，用map类型存储；
<br><br>
由于在解码消息时使用的是Netty自带的WebSocket的解码器，只支持文本帧的消息，解码出来的都是一个完整的帧消息，即上面格式的消息，所以协议上没有用长度字段。

<br><br>
## 交流1074455781
<br>
<br>
<br>

 
