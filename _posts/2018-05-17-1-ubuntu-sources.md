---
layout:     post
title:      ubuntu换源
subtitle:   针对 ubuntu 16.04
date:       2018-05-17
author:     LQ
header-img: img/post/20180517/ubuntu-sources/us-pg.jpg
catalog: true
tags:
    - ubuntu
    - 源
---
# 步骤
---

#### Step 1： 替换源文件内容（不放心可以先备份一下）

```
>>> sudo vim /etc/apt/sources.list
```

网易源：

```
deb http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse
```

效果如下：

！[replace sources](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/ubuntu-sources/us-rs.png)

#### Step 2： 更新源

```
>>> sudo apt-get update
```

- 更新成功

！[update success](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/ubuntu-sources/us-us.png)

- 更新失败（换新的源重试）

！[update fail](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/ubuntu-sources/us-uf.png)


