# systemd介绍
首先介绍systemd，Systemd(Systemd 入门教程：命令篇 - 阮一峰的网络日志 (ruanyifeng.com)) 是 Linux 系统工具，是一套命令，用来启动守护进程，它已成为大多数Linux发行版的标准配置。
# systemctl命令介绍
1. systemd 相关的绝大多数任务都是通过 systemctl 命令管理的。  
2. systemctl 命令有两大类功能：a,控制 systemd 系统 b.管理系统上运行的服务
# 对Unit file的解释
```
A unit file is ***a plain text ini-style file that encodes information about*** a service, a socket, a device, a mount point, an automount point, a swap file or partition, a start-up target, a watched file system path, a timer controlled and supervised by systemd(1), a resource management slice or a group of externally created processes. See systemd.syntax(7) for a general description of the syntax.
```
#参考文章
1.    [systemd.unit ](www.freedesktop.org)
2.    [12052018_systemd_6.pdf ](redhat.com)
3.    [linux systemctl 命令 - sparkdev - 博客园 ](cnblogs.com)
4.    [Systemd 入门教程：命令篇 - 阮一峰的网络日志 ](ruanyifeng.com)
