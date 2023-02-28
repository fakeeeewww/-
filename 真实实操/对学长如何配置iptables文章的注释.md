# 解释
1. iptables -t nat -A POSTROUTING -j MASQUERADE#这里的NAT: POSTROUTING修改的是源IP`
1.  -t, --table table 对指定的表 table 进行操作， table 必须是 raw， nat，filter，mangle 中的一个。如果不指定此选项，默认的是 filter 表。
2.  -A, --append chain rule-specification 在指定链 chain 的末尾插入指定的规则，也就是说，这条规则会被放到最后，最后才会被执行。规则是由后面的匹配来指定。这里指定POSTROUTING。证明这里是指定iptables的**POSTROUTING链**，对源IP继续修改。
    3.    -j, --jump target <指定目标> ：即满足某条件时该执行什么样的动作。target 可以是内置的目标，比如 ACCEPT，也可以是用户自定义的链。这里的MASQUERADE(Linux防火墙 (maodanp.github.io))，地址伪装，在iptables中有着和SNAT相近的效果，但也有一些区别。使用SNAT的时候，出口ip的地址范围可以是一个，也可以是多个。***MASQUERADE作用是，从服务器的网卡上，自动获取当前ip地址来做NAT，就不用手动指定转换的目的IP了，实现了动态的SNAT***。
2.    `chmod +x start_nat.sh`
    1.    这一步的意思就是给**start_nat.sh**权限（(19条消息) linux下chmod +x的意思？为什么要进行chmod +x_yunlive的博客-CSDN博客）。LINUX下不同的文件类型有不同的颜色，这里。
    
     ```
    蓝色表示目录;
    绿色表示可执行文件，可执行的程序;
    红色表示压缩文件或包文件;
    浅蓝色表示链接文件;
    灰色表示其它文件;
    ```
3.    `  pwd|awk '{print $1"/start_nat.sh"}'  `
    1.    目的是打印出咱们要找的start_nat.sh文件的路径。
4.  ![image](https://user-images.githubusercontent.com/74806701/221848746-d830bbe0-d29d-4c57-9a7c-fa182bf09f44.png)


5.      `systemctl daemon-reload`
        `systemctl enable start_nat`
        `systemctl start start_nat`
        `systemctl status start_nat`
6.    自己写的总结性文章：关于Linux上的systemctl命令.md
    1.     `systemctl daemon-reload`：重新加载咱们刚刚修改的unit file(单元文件)，这里的单元文件指的上面咱们修改的start_nat.service这个service文件。
    2.    `systemctl enable start_nat`：根据`systemctl enable service`这个命令我们可知，这句命令的意思是Enable a service to start on boot(允许该服务开机自启)。
    3.    `systemctl start start_nat`：根据`systemctl start start_nat`这个命令可知，这句命令的意思是Start a service(开启服务)。
    4.    `systemctl status start_nat`：根据`systemctl status service`这个命令可知，这句命令的意思是See if service is running/enabled(查看命令是否运行)。




# 参考文章
1.    [iptables 命令，Linux iptables 命令详解：Linux上常用的防火墙软件 - Linux 命令搜索引擎 ](wangchujiang.com)
2.    [Linux防火墙 ](maodanp.github.io)
3.    [(19条消息) linux下chmod +x的意思？为什么要进行chmod +x_yunlive的博客-CSDN博客](https://blog.csdn.net/u012106306/article/details/80436911)
4.    [12052018_systemd_6.pdf (redhat.com) (***systemctl***命令解析)](https://access.redhat.com/sites/default/files/attachments/12052018_systemd_6.pdf)

