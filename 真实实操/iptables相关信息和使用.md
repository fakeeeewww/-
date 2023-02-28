#iptables相关概念
1.    按照惯例先贴上wiki对它的解释。
![image](https://user-images.githubusercontent.com/74806701/221851374-8e2d6039-72b0-4b1f-93fc-b6bcc21958f2.png)

    1.    iptables命令 是Linux上常用的***防火墙***软件，是netfilter项目的一部分。
    2.    iptables、ip6tables等都使用Xtables框架。存在“表（tables）”、“链（chain）”和“规则（rules）”三个层面。
    3.    每个**“表”**指的是不同类型的数据包处理流程，如filter表表示进行数据包过滤，而nat表针对连接进行地址转换操作。每个表中又可以存在多个“链”，系统按照预订的规则将数据包通过某个内建链，例如将从本机发出的数据通过OUTPUT链。**笔者的话：联系防火墙的知识总结：iptables是一个防火墙软件，防火墙软件按照工作方式分为包过滤型和代理型防火墙，而iptables就是典型的包过滤型防火墙，不同的'表'用于不同的操作，至于‘链’本质上就是它自己设置的过滤规则。就像一个公司保安，负责看大门，'表'上写着它要去那个部门工作，'链'就是一个名单，默认是一个白名单，上面是允许进入的人员名单，也可以将其设置为黑名单，禁止名单上的人员进入。**
2.    Iptables服务不是真正的防火墙，只是用来定义防火墙规则功能的"防火墙管理工具"，将定义好的规则交由内核中的netfilter即网络过滤器来读取，从而真正实现防火墙功能。
3.    iptables抵挡封包的方式：
    1.    拒绝让 Internet 的封包进入 Linux 主机的某些 port。
    2.    拒绝让某些来源 IP 的封包进入。
    3.     拒绝让带有某些特殊标志( flag )的封包进入。
    4.     分析硬件地址(MAC)来提供服务。
4.    iptables命令中设置数据过滤或处理数据包的策略叫做规则，将多个规则合成一个链，叫规则链。规则链则依据处理数据包的位置不同分类：
    1.    PREROUTING: 在进行路由判断之前所要进行的规则(DNAT/REDIRECT)
    2.    INPUT:处理入站的数据包。
    3.    OUTPUT:处理出站的数据包。
    4.    FORWARD:处理转发的数据包。
    5.    POSTROUTING: 在进行路由判断之后所要进行的规则(SNAT/MASQUERADE)。
    6.    规则表的先后顺序:raw→mangle→nat→filter。

#iptables在做网络地址转换(NAT)上的作用
1.    POSTROUTING修改的是源IP，PREROUTING修改的是目的IP。
用一句话来总结：**linux主机通过iptables的NAT tablespoon内的Postrouting链将数据包表头的来源伪装成linux的Public IP，而反过来就是通过PREROUTING链将数据包表头的来源伪装成Linux的Public IP。**
2.    具体的流程：当客户端192.168.1.100这台主机要联机到 http://tw.yahoo.com时，它的数据包表头会如何变化：
NAT的简单流程_nat iptables
    1.    客户端所发出的数据包表头中，来源是192.168.1.100，然后传送到NAT这台主机。
    2.    NAT这台主机的内部接口（192.168.1.2）接收到这个数据包后，会主动分析表头数据，
    因为表头数据显示数目的并非linux本机，所以开始经过路由分析，将此数据包转到
    可以连接到Internet的Public IP处。
    3.    由于Private IP与Public IP不能互通，所以linux主机通过iptables的NAT tablespoon内的       Postrouting链将数据包表头的来源伪装成linux的Public IP，并且将两个不同来源                (192,168.1.100及Public IP）的数据包对应写入暂存内存中，然后将此数据包传送出去在此过程中Internet上看到的这个数据包时，都只会知道这个数据包来自Public IP，而不知道其实来自内部，现在我们来看下回传数据包：
        1.    在Internet上的主机接到这个数据包时，会将响应数据传送给那个Public IP的主机
        2.    当linux NAT主机收到来自Internet的响应数据包后，会分析该数据包的序号，并比对刚刚记录到内存中的数据，由于发现该数据包为后端主机之前传送出去的，因此在NAT Prerouting链中，会将目标IP修改成为后端主机，亦即那台192.168.1.100，然后发现目标已经不是本机（Public IP），所以开始通过路由分析数据包流向。
        3.    数据包会传送到192.168.1.2这个内部接口，然后再传到最终目标192.168.1.100机器上去。

#参考文章：
1.    [(19条消息) IPtables中SNAT、DNAT和MASQUERADE的含义_jk110333的专栏-CSDN博客_masquerade](https://blog.csdn.net/jk110333/article/details/8229828)
2.    [iptables - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/Iptables)
3.    防火墙和iptables - 骏马金龙 - 博客园 (cnblogs.com)
4.    Linux iptables用法与NAT - 风住 - 博客园 (cnblogs.com)
5.    (19条消息) IPtables中SNAT、DNAT和MASQUERADE的含义_jk110333的专栏-CSDN博客_masquerade
6.    iptables 命令，Linux iptables 命令详解：Linux上常用的防火墙软件 - Linux 命令搜索引擎 (wangchujiang.com)
    
