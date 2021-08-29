# 消息头

## 响应行

### 状态码

* `400` 可能的原因
  * 请求体字段格式错误
    * `Host : localhost` - `Host` 与 `:` 直接不能有空格
  * `Content-Length` 请求体的长度计算错误
