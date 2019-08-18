---
title: 评测鸽服务的部署
---

# 评测鸽服务的部署

本文将介绍评测鸽服务（`judge-pigeon-service`）的部署。

## 配置评测鸽服务所需环境

```bash
$ sudo pip3 install Django
$ sudo pip3 install markdown2
$ sudo apt install unzip
```

## 下载和初始化评测鸽服务

下载评测鸽服务：

```bash
$ git clone git@github.com:JudgeDuck/judge-pigeon-service.git
$ cd judge-pigeon-service
```

初始化评测鸽服务：

```bash
$ mkdir jp_data
$ mkdir jp_data/problems
$ mkdir jp_data/files
$ mkdir jp_data/tasks
$ python3 manage.py migrate
```

当最后一个命令卡住时，按下 `Ctrl-C` 键，即可完成初始化。

## 运行评测鸽服务

```bash
$ tmux
$ python3 manage.py runserver 0.0.0.0:8100
```

至此，评测鸽服务已在鸽子上运行，端口为 `8100`。
