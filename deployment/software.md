---
title: 软件配置
---

# 软件配置

本文将介绍“鸽子”和“鸭子”的软件配置。

## 鸽子

鸽子使用 Ubuntu 作为其操作系统，版本为 Ubuntu 18.04 LTS。

在安装后，请配置互联网（Internet）连接，并使用 `apt install` 安装必要的软件：

```bash
$ sudo apt update
$ sudo apt install openssh-server tmux vim git python3 python3-pip gcc-8 g++-8 gcc-8-multilib g++-8-multilib unzip qemu-system-x86
```

安装完成后，请配置 SSH 密钥：

```bash
$ ssh-keygen -t rsa -b 4096
```

然后配置 GCC，设置 `gcc-8` 为默认 GCC：

```bash
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 100 --slave /usr/bin/g++ g++ /usr/bin/g++-8
$ sudo update-alternatives --config gcc
```

最后配置连接鸽子和交换机的千兆网络：

* IP 地址：`10.0.123.2`
* 子网掩码：`255.255.255.0`
* 默认网关：无
* DNS 服务器：无

*IP 地址中的 `123` 可替换为任意 0 到 255 之间的数字。另外，使用任何局域网（LAN）地址都是可以的。*

## 鸭子

鸭子运行 JudgeDuck-OS，其通过网络启动。因此，需要进入 BIOS 调整以下设置：

* CPU：关闭 Hyper-threading（如有），设置 Active Processor Cores 为 2
* 启动：设置默认通过网络（PXE）启动

完成 BIOS 设置后，关闭鸭子的电源。
