## OSI网络七层模型

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Socket/Socket/images/Image.png)
![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Socket/Socket/images/Image1.png)

网络七层模型详解地址 ：http://www.2cto.com/net/201310/252965.html

## OSI网络七层模型与TCP/IP四层模型对比

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Socket/Socket/images/Image2.png)

## 详细的TCP/IP网络模型

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Socket/Socket/images/Image3.png)

##　TCP/IP定义以及模型各层的概念

* TCP/IP（Transmission Control Protocol/Internet Protocol）即传输控制协议/网间协议，是一个工业标准的协议集，它是为广域网（WANs）设计的。
* UDP（User Data Protocol，用户数据报协议）是与TCP相对应的协议。它是属于TCP/IP协议族中的一种。
* 应用层 (Application)：应用层是个很广泛的概念，有一些基本相同的系统级 TCP/IP 应用以及应用协议，也有许多的企业商业应用和互联网应用。
* 传输层 (Transport)：传输层包括 UDP 和 TCP，UDP 几乎不对报文进行检查，而 TCP 提供传输保证。
* 网络层 (Network)：网络层协议由一系列协议组成，包括 ICMP、IGMP、RIP、OSPF、IP(v4,v6) 等。
* 链路层 (Link)：又称为物理数据网络接口层，负责报文传输。

## 网络互交

###　网络编程相关

互联网 通过 IP 定位电脑
在电脑中通过 Port 定位程序
程序和程序间 通过 协议定义通信数据格式

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Socket/Socket/images/Image4.png)

## Socket相関概念

IP地址

* 每台联网的电脑都有一个唯一的IP地址。
* 长度32位，分为四段，每段8位，用十进制数字表示，每段范围 0 ~ 255
* 特殊IP：127.0.0.1 用户本地网卡测试
* 版本：V4(32位) 和 V6(128位，分为8段，每段16位)

## 端口

* 在网络上有很多电脑，这些电脑一般运行了多个网络程序。每种网络程序都打开一个Socket，并绑定到一个端口上，不同的端口对应于不同的网络程序。
* 常用端口：21 FTP ,25 SMTP ,110 POP3 ,80 HTTP , 443 HTTPS

## 有两种常用Socket类型：

* 流式Socket（STREAM）：是一种面向连接的Socket，针对于面向连接的TCP服务应用，安全，但是效率低
* 数据报式Socket（DATAGRAM）：是一种无连接的Socket,对应于无连接的UDP服务应用.不安全(丢失,顺序混乱,在接收端要分析重排及要求重发),但效率高.
Socket定义

* Socket的英文原义是“孔”或“插座”。作为进程通信机制，取后一种意思。通常也称作“套接字”，用于描述IP地址和端口，是一个通信链的句柄。(其实就是两个程序通信用的。)

* Socket非常类似于电话插座。以一个电话网为例。电话的通话双方相当于相互通信的2个程序，电话号码就是IP地址。任何用户在通话之前，首先要占有一部电话机，相当于申请一个Socket；同时要知道对方的号码，相当于对方有一个固定的Socket。然后向对方拨号呼叫，相当于发出连接请求。对方假如在场并空闲，拿起电话话筒，双方就可以正式通话，相当于连接成功。双方通话的过程，是一方向电话机发出信号和对方从电话机接收信号的过程，相当于向Socket发送数据和从Socket接收数据。通话结束后，一方挂起电话机相当于关闭Socket，撤消连接。

* 人通过【电话】可以通信

* 程序通过【Socket】来通信。
* 套接字 就是 程序间的 电话机。

## Socket流式(服务器端和客户端)

![](https://nts.newbieol.com/static/k25/03_%E5%BC%95%E6%93%8E%E9%AB%98%E7%BA%A7%E8%BF%9B%E9%98%B6/Socket%E9%80%9A%E4%BF%A1/Socket/Socket/images/Image5.png)

* 1.服务端welcoming socket 开始监听端口(负责监听客户端连接信息)
* 2.客户端client socket连接服务端指定端口(负责接收和发送服务端消息)
* 3.服务端welcoming socket 监听到客户端连接，创建connection socket。
(负责和客户端通信)


















































