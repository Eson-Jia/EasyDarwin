# Learn

## RTSP

Real Time Stream Protocol


### 推模式

`C/S`通讯信令流程为:OPTIONS(optional,直接发`ANNOUNCE`也行),ANNOUNCE(客户端发送`sdp`,这时候服务端回复的时候可以携带`Session`,客户端拿到后每次请求都要携带),SETUP(客户端建立`sdp`中的那些流),RECORD(通知服务端要开始推流了).

[参考](./Capture.md#推流模式下)

### 拉模式

`C/S`通讯信令流程为:OPTIONS(optional,直接发`DESCRIBE`也行),DESCRIBE(请求服务器的`sdp`信息),SETUP(客户端根据`sdp`提供的流信息建立连接,其中服务器回复头部携带`Session`,客户端拿到后每次请求都要携带),PLAY(通知服务端开始发送数据).

### RTP/RTCP

在安防行业，`RTSP`携带的`sdp`信息中至少会有两个流(audio,video)，如果在`SETUP`阶段选择`UDP`承载这两个流的话，则需要两对端口:[(音频 RTP,音频 RTCP),(视频 RTP,视频 RTCP)]。

有些网络环境因为防火墙设计问题等，会强迫服务器交织传输信令和媒体流数据，除非必要情况下才会这样做，因为这会使`client/server`的实现变得复杂。而且，交织传输二进制数据应该只在`RTSP over TCP`的情况下使用。
那么如何区分这些交织在一起包是音频包还是视频包，或者是`RTP`包还是`RTCP`呢。
解决方法是在`RTP`层之上引入`rtsp interleave frame`层,他的结构如下:

| Magic     | Channel                                  | Length          | Payload              |
| --------- | ---------------------------------------- | --------------- | -------------------- |
| 魔数 0x24 | 通道标记,标记`payload`是音频/视频的RTP/RTCP | payload 的长度 | 负载,也就是 音频/视频的RTP/RTCP |
Channel标记的类型一般如下：

- 0x00 video RTP
- 0x01 video RTCP
- 0x02 audio RTP
- 0x03 audio RTCP


如果采用`interleave`的方式，
一般情况下用`UDP`承载`RTP/RTCP`

## vcodec

### I P B 帧

I 帧:Intra-coded picture(帧内编码图像帧)，不参考其他图像帧，只利用本帧的信息进行编码
P 帧:Predictive-coded picture(预测编码图像帧)，利用之前的(I/P)帧，采用运动预测的方式进行帧间预测编码
B 帧:Bidirectionally predicted picture(双向预测编码图像帧)，提供最高压缩比，它即需要之前的图像帧(I/P)，也需要后来的图像帧(P)，采用运动预测的方式进行帧间双向预测编码

### GOP

GOP(group of picture):图像组，指两个 I 帧之间的距离，也就是 I 帧间隔，两个 I 帧之间有多少 P/B 帧
Reference:参考周期，指两个 P 帧之间的距离

在

### PTS DTS

因为双向预测编码帧，即 B 帧需要分别参考前面和后面的帧

