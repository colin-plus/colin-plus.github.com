---
layout: post
title: Repo 快速入门
categories:
 - 工具
tags:
  - repo
description: 'Repo 快速入门。'
---

### 基本工作流：

1. 下载代码。
2. 使用<code>repo start</code>创建新分支。
3. 编辑文件。
4. 使用<code>git add</code>等命令添加文件到Stage。
5. 使用<code>git commit</code>提交。
6. 使用<code>repo upload</code>上传代码到Gerrit。

### 下载代码

只要环境是OK的，执行如下命令即可：

    repo init -u ssh://gerrit帐户@host:port/smaple/manifest -b master
    repo sync

> 下载代码时，请替换自己的帐号和网址等信息。

### 创建分支

新下载的代码，没有任何分支，所以第一步就需要新建分支。

> 不创建分支，就不能提交代码到Gerrit。  
> 提交会出现 <code>"no branches ready for upload"</code>错误。

创建分支有两种方式：

+ 为所有工程都创建分支
+ 为特定的工程创建分支

代码如下：

    repo start zhanglubing --all # 在所有的项目上创建名为“zhanglubing”的分支 
    repo start zhanglubing Sample/Demo/ # 只为项目“Sample/Demo/”创建名为“zhanglubing”的分支
    repo list # 可查看所有项目列表

### 提交代码

使用喜欢的IDE打开工程，修改文件，然后提交代码：

    git add file1 file2
    git commit -m "cool feature"
    git add file3
    git commit -m "fix #1024"

上传前做一次代码同步，也可查看一下状态，确认即将上传的提交：

    repo overview # 查看即将上传的提交
    repo sync # 同步代码
    repo upload # 上传代码

一些简单的交互式回答之后，代码就到Gerrit上去了。

### 处理冲突

冲突不可避免，你总会遇到她（真是件忧伤的事）!  
修改代码前一定要先同步最新代码，这样可以避免大多数冲突。  

> 请保持这个同步代码的好习惯。

冲突一般在上传代码时，同步代码的步骤中出现，即<code>repo sync</code>时出现。  
处理方式：

    git commit -m "cool feature"
    repo sync # 在这一步出现冲突
    # 只有编辑冲突文件，自己解决冲突啦
    git add conflict-files
    git rebase --continue
    repo upload

### 常用命令

前面已经提到了诸多命令，但是都比较简单的使用，大多数命令都有参数可设置。

还有几个常用查看信息的命令，非常有帮助：

+ <code>repo info</code> 查看工程列表，分支信息等。
+ <code>repo list</code> 查看工程列表，工程所在目录。
+ <code>repo status</code> 查看所有工程的状态。
+ <code>repo overview</code> 和<code>repo info</code>差不多，精简显示即将上传的提交。

想了解更多的话，后面的相关阅读有详细讲解，使用<code>repo help command</code>查看帮助也是个好办法。

作为简单入门，到此为止。

### 7. 相关阅读


+ [Developing (Android官方文档)](http://source.android.com/source/developing.html)
+ [Repo command reference (Android官方文档)](http://source.android.com/source/using-repo.html)
+ [Android repo 魔法](http://www.worldhello.net/2010/08/31/1915.html)

