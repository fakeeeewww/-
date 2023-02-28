#定义

DHCP又名动态主机设置协议（英语：Dynamic Host Configuration Protocol，缩写：DHCP），又称动态主机组态协定，是一个用于**局域网内**IP网络的网络协议，位于OSI模型的应用层，默认客户端是68端口, 服务器是67端口，使用UDP协议工作，前身是BOOTP协议。DHCP服务器会从IP地址池中, 挑选一个IP地址 "出租" 给客户端一段时间, 时间到了就回收它们。主要有两个用途：
    1.    用于内部网或网络服务供应商自动分配IP地址给用户。
    2.    用于内部网管理员对所有电脑作中央管理。

#作用：
动态管理IP地址等参数(ip地址，子网掩码，默认网关，DNS指向)，给内部网络或网络服务供应商自动分配IP地址，给用户或者内部网络管理员作为对所有计算机作中央管理的手段。
#协议操作：
![](index_files/0.14800208608949436.png)
#DHCP工作原理
![](index_files/0.08145434995168242.png)
*    当DHCP客户端第一次登录网络的时候，也就是客户发现本机上没有任何 IP 数据设定，它会向网络发出一个 DHCP DISCOVER封包(广播包)。因为客户端还不知道自己属于哪一个网络，所以封包的来源地址会为 0.0.0.0 ，而目的地址则为 255.255.255.255 ，然后再附上DHCP discover 的信息，向网络进行广播。
*    当DHCP服务器监听到客户端发出的 DHCP discover 广播后，它会从那些还没有租出的地址范围内，选择最前面的空置 IP ，连同其它 TCP/IP 设定，响应给客户端一个 DHCP OFFER封包。
*    如果客户端收到网络上多台 DHCP 服务器的响应，只会挑选其中一个 DHCP offer 而已（通常是最先抵达的那个），并且会向网络发送一个DHCP request广播封包，告诉所有 DHCP 服务器它将指定接受哪一台服务器提供的 IP 地址。
*    当 DHCP 服务器接收到 客户端的 DHCP request 之后，会向客户端发出一个DHCPACK 响应，以确认 IP 租约的正式生效，也就结束了一个完整的 DHCP 工作过程。
对四步的分析：
*    Discover
    *    由于 DHCP Server 对于 client 来说是未知的，因此发现的操作的报文是广播的。
*    Offer
    *    所有支持 TCP/IP 的主机都会接受到此报文，然而只有 DHCP Server 会回应。Offer也需要是广播，因为 client 此时可能还没有 IP 地址。
*    Request
    *    Request也需要广播，通知其他 DHCP Server 自己做出的选择。
*    ACK
    *    仍需要广播，其他 DHCP Server 将收回之前提供的 IP 地址。
#DHCP分配IP地址机制：
*    自动分配方式（Automatic Allocation），DHCP服务器为主机指定一个永久性的IP地址，一旦DHCP客户端第一次成功从DHCP服务器端租用到IP地址后，就可以永久性的使用该地址。
*    动态分配方式（Dynamic Allocation），DHCP服务器给主机指定一个具有时间限制的IP地址，时间到期或主机明确表示放弃该地址时，该地址可以被其他主机使用。
*    手工分配方式（Manual Allocation），客户端的IP地址是由网络管理员指定的，DHCP服务器只是将指定的IP地址告诉客户端主机。**更改手机WLAN地址与电脑IP地址一致便是使用手工分配方式IP地址。**
*    三种地址分配方式中，只有动态分配可以重复使用客户端不再需要的地址。 
*    DHCP消息的格式是基于BOOTP（Bootstrap Protocol）消息格式的，这就要求设备具有BOOTP中继代理的功能，并能够与BOOTP客户端和DHCP服务器实现交互。BOOTP中继代理的功能，使得没有必要在每个物理网络都部署一个DHCP服务器。RFC 951和RFC 1542对BOOTP协议进行了详细描述。
#应用
1.    Windows：
2.    Android：WLAN中修改wifi配置。
#参考文章
[dhcp 的应用【图文】_刘恒友_51CTO博客](https://blog.51cto.com/liuhengyou/1275831)
[DHCP_百度百科 (baidu.com)](https://baike.baidu.com/item/DHCP/218195)
https://zh.wikipedia.org/zh-hans/动态主机设置协议
[【TCP/IP详解 卷一：协议】第六章：DHCP 和自动配置 - 畅畅1 - 博客园 (cnblogs.com)](https://www.cnblogs.com/ZCplayground/p/7594792.html)
