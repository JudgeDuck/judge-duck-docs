---
title: JudgeDuck-OS 的运行
---

# JudgeDuck-OS 的运行

本文将介绍如何在鸭子上运行 JudgeDuck-OS。

## TFTP 服务器的配置

下载 `tftp-server` 仓库：

```bash
$ git clone git@github.com:JudgeDuck/tftp-server.git
```

拷贝编译好的 JudgeDuck-OS 镜像：

```bash
$ cp JudgeDuck-OS/obj/jos-grub-* tftp-server/
```

启动 TFTP 服务器：

```bash
$ tmux
$ cd tftp-server
$ sudo python3 server.py
```

*启动 TFTP 服务器后，按下 `Ctrl-B`，再按 `D` 键，来退出 tmux 环境。* 

## DHCP 服务器的配置

安装 `isc-dhcp-server`：

```bash
$ sudo apt install isc-dhcp-server
```

编写 DHCP 服务器的配置 `/etc/dhcp/dhcpd.conf`，如下：

```
option domain-name "JudgeDuck";

allow bootp;
subnet 10.0.123.0 netmask 255.255.255.0 {
		range 10.0.123.100 10.0.123.199;
		option subnet-mask 255.255.255.0;
		option broadcast-address 10.0.123.255;

		class "pxeclients" {
				match if substring (option vendor-class-identifier, 0, 9) = "PXEClient";
				option tftp-server-name "10.0.123.2";
				option bootfile-name "/boot/grub/i386-pc/core.0";
		}

		class "normal" {
				match if substring (option vendor-class-identifier, 0, 9) != "PXEClient";
		}
### 此处插入鸭子的 DHCP 配置 ###
}
```

其中需在倒数第二行处插入鸭子的 DHCP 配置，其可通过 `cat JudgeDuck-OS/dhcp-config.txt` 获得。

*请根据在[软件配置](./software.md)中鸽子的网络配置来设置此处的 IP 地址、子网掩码等。*

重启 DHCP 服务器：

```bash
$ sudo service isc-dhcp-server restart
```

查看 DHCP 服务器的状态，确认其正常运行（显示 `active (running)`）：

```bash
$ service isc-dhcp-server status
```

## 启动鸭子

按下鸭子的电源，等待约半分钟。如在屏幕上看到评测鸭的 logo，即为启动成功。

完成启动后，可用 `ping` 命令来检测鸽子和鸭子之间的网络连通性：

```bash
$ ping 10.0.123.51
```

*此处的 IP 地址需根据 `JudgeDuck-OS/dhcp-config.txt` 中的内容进行修改。*
