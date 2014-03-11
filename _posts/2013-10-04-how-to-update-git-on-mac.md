---
layout: post
title: Mac上如何更新Git
categories: 
 - 工具
tags:
 - Git
description: 'Mac上如何更新Git'
---

Mac自带安装了Git，但版本相对较低，比如我这里才1.7。

    $ git --version
    git version 1.7.12.4 (Apple Git-37)

目前Git版本已经是1.8.3了，简单几步，替换系统默认的Git，安装最新版的Git。

删除老版本的git，不过还是建议采取备份的方式保留。

    $ cd /usr/bin  
    $ sudo mkdir old-git-backup  
    $ sudo mv git* old-git-backup  

下载[最新版的Git](http://code.google.com/p/git-osx-installer/downloads/list)，正常安装即可。
安装完成后，输入git --version，发现git已是最新版了。

    $ git --version  
    git version 1.8.3.2  

后续升级重新下载最新版的安装即可。