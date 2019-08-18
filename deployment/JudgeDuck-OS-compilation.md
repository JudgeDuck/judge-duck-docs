---
title: JudgeDuck-OS 的编译
---

# JudgeDuck-OS 的编译

本文将介绍 JudgeDuck-OS 的编译。

## 编译依赖库

下载 `judge-duck-libs` 仓库：

```bash
$ git clone git@github.com:JudgeDuck/judge-duck-libs.git
```

编译 libducknet：

```bash
$ cd judge-duck-libs/libducknet
$ make V=0
```

## 编译 JudgeDuck-OS

首先下载并进入 `JudgeDuck-OS` 仓库（需要与 `judge-duck-libs` 在同一层目录）：

```bash
$ git clone git@github.com:JudgeDuck/JudgeDuck-OS.git
$ cd JudgeDuck-OS
```

然后按照 `README-ducks.md` 的要求，将鸭子网卡的 MAC 地址写入 `ducks.txt`：

```bash
$ echo "52:54:10:12:34:56" > ducks.txt
```

*此处的 `52:54:10:12:34:56` 应更换为鸭子的网卡 MAC 地址。该地址可以从鸭子开机时 PXE 显示的信息中获得。*

再按照 `README-memory.md` 的要求，配置 JudgeDuck-OS 可使用的最大内存：

```bash
$ echo "#define MAX_SYSTEM_MEMORY 2097152" > mem-config.h
```

*`2097152` 表示 2GB（2097152KB）。*

修改 `build.py` 的前几行，填入鸽子的网络设置：

```python
PREFIX = "10.0.123."
MASK = "255.255.255.0"
PIGEON = "10.0.123.2"
```

*请根据在[软件配置](./software.md)中鸽子的网络配置进行设置。*

开始编译 JudgeDuck-OS：

```bash
$ make clean
$ python3 build.py
```

检查编译是否成功：

```bash
$ ls obj/jos-grub-*
```

如果存在 `jos-grub-<addr>`（`<addr>` 是一个 IP 地址），则 JudgeDuck-OS 编译成功。
