---
layout:     post
title:      SSH登录远程服务器
subtitle:   上传和下载文件
date:       2018-05-20
author:     LQ
header-img: img/post/20180519/host-guest-ping/so-pg.jpg
catalog: true
tags:
    - ssh
---
# 前言
---
>`SSH` 为建立在应用层基础上的安全协议。`SSH` 是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。利用 `SSH` 协议可以有效防止远程管理过程中的信息泄露问题。

# 命令
---
#### 通过ssh连接Linux服务器
```
>>> ssh cg@server.rl-nju.com -p 65001
```

#### 上传文件到Linux服务器
```
>>> scp -P 65001 /home/rex/Downloads/testfile cg@server.rl-nju.com:/home/cg/L4T
```

#### 从Linux服务器下载文件
```
>>> scp -P 65001 cg@server.rl-nju.com:/home/cg/L4T/testfile /home/rex/Downloads/
```

