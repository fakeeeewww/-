需要配置DHCP服务器才能自动推送IP、dns等信息
```
apt install isc-dhcp-server
```
```
rm /etc/dhcp/dhcpd.conf
nano /etc/dhcp/dhcpd.conf
写入以下内容：
ddns-update-style none;
default-lease-time 600;
max-lease-time 7200;
log-facility local7;

subnet 10.10.10.0 netmask 255.255.255.0 {  # 注意这个子网的前24位，应当和路由器是一致的，否则建立的子网中不包含路由器的IP，那一定是错误的
  range 10.10.10.100 10.10.10.200;
  option routers 10.10.10.1;               # 路由器的局域网IP，即软路由的LAN口IP
  option subnet-mask 255.255.255.0;
  option domain-name-servers 114.114.114.114;
}
```
```
systemctl restart isc-dhcp-server
systemctl status isc-dhcp-server
```
