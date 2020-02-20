# 第2章 HTTP协议
## 1 请求和响应

请求从客户端发出，最后服务器端响应该请求并返回。

### 1.1 请求报文

```
GET	/index.html HTTP/1.1
Host: example.com

```

第1行：请求方法（method）、请求URI（request-URI）、协议版本

第2行：请求首部字段（可选）

第3行：内容实体（可选）

### 1.2 响应报文

接收到请求的服务器，会将请求内容的处理结构以响应的形式返回。

```
HTTP/1.1 200 OK
Date: Wed, 19 Feb 2020 12:39:36 GMT
Content-Length: 379
Content-Type: text/html

<html>
...
```

第1行：协议版本、状态码、状态码的原因短语（reason-phrase）

第2-4行：响应首部字段（header field）

第5行：空格

第6-7行：主体（entity body）



HTTP是一种无状态（stateless）协议。协议对于发送过的请求或响应都不做持久化处理。

HTTP通过URI定位互联网上的资源。例如：GET http://baidu.com HTTP/1.1

### 1.3 HTTP方法（8种）

#### GET：获取资源

:shark:我想访问你的某个资源！

GET方法用来请求访问已被URI识别的资源。

如果请求的资源是文本，那就保持原样返回；如果是CGI（Common Gateway Interface，通用网关接口）那样的程序，则返回经过执行后的输出结果。
p.s.大部分CGI程序用来处理来自表单的输入信息，并在服务器产生相应的处理，或将相应的信息反馈给浏览器。CGI程序使网关具有交互功能。

#### POST：传输实体主体

:shark:我想把这条信息告诉你！

#### PUT：传输文件

:open_file_folder:我要把这份文件传给你！

HTTP/1.1的PUT方法无验证机制，任何人都可以上传文件，存在安全问题。一般需配合Web应用程序的验证机制，或构架设计采用REST（REpresentation State Tranfer，表征状态转移）标准的Web网站使用。

#### HEAD：获得报文首部

同GET方法一样，只是不返回报文主体部分。用来确定URI的有效性及资源更新的日期等。

#### DELETE：删除文件

按请求URI删除指定资源。

同PUT请求，不安全。

#### OPTIONS：询问支持的方法

:astonished:-你支持哪类方法？-支持GET和HEAD方法。

用来查询针对请求URI指定的资源支持的方法。

#### TRACE：追踪路径

让Web服务器将之前的请求通信还会给客户端。

#### CONNECT：要求用隧道协议连接代理

要求在代理服务器通信时建立隧道，实现用隧道协议进行TCP通信。

主要使用SSL（Secure Sockets Layer，安全套接层）和TLS（Transport Layer Security，传输层安全）协议把通信内容加密后经网络隧道传输。

格式：

```
CONNECT 代理服务器名:端口号 HTTP版本
```

## 2 持久连接节省通信量

每进行一次HTTP通讯就要断开一次TCP连接。

若请求一个包含多张图片的HTML页面时，在发送请求访问HTML页面资源时，也会请求该HTML页面里包含的其他资源。每次请求都会造成无谓的TCP连接建立和断开，增加通信量的开销。

### 2.1 持久连接

持久连接（HTTP Persistent Connections，也称HTTP keep-alive或HTTP connection reuse）。

特点：只要任意一端没有明确提出断开连接，则保持TCP连接状态。

### 2.2 管线化

管线化（pipeline），不用等待响应亦可直接发送下一个请求。

这样可以同时发送多条请求，而不需要一个接一个地等待响应了。

## 3 Cookie的状态管理

Cookie技术通过在请求和响应报文中写入Cookie信息来控制客户端的状态。

Cookie会根据从服务器端发送的响应报文内的一个叫做Set-Cookie的首部字段信息，通知客户端保存Cookie。当下次客户端再往服务器发送请求时，客户端会自动在请求报文中加入Cookie值发送过去。

服务器端发现客户端发送来的Cookie后，会去检查究竟是从哪一个客户端发来的连接请求，然后对比服务器上的记录，最后得到之前的状态信息。









