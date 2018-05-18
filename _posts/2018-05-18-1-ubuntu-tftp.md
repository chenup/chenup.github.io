---
layout:     post
title:      NJU-OS 之u-boot阶段（一）
subtitle:   在ubuntu上安装tftp服务器
date:       2018-05-18
author:     LQ
header-img: img/post/20180518/ubuntu-tftp/ut-pg.jpg
catalog: true
tags:
    - u-boot
    - tftp
    - ubuntu
---
# 前言
---
>`TFTP`（Trivial File Transfer Protocol，简单文件传输协议）是 `TCP/IP` 协议族中的一个用来在客户机与服务器之间进行简单文件传输的协议，提供不复杂、开销不大的文件传输服务。

>`u-boot` 提供了 `tftp` 命令，使得内核镜像（比如 `Image`）通过网络的方式加载到 `RAM` 当中。 相比于烧写内核镜像到 `eMMC` ，然后从 `eMMC` 加载到 `RAM` 的过程，`tftp` 无疑更加简单，更适合于系统内核开发阶段的调试。

>本文将介绍如何在 `ubuntu 16.04` 上安装 **tftp 服务器**。

# 步骤
---

#### Step 1

下载并安装程序

- `tftp` 是客户端程序
- `tftpd` 是服务器程序
- `openbsd-inetd` 是 Telnet 配置

```
>>> sudo apt-get install tftp tftpd openbsd-inetd
```

#### Step 2

建立 **tftp 服务器** 目录
```
>>> cd /

>>> sudo mkdir tftpboot

>>> sudo chmod 777 tftpboot
```

#### Step 3

修改 **tftp 服务器** 配置
```
>>> sudo vim /etc/inetd.conf

# inetd.conf 文件里要填写的内容
>>> tftp dgram udp wait nobody /usr/sbin/tcpd /usr/sbin/in.tftpd /tftpboot
```

![vim conf](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180518/ubuntu-tftp/ut-vc.png)

#### Step 4

重新启动服务
```
>>> sudo /etc/init.d/openbsd-inetd restart

>>> sudo in.tftpd –l /tftpboot
```

#### Step 5

测试 **tftp 服务器**，在 `/tftpboot` 目录下面新建一个 `testfile` 文件
```
>>> cd /tftpboot

>>> touch testfile
```

![touch testfile](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180518/ubuntu-tftp/ut-tt.png)

在某一目录下通过 `tftp` 下载 `testfile`，比如 `~/Downloads` 目录
```
>>> cd ~/Downloads

>>> tftp 127.0.0.1

>>> tftp> get testfile
```

![download testfile](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180518/ubuntu-tftp/ut-dt.png)

下载成功则代表 **tftp 服务器** 安装成功