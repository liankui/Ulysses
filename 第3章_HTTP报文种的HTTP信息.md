# 第3章.HTTP报文种的HTTP信息
## 1.HTTP报文

分为3部分：

【报文首部】服务器端或客户端需处理的请求或响应的内容及属性

【空行（CR+LF）】CR（Carriage Return，回车符）和LF（Line Feed，换行符）

【报文主体】应被发送的数据

其中报文首部又分为：

请求/响应行
请求/响应首部字段
通用首部字段
实体首部字段
其他

## 2.编码提升传输速率

HTTP协议中**内容编码**指明应用在实体内容上的编码格式，并保持实体信息原样压缩。

内容编码后的实体由客户端接收并负责解码。

在传输大容量数据时，使用分块传输编码（Chunked Transfer Coding）通过把数据分割成多块，能够让浏览器逐步显示页面。

## 3.发送多种数据的多部分对象集合

HTTP协议采用多部分对象集合（Multipart），发送的一份报文主体内可包含多类型实体。通常在图片或这文本文件等上传时使用。需要在首部字段里夹上Content-Type。

* multipart/from-data	在Web表单文件上传时使用
* multipart/byteranges    状态码206（Partial Context，部分内容）

## 4.获取部分内容的分为请求

能从之前下载中断处恢复下载。使用范围请求（Range Request）指定范围发送的请求。

例如：

在首部字段Range来指定资源的byte范围。

Range：bytes=-3000, 5001- 		// 从一开始到3000字节和从5001字节之后全部的多重范围

## 5.内容协商返回最合适的内容

内容协商（Content Negotiation）机制是指客户端和服务器端就响应的资源内容进行交涉，然后提供给客户端最为适合的资源。例如：google对不同国家不同语言的显示。

包含在请求报文中的某些首部字段就是判断的基准。

* Accept
* Accept-Charset
* Accept-Encoding
* Accept-Language
* Content-Language



