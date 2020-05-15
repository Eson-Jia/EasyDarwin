# 协议抓包

## RTSP

### 推流模式下

Server: 192.168.1.22 EasyDarwin
Client: ffmpeg
Action: ffmpeg 取流推给 darwin

```rtsp
OPTIONS rtsp://192.168.1.22:10554/test RTSP/1.0
CSeq: 1
User-Agent: Lavf57.73.100

RTSP/1.0 200 OK
CSeq: 1
Session: ImAuCKRMg
Public: DESCRIBE, SETUP, TEARDOWN, PLAY, PAUSE, OPTIONS, ANNOUNCE, RECORD

ANNOUNCE rtsp://192.168.1.22:10554/test RTSP/1.0
Content-Type: application/sdp
CSeq: 2
User-Agent: Lavf57.73.100
Session: ImAuCKRMg
Content-Length: 488

v=0
o=- 0 0 IN IP4 127.0.0.1
s=Media Presentation
c=IN IP4 192.168.1.22
t=0 0
a=tool:libavformat 57.73.100
m=video 0 RTP/AVP 96
a=rtpmap:96 H264/90000
a=fmtp:96 packetization-mode=1; sprop-parameter-sets=Z0IAKp2oHgCJ+WbgICAoAAADAAgAAAMBlCA=,aM48gA==; profile-level-id=42002A
a=control:streamid=0
m=audio 0 RTP/AVP 97
a=rtpmap:97 MPEG4-GENERIC/16000/1
a=fmtp:97 profile-level-id=1;mode=AAC-hbr;sizelength=13;indexlength=3;indexdeltalength=3; config=1408
a=control:streamid=1
RTSP/1.0 200 OK
CSeq: 2
Session: ImAuCKRMg

SETUP rtsp://192.168.1.22:10554/test/streamid=0 RTSP/1.0
Transport: RTP/AVP/TCP;unicast;interleaved=0-1;mode=record
CSeq: 3
User-Agent: Lavf57.73.100
Session: ImAuCKRMg

RTSP/1.0 200 OK
Transport: RTP/AVP/TCP;unicast;interleaved=0-1;mode=record
CSeq: 3
Session: ImAuCKRMg

SETUP rtsp://192.168.1.22:10554/test/streamid=1 RTSP/1.0
Transport: RTP/AVP/TCP;unicast;interleaved=2-3;mode=record
CSeq: 4
User-Agent: Lavf57.73.100
Session: ImAuCKRMg

RTSP/1.0 200 OK
Transport: RTP/AVP/TCP;unicast;interleaved=2-3;mode=record
CSeq: 4
Session: ImAuCKRMg

RECORD rtsp://192.168.1.22:10554/test RTSP/1.0
Range: npt=0.000-
CSeq: 5
User-Agent: Lavf57.73.100
Session: ImAuCKRMg

RTSP/1.0 200 OK
CSeq: 5
Session: ImAuCKRMg

TEARDOWN rtsp://192.168.1.22:10554/test RTSP/1.0
CSeq: 6
User-Agent: Lavf57.73.100
Session: ImAuCKRMg

RTSP/1.0 200 OK
CSeq: 6
Session: ImAuCKRMg
```

### 拉流模式下

Server: 192.168.10.147 监控相机
Client: ffplay
Action: 播放相机流

```rtsp
OPTIONS rtsp://192.168.10.147:554 RTSP/1.0
CSeq: 1
User-Agent: Lavf57.83.100

RTSP/1.0 200 OK
CSeq: 1
Public: OPTIONS, DESCRIBE, PLAY, PAUSE, SETUP, TEARDOWN, SET_PARAMETER, GET_PARAMETER
Date:  Thu, May 14 2020 16:45:35 GMT

DESCRIBE rtsp://192.168.10.147:554 RTSP/1.0
Accept: application/sdp
CSeq: 2
User-Agent: Lavf57.83.100

RTSP/1.0 401 Unauthorized
CSeq: 2
WWW-Authenticate: Digest realm="IP Camera(C2875)", nonce="938032d91ffc30ca80b5da94c18887ac", stale="FALSE"
Date:  Thu, May 14 2020 16:45:35 GMT

DESCRIBE rtsp://192.168.10.147:554 RTSP/1.0
Accept: application/sdp
CSeq: 3
User-Agent: Lavf57.83.100
Authorization: Digest username="admin", realm="IP Camera(C2875)", nonce="938032d91ffc30ca80b5da94c18887ac", uri="rtsp://192.168.10.147:554", response="271d713c3058c90bc2414ed4ac9e0faa"

RTSP/1.0 200 OK
CSeq: 3
Content-Type: application/sdp
Content-Base: rtsp://192.168.10.147:554/
Content-Length: 842

v=0
o=- 1589474735691720 1589474735691720 IN IP4 192.168.10.147
s=Media Presentation
e=NONE
b=AS:5100
t=0 0
a=control:rtsp://192.168.10.147:554/
m=video 0 RTP/AVP 96
c=IN IP4 0.0.0.0
b=AS:5000
a=recvonly
a=x-dimensions:1920,1080
a=control:rtsp://192.168.10.147:554/trackID=1
a=rtpmap:96 H264/90000
a=fmtp:96 profile-level-id=420029; packetization-mode=1; sprop-parameter-sets=Z0IAKp2oHgCJ+WbgICAoAAADAAgAAAMBlCA=,aM48gA==
m=audio 0 RTP/AVP 104
c=IN IP4 0.0.0.0
b=AS:50
a=recvonly
a=control:rtsp://192.168.10.147:554/trackID=2
a=rtpmap:104 mpeg4-generic/16000/1
a=fmtp:104 profile-level-id=15; streamtype=5; mode=AAC-hbr; config=1408;SizeLength=13; IndexLength=3; IndexDeltaLength=3; Profile=1;
a=Media_header:MEDIAINFO=494D4B48010200000400000101200110803E0000803E000000000000000000000000000000000000;
a=appversion:1.0

SETUP rtsp://192.168.10.147:554/trackID=1 RTSP/1.0
Transport: RTP/AVP/UDP;unicast;client_port=24230-24231
CSeq: 4
User-Agent: Lavf57.83.100
Authorization: Digest username="admin", realm="IP Camera(C2875)", nonce="938032d91ffc30ca80b5da94c18887ac", uri="rtsp://192.168.10.147:554/trackID=1", response="415ff004265583c57ae395185d53c314"

RTSP/1.0 200 OK
CSeq: 4
Session:        708732579;timeout=60
Transport: RTP/AVP/UDP;unicast;client_port=24230-24231;server_port=8318-8319;ssrc=1cdebfaf;mode="play"
Date:  Thu, May 14 2020 16:45:35 GMT

SETUP rtsp://192.168.10.147:554/trackID=2 RTSP/1.0
Transport: RTP/AVP/UDP;unicast;client_port=24232-24233
CSeq: 5
User-Agent: Lavf57.83.100
Session: 708732579
Authorization: Digest username="admin", realm="IP Camera(C2875)", nonce="938032d91ffc30ca80b5da94c18887ac", uri="rtsp://192.168.10.147:554/trackID=2", response="22de5d568f39e5e6d380a71a98056a3f"

RTSP/1.0 200 OK
CSeq: 5
Session:        708732579;timeout=60
Transport: RTP/AVP/UDP;unicast;client_port=24232-24233;server_port=8320-8321;ssrc=4208c616;mode="play"
Date:  Thu, May 14 2020 16:45:35 GMT

PLAY rtsp://192.168.10.147:554/ RTSP/1.0
Range: npt=0.000-
CSeq: 6
User-Agent: Lavf57.83.100
Session: 708732579
Authorization: Digest username="admin", realm="IP Camera(C2875)", nonce="938032d91ffc30ca80b5da94c18887ac", uri="rtsp://192.168.10.147:554/", response="cbe708907c4c577bc72522e82c4df551"

RTSP/1.0 200 OK
CSeq: 6
Session:        708732579
RTP-Info: url=rtsp://192.168.10.147:554/trackID=1;seq=11785;rtptime=749374048,url=rtsp://192.168.10.147:554/trackID=2;seq=22266;rtptime=1660321632
Date:  Thu, May 14 2020 16:45:35 GMT

TEARDOWN rtsp://192.168.10.147:554/ RTSP/1.0
CSeq: 7
User-Agent: Lavf57.83.100
Session: 708732579
Authorization: Digest username="admin", realm="IP Camera(C2875)", nonce="938032d91ffc30ca80b5da94c18887ac", uri="rtsp://192.168.10.147:554/", response="9fa34c8f17c94c6421404a642f8b2489"

RTSP/1.0 200 OK
CSeq: 7
Session:        708732579
Date:  Thu, May 14 2020 16:45:36 GMT
```

### 拉 Darwin in Golang 流

Server: EasyDarwin in Golang
Client: ffplay
Action: 播放 darwin 上的流

```tcp
OPTIONS rtsp://192.168.1.22:10554/test RTSP/1.0
CSeq: 2
User-Agent: LibVLC/3.0.8 (LIVE555 Streaming Media v2016.11.28)

RTSP/1.0 200 OK
CSeq: 2
Session: EFKONhgMR
Public: DESCRIBE, SETUP, TEARDOWN, PLAY, PAUSE, OPTIONS, ANNOUNCE, RECORD

DESCRIBE rtsp://192.168.1.22:10554/test RTSP/1.0
CSeq: 3
User-Agent: LibVLC/3.0.8 (LIVE555 Streaming Media v2016.11.28)
Accept: application/sdp

RTSP/1.0 200 OK
CSeq: 3
Session: EFKONhgMR
Content-Length: 830

v=0
o=- 1589550732352122 1589550732352122 IN IP4 192.168.10.147
s=Media Presentation
e=NONE
b=AS:5100
t=0 0
a=control:rtsp://192.168.10.147/
m=video 0 RTP/AVP 96
c=IN IP4 0.0.0.0
b=AS:5000
a=recvonly
a=x-dimensions:1920,1080
a=control:rtsp://192.168.10.147/trackID=1
a=rtpmap:96 H264/90000
a=fmtp:96 profile-level-id=420029; packetization-mode=1; sprop-parameter-sets=Z0IAKp2oHgCJ+WbgICAoAAADAAgAAAMBlCA=,aM48gA==
m=audio 0 RTP/AVP 104
c=IN IP4 0.0.0.0
b=AS:50
a=recvonly
a=control:rtsp://192.168.10.147/trackID=2
a=rtpmap:104 mpeg4-generic/16000/1
a=fmtp:104 profile-level-id=15; streamtype=5; mode=AAC-hbr; config=1408;SizeLength=13; IndexLength=3; IndexDeltaLength=3; Profile=1;
a=Media_header:MEDIAINFO=494D4B48010200000400000101200110803E0000803E000000000000000000000000000000000000;
a=appversion:1.0

SETUP rtsp://192.168.10.147/trackID=1 RTSP/1.0
CSeq: 4
User-Agent: LibVLC/3.0.8 (LIVE555 Streaming Media v2016.11.28)
Transport: RTP/AVP;unicast;client_port=57214-57215

RTSP/1.0 200 OK
CSeq: 4
Session: EFKONhgMR
Transport: RTP/AVP;unicast;client_port=57214-57215

SETUP rtsp://192.168.10.147/trackID=2 RTSP/1.0
CSeq: 5
User-Agent: LibVLC/3.0.8 (LIVE555 Streaming Media v2016.11.28)
Transport: RTP/AVP;unicast;client_port=57216-57217
Session: EFKONhgMR

RTSP/1.0 200 OK
Session: EFKONhgMR
Transport: RTP/AVP;unicast;client_port=57216-57217
CSeq: 5

PLAY rtsp://192.168.10.147/ RTSP/1.0
CSeq: 6
User-Agent: LibVLC/3.0.8 (LIVE555 Streaming Media v2016.11.28)
Session: EFKONhgMR
Range: npt=0.000-

RTSP/1.0 200 OK
Range: npt=0.000-
CSeq: 6
Session: EFKONhgMR

TEARDOWN rtsp://192.168.10.147/ RTSP/1.0
CSeq: 7
User-Agent: LibVLC/3.0.8 (LIVE555 Streaming Media v2016.11.28)
Session: EFKONhgMR

RTSP/1.0 200 OK
CSeq: 7
Session: EFKONhgMR
```

### 拉 Darwin in C++ 流

Server: EasyDarwin in C++
Client: ffplay
Action: 播放 darwin 上的流

```tcp
OPTIONS rtsp://192.168.1.74:10554/18?channel=1 RTSP/1.0
CSeq: 1
User-Agent: Lavf57.83.100

RTSP/1.0 200 OK
Server: VDMSDarwin/2.0 (Build/4.0; Platform/Linux; Release/EasyDarwin; State/Development; )
Cseq: 1
Public: DESCRIBE, SETUP, TEARDOWN, PLAY, PAUSE, OPTIONS, ANNOUNCE, GET_PARAMETER, RECORD

DESCRIBE rtsp://192.168.1.74:10554/18?channel=1 RTSP/1.0
Accept: application/sdp
CSeq: 2
User-Agent: Lavf57.83.100

RTSP/1.0 200 OK
Server: VDMSDarwin/2.0 (Build/4.0; Platform/Linux; Release/EasyDarwin; State/Development; )
Cseq: 2
Cache-Control: no-cache
Content-length: 503
Date: Fri, 15 May 2020 07:09:47 GMT
Expires: Fri, 15 May 2020 07:09:47 GMT
Content-Type: application/sdp
x-Accept-Retransmit: our-retransmit
x-Accept-Dynamic-Rate: 1
Content-Base: rtsp://192.168.1.74:10554/18?channel=1/

v=0
o=- 0 0 IN IP4 127.0.0.1
s=No Name
c=IN IP4 0.0.0.0
t=0 0
a=tool:libavformat 58.18.100
a=control:*
m=video 0 RTP/AVP 96
b=AS:200
a=rtpmap:96 H264/90000
a=fmtp:96 packetization-mode=1; sprop-parameter-sets=Z00AKZpkA8ARPyzUBAQFAAADA+gAAMNQBA==,aO48gA==; profile-level-id=4D0029
a=control:trackID=0
m=audio 0 RTP/AVP 97
b=AS:128
a=rtpmap:97 MPEG4-GENERIC/16000/1
a=fmtp:97 profile-level-id=1;mode=AAC-hbr;sizelength=13;indexlength=3;indexdeltalength=3; config=1408
a=control:trackID=1
SETUP rtsp://192.168.1.74:10554/18?channel=1/trackID=0 RTSP/1.0
Transport: RTP/AVP/UDP;unicast;client_port=24816-24817
x-Dynamic-Rate: 0
CSeq: 3
User-Agent: Lavf57.83.100

RTSP/1.0 200 OK
Server: VDMSDarwin/2.0 (Build/4.0; Platform/Linux; Release/EasyDarwin; State/Development; )
Cseq: 3
Cache-Control: no-cache
Session: 364160928834678926
Date: Fri, 15 May 2020 07:09:47 GMT
Expires: Fri, 15 May 2020 07:09:47 GMT
Transport: RTP/AVP/UDP;unicast;source=172.17.0.11;client_port=24816-24817;server_port=6970-6971
x-Dynamic-Rate: 0

SETUP rtsp://192.168.1.74:10554/18?channel=1/trackID=1 RTSP/1.0
Transport: RTP/AVP/UDP;unicast;client_port=24818-24819
x-Dynamic-Rate: 0
CSeq: 4
User-Agent: Lavf57.83.100
Session: 364160928834678926

RTSP/1.0 200 OK
Server: VDMSDarwin/2.0 (Build/4.0; Platform/Linux; Release/EasyDarwin; State/Development; )
Cseq: 4
Session: 364160928834678926
Cache-Control: no-cache
Date: Fri, 15 May 2020 07:09:47 GMT
Expires: Fri, 15 May 2020 07:09:47 GMT
Transport: RTP/AVP/UDP;unicast;source=172.17.0.11;client_port=24818-24819;server_port=6970-6971
x-Dynamic-Rate: 0

PLAY rtsp://192.168.1.74:10554/18?channel=1/ RTSP/1.0
Range: npt=0.000-
CSeq: 5
User-Agent: Lavf57.83.100
Session: 364160928834678926

RTSP/1.0 200 OK
Server: VDMSDarwin/2.0 (Build/4.0; Platform/Linux; Release/EasyDarwin; State/Development; )
Cseq: 5
Session: 364160928834678926
Range: npt=now-
RTP-Info: url=rtsp://192.168.1.74:10554/18?channel=1/18,url=rtsp://192.168.1.74:10554/18?channel=1/18

TEARDOWN rtsp://192.168.1.74:10554/18?channel=1/ RTSP/1.0
CSeq: 6
User-Agent: Lavf57.83.100
Session: 364160928834678926

RTSP/1.0 200 OK
Server: VDMSDarwin/2.0 (Build/4.0; Platform/Linux; Release/EasyDarwin; State/Development; )
Cseq: 6
Session: 364160928834678926
Connection: Close

```
