---
title: 评测鸭在线的部署
---

# 评测鸭在线的部署

本文将介绍评测鸭在线的部署。

## 配置评测鸭在线所需环境

```bash
$ sudo pip3 install Django
$ sudo pip3 install markdown2
$ sudo apt install unzip
```

## 下载评测鸭在线

```bash
$ git clone git@github.com:JudgeDuck/judge-duck-service.git
$ cd judge-duck-service
```

## 初始化评测鸭在线

建立评测鸭在线所需的文件夹：

```bash
$ cd server
$ mkdir -p jd_data/temp/
$ mkdir -p jd_data/problems/
$ mkdir -p jd_data/code/
$ mkdir -p jd_data/metadata/
$ mkdir -p jd_data/result/
$ mkdir -p jd_data/pending/
$ mkdir -p jd_data/pending_rejudge/
$ mkdir -p jd_data/users/
$ mkdir -p jd_data/blogs/
$ mkdir -p jd_data/problem_zips/
```

初始化数据库：

```bash
$ sudo apt install sqlite3
$ sqlite3 jd.sqlite3 < jd-schema.sql
```

按照 `judge-duck-service/server/database-notes.md` 的要求，插入数据库版本信息：

```bash
$ sqlite3 jd.sqlite3 "insert into jd_meta values ('version', '20180822-1')"
```

*请再次检查 `database-notes.md`，以确定版本信息正确。*

初始化评测鸭在线：

```bash
$ python3 manage.py migrate
```

当此命令卡住时，按下 `Ctrl-C` 键，即可完成初始化。

## 配置评测鸽地址

```bash
$ echo "http://127.0.0.1:8100/" > pigeon-url.txt
```

## 启动评测鸭在线

```bash
$ tmux
$ python3 manage.py runserver 0.0.0.0:8000
```

恭喜！评测鸭在线已开始运行，地址是 `http://[鸽子的IP地址]:8000/`。
