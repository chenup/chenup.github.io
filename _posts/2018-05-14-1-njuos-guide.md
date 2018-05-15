---
layout:     post
title:      github协同开发指导
subtitle:   如何参与 NJU-OS 项目的开发
date:       2018-05-14
author:     LQ
header-img: img/post/20180514/git-os-guide/gog-pg.jpg
catalog: true
tags:
    - git
    - 协同开发
    - github
    - NJU-OS
---
# 前言
---
>很多项目开发都会采用 `git` 这一优秀的分布式版本管理工具进行项目版本管理，使用 `github` 开源平台作为代码仓库托管平台。由于 git 的使用非常灵活，在实践当中衍生了很多种不同的工作流程，不同的项目、不同的团队会有不同的协作方式。

>本文针对 [NJU-OS](https://github.com/NJU-OS) 项目提出一种 **git工作流**，便于开发者加入到该项目的开发当中。

# 必要知识
---

#### 仓库（Repository）

在项目的开始到结束，我们会有两种仓库。一种是源仓库（origin），一种是开发者仓库。

- **源仓库**

    在项目的开始，项目的发起者构建起一个项目的最原始的仓库，我们把它称为 `origin`，例如 [vtos-nju](https://github.com/NJU-OS/vtos-nju) 。
    
    源仓库的有两个作用：
    &nbsp;
    **1、汇总参与该项目的各个开发者的代码**
    &nbsp;
    **2、存放趋于稳定和可发布的代码**
    &nbsp;
    源仓库应该是受保护的，开发者不应该直接对其进行开发工作。只有项目管理者（通常是项目发起人）能对其进行较高权限的操作。
    &nbsp;
- **开发者仓库** 

    任何开发者都不会对源仓库进行直接的操作，源仓库建立以后，每个开发者需要做的事情就是把源仓库的“复制”一份，作为自己日常开发的仓库。这个复制，也就是github上面的 `fork`。

    每个开发者所 `fork` 的仓库是完全独立的，互不干扰，甚至与源仓库都无关。每个开发者仓库相当于一个源仓库实体的影像，开发者在这个影像中进行编码，提交到自己的仓库中，这样就可以轻易地实现团队成员之间的并行开发工作。而开发工作完成以后，开发者可以向源仓库发送 `pull request`，请求管理员把自己的代码合并到源仓库中，这样就实现了**分布式开发工作**和**集中式管理**。

#### 分支（Branch）

在我们的分支模型中，分支有两类：

- **永久性分支**

    `master branch`：主分支

    `develop branch`：开发分支


- **临时性分支**

    `feature branch`：功能分支

##### 永久性分支

永久性分支是寿命无限的分支，存在于整个项目的开始、开发、迭代、终止过程中。永久性分支只有两个: `master` 和 `develop` 。

###### master

主分支从项目一开始便存在，它用于存放经过测试，已经完全稳定代码；在项目开发以后的任何时刻当中，`master`存放的代码应该是可作为产品供用户使用的代码。所以，应该随时保持 `master`仓库代码的清洁和稳定，确保入库之前是通过完全测试和代码 `review` 的。`master` 分支是所有分支中最不活跃的，大概每个月或每两个月更新一次，每一次 `master` 更新的时候都应该用 git 打上 `tag` ，说明你的产品有新版本发布了。

###### develop

开发分支，一开始从 `master`分支中分离出来，用于开发者存放基本稳定代码。每个开发者的仓库相当于源仓库的一个镜像，每个开发者自己的仓库上也有 `master` 和 `develop` 。开发者把功能做好以后，是存放到自己的 `develop` 中，当测试完以后，可以向管理者发起一个 `pull request` ，请求把自己仓库的 `develop` 分支合并到源仓库的 `develop` 中。

所有开发者开发好的功能会在源仓库的 `develop` 分支中进行汇总，当 `develop` 中的代码经过不断的测试，已经逐渐趋于稳定了，接近产品目标了。这时候，我们就可以把 `develop` 分支合并到 `master` 分支中，发布一个新版本。

一个产品不断完善和发布的过程如下图所示：

![master and develop](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-mad.png)

**Note**：任何人都不应该向 `master` 直接进行无意义的合并、提交操作。正常情况下，`master` 只应该接受 `develop` 的合并，也就是说，`master` 所有代码更新应该源于合并 `develop` 的代码。

##### 临时性分支

临时性分支和永久性分支不同，临时性分支在开发过程中是一定会被删除的。所有临时性分支一般源于 `develop` ，最终也会合并到 `develop` 中。

###### feature

功能性分支，是用于开发项目的功能的分支，是开发者主要的战斗阵地。开发者在本地仓库从 `develop` 分支分出功能分支，在该分支上进行功能的开发，开发完成以后再合并到 `develop` 分支上，这时候功能性分支已经完成任务，可以删除。功能性分支的命名一般为`feature-*` ，`*` 为需要开发的功能的名称。

![develop and feature](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-daf.png)

**example**：假设我是一名 NJU-OS 的开发者，已经把源仓库 `fork` 了，并且 `clone` 到了本地。现在要开发出 NJU-OS 的 `debug` 功能，我在本地仓库中可以这样做：

**step 1**：切换到 `develop` 分支
```
>>> git checkout develop
```

**step 2**：分出一个功能性分支
```
>>> git checkout -b feature-debug
```

**step 3**：在功能性分支上进行开发工作，多次 `commit` ，并且测试成功
```
# 省略了对分支中文件的更改操作
>>> ...

# 提交更改
>>> git add .
>>> git commit -m "finish debug feature"

# 省略了测试操作
>>> ...
```

**step 4**：把做好的功能合并到 `develop` 中
```
# 回到develop分支
>>> git checkout develop

# 把做好的功能合并到develop中
>>> git merge --no-ff feature-debug

# 删除功能性分支
>>> git branch -d feature-debug

# 把develop提交到自己的远程仓库中
>>> git push origin develop
```

这样，就完成一次功能的开发和提交。

# 工作流（Workflow）
---
下面以 NJU-OS 项目里面的 u-boot-nju 为例，一步步操作上面所说的工作流程：

#### Step 1： 找到源仓库

[NJU-OS](https://github.com/NJU-OS/) 项目的管理员已经建立了一个源仓库 [NJU-OS/u-boot-nju](https://github.com/NJU-OS/u-boot-nju) ，并且也已经初始化了两个永久性分支 `master` 和 `develop` ，如图：

![origin repo](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-or.png)

#### Step 2： 开发者fork源仓库

找到源仓库以后，每个开发者就可以复制一份源仓库到自己的github账号中，然后作为自己开发所用的仓库。假设我是项目中的开发者，我就到 [NJU-OS/u-boot-nju](https://github.com/NJU-OS/u-boot-nju) 主页上去 `fork`:

![fork u-boot-nju](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-fu.png)

`fork`完以后，我就可以在我自己的仓库列表中看到一个和源仓库一模一样的仓库了：

![my u-boot-nju](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-mu.png)

#### Step 3： 开发者把自己的仓库clone到本地

我的操作环境是 ubuntu 16.04，当然 windows 和 mac 也可以。在 `clone` 之前需要在本机上配置 `git` ，请自行百度。

首先从开发者自己的仓库获取地址，如 `https://github.com/xxx/u-boot-nju.git`：

![clone u-boot-nju address](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-cua.png)

```
# 把远程仓库复制到本地
>>> git clone https://github.com/xxx/u-boot-nju.git

# 进入到本地仓库所在的目录中
>>> cd u-boot-nju/
```

![git clone](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-gc.png)

查看当前所在的分支，当前所在分支的前面用 `*` 标记

```
# 列出本地已经存在的分支，并且在当前分支的前面用"*"标记
>>> git branch
```

![git clone](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-gb.png)

#### Step 4： 构建功能分支进行开发

进入仓库后，按照前面所说的构建功能性分支的步骤，构建功能分支进行开发、合并，假设我现在要开发一个 `debug` 功能：

```
# 切换到 develop 分支
>>> git checkout develop

# 分出一个功能性分支，并切换到它
>>> git checkout -b feature-debug

# 查看当前分支
>>> git branch
```

![git checkout feature-debug](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-gcfd.png)

```
# 打开了调试功能
>>> vim include/common.h

# 提交更改
>>> git add .
>>> git commit -m "finish debug feature"
```

![git commit debug](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-gcd.png)

```
# 回到 develop 分支
>>> git checkout develop

# 把已经完成并确认正确的功能合并到 develop 中
>>> git merge --no-ff feature-debug

# 删除功能性分支
>>> git branch -d feature-debug

# 把 develop 分支提交到自己的远程仓库中
>>> git push origin develop
```

![git push develop](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-gpd.png)

在此过程之后，访问自己github的 u-boot-nju 主页的 `develop` 分支，你将看到修改的结果。

#### Step 5： 向管理员提交pull request

假设我已经完成了 `debug` 功能（当然，你还可能对自己的 `develop` 进行了多次合并，完成了多个功能），经过测试确认没有问题后，就可以请求管理员把自己仓库的 `develop` 分支合并到源仓库的 `develop` 分支中，这就是 `pull request` 。

点击 `Compare & pull request` 按钮：

![pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-pr.png)

点击 `Create pull request` 按钮，开发者就可以静静地等待管理员对你的提交的评审了：

![open pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-opr.png)

完成 `pull request` 的提交，到这里为止，开发者一个阶段的工作就结束了，恭喜：

![open pull request](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-opr.png)

#### Step 6： 管理员测试、合并

接下来就是管理员的操作了，管理员登陆github，处理开发者对源仓库发起的pull request。

以上，就是一个git & github协同工作流的基本步骤。

# 总结
---
送上一幅神图供大家参悟：

![git model](https://raw.githubusercontent.com/chenup/chenup.github.io/master/img/post/20180514/git-os-guide/gog-gm.png)

# 参考资料
---
- [使用git和github进行协同开发流程](https://segmentfault.com/a/1190000002413519)

