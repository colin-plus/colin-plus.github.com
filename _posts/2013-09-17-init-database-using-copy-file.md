---
layout: post
title: Android - 使用拷贝的方式初始化数据库
categories:
 - Android
tags:
  - Database
description: 'Android - 使用拷贝的方式初始化数据库'
---

在开发Android应用时，会遇到发布APK时需要附带一个数据库，比如说：省市区级联数据库。这样的数据库变动非常小，从服务器上获取数据就显得没有必要，使用内置的数据库来做是个不错的主意。

按照Android的设计，在第一次访问数据库的时候会检查是否创建数据库，若没有，会调用[onCreate(SQLiteDatabase db)][onCreate]方法初始化数据库（创建数据库并插入数据等）。但显然不应该这样做，上千条的SQL语句会告诉别人你很傻。

所以拷贝已初始化好的数据库就是一个解决办法，思路很简单：

1. 将初始化好的数据库存放在 **assets** 目录
2. 将数据库拷贝到 **/data/data/<your.app.package.name>/databases/** 目录
4. 打开数据库，查询数据

看下面的代码实现：

{% gist 6590273 DatabaseManager.java %}

需要获取数据时创建实例，调用方法即可：

{% gist 6590273 Demo.java %}

[onCreate]: http://developer.android.com/reference/android/database/sqlite/SQLiteOpenHelper.html#onCreate(android.database.sqlite.SQLiteDatabase)
