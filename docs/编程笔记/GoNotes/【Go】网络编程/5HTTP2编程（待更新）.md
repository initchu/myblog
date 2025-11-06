# 5 HTTP 2 编程（待更新）

# <font style="color:rgb(0, 0, 0);">HTTP/2协议</font>
`go get golang.org/x/net/http2`

<font style="color:rgb(0, 0, 0);">HTTP/2 协议握手分2种方式，一种叫 h2，一种叫 h2c。</font>

<font style="color:rgb(0, 0, 0);">h2 要求必须使用 TLS 加密，在 TLS 握手期间会顺带完成 HTTPS/2 协议的协商，如果协商失败（比如客户端不支持或者服务端不支持），则会使用 HTTPS/1 继续后续通讯。</font>

<font style="color:rgb(0, 0, 0);">h2c 不使用 TLS，而是多了一次基于 HTTP 协议的握手往返来完成向 HTTP/2 协议的升级，一般不建议使用。</font>



> 更新: 2022-08-10 14:47:11  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/kyyzsr>