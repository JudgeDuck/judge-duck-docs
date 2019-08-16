---
title: 硬件配置
---

# 硬件配置

一个完整的评测鸭部署包括至少两台**物理**机器：一台“鸽子”（运行 Linux，对外提供服务）和一台“鸭子”（运行 JudgeDuck-OS）。
这两台机器通过以太网连接，因此通常情况下还需相应的网络设备。

## 鸽子

鸽子对硬件配置没有硬性要求。其中：

* CPU：兼容 x86-64 指令集即可
* 内存：至少 4GB，建议 8GB
* 硬盘：建议至少 120GB，建议使用 SSD
* 网卡：至少两张以太网卡，其中至少一张网卡支持千兆以太网（GbE）

## 鸭子

鸭子对硬件配置有要求，并非任何硬件都能运行 JudgeDuck-OS。

以下是一种已经验证能运行 JudgeDuck-OS 的硬件配置：

* CPU：Intel® Core™ i3-4130 Processor @ 3.40 GHz
* 内存：4GB DDR3-1600，型号为 KVR16N11S8/4-SP
* 主板：任何兼容上述 CPU 和内存的主板
* 硬盘：无硬盘
* 网卡：Intel® 82574L Gigabit Ethernet Controller

以下是另一种已经验证能运行 JudgeDuck-OS 的硬件配置：

* CPU：Intel® Core™ i3-8100 Processor @ 3.60 GHz
* 内存：2 x 4GB DDR4-2400，型号为 KVR24N17S8/4
* 主板：ASRock H310M-ITX/ac
* 硬盘：无硬盘
* 网卡：Intel® 82574L Gigabit Ethernet Controller

## 网络设备

评测鸭部署在独立的局域网内，需要以下的网络设备：

* 千兆以太网交换机（型号没有要求）一台
* 超五类（CAT5e）或六类（CAT6）网线若干

在完成硬件配置后，将鸭子的千兆网卡，和鸽子的其中一张千兆网卡，分别使用网线与交换机连接，然后将鸽子的另一张网卡与互联网（Internet）连接，再进行后续部署步骤。
