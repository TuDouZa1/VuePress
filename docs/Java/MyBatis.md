---
title: MyBatis
createTime: 2025/07/08 17:03:15
permalink: /article/6a24fkeq/
---
# MyBatis

> 化简JDBC
> [入门_MyBatis中文网](https://mybatis.net.cn/getting-started.html)

## 配置

**pom.xml**

```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.16</version>
</dependency>

<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.2.0</version> <!-- 保持版本一致 -->
</dependency>

<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>

<!--slf4j日志api-->
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>2.0.16</version>
</dependency>
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version> 1.5.11</version>
</dependency>
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-core</artifactId>
    <version>1.5.13</version>
</dependency>
```

**在 main 目录下的 resoures 配置文件目录下创建一个名为 logback.xml 的配置文件，粘贴一下内容：**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
<!--
CONSOLE ：表示当前的日志信息是可以输出到控制台的。
-->
<appender name="Console" class="ch.qos.logback.core.ConsoleAppender">
<encoder>
<pattern>【%level】 %blue(%d{HH:mm:ss.SSS}) %cyan(【%thread】) %boldGreen(%logger{15}) - %msg %n</pattern>
</encoder>
</appender>

<logger name="com.itheima" level="DEBUG" additivity="false">
<appender-ref ref="Console"/>
</logger>

<root level="DEBUG">
<appender-ref ref="Console"/>
</root>
</configuration>
```

**编写 MyBatis 核心配置文件**
在 main 目录下的 resoures 配置文件目录下创建一个名为 mybatis-config.xml 的配置文件，内容在MyBatis官网
修改对应的数据库，用户名，密码即可

**编写 sql 映射文件**
在 main 目录下的 resoures 配置文件目录下创建一个名为 UserMapper.xml 的配置文件，内容在MyBatis官网
修改Mapper里对应的数值即可

## 编码

**加载mybatis核心配置文件，构建 SqlSessionFactory**
在官网复制

## 动态sql

### 1. `<if>` 标签

`<if>` 标签用于根据条件判断是否包含某段 SQL 语句。

**示例：**

xml

复制

```xml
<select id="selectUsers" resultType="User">
    SELECT * FROM users
    WHERE 1=1
    <if test="name != null">
        AND name = #{name}
    </if>
    <if test="age != null">
        AND age = #{age}
    </if>
</select>
```

- 如果 `name` 不为 `null`，则会添加 `AND name = #{name}`。
- 如果 `age` 不为 `null`，则会添加 `AND age = #{age}`。

### 2. `<where>` 标签

`<where>` 标签用于自动处理 `WHERE` 子句的逻辑，避免手动添加 `AND` 或 `OR` 时的错误。

**示例：**

xml

复制

```xml
<select id="selectUsers" resultType="User">
    SELECT * FROM users
    <where>
        <if test="name != null">
            name = #{name}
        </if>
        <if test="age != null">
            AND age = #{age}
        </if>
    </where>
</select>
```

- `<where>` 会自动去除多余的 `AND` 或 `OR`，确保 `WHERE` 子句的正确性。

### 3. `<foreach>` 标签

`<foreach>` 标签用于处理集合或数组，常用于 `IN` 子句。

**示例：**

xml

复制

```xml
<select id="selectUsersByIds" resultType="User">
    SELECT * FROM users
    WHERE id IN
    <foreach item="id" collection="ids" separator="," open="(" close=")">
        #{id}
    </foreach>
</select>
```

- `collection`：指定要遍历的集合（如 `list`、`array` 等）。
- `item`：集合中的每个元素的名称。
- `separator`：元素之间的分隔符。
- `open` 和 `close`：指定开始和结束的符号。
- 如果传入的 `ids` 是 `[1, 2, 3]`，生成的 SQL 会是 `SELECT * FROM users WHERE id IN (1, 2, 3)`。

### 4. `<choose>`、`<when>`、`<otherwise>` 标签

`<choose>` 标签类似于 Java 的 `switch` 语句，用于多条件选择。

**示例：**

xml

复制

```xml
<select id="selectUsersByCondition" resultType="User">
    SELECT * FROM users
    <where>
        <choose>
            <when test="name != null">
                name = #{name}
            </when>
            <when test="email != null">
                email = #{email}
            </when>
            <otherwise>
                1=1
            </otherwise>
        </choose>
    </where>
</select>
```

- 如果 `name` 不为 `null`，则使用 `name = #{name}`。
- 如果 `email` 不为 `null`，则使用 `email = #{email}`。
- 如果都不满足，则使用 `1=1`。

### 5. `<trim>` 标签

`<trim>` 标签用于去除多余的前缀或后缀，常用于动态生成 `SET` 或 `WHERE` 子句。

**示例：**

xml

复制

```xml
<update id="updateUser">
    UPDATE users
    <set>
        <if test="name != null">
            name = #{name},
        </if>
        <if test="age != null">
            age = #{age},
        </if>
    </set>
    WHERE id = #{id}
</update>
```

- `<set>` 是 `<trim>` 的一个特例，自动处理多余的逗号。
- 如果传入的参数是 `name` 和 `age` 都不为 `null`，生成的 SQL 会是 `UPDATE users SET name = 'newName', age = 25 WHERE id = 1`。

### 6. `<bind>` 标签

`<bind>` 标签用于在 SQL 中定义变量，方便后续使用。

**示例：**

xml

复制

```xml
<select id="selectUsersByLikeName" resultType="User">
    <bind name="likeName" value="'%' + name + '%'" />
    SELECT * FROM users
    WHERE name LIKE #{likeName}
</select>
```

- `bind` 定义了一个变量 `likeName`，用于模糊查询。

## XML 映射文件语法

### 增删改查基本语法

- **select** ：用于执行查询操作，例如：

  ```xml
  <select id="selectUser" parameterType="int" resultType="User">
    SELECT * FROM users WHERE id = #{id}
  </select>
  ```

- **insert** ：用于执行插入操作，例如：

  ```xml
  <insert id="insertUser" parameterType="User">
    INSERT INTO users (name, age, email)
    VALUES (#{name}, #{age}, #{email})
  </insert>
  ```

- **update** ：用于执行更新操作，例如：

  ```xml
  <update id="updateUser" parameterType="User">
    UPDATE users
    SET name = #{name}, age = #{age}, email = #{email}
    WHERE id = #{id}
  </update>
  ```

- **delete** ：用于执行删除操作，例如：

  ```xml
  <delete id="deleteUser" parameterType="int">
    DELETE FROM users WHERE id = #{id}
  </delete>
  ```

### resultMap 高级结果映射

> 当查询结果集的列名与实体类的属性名不一致，或者存在一对多、多对多等复杂关系时，可以使用 resultMap 进行映射

**Association（一对一映射）**

`association` 用于将查询结果中的某个字段或部分字段映射到一个关联的对象。它适用于一对一的关系，例如一个用户关联一个地址信息。

**Collection（一对多映射）**

`collection` 用于将查询结果中的多个记录映射到一个集合中。它适用于一对多的关系，例如一个用户关联多个订单。

**Key Attributes**

`association` 和 `collection` 有一些共同的属性，但也有一些特定的属性用于不同的场景：

- `property`：指定要映射的 Java 对象中的属性名。
- `javaType`：指定映射的 Java 对象类型（`association` 使用）。
- `ofType`：指定集合中元素的类型（`collection` 使用）。
- `resultMap`：引用另一个 `resultMap`，用于更复杂的映射。
- `column`：指定结果集中用于关联的列名。
- `select`：指定一个查询语句来加载关联对象或集合。
- `fetchType`：指定是否使用延迟加载（`lazy`）或立即加载（`eager`）。

**Example Use Cases**

- 一对一：用户和地址。
- 一对多：用户和订单。

### 嵌套结果映射

嵌套结果映射用于处理对象之间的一对一嵌套关系。例如一个用户关联一个地址信息：

- 数据库表：

```sql
CREATE TABLE user (
    id INT PRIMARY KEY,
    username VARCHAR(50),
    address_id INT
);

CREATE TABLE address (
    id INT PRIMARY KEY,
    street VARCHAR(100),
    city VARCHAR(50)
);
```

- Java 类：

```java
public class User {
    private Integer id;
    private String username;
    private Address address;
    // Getter 和 Setter 略
}

public class Address {
    private Integer id;
    private String street;
    private String city;
    // Getter 和 Setter 略
}
```

- `resultMap` 映射：

```xml
<resultMap id="addressResultMap" type="com.example.Address">
    <id column="id" property="id" />
    <result column="street" property="street" />
    <result column="city" property="city" />
</resultMap>

<resultMap id="userResultMap" type="com.example.User">
    <id column="id_user" property="id" />
    <result column="username" property="username" />
    <association property="address" javaType="com.example.Address" resultMap="addressResultMap" />
</resultMap>
```

- SQL 查询：

```sql
<select id="getUserWithAddress" resultMap="userResultMap">
    SELECT u.id AS id_user, u.username, a.id AS id_address, a.street, a.city
    FROM user u
    LEFT JOIN address a ON u.address_id = a.id
    WHERE u.id = #{id}
</select>
```

### 嵌套集合映射

嵌套集合映射用于处理对象之间的一对多嵌套关系。例如一个用户关联多个订单：

- 数据库表：

```sql
CREATE TABLE user (
    id INT PRIMARY KEY,
    username VARCHAR(50)
);

CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    order_name VARCHAR(100)
);
```

- Java 类：

```java
public class Order {
    private Integer id;
    private String orderName;
    // Getter 和 Setter 略
}

public class User {
    private Integer id;
    private String username;
    private List<Order> orders;
    // Getter 和 Setter 略
}
```

- `resultMap` 映射：

```xml
<resultMap id="orderResultMap" type="com.example.Order">
    <id column="id" property="id" />
    <result column="order_name" property="orderName" />
</resultMap>

<resultMap id="userResultMap" type="com.example.User">
    <id column="id_user" property="id" />
    <result column="username" property="username" />
    <collection property="orders" ofType="com.example.Order" resultMap="orderResultMap" />
</resultMap>
```

- SQL 查询：

```sql
<select id="getUserWithOrders" resultMap="userResultMap">
    SELECT u.id AS id_user, u.username, o.id AS id_order, o.order_name
    FROM user u
    LEFT JOIN orders o ON u.id = o.user_id
</select>
```

### 多表联合查询映射

在多表联合查询中，可以通过`resultMap`将多张表的数据映射到多个对象中。例如一个用户关联多个角色，每个角色关联多个权限：

- 数据库表：

```sql
CREATE TABLE user (
    id INT PRIMARY KEY,
    username VARCHAR(50)
);

CREATE TABLE role (
    id INT PRIMARY KEY,
    role_name VARCHAR(50)
);

CREATE TABLE permission (
    id INT PRIMARY KEY,
    permission_name VARCHAR(50)
);

CREATE TABLE user_role (
    user_id INT,
    role_id INT
);

CREATE TABLE role_permission (
    role_id INT,
    permission_id INT
);
```

- Java 类：

```java
public class Permission {
    private Integer id;
    private String permissionName;
    // Getter 和 Setter 略
}

public class Role {
    private Integer id;
    private String roleName;
    private List<Permission> permissions;
    // Getter 和 Setter 略
}

public class User {
    private Integer id;
    private String username;
    private List<Role> roles;
    // Getter 和 Setter 略
}
```

- `resultMap` 映射：

```xml
<resultMap id="permissionResultMap" type="com.example.Permission">
    <id column="id" property="id" />
    <result column="permission_name" property="permissionName" />
</resultMap>

<resultMap id="roleResultMap" type="com.example.Role">
    <id column="id" property="id" />
    <result column="role_name" property="roleName" />
    <collection property="permissions" ofType="com.example.Permission" resultMap="permissionResultMap" />
</resultMap>

<resultMap id="userResultMap" type="com.example.User">
    <id column="id" property="id" />
    <result column="username" property="username" />
    <collection property="roles" ofType="com.example.Role" resultMap="roleResultMap" />
</resultMap>
```

- SQL 查询：

```sql
<select id="getUserWithRolesAndPermissions" resultMap="userResultMap">
    SELECT
        u.id AS user_id, u.username,
        r.id AS role_id, r.role_name,
        p.id AS permission_id, p.permission_name
    FROM user u
    LEFT JOIN user_role ur ON u.id = ur.user_id
    LEFT JOIN role r ON ur.role_id = r.id
    LEFT JOIN role_permission rp ON r.id = rp.role_id
    LEFT JOIN permission p ON rp.permission_id = p.id
</select>
```

### ResultMap 继承

如果多个`resultMap`有部分相同的映射配置，可以使用继承来避免重复代码。例如：

```xml
<resultMap id="baseUserResultMap" type="com.example.User">
    <id column="id" property="id" />
    <result column="username" property="username" />
</resultMap>

<resultMap id="adminUserResultMap" type="com.example.AdminUser" extends="baseUserResultMap">
    <result column="permission_level" property="permissionLevel" />
</resultMap>
```

在这个例子中，`adminUserResultMap`继承了`baseUserResultMap`的配置，并添加了自己的特定映射。

### 延迟加载

延迟加载是一种优化技术，它允许关联对象在需要时才加载，而不是在主对象加载时就立即加载。这可以减少初始查询的负载，提高查询效率。例如：

```xml
<resultMap id="lazyUserResultMap" type="com.example.User">
    <id column="id" property="id" />
    <result column="username" property="username" />
    <association property="address" javaType="com.example.Address" resultMap="addressResultMap" fetchType="lazy" />
</resultMap>
```

在这个例子中，`fetchType="lazy"`配置使`address`关联对象在`User`对象加载时不立即加载，而是等到访问`address`属性时才加载。
