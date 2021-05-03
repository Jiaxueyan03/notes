# HTTPS 加密过程

HTTPS（安全的 HTTP）是 HTTP 协议的加密版本。它通常使用 SSL 或者 TLS 来加密客户端和服务器之间所有的通信。允许客户端与服务器安全地交换敏感的数据。

![HTTPS 通信](https://www.ituring.com.cn/figures/2014/PIC%20HTTP/11.d07z.011.png ':size=600')

通过加密，防止通信内容被窃听、篡改或伪装。防 [中间人攻击](https://zh.wikipedia.org/wiki/%E4%B8%AD%E9%97%B4%E4%BA%BA%E6%94%BB%E5%87%BB)

1. 加密传输：第三方无法窃听。
2. 校验机制：一旦被篡改，通信双方会立刻发现。
3. 身份证书：防止身份被冒充。

加密大致过程：

1. 客户端请求服务器获取证书`公钥`。
2. 客户端（SSL/TLS）解析证书`获取公钥`。
3. 生成`随机值`，用`公钥`加密随机值生成`密钥`,传给服务器。
4. 服务器用`私钥`解密密钥得到随机值。
5. 将信息和随机值混合在一起进行`对称加密`，传给客户端。
6. 客户端用`密钥`解密信息。


### 相互交换密钥的公开密钥加密技术

`SSL` 采用`公开密钥加密`的加密方式。

近代的加密方法中加密算法是公开的，而密钥却是保密的。通过这种方式得以保持加密方法的安全性。

加密和解密都会用到密钥。没有密钥就无法对密码解密，反过来说，任何人只要持有密钥就能解密了。如果密钥被攻击者获得，那加密也就失去了意义。

#### 共享密钥加密（对称密钥加密）

加密和解密同用`一个密钥`的方式称为共享密钥加密，也被叫做`对称密钥加密`。

![共享密钥加密](https://www.ituring.com.cn/figures/2014/PIC%20HTTP/11.d07z.014.png ':size=600')

密钥发送问题：无法安全的发送密钥给对方。发送密钥有被窃听的风险。

![对称加密](https://www.ituring.com.cn/figures/2014/PIC%20HTTP/11.d07z.015.png ':size=600')

#### 公开密钥加密（非对称密钥加密）

`公开密钥加密`方式很好地解决了`共享密钥加密`的困难。它使用一对`非对称`的密钥（`私有密钥`和`公开密钥`）。私钥不能让其他任何人知道，公钥可以随意发布，任何人都可以获取。

1. 发送密文的一方使用`对方的公钥`进行加密处理。
2. 对方收到被加密的信息后，在用`自己的私钥`进行解密。

利用这种方式，不需要发送用来解密的私钥，也不必担心密钥被攻击者窃听而盗走。

另外，要想根据密文和公开密钥，恢复到信息原文是异常困难的，因为解密过程就是在对离散对数进行求值，这并非轻而易举就能办到。退一步讲，如果能对一个非常大的整数做到快速地因式分解，那么密码破解还是存在希望的。但就目前的技术来看是不太现实的。

![非对称加密](https://www.ituring.com.cn/figures/2014/PIC%20HTTP/11.d07z.016.png ':size=600')

#### HTTPS 采用混合加密机制

HTTPS 采用`共享密钥加密`（对称加密）和`公开密钥加密`（非对称加密）两者并用的`混合`加密机制。

公开密钥加密与共享密钥加密相比，其处理速度要慢。结合两者各自的优势：

1. 在交换密钥环节使用`公开密钥加密`方式
2. 之后的建立通信交换报文阶段则使用`共享密钥加密`方式。

![混合加密机制](https://www.ituring.com.cn/figures/2014/PIC%20HTTP/11.d07z.017.png ':size=600')

### 证明公开密钥正确性的证书

公钥加密存在一些问题，无法证明公钥本身的真实性。比如公钥在传输中被攻击者替换（[HTTPS 中间人攻击](http/note11.md)）。

为了证明公钥的正确性，使用由数字证书认证机构（`CA`，Certificate Authority）和其相关机关颁发的公开密钥`证书`。数字证书认证机构处于客户端与服务器双方都可信赖的第三方机构的立场上。

![数字证书认证步骤](https://www.ituring.com.cn/figures/2014/PIC%20HTTP/11.d07z.018.png ':size=600')

证书（EV SSL 证书）的作用：

1. 证明作为通信一方的服务器是否规范。
2. 可确认对方服务器背后运营的企业是否真实存在。

### HTTPS 的安全通信机制

HTTPS 的通信步骤：

![HTTPS 的通信步骤](https://www.ituring.com.cn/figures/2014/PIC%20HTTP/11.d07z.021.png ':size=600')

> 参考《图解HTTP》[第七章](https://www.ituring.com.cn/book/miniarticle/74663)