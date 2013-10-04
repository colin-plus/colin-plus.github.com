---
layout: post
title: Mac上如何更新Git
categories: 
 - 工具
tags:
 - Git
description: 'Mac上如何更新Git'
---

Mac自带安装了Git，但版本相对较低，比如我这里才1.7。{% gist 6821700 old-git.sh %}
目前Git版本已经是1.8.3了，简单几步，替换系统默认的Git，安装最新版的Git：

1. 删除老版本的git。建议采用备份的方式保留。{% gist 6821700 backup-git.sh %}
2. 下载[最新版的Git](http://code.google.com/p/git-osx-installer/downloads/list)，正常安装即可。
3. 安装完成后，输入git --version，发现git已是最新版了。{% gist 6821700 latest-git.sh %}
4. 后续升级重新下载最新版的安装即可。