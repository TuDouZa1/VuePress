---
title: JDBC
createTime: 2025/07/08 17:03:15
permalink: /article/vj01jn3j/
---
# JDBC

> JDBC 是 JAVA 操作关系型数据库的一套 API

## 下载 jar 包

[MySQL :: Download MySQL Connector/J (Archived Versions)](https://downloads.mysql.com/archives/c-j/)
*select Operating System* 选 Platform Independent 下 zip，解压后的 mysql-connector-j-9.2.0.jar 就是
**记得下载的版本要高于sql版本**

## DriverManager

### 注册驱动

> MySQL5 之后可以省略注册驱动，可以自动加载

```java
Class.forName("com.mysql.jdbc.Driver");
```

### 获取数据库连接

```java
String url = "jdbc:mysql://127.0.0.1:3306/test_db";
String username = "root";
String password = "123456";
Connection connection = DriverManager.getConnection(url, username, password);
// 语法：jdbc:mysql://ip地址(域名):端口号/数据库名称?参数键值对1&参数键值对2...
// 细节：如果连接的是本机mysql服务器，并且mysql服务默认端口是3306，则url可以简写为：jdbc:mysql:///数据库名称?参数键值对
// 配置 useSSL=false 参数，禁用安全连接方式，解决警告提示
```

## Connection

### 获取执行SQL的对象

。。。

### 事务管理

> 对应MySQL的事务管理

开启事务：`setAutoCommit(boolean autoCommit)`：true为自动提交事务；false为手动提交事务，即为开启事务
提交事务：`commit()`
回滚事务：`rollback()`

```java
try {
    // 开启事务
    conn.setAutocommit(false);
    
    int count1 = stmt.executeUpdate(sqL1);//受影响的行数
    System.out.println(count1);
    
    int count2 = stmt.executeUpdate(sqL2);//受影响的行数
    System.out.println(count2);
    // 提交事务
    conn.commit();
} catch (Exception throwables) {
	// 回滚事务
    conn.rollback();
	throwables.printStackTrace();
}
```

## Statement

```java
int executeUpdate(sql) // 执行DML,DDL
// return：1.DML影响的行数2.DDL执行成功后也可能返回0
ResultSet executeQuery(sql) // 执行DQL
// return：ResultSet 结果集对象
```

## ResultSet

```java
boolean next(); // true 有效行， false 无效行
while (rs.next()) {
    rs.getInt(1); // 参数可以填第几列，也可以填那一列的名字
    rs.getString("name");
    ...
}
```

## PreparedStatement

> 预编译SQL，性能更好。预防SQL注入，将敏感字符转义

```sql
select from tb_user where username = 'hfkisfhskj' and password = '' or '1' = '1'
```

**开启预编译**

```java
// 在url后加
&useServerPrepStmts = true
```

**配置MySQL执行日志(MySQL.ini)**
mysql8 的 my.ini 在C:\ProgramData\MySQL\MySQL Server 8.0

```bat
log-output=FILE
general-log=1
general_log_file="D:\mysql.log"
slow-query-log=1
slow_query_log_file="D:\mysql_slow.log"
long_query_time=2
```

```java
// SQL语句中的参数值，使用？占位符替代
String sql = "select * from user where username = ? and password = ?";
// 通过Connection对象获取，并传入对应的sql语句
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setString(1, name); // 1: 代表第一个?      name：设置?为name的值
// 执行sql
ResultSet rs = pstmt.executeQuery();
```

## 数据库连接池

> 可多次使用数据库连接

### 导入druid jar包

[Central Repository: com/alibaba/druid](https://repo1.maven.org/maven2/com/alibaba/druid/)

在src下写配置文件`druid.properties`
```properties
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/test_db
username=root
password=123456
# 初始化连接数量
initialSize=5
# 最大连接数
maxActive=10
# 最大超时时间
maxWait=3000
```

```java
//3.加载配置文件
Properties prop = new Properties();
prop.load(new FileInputStream("jdbc-demo/src/druid.properties"));
//4.获取连接池对象
DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
//5.获取数据库连接Connection
Connection connection = dataSource.getConnection();

// System.out.println(System.getProperty("user.dir")); // 返回当前class的路径
```

