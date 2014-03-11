---
layout: post
title: 使用Ant构建Android应用
categories:
 - Android
tags:
  - Ant
  - 自动化
description: '使用Ant构建Android应用。'
---

> 古人云，“工欲善其事，必先利其器”，这对于软件开发而言是再合适不过了。软件项目的自动化构建工具的好处不仅在于高效省时、任劳任怨，而且还可以保证结果的连续性和一致性。

我相信做Java开的，没有听说过[Ant][1]的人，简直比踢足球的不知道贝克汉姆的还少。  
Ant是老一辈的构建工具了，如今有更多的出现，比如[Maven][2]、[Gradle][3]等。  
但Android采用了比较保守的做法，Android SDK默认的构建工具就是Ant。  

下面来看看我们该如何使用：

## 准备工作

+ 搭建Android开发环境
+ 安装Ant
+ 使用Git管理源代码

## 初试牛刀

创建项目，在终端切换到项目根目录。执行如下命令：

    $ android update project -p .

> 若是执行失败，一般来说是需要增加--target参数，具体请参考帮助：  
> $ android -h update project

执行成功后，项目下自动增加build.xml等文件，就可以使用Ant来完成编译、打包等工作了。  
试如下命令：

    $ ant help
    $ ant release

构建完成后，生成的apk位于bin目录下。

通过简单几步，就搞定了Ant构建Android应用了，是不是想立刻把build.xml提交到版本库里去了？

> 你应该这样做，立刻！  
> 请注意排除local.properties文件，你的小伙伴可以用同样的命令生成该文件。

## 增加构建版本

我们总是有自己的需求，Android采用Ant的时候，已经考虑到了，给了我们自由。  
一个常见的需求是：构建apk的时候，需要增加构建信息，即构建时间和git最后提交sha1值。

> 需要在构建前修改"AndroidManifest.xml"文件，  
> 比如将"versionCode"修改为"20140213"，将"versionName"修改为"build-2c49340"。

接下来看如何使用Ant来完成这个去修，并把它当作一个小小的使用进阶。

打开项目项目根目录下的build.xml文件，增加如下内容：

    <target name="-pre-build">
        <!-- 构建时间 -->
        <tstamp>
            <format property="build.time" pattern="yyyyMMdd"/>
        </tstamp>
        <!-- 最后提交的SHA1 -->
        <exec executable="git" outputproperty="last.commit">
            <arg value="log"/>
            <arg value="-1"/>
            <arg value="--format=%h"/>
        </exec>
        <!-- versionCode -->
        <replaceregexp file="AndroidManifest.xml"
            match="android:versionCode=&quot;\d*&quot;"
            replace="android:versionCode=&quot;${build.time}&quot;"/>
        <!-- versionName -->
        <replaceregexp file="AndroidManifest.xml"
            match="android:versionName=&quot;.*&quot;"
            replace="android:versionName=&quot;build-${last.commit}&quot;"/>
    </target>

重写了${sdk.dir}/tools/ant/build.xml里定义的钩子任务，增加了构建信息。  
当再次打包apk，你就会发现，新生成的apk的版本号有所不同啦！

## Enjoy

下一篇将结合Jenkins来将如何构建Android应用。

[1]: http://ant.apache.org/
[2]: http://maven.apache.org/
[3]: http://gradle.org/











