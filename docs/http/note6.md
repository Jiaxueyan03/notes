# HTTP不同版本的特点

### HTTP/0.9 单行协议

HTTP/0.9 极其简单：

1. 请求只有`一行`，以唯一可用方法`GET`开头，后面跟着目标`资源路径`（一旦连接到服务器，协议、服务器、端口号这些都不是必须的）。
2. 只包含响应文档本身。没有响应头，只有`HTML`文件可以传送，无法传输其他类型的文件。也`没有状态码`。

```
GET /mypage.html

<HTML>
这是一个非常简单的HTML页面
</HTML>
```

### HTTP/1.0 构建可扩展性

由于 HTTP/0.9 协议的应用十分有限，浏览器和服务器迅速扩展内容使其用途更广：

1. 协议`版本`信息也会被发送，追加到 GET 行。
2. 响应包含`状态码`，使浏览器能知道请求成功或失败。
3. 引入`HTTP 头`的概念，无论是请求还是响应，允许传输元数据，使协议变得非常灵活，更具扩展性。
4. 在新 HTTP 头的帮助下，具备了传输除纯文本 HTML 文件以外`其他类型`文档的能力（感谢 [Content-Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type) 头）。

在 1991-1995 年，这些新扩展并没有被引入到标准中。直到 1996 年 11 月，文档（RFC 1945）被发表，此文档定义了 HTTP/1.0，但它是狭义的，并不是官方标准。

### HTTP/1.1 标准化协议

在 1997 年初，HTTP/1.1 标准发布（HTTP 的第一个标准化版本），就在 HTTP/1.0 发布的几个月后。HTTP/1.1 在 1997 年 1 月以 [RFC 2068](https://tools.ietf.org/html/rfc2068) 文件发布。

HTTP/1.1 消除了大量歧义内容并引入了多项改进：

1. 连接`复用`，节省了多次打开 TCP 连接加载网页文档资源的时间。（[长连接](http/note8.md)）
2. 增加 [管线化](https://zh.wikipedia.org/wiki/HTTP%E7%AE%A1%E7%B7%9A%E5%8C%96) 技术，可以将多个请求整批提交，而在发送过程中不需要先等待服务器的回应，以降低通信延迟。
3. 支持响应`分块`。
4. 引入额外的`缓存控制`机制。
5. 引入`内容协商`机制，包括语言，编码，类型等，并允许客户端和服务器之间约定以最合适的内容进行交换。
6. 感谢 [Host](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Host) 头，能够使不同域名配置在同一个 IP 地址的服务器上。

注释：`管线化技术`（HTTP pipelining）是将`多个` HTTP 请求整批提交的技术，而在发送过程中不需先等待服务器的回应。但由于需要遵循 HTTP/1.1，必须按照客户端发送的`请求顺序`来回复请求，这样整个连接还是`先进先出`的，[队头阻塞](https://zh.wikipedia.org/wiki/%E9%98%9F%E5%A4%B4%E9%98%BB%E5%A1%9E) 可能会发生，造成延迟。

### 超过 15 年的扩展

由于 HTTP 协议的`可扩展性`，创建新的头部和方法是很容易的，即使 HTTP/1.1 协议进行过两次修订，[RFC 2616](https://tools.ietf.org/html/rfc2616) 发布于 1999 年 6 月，而另外两个文档 [RFC 7230](https://tools.ietf.org/html/rfc7230) [RFC 7235](https://tools.ietf.org/html/rfc7235) 发布于 2014 年 6 月，作为 HTTP/2 的预览版本。HTTP 协议已经稳定使用超过 15 年了。

HTTP 在基本的`TCP/IP`协议栈上发送信息，网景公司（Netscape Communication）在此基础上创建了一个额外的`加密传输层（SSL）`。允许`通过加密`来保证服务器和客户端之间交换消息的`真实性`。`SSL`在标准化道路上最终成为 [TLS](https://developer.mozilla.org/zh-CN/docs/Glossary/TLS)。

人们对`加密传输层`的需求也愈发高涨，对`TLS`的需求也变得普遍。

[HTTPS](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%AE%89%E5%85%A8%E5%8D%8F%E8%AE%AE)（安全的 HTTP）是 HTTP 协议的`加密`版本。它通常使用 SSL 或者 TLS 来加密客户端和服务器之间所有的通信。允许客户端与服务器安全地交换敏感的数据。

### HTTP/2 为了更优异的表现

HTTP/1.1 链接需要请求以正确的顺序发送，理论上可以用一些并行的链接（尤其是5到8个），带来的成本和复杂性堪忧。比如，HTTP 管线化（pipelining）就成为了 Web 开发的负担。

在 2010 年到 2015 年，谷歌通过实践了一个实验性的`SPDY`协议，证明了一个在客户端和服务器端交换数据的另类方式。明确了响应数量的增加和解决复杂的数据传输，SPDY 成为了`HTTP/2`协议的基础。在 2015 年 5 月正式标准化后，HTTP/2 取得了极大的成功。

HTTP/2 在 HTTP/1.1 有几处基本的不同：

1. HTTP/2 是`二进制协议`而不是文本协议。不再可读，也不可无障碍的手动创建，改善的优化技术现在可被实施。（二进制分帧）
2. 这是一个`复用协议`。并行的请求能在同一个链接中处理，移除了 HTTP/1.x 中顺序和阻塞的约束。（[多路复用](http/note7.md)）
3. `压缩`了 headers。因为 headers 在一系列请求中常常是相似的，其移除了重复和传输重复数据的成本。（头部压缩）
4. 允许服务器在客户端缓存中填充数据，通过`服务器推送`机制来提前请求。

### 后 HTTP/2 进化

HTTP 没有停止进化，HTTP 的`扩展性`依然被用来添加新的功能。

2016 年里 HTTP 的新扩展：

1. 对 Alt-Svc 的支持允许了给定资源的位置和资源鉴定，允许了更智能的 CDN 缓冲机制。
2. Client-Hints 的引入允许浏览器或者客户端来主动交流它的需求，或者是硬件约束的信息给服务端。
3. 在 Cookie 头中引入安全相关的的`前缀`，现在帮助保证一个安全的 cookie 没被更改过。

> [MDN HTTP的发展](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)