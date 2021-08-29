# HTTP 超文本传输协议

[![website][website-image]][website-href]

[website-image]: https://img.shields.io/website-up-down-green-red/https/githome.io/http/.svg
[website-href]: https://githome.io/http/

## 简史

* HTTP/0.9
* HTTP/1.0
* HTTP/1.1
* HTTP/2
* HTTP/3

## 功能

HTTP/1.1 即 HTTP over TCP/IP，可以在 TCP/IP 之上实现以下功能：

* 连接控制
* 缓存管理
* 数据编码
* 内容协商

## 基本结构

* 起始行（start line）
  * 请求行（request line）：使用空格符 SP 分隔，使用换行符 CRLF 结束
    * 请求方法
    * 请求目标：URI
    * 版本号
  * 状态行（status line）
    * 版本号
    * 状态码（statis code）
    * 原因短语
* 消息头（header） - 必须；可以自定义；键值对字段的集合，每个字段末尾以 CRLF 换行符结束
  * 请求头
  * 响应头
* CRLF - 空行；16 进制为 0D0A
* 消息体（entry/body） - 可空

起始行和消息头通常合称为 `请求头` 或 `响应头`。

```txt
// 请求行格式
┌─────────────────────────────────────────┐
│ Method │ SP | URI | SP | Version | CRLF |
└─────────────────────────────────────────┘

// 示例
GET / HTTP/1.1\r\n
```

```txt
// 状态行格式
┌─────────────────────────────────────────────────┐
│ Version │ SP | Status Code | SP | Reason | CRLF |
└─────────────────────────────────────────────────┘

// 示例
HTTP/1.1 200 OK\r\n
```

## 特点

* 可扩展
* 可靠，HTTP over TCP/IP
* 应用层协议
* 跨语言、跨平台
* “请求 - 应答” 通信模式
* 无状态
* 明文传输 - HTTP 报文消息头使用文本形式，而非二进制形式
  * 好处：便于阅读和修改
  * 坏处：容易在传输过程中被窥视

### 无状态

HTTP 1.x 是无状态协议，即每个请求和响应都是独一无二的，请求与请求之间、响应与响应之间没有上下文关系。

UDP 是无连接无状态协议，“顺序发包乱序收包”，接收方不会整理包的先后顺序。

TCP 是有连接有状态协议，最初是 CLOSED 状态，连接成功后是 ESTABLISHED 状态，断开连接后是 FIN-WAIT 状态，最后又是 CLOSED 状态。

HTTP 是有连接无状态协议，“顺序发包顺序收包”，双方按收发的顺序整理报文。

好处：

* 每个请求都是独立的，不存在 “状态” 差异，进而使得后端所有服务器可以完全相同，组成集群后可以通过负载均衡转发请求到 **任意** 一台服务器，轻松实现高可用高并发。

坏处：

* 无法直接支持连续多个有关联的事务操作 - 可以通过 Cookie/Session 来间接实现
* 没有身份认证和完整性校验
* “请求 - 应答” 模式会造成 「队头阻塞」（Head of line blocking）。在顺序发送的请求序列中，某个请求出现阻塞，会造成其后的所有请求一同被阻塞。因为 HTTP/1.1 存在的该缺陷，进而出现了一些 “Web 性能优化” 技术：缓存、切图、数据内嵌与合并、域名分片、JS 黑科技（合并等）

## LICENSE

[![CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](LICENSE)

## 参考

* [HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)
