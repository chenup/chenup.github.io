---
layout:     post
title:      参与 NJU-OS 项目的开发（二）
subtitle:   fork源仓库后，同步源仓库的更新
date:       2018-05-17
author:     LQ
header-img: img/post/20180517/upstream-repo/ur-pg.jpg
catalog: true
tags:
    - git
    - upstream
    - 同步更新
    - github
    - fork
    - 源仓库
---
# 前言
---
>在 `github` 上 `fork` 源仓库之后，如果**源仓库**的某个分支出现了新的改动，那么开发者该如何将**自己仓库**的分支同步到**源仓库**的分支，有两种方法可供使用。

>以 doc-nju 为例，实现将 [chenup/doc-nju](https://github.com/chenup/doc-nju) 的 `develop` 分支**同步**到 [NJU-OS/doc-nju](https://github.com/NJU-OS/doc-nju) 的 `develop` 分支。

# 第一种： 在 github 主页上进行操作
---

#### Step 1

进入自己的 doc-nju 仓库，选择 `develop` 分支，点击 `New pull request`
![new pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-npr.png)

#### Step 2

选择仓库和分支

- `base fork`：选择自己的仓库（chenup/doc-nju）
- `base`：选择自己仓库的分支（develop）
- `head fork`：选择源仓库（NJU-OS/doc-nju）
- `compare`：选择源仓库的分支（develop）

点击 `Create pull request`
![create pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-cpr.png)

#### Step 3
点击 `Merge pull request` ，开始同步源仓库（NJU-OS/doc-nju）的 `develop` 分支
![merge pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-mpr.png)

同步成功
![merge success](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-ms.png)

#### Step 4
```
# 在本地仓库更新并合并自己远程仓库的代码
>>> git pull origin develop
```

![pull origin](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-puo.png)

# 第二种： git 命令操作
---
#### Step 1
```
# 查看远程仓库信息
>>> git remote -v

# 添加上游仓库 NJU-OS/doc-nju
>>> git remote add upstream https://github.com/NJU-OS/doc-nju.git

# 查看远程仓库信息
>>> git remote -v
```

![add upstream](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-au.png)

#### Step 2
```
# 切换 develop 分支
>>> git checkout develop

# 把上游仓库新的更新取回到本地，但是不合并
>>> git fetch upstream

# 把上游仓库的 develop 分支合并到本地的 develop 分支
>>> git merge upstream/develop
```

![merge upstream](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-mu.png)

#### Step 3
```
# 向自己的远程仓库推送同步源仓库的代码
>>> git push origin develop
```

![push orign](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-po.png)

# 注意
1. 上游仓库和远程仓库一般不同，上游仓库一般是源仓库。
2. 虽然本文是以 develop 分支为例，但是一般和源仓库同步的分支都是 `master` 分支，`master` 分支是最稳定的分支。

# 参考资料
---
- [github上fork了别人的项目后，再同步更新别人的提交](https://blog.csdn.net/qq1332479771/article/details/56087333)

