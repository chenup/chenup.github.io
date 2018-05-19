---
layout:     post
title:      host与guest实现互ping
subtitle:   针对虚拟机VirtualBox
date:       2018-05-19
author:     LQ
header-img: img/post/20180519/host-guest-ping/hgp-pg.jpg
catalog: true
tags:
    - ping
    - host
    - 虚拟机
    - guest
    - VirtualBox
---
# 前言
---
>本文的目标是实现 `host`系统 和运行在虚拟机（`VirtualBox`）上的 `guest`系统 可以互相 `ping` 通。`host` 是 **windows 10**，而 `guest` 是 **ubuntu 16.04**。

>`host` 要和 `guest` 处于**同一个子网**下。举例来说，我们将 `host` 的 **ip** 设置为 `192.168.1.118`， 而 `guest` 的 **ip** 设置为 `192.168.1.116`（这两个 **ip** 可以根据自己的需求改变）。 

# 步骤
---

#### Step 1： host（windows 10）设置

配置 `IPv4` 属性

- `ip`：**192.168.1.118**
- `netmask`：**255.255.255.0**
- `gateway`：**192.168.1.1**

![host ip](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-hi.png)

关闭防火墙

![close firewall](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-cf.png)

运行 `cmd` 并输入 `ipconfig` 查看配置结果

![cmd ipconfig](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-ci.png)

#### Step 2： 虚拟机（VirtualBox）设置

网卡1设置成**桥接**

![net bridge](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-nb.png)

#### Step 3： guest（ubuntu 16.04）设置

修改 `/etc/hosts` 文件

```
>>> sudo vim /etc/hosts
```

![vim hosts](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-vh.png)

修改 `/etc/network/interfaces` 文件

``` 
>>> sudo vim /etc/network/interfaces
```

![vim interfaces](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-vi.png)

修改 `/etc/resolv.conf` 文件

```
>>> sudo vim /etc/resolv.conf
```

![vim conf](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-vc.png)

重启网络服务

```
>>> sudo /etc/init.d/networking restart
```

关闭防火墙

```
>>> sudo ufw disable
```

重启（可选）

显示网络配置信息

```
>>> ifconfig -a
```

![ifconfig](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-if.png)

#### Step 4： 验证

`host ping guest`

```
>>> ping 192.168.1.116
```

![ping guest](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-pig.png)

`guest ping host`

```
>>> ping 192.168.1.118
```

![ping host](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180519/host-guest-ping/hgp-pih.png)

