1.配置iptables是为了配置防火墙.不要使用iptables-persistent，这个至少在18.04上是不起作用的
```
nano start_nat.sh
```
2.添加以下内容
```
#!/bin/sh
iptables -t nat -A POSTROUTING -j MASQUERADE#这里的NAT: POSTROUTING修改的是源IP
```
```
chmod +x start_nat.sh # 这句非常重要，否则systemctl无法执行
```
3.查看start_nat.sh的绝对路径：
```
pwd|awk '{print $1"/start_nat.sh"}'
nano /lib/systemd/system/start_nat.service
```
4.添加以下内容
```
[Unit]
Description=Start NAT

[Service]
Type=simple
ExecStart=/root/start_nat.sh
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```
```
systemctl daemon-reload
systemctl enable start_nat
systemctl start start_nat
systemctl status start_nat
```
5.通过systemctl status start_nat是否含SUCCESS来判断是否执行成功。
且注意Active的执行时间。
# 参考文章:[Kali 防火墙配置【图文】_E书吧_51CTO博客    ](https://blog.51cto.com/itschool/1914803)
