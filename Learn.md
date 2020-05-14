# Learn

## RTSP

### 推模式

`C/S`通讯信令流程为:OPTIONS(optional,直接发`ANNOUNCE`也行),ANNOUNCE(客户端发送`sdp`,这时候服务端回复的时候可以携带`Session`,客户端拿到后每次请求都要携带),SETUP(客户端建立`sdp`中的那些流),RECORD(通知服务端要开始推流了).

[参考](./Capture.md#推流模式下)

### 拉模式

`C/S`通讯信令流程为:OPTIONS(optional,直接发`DESCRIBE`也行),DESCRIBE(请求服务器的`sdp`信息),SETUP(客户端根据`sdp`提供的流信息建立连接,其中服务器回复头部携带`Session`,客户端拿到后每次请求都要携带),PLAY(通知服务端开始发送数据).