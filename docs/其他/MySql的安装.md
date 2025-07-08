---
title: MySql的安装
createTime: 2025/07/08 17:03:15
permalink: /article/b6uirb4j/
---
# MySql的安装

## 安装

1. 下载zip[MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/)

2. 解压并把bin文件夹加入环境变量path中

3. mysql根目录下新建`my.ini`文件并写入

   ```ini
   [mysql]
   default-character-set=utf8
   [mysqld]
   # 设置3306端口
   port = 3306
   # 设置mysql的安装目录
   basedir = C:\\web_soft\\mysql-8.0.17-winx64\\
   # 设置mysql数据库的数据的存放目录
   datadir = C:\\web_soft\\mysql-8.0.17-winx64\\data
   # 允许最大连接数
   max_connections=20
   # 服务端使用的字符集默认为8比特编码的latin1字符集
   character-set-server=utf8
   # 创建新表时将使用的默认存储引擎
   default-storage-engine=INNODB
   # 创建模式
   sql_mode = NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
   ```

4. 终端管理员下运行命令

   bin下执行

   ```cmd
   mysqld --initialize-insecure
   ```

   mysql根目录下执行

   ```cmd
   mysqld --install
   net start mysql
   ```


## 登录

```cmd
mysql -u root -p
use mysql；
ALTER user 'root'@'localhost' IDENTIFIED BY '123456';
FLUSH PRIVILEGES;
```

