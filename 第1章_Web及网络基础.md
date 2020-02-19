# 第一章.web及网络基础

TCP/IP协议族，是在IP协议的通信过程中，使用到的协议族的统称。HTTP属于其内部的一个子集。

## 1 TCP/IP的分层管理

依次分为一下4层：应用层、传输层、网络层、数据链路层。

### 应用层

应用层决定了向用户提供应用服务时通信的活动。

* FTP（File Transfer Protocol，文件传输协议）
* DNS（Domain Name System，域名系统）
* HTTP

### 传输层

传输层对上层应用层，提供处于网络连接中 的两台计算机之间的数据传输。

* TCP（Transmission Control Protocol，传输控制协议）
* UDP（User Data Protocol，用户数据报协议）

### 网络层

网络层用来处理在网络上流动的数据包。

* IP（Internet Protocol），IP协议（和IP地址区分开）

### 链路层

用来处理链接网络的硬件部分。



数据在层与层之间会有数据信息的包装起来的做法称为**封装**（encapsulate）。

## 2 与HTTP关系密切的协议

### 2.1 负责传输的IP协议

作用：把各种数据包传送给对方。

为了满足传输的准确，需要**IP地址**和**MAC地址**（Media Access Control Address）

IP地址指明了节点被分配到的地址，MAC地址是指网卡所属的固定地址。（这其中还会采用ARP协议，通过通信方的IP地址反查出对应的MAC地址）

### 2.2 确保可靠性的TCP协议

TCP提供可靠的字节流服务。**字节流服务**（Byte Stream Service），为了方便传输，将大块数据分割为以**报文段**（segment）为单位的数据包进行管理。

确保数据能到达目标，TCP采用三次握手（three-way handshaking）策略。
握手过程中使用了TCP的标志（flag）——SYN（synchronize）和ACK（acknowledge）。

发送端    |    ———SYN———》   		| 接收端
​	       |    《———SYN/ACK———	| 
​	       |	———ACK———》		|

### 2.3 负责域名解析的DNS服务

DNS提供域名到IP地址之间的解析服务。（通过域名查找IP地址，或逆向从IP地址反查域名的服务。）

## 3 URI和UPL

URL（Uniform Resource Locator，统一资源定位符），如www.baidu.com

URI（Uniform Resource Identifier，统一资源标识符）
URI是由某个协议方案表示的资源的定位标识符。协议方案是指访问资源所使用的协议类型名称。比如http、ftp、mailto、telnet、file等。

URI用字符串标识某一互联网资源，而URL表示资源的地点。URL是URI的子集。

URI格式：

http://user:pass@www.example.com:8080/dir/index.html?uid=1#ch1

| http://    | user:pass@             | www.example.com | :8080                              | /dir/index.html  | ?uid=1             | #ch1               |
| ---------- | ---------------------- | --------------- | ---------------------------------- | ---------------- | ------------------ | ------------------ |
| 协议方案名 | 登录信息（认证，可选） | 服务器地址      | 服务器端口号（若无则为默认端口号） | 带层次的文件路径 | 查询字符串（可选） | 片段标识符（可选） |

