```/etc/resolv.conf```经常会被各种系统进程覆盖，从而导致无法访问域名网站，这时应当设置该文件无法被写入。
通过修改以下文件达到永久修改上面文件的目的，这是ubuntu18.04的唯一有效方法：
```
rm /etc/resolv.conf
nano /etc/resolv.conf
# 写入 nameserver 114.114.114.114
chattr -e /etc/resolv.conf
chattr +i /etc/resolv.conf
nano /etc/resolv.conf
```

# 参考文章
1.    [Linux系列教程（十七）——Linux权限管理之文件系统系统属性chattr权限和sudo命令 - 云+社区 - 腾讯云 ](tencent.com)
2.    [Linux chattr命令 | 菜鸟教程 ](runoob.com)
