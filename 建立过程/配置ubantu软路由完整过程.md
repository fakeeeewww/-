# 参考文献：
1. https://www.networkreverse.com/2020/06/how-to-build-linux-router-with-ubuntu.html
2. https://www.huaweicloud.com/articles/942c47777ba123e75aef27e595e29b12.html
```
ip add
```
查看网卡，记下wan口与lan口的网卡名。
为路由器1(ubuntu)配置ip和静态路由。
```
nano /etc/netplan/00-installer-config.yaml
````
填写内容如下，注意空格符：
```
network:
  ethernets:
    ens33:
      dhcp4: true
    ens38:
      addresses:
        - 10.10.10.1/24
  version: 2
```
```
netplan apply
Make sure all the configuration have applied
ip addr
Enable Packet forwarding for IPv4
nano /etc/sysctl.conf
# Find and uncomment 
net.ipv4.ip_forward=1 
sysctl -p
```

[永久配置iptables的方法](https://github.com/fakeeeewww/virtual-router/blob/main/%E5%BB%BA%E7%AB%8B%E8%BF%87%E7%A8%8B/%E6%B0%B8%E4%B9%85%E9%85%8D%E7%BD%AEiptables.md)
[永久配置DNS]
[永久配置iptabls方法](https://github.com/fakeeeewww/virtual-router/blob/main/%E5%BB%BA%E7%AB%8B%E8%BF%87%E7%A8%8B/%E6%B0%B8%E4%B9%85%E9%85%8D%E7%BD%AEiptables.md)

注意DNS修改为
```
114.114.114.114
```
配置dhcp服务器

到此为止，便可以将lan口连接无线路由器wan口，实现无线路由器联网了。
