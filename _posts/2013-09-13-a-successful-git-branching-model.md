---
layout: post
title: 一种成功的Git分支模型
categories:
 - 最佳实践
tags:
 - Git
 - Gitflow
description: '一种成功的Git分支模型'
---

### 最佳实践

先说一点题外话，软件开发中有一个常见的词，叫做最佳实践（Best Practice），所谓最佳实践，是那些前辈先驱用自己的亲身经验，总结出的一套最优的方案，告诉后来者应该做什么和避免做什么。在软件开发中，遵循最佳实践，往往给人带来便利和效率。

### Gitflow

在我用过的源代码管理中，我认为Git是最棒的！虽然刚接触它时会有点难度。在使用Git的过程中，无意中发现了 [Gitflow][1] 这样个好工具，它是对 [A successful Git branching model][3] 博文中提到的分支哲学制作的一个工具，帮助我们更好的管理这种分支模型。

试用之后，立马有种相见恨晚的感觉！这种分支模型无疑是Git分支的最佳实践，值得我们好好理解，好好使用。

### Gitflow分支哲学

先上一张分支模型大图：

![a-successful-git-branching-model][5]

这种模型把Git分支分为五个分支：

1. master 主分支
2. develop 开发分支
3. feature 特性分支
4. release 发布分支
5. hotfix 热补丁分支

其中master和developer分支称为主要分支，它们永远存在，master分支永远在产品状态，developer分支上是最新开发的代码。其他的分支又称为支持性分支，一旦分支上的开发完成就会被删除。

### 使用场景

看看这种分支模式下的一些常见的使用场景：

1. 小功能修改
    1. 直接在develop上修改代码并提交
2. 开发新功能
    1. 基于develop分支新建feature分支
    2. 在feature分支上开发代码，提交
    3. 合并feature分支到develop分支
    4. 删除feature分支
3. 发布版本
    1. 基于develop分支新建release分支
    2. 可在release分支上进行小量修改
    3. 合并release分支到master和develop分支
    4. 在master分支上打Tag
    5. 删除release分支
4. 紧急修复
    1. 基于master分支创建hotfix分支
    2. 在hotfix分支上修改bug
    3. 合并hotfix分支到master和develop分支
    4. 在master分支上打Tag
    5. 删除hotfix分支

### 参考阅读

+ [Gitflow][1]
+ [Gitflow installation][2]
+ [A successful Git branching model][3]
+ [介绍一个成功的 Git 分支模型(译文)][4]

[1]: https://github.com/nvie/gitflow
[2]: https://github.com/nvie/gitflow/wiki/Installation
[3]: http://nvie.com/posts/a-successful-git-branching-model
[4]: http://www.oschina.net/translate/a-successful-git-branching-model

[5]: /uploads/2013-09-13/a-successful-git-branching-model.png
