---
layout: post
title: Android - 使用拷贝的方式初始化数据库
categories:
 - Android
tags:
 - 数据库
description: 'Android - 使用拷贝的方式初始化数据库'
---

在开发Android应用时，会遇到发布APK时需要附带一个数据库，比如说：省市区级联数据库。这样的数据库变动非常小，从服务器上获取数据就显得没有必要，使用内置的数据库来做是个不错的主意。

按照Android的设计，在第一次访问数据库的时候会检查是否创建数据库，若没有，会调用[onCreate(SQLiteDatabase db)][onCreate]方法初始化数据库（创建数据库并插入数据等）。但显然不应该这样做，上千条的SQL语句会告诉别人你很傻。

所以拷贝已初始化好的数据库就是一个解决办法，思路很简单：

1. 将初始化好的数据库存放在 **assets** 目录
2. 将数据库拷贝到 **/data/data/<your.app.package.name>/databases/** 目录
4. 打开数据库，查询数据

看下面的代码实现：

    public class DatabaseManager {
     
        public static final String DB_PATH = "/data/data/com.colinz.app/databases/";
        public static final String DB_NAME = "test.db";
        public static final int DB_VERSION = 1;
     
        private SQLiteDatabase database;
     
        private DatabaseManager(SQLiteDatabase database) {
            this.database = database;
        }
     
        public static DatabaseManager newInstance(Context context) {
            copyDatabaseIfNeed(context);
            SQLiteDatabase database = SQLiteDatabase.openOrCreateDatabase(DB_PATH + DB_NAME, null);
            return new DatabaseManager(database);
        }
     
        public void close() {
            database.close();
        }
     
        private static void copyDatabaseIfNeed(Context context) {
            if (!new File(DB_PATH + DB_NAME).exists()) {
                File f = new File(DB_PATH);
                if (!f.exists()) {
                    f.mkdir();
                }
                try {
                    InputStream is = context.getAssets().open(DB_NAME);
                    OutputStream os = new FileOutputStream(DB_PATH + DB_NAME);
                    byte[] buffer = new byte[1024];
                    int length;
                    while ((length = is.read(buffer)) > 0) {
                        os.write(buffer, 0, length);
                    }
                    os.flush();
                    os.close();
                    is.close();
                } catch (IOException e) {
                    Toast.makeText(context, e.getMessage(), Toast.LENGTH_LONG).show();
                }
            }
        }
     
        // ----------
     
        public Cursor queryAllUsers() {
            return database.rawQuery("select * from users", null);
        }
     
    }

需要获取数据时创建实例，调用方法即可：

    DatabaseManager manager = DatabaseManager.newInstance(context);
    Cursor cursor = manager.queryAllUsers();

[onCreate]: http://developer.android.com/reference/android/database/sqlite/SQLiteOpenHelper.html#onCreate(android.database.sqlite.SQLiteDatabase)
