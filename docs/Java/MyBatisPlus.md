---
title: MyBatisPlus
createTime: 2025/07/08 17:03:15
permalink: /article/ax47303i/
---
# MyBatisPlus

> [MyBatis-Plus 🚀 为简化开发而生](https://baomidou.com/)

## 配置

看官网就行

**SpringMVC纯注解配置**

```java
@Bean
public SqlSessionFactoryBean sqlSessionFactoryBean(DataSource dataSource) {
    SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
    // 设置实体包类扫描
    sqlSessionFactoryBean.setTypeAliasesPackage("org.example.domain");
    sqlSessionFactoryBean.setDataSource(dataSource);
    // 启用mybatisplus
    sqlSessionFactoryBean.setPlugins(new MybatisPlusInterceptor());
    return sqlSessionFactoryBean;
}
// 另一个
@Configuration
@MapperScan("org.example.dao")
public class MyBatisPlusConfig {
}
```

## lombok

pom.xml

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.34</version>
</dependency>
```

注解

**一、简化 getter 和 setter 方法的注解**

1. **@Getter/@Setter**
   - **作用** ：自动生成类属性的 getter 方法和 setter 方法。@Getter 用于生成 getter 方法，@Setter 用于生成 setter 方法。例如，对于一个具有私有属性 name 的类，使用 @Getter/@Setter 后，会自动生成 public String getName() 和 public void setName(String name) 方法。
   - **示例代码** ： *注解定义在类上可以对类中的所有属性生效，也可以单独注解在属性上只对该属性生效。
   - 适用于需要为类的属性提供基本的获取和设置功能的场景。
2. **@Data**
   - **作用** ：它是一个组合注解，包含了 @Getter/@Setter、@ToString、@EqualsAndHashCode 和 @RequiredArgsConstructor 等功能。当在一个类上使用 @Data 注解时，会为类中的每个字段生成 getter 和 setter 方法，还会生成 toString()、equals() 和 hashCode() 方法以及一个包含所有字段的构造函数。
   - **示例代码** ：
   - 这个注解非常适合用于普通的 Java Bean 类，能够大大减少样板代码的编写。

**二、简化构造函数的注解**

1. **@NoArgsConstructor**
   - **作用** ：生成一个无参构造函数。如果类中没有定义任何构造函数，Java 默认会提供一个无参构造函数。但如果类中定义了其他构造函数，这个默认的无参构造函数就不会自动生成。此时使用 @NoArgsConstructor 就可以明确地生成一个无参构造函数。
   - **示例代码** ：
   - 常用于需要实例化对象而又不需要传入参数的场景。
2. **@AllArgsConstructor**
   - **作用** ：生成一个包含类中所有字段的构造函数。这个构造函数的参数列表与类中的字段顺序和类型一一对应。
   - **示例代码** ：
   - 在需要快速创建一个对象并为其所有字段赋值时非常有用。
3. **@RequiredArgsConstructor**
   - **作用** ：生成一个构造函数，其参数列表包含类中所有 final 修饰的字段和 @NonNull 注解的字段。这个注解通常用于保证对象的不可变性或者在对象创建时必须初始化某些关键字段。
   - **示例代码** ：
   - 适用于需要确保对象在创建时必须初始化部分字段的场景。

**三、简化日志记录的注解**

1. **@Slf4j/@Log4j 等**
   - **作用** ：用于简化日志记录代码。Lombok 提供了多种与不同日志框架（如 SLF4J、Log4j 等）对应的注解。使用这些注解后，会在类中自动生成日志记录器的私有静态 final 变量，例如使用 @Slf4j 会在类中生成 private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(Class.class)。
   - **示例代码** ：
   - 可以方便地在代码中进行日志记录操作，减少日志记录器的重复定义和初始化代码。

**四、其他注解**

1. **@ToString**
   - **作用** ：自动生成 toString() 方法。可以指定包含和排除的字段，还可以设置调用父类的 toString() 方法等参数。
   - **示例代码** ：
   - 有助于快速生成对象的字符串表示形式，方便调试和日志输出。
2. **@EqualsAndHashCode**
   - **作用** ：自动生成 equals() 和 hashCode() 方法。可以指定使用哪些字段来生成这两个方法，也可以指定是否调用父类的 equals() 和 hashCode() 方法。
   - **示例代码** ：
   - 在需要比较对象是否相等或者将对象作为哈希表键值等场景下非常有用。
3. **@Delegate**
   - **作用** ：实现委托模式。可以将类中某些方法的调用委托给另一个对象。例如，有一个类 A，它有一个成员变量 B。使用 @Delegate 注解在 B 上，那么 A 可以直接调用 B 中的方法，就好像这些方法是 A 自己的方法一样。
   - **示例代码** ：
   - 适用于需要将某些功能委托给其他对象实现的场景，有助于代码的解耦。

## 实体类

```java
@Data
@TableName("user")  // 指定表名（若表名与类名不一致）
public class User {
    @TableId(type = IdType.AUTO)  // 主键自增
    private Long id;
    
    @TableField("user_name")  // 字段映射（若字段名与属性名不一致）
    private String userName;
    
    @TableField(exist = false)  // 标记非数据库字段
    private String transientField;
}
```

## Mapper接口

```java
public interface UserMapper extends BaseMapper<User> {
    // 可自定义扩展方法
}
```

## 分页查询