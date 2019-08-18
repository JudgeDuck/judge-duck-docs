---
title: 评测依赖库的配置
---

# 评测依赖库的配置

本文将介绍评测依赖库的配置。这些库是编译和运行被测程序所必需的。

## 编译 libjudgeduck

```bash
$ cd judge-duck-libs/libjudgeduck
$ make V=0
```

## 编译 libtaskduck

```bash
$ cd judge-duck-libs/libtaskduck
$ make V=0
```

## 编译和配置 libpigeon

```bash
$ cd judge-duck-libs/libpigeon
$ make
```

请按照 `judge-duck-libs/libpigeon/readme.md` 的要求来配置 libpigeon。
或者可以跳过此步骤（可能存在安全风险），方法如下：

```bash
$ echo "+" > judge-duck-libs/libpigeon/config.txt
```

## 编译 libc-duck

下载 `libc-duck` 仓库：

```bash
$ git clone git@github.com:JudgeDuck/libc-duck.git
```

按照仓库中 `BUILD-duck.md` 的要求进行编译：

```bash
$ cd libc-duck
$ ./configure CFLAGS='-m32 -O2 -U_FORTIFY_SOURCE' CXXFLAGS='-m32 -O2 -U_FORTIFY_SOURCE' LDFLAGS=-m32 --disable-shared duck
$ make
```
## 编译 judge-duck-tools

安装 Qt5：

```bash
$ sudo apt install qt5-default
```

下载并编译 `judge-duck-tools`：

```bash
$ git clone git@github.com:JudgeDuck/judge-duck-tools.git
$ cd judge-duck-tools/compile
$ qmake && make
$ cd ../run
$ qmake && make
```
