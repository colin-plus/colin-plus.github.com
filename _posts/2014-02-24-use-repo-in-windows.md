---
layout: post
title: 在Windows下使用repo
categories:
 - Android
tags:
  - Windows
  - repo
description: '在Windows下使用repo。'
---

使用repo，需要Python、Git、SSH等环境。使用Cygwin可以很好的解决这些问题。

### 下载Cygwin

官方网站：[http://www.cygwin.com/](http://www.cygwin.com/)

直接下载：

+ 32bit: [http://cygwin.com/setup-x86.exe](http://cygwin.com/setup-x86.exe)
+ 64bit: [http://cygwin.com/setup-x86_64.exe](http://cygwin.com/setup-x86_64.exe)

### 安装Cygwin

1. 双击运行  
![][1]  
2. 安装类型，第一次安装必须选择"Install from Internet"  
![][2]  
3. 安装目录  
![][3]  
4. 选择本地包目录  
![][4]  
5. 选择连接类型  
![][5]  
6. 选择下载站点，根据自己的网络状况选吧  
![][6]  
7. 选择安装包，选择安装包时可搜索，快速定位  
![][7]  
这里必须选择的安装的包为：
    + Net -> curl, openssh
    + Devel -> git, git-completion, git-gui, gitk
    + Libs -> libreadline6,libiconv2
    + Editors -> vim
    + Python -> python
8. 以后全部选择"下一步"即可，略过截图。  
其中下载过程取决于网络情况，请耐心等待。  
若发现缺少安装包，可以再次执行安装步骤，选择缺少的安装包安装即可。

### 修改用户名

打开Cygwin Terminal，显示的用户名可能是中文的，就需要修改。  
若用户名不是中文的，请略过该步骤。

> 为什么需要修改用户名？  
> 因为repo的工作目录要求是非中文的。

修改方式：

1. 打开C:\cygwin\etc\password，替换所有中文用户名为英文用户名
2. 修改C:\cygwin\home目录下的"用户Home文件夹"名称为对应英文名称

### 下载代码

到这一步基本成功了，你可以和使用Linux一样执行命令，比如：

+ 生成ssh的key，添加到Gerrit
+ Git已经安装，只需安装repo
+ 使用repo下载代码
+ 提交并上传代码

[1]: /uploads/2014-02-24/1.png
[2]: /uploads/2014-02-24/2.png
[3]: /uploads/2014-02-24/3.png
[4]: /uploads/2014-02-24/4.png
[5]: /uploads/2014-02-24/5.png
[6]: /uploads/2014-02-24/6.png
[7]: /uploads/2014-02-24/7.png