#目的：参考原文
`Source routing is an Internet Protocol mechanism that allows an IP packet to carry information, a list of addresses, that tells a router the path the packet must take.`
`This allows the source (the sending host) to specify the route, loosely or strictly, ignoring the routing tables of some or all of the routers. It can allow a user to redirect network traffic for malicious purposes. Therefore, source-based routing should be disabled.`
简而言之Source Routing 并不安全(详情参见文章2)，为了安全着想，咱们通过设置`sysctl`命令来disable the source routing。
#命令解析
>The `accept_source_route` option causes network interfaces to accept packets with the Strict Source Route (SSR) or Loose Source Routing (LSR) option set.输出下面的命令可以在SSR(Strict Source Route严格源路由)和LSR(Loose Source Route松散源路由)两种Source Route下丢弃包。避免由于Source Route而出现安全问题。
>`/sbin/sysctl -w net.ipv4.conf.all.accept_source_route=0`
>Disabling the forwarding of packets should also be done in conjunction with the above when possible。Disable 包转发应该同时disable ipv4和ipv6的包转发。
>`/sbin/sysctl -w net.ipv4.conf.all.forwarding=0`
>#`/sbin/sysctl -w net.ipv6.conf.all.forwarding=0`
>These commands disable forwarding of all multicast packets on all interfaces.
>`/sbin/sysctl -w net.ipv4.conf.all.mc_forwarding=0`
>`/sbin/sysctl -w net.ipv6.conf.all.mc_forwarding=0`
>These commands disable acceptance of all ICMP redirected packets on all interfaces:
>`/sbin/sysctl -w net.ipv4.conf.all.accept_redirects=0`
>`/sbin/sysctl -w net.ipv6.conf.all.accept_redirects=0`
>This command disables acceptance of secure ICMP redirected packets on all interfaces
>`/sbin/sysctl -w net.ipv4.conf.all.secure_redirects=0`
>This command disables sending of all IPv4 ICMP redirected packets on all interfaces:
>#`/sbin/sysctl -w net.ipv4.conf.all.send_redirects=0`

#参考文章
1.    2.2.10. Disable Source Routing Red Hat Enterprise Linux 6 | Red Hat Customer Portal
2.    What is Source Routing and Why is It a Security Concern? - Cyber Sophia
