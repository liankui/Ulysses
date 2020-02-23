# 第6章_HTTP首部
## HTTP首部字段

使用首部字段是为了给浏览器和服务器提供报文主体大小、所使用的语言、认证信息等。

| HTTP报文      | 分类描述（请求报文/响应报文） | 详细描述            |
| ------------- | ----------------------------- | ------------------- |
| 报文首部      | 请求行/状态行                 | 方法、URI、HTTP版本 |
|               | 请求首部字段/响应首部字段     | HTTP首部字段        |
|               | 通用首部字段                  | HTTP首部字段        |
|               | 实体首部字段                  | HTTP首部字段        |
|               | 其他                          |                     |
| 空行（CR+LF） |                               |                     |
| 报文主体      |                               |                     |

### HTTP首部字段结构

首部字段名：字段值

例如：

Content-Type: text/html 	表示报文主体的对象类型

Keep-Alive: timeout=15, max=100	HTTP首部字段可以有多个值



HTTP/1.1 规范定义了47种首部字段，除此之外还有Cookie、Set-Cookie和Content-Disposition等首部字段。

#### 缓存代理行为

HTTP首部字段定义缓存代理和非缓存代理的行为，分为2类。

端对端首部（End-to-end Header）

此类中首部会转发给请求/响应对应的最终接收目标，且必须保存在有缓存生成的响应中，它必须被转发。

逐跳首部（Hop-by-hop Header）

此类中首部只对单次转发有效，会因通过缓存或代理而不再转发，需提供Connection字段。

### HTTP/1.1 通用首部字段

#### Cache-Control

操作缓存的工作机制。

```
Cache-Control: private, max-age=0, no-cache
```

**表示能否缓存的指令**

public：明确表明其他用户也可利用缓存。

private：响应只以特定的用户作为对象。

no-cache：防止从缓存中返回过期的资源。（缓存会向服务器进行有效期确认后再处理资源）

**控制可执行缓存的对象的指令**

no-store：请求或响应中包含机密信息，缓存不能在本地存储请求或响应的任一部分。

**指定缓存期限和认证的指令**

s-maxage：适用于供多位用户使用的公共缓存服务器

max-age：如果判定缓存资源的缓存时间数值比指定时间的数值更小，那么客户端就接收缓存的资源。若执行max-age=0，那么缓存服务器通常需要将请求转发给源服务器。

min-fresh：要求缓存服务器返回至少还未过指定时间的缓存资源。

max-stale：指示缓存资源即使过期也照常接收。

only-if-cached：客户端仅在缓存服务器本地缓存目标资源的情况下才会要求其返回。

。。。。。。

#### Connection

* 控制不再转发给代理的首部字段
* 控制持久连接

#### Date

表明创建HTTP报文的日期和时间。

#### Pragma

历史遗留字段，只有一种形式Pragma：no-cache，

发送的请求一般同时包含以下两个首部字段

```
Cache-Control: no-cache
Pragma: no-cache
```

#### Trailer

事先说明在报文主体后记录了哪些首部字段。

#### Transfer-Encoding

规定了传输报文主体时采用的编码方式。

例如：Transfer-Encoding： chhunked

#### Upgrade

用于检测HTTP协议及其他协议是否可使用更高的版本进行通信。

#### Via

为了追踪客户端与服务器之间的请求和响应报文的传输路径。

#### Warning

通常会告知用户一些与缓存相关的问题的警告。

### 请求首部字段

是从客户端往服务器端发送请求报文中所使用的字段，用来补充请求的附加信息、客户端信息、对响应内容相关的优先级等内容。

#### Accept

通知服务器，用户代理能够处理的媒体类型及媒体类型对应的优先级。

媒体类型：

文本文件：text/html, text/plain, text/css ...  application/xhtml+xml, application/xml ...

图片文件：image/jpeg, image/gif, image/png ...

视频文件：video/mpeg, video/quicktime ...

应用程序使用的二进制文件：aplication/octet-stream, application.zip ...

使用q=来表示权重值，范围在0-1，默认权重为q=1.0。

#### Accept-Charset

通知服务器用户代理支持的字符集及字符集的相对优先顺序。

#### Accept-Encoding

用来告知服务器用户代理支持的内容编码及内容编码的优先顺序。

例子：

```
Accept-Encoding: gzip, deflate
```

编码格式：gzip、compress、deflate、identity

#### Accept-Language

告知服务器用户代理能够处理的自然语言集（中文或英文等），以及自然语言集的相对优先级。

#### Authorization

用来告知服务器，用户代理的认证信息（证书值）。

#### Expect

告知服务器期望出现的某种特定行为。

#### From

告知服务器使用用户代理的用户的电子邮件地址。

#### Host

告知服务器，请求的资源所处的互联网主机名和端口号。

#### If-Match

服务器会比对If-Match的字段值和资源的Etag值，仅当两者一致时才会执行请求。

若If-Match的字段值为*时，服务器将会忽略Etag的值，只要资源存在就处理请求。

If-Modified-Since

if-None-Match

If-Range

If-Unmodified-Since

Max-Forwards

Proxy-Authorization

Range

Referfer

TE

User-Agent

### 响应首部字段

#### Accept-Ranges

#### Age

#### Etag

#### Location

#### Proxy-Authenticate

#### Retry-After

Server

Vary

WWW-Authenticate

### 实体首部字段

#### Allow

#### Content-Encoding

Content-Language

Content-Length

Content-Location

Content-MD5

Content-Range

Content-Type

Expires

Last-Modified

### 为Cookie服务的首部字段

Cookie的工作机制是用户识别及状态管理。

| 首部字段名 | 说明                           | 首部类型     |
| ---------- | ------------------------------ | ------------ |
| Set-Cookie | 开始状态管理所使用的Cookie信息 | 响应首部字段 |
| Cookie     | 服务器接收到的Cookie信息       | 请求首部字段 |

#### Set-Cookie

当服务器准备开始管理客户端的状态时，会事先告知的各种信息。

Set-Cookie的字段值：

| 属性         | 说明                                         |
| ------------ | -------------------------------------------- |
| NAME=VALUE   | 赋予Cookie的名称和值                         |
| expires=DATE | Cookie的有效期（若无则默认浏览器关闭前为止） |
| path=PATH    | 将服务器上的文件目录作为Cookie的使用对象     |
| domain=域名  | 作为Cookie适用对象的域名                     |
| Secure       | 仅在HTTPS安全通信时才会发送Cookie            |
| HttpOnly     | 加以限制，使Cookie不能被JavaScript脚本访问   |

#### Cookie

```
Cookie: status=enable
```



