# HTTP 协议的基本工作流程

本文以浏览器访问 `http://weplay.me` 为例进行讲解。其中 `weplay.me` 为域名，全称是 `weplay.me.`

## DNS 解析

HTTP/1.x 是建立在 TCP/IP 之上的，即 HTTP over TCP/IP。因此，在建立 TCP 连接之前，需要先获取 IP 地址。

1. 浏览器缓存
2. 操作系统缓存
3. hosts 文件
4. resolver 文件或网关服务器中配置的 DNS 服务器，如 114.114.114.114
5. nameserver 服务商向 「根域名服务器」（即 `weplay.me` 准确的是 `weplay.me.`，根域名指的是最后那个 `.`）请求查询 「顶级域名服务器」 `.me` 的 IP 地址
6. `.me` 顶级域名服务器会返回 `weplay.me` 的 IP 地址

## TCP 三次握手

1. SYN
2. SYN,ACK
3. ACK
