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

进入自己的 doc-nju 仓库，选择 `develop` 分支，点击 `new pull request`
![new pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-npr.png)

#### Step 2

选择仓库和分支

- `base fork` -> 选择自己的仓库（chenup/doc-nju）
- `base` -> 选择自己仓库的分支（develop）
- `head fork` -> 选择源仓库（NJU-OS/doc-nju）
- `compare` -> 选择源仓库的分支（develop）

点击 `Create pull request`
![create pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-cpr.png)

#### Step 3
点击 `Merge pull request` ，开始同步源仓库的 `develop` 分支
![merge pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-mpr.png)

同步成功
![merge success](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180517/upstream-repo/ur-ms.png)

# 第二种： git 命令操作
---

#### 仓库（Repository）

在项目的开始到结束，我们会有两种仓库。一种是源仓库（origin），一种是开发者仓库。

- **源仓库**

    在项目的开始，项目的发起者构建起一个项目的最原始的仓库，我们把它称为 `origin`，例如 [u-boot-nju](https://github.com/NJU-OS/u-boot-nju) 。
    
    源仓库有两个作用：

    **1、汇总参与该项目的各个开发者的代码**

    **2、存放趋于稳定和可发布的代码**

    源仓库应该是**受保护**的，开发者不应该直接对其进行开发工作。只有项目管理者能对其进行较高权限的操作。
    &nbsp;

- **开发者仓库** 

    任何开发者都不会对源仓库进行直接的操作，源仓库建立以后，每个开发者需要做的事情就是把源仓库“复制”一份，作为自己日常开发的仓库。这个复制，也就是github上面的 `fork` 操作。

    每个开发者所 `fork` 的仓库是完全独立的，互不干扰的，甚至与源仓库都无关。每个开发者仓库相当于一个源仓库实体的影像，开发者在这个影像中进行编码，提交到自己的仓库中，这样就可以轻易地实现团队成员之间的并行开发工作。而开发工作完成以后，开发者可以向源仓库发送 `pull request`，请求管理员把自己的代码合并到源仓库中，这样就实现了**分布式开发**和**集中式管理**。

#### 分支（Branch）


# 参考资料
---
- [github上fork了别人的项目后，再同步更新别人的提交](https://blog.csdn.net/qq1332479771/article/details/56087333)

