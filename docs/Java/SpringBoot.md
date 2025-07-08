---
title: SpringBoot
createTime: 2025/07/08 17:03:15
permalink: /article/fva1s3zv/
---
# SpringBoot

> 简化Spring配置

## 创建SpringBoot项目

### 手动创建

1. 创建项目选择Maven-Archetype

2. 在Archetype中选择`org.apache.maven.archetypes:maven-archetype-quickstart`

3. 在pom中添加

   ```xml
   <parent>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-parent</artifactId>
       <version>3.4.5</version>
   </parent>
   
   <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

4. 建资源文件夹，并在里面建springboot配置文件`application.properties/yml`等

5. ```java
   @SpringBootApplication // 默认扫描包所在目录内的bean
   public class SpringBootCreateTestApplication {
       public static void main( String[] args ) {
           SpringApplication.run(SpringBootCreateTestApplication.class, args);
       }
   }
   ```

## 配置文件

### application.properties

```properties
server.port=9191
server.servlet.context-path=/SpringBootTest
```

### application.yml

```yaml
server:
  port: 9191
  servlet:
    context-path: /SpringBootTest
```

### yml

**yml配置信息获取**

```java
@Value("${user.name}")
```

```java
@ConfigurationProperties(prefix = "user") // 前缀
public class User {

    @Value("${name}")
    private String name;
```

## 整合MyBatis

pom.xml

```xml
<dependency>
  <groupId>org.mybatis.spring.boot</groupId>
  <artifactId>mybatis-spring-boot-starter</artifactId>
  <version>3.0.3</version>
</dependency>

<dependency>
  <groupId>com.mysql</groupId>
  <artifactId>mysql-connector-j</artifactId>
</dependency>
```

application.yml

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/abc?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=Asia/Shanghai
    username: root
    password: 123456
```

### 开启驼峰命名和下划线命名的自动转换

yml

```yaml
mybatis:
  configuration:
    map-underscore-to-camel-case: true # 开启驼峰命名和下划线命名的自动转换
```

xml

```xml
<setting name="mapUnderscoreToCamelCase" value="true"/>
```



## 整合Redis

pom.xml

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```



## Bean

### Bean扫描

### Bean注册

### Bean注册条件

## SpringValidation

> 对参数进行校验
>

pom.xml

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

### 匹配正则表达式

```java
@Validated
public class UserController {
    @Autowired
    UserService userService;
    @PostMapping("/register")
    public Result register(@Pattern(regexp = "^(?=.*[A-Z])(?=.*[a-z])(?=.*\\d).{8,}$", message = "Password must be at least 8 characters long and contain at least one uppercase letter, one lowercase letter, and one digit") String username, @Pattern(regexp = "^\\S{5,16}$")String password) {}
}
```

**正则表达式解释**

- `^`：表示字符串的开始。
- `(?=.*[A-Z])`：确保字符串中至少有一个大写字母。
- `(?=.*[a-z])`：确保字符串中至少有一个小写字母。
- `(?=.*\\d)`：确保字符串中至少有一个数字。
- `.{8,}`：确保字符串长度至少为8个字符。
- `$`：表示字符串的结束。

### 对pojo进行限制

```java
@NotNull
private Integer id;//主键ID
@JsonIgnore
private String password;//密码
@NotEmpty
@Pattern(regexp = "^\\S{1,10}$")
private String nickname;//昵称
@NotEmpty
@Email
private String email;//邮箱
@JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
private LocalDateTime createTime;//创建时间
```

别忘了在Controller的pojo参数前添加`@Validated`注解

### 自定义Validation

自定义注解State

```java
package org.example.anno;

import jakarta.validation.Constraint;
import jakarta.validation.Payload;
import org.example.validation.StateValidation;

import java.lang.annotation.*;

@Documented // 元注解
@Constraint( // 指定提供校验规则的类
        validatedBy = {StateValidation.class}
)
@Target({ElementType.FIELD}) // 元注解，可以作用在哪里，属性
@Retention(RetentionPolicy.RUNTIME) // 元注解，作用的阶段，运行时阶段
public @interface State {
    // 校验失败的提示信息
    String message() default "state只能是已发布的分类或草稿";

    // 指定分组
    Class<?>[] groups() default {};

    // 负载    获取到State注解的附加信息
    Class<? extends Payload>[] payload() default {};
}
```

自定义校验数据类StateValidation

```java
package org.example.validation;

import jakarta.validation.ConstraintValidator;
import jakarta.validation.ConstraintValidatorContext;
import org.example.anno.State;

public class StateValidation implements ConstraintValidator<State, String> {
    /**
     *
     * @param s 要校验的数据
     * @param constraintValidatorContext
     * @return true：校验通过   false：校验失败
     */
    @Override
    public boolean isValid(String s, ConstraintValidatorContext constraintValidatorContext) {
        // 提供校验规则
        return s.equals("已发布") || s.equals("草稿");
    }
}
```



## JWT

> [JSON Web Tokens - jwt.io](https://jwt.io/)
>
> 用于通信双方以`JSON`数据格式安全的传输信息

pom.xml

```xml
<dependency>
  <groupId>com.auth0</groupId>
  <artifactId>java-jwt</artifactId>
  <version>4.4.0</version>
</dependency>
```

示例代码

```java
package org.example.utils;

import com.auth0.jwt.JWT;
import com.auth0.jwt.algorithms.Algorithm;

import java.util.Date;
import java.util.Map;

public class JwtUtil {

    private static final String KEY = "wtf";
	
	//接收业务数据,生成token并返回
    public static String genToken(Map<String, Object> claims) {
        return JWT.create()
                .withClaim("claims", claims)
                .withExpiresAt(new Date(System.currentTimeMillis() + 1000 * 60 * 60 * 12))
                .sign(Algorithm.HMAC256(KEY));
    }

	//接收token,验证token,并返回业务数据
    public static Map<String, Object> parseToken(String token) {
        return JWT.require(Algorithm.HMAC256(KEY))
                .build()
                .verify(token)
                .getClaim("claims")
                .asMap();
    }
}

```

## 拦截器

配置拦截器

```java
@Component
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        String token = request.getHeader("Authorization");
        try {
            Map<String, Object> claims = JwtUtil.parseToken(token);
            ThreadLocalUtil.set(claims);
            return true;
        } catch (Exception e) {
            response.setStatus(401);
            return false;
        }
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        ThreadLocalUtil.remove();
    }
}
```

添加拦截器

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Autowired
    private LoginInterceptor loginInterceptor;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(loginInterceptor).excludePathPatterns("/user/login", "/user/register");
    }
}
```

### 搭配异常处理

```java
@RestControllerAdvice
public class GlobalExceptionHandle {
    @ExceptionHandler(Exception.class)
    public Result handleException(Exception e) {
        e.printStackTrace();
        return Result.error(StringUtils.hasLength(e.getMessage()) ? e.getMessage() : "出错了，请稍后再试！");
    }
}
```



## ThreadLocal

```java
/**
 * ThreadLocal 工具类
 */
@SuppressWarnings("all")
public class ThreadLocalUtil {
    //提供ThreadLocal对象,
    private static final ThreadLocal THREAD_LOCAL = new ThreadLocal();

    //根据键获取值
    public static <T> T get(){
        return (T) THREAD_LOCAL.get();
    }
	
    //存储键值对
    public static void set(Object value){
        THREAD_LOCAL.set(value);
    }


    //清除ThreadLocal 防止内存泄漏
    public static void remove(){
        THREAD_LOCAL.remove();
    }
}
```



## 分类分页列表查询

### PageBean.class

```java
//分页返回结果对象
@Data
@NoArgsConstructor
@AllArgsConstructor
public class PageBean <T>{
    private Long total;//总条数
    private List<T> items;//当前页数据集合
}
```

### PageHelper

pom.xml

```xml
<dependency>
  <groupId>com.github.pagehelper</groupId>
  <artifactId>pagehelper-spring-boot-starter</artifactId>
  <version>1.4.7</version>
</dependency>
```

### controller

```java
@GetMapping
public Result<PageBean<Article>> list(
        Integer pageNum,
        Integer pageSize,
        @RequestParam(required = false) Integer categoryId,
        @RequestParam(required = false) String state
) {
    PageBean<Article> pageBean = articleService.list(pageNum, pageSize, categoryId, state);
    return Result.success(pageBean);
}
```

### service

```java
@Override
public PageBean<Article> list(Integer pageNum, Integer pageSize, Integer categoryId, String state) {
    PageBean<Article> pageBean = new PageBean<>();

    PageHelper.startPage(pageNum, pageSize);

    Map<String, Object> map = ThreadLocalUtil.get();
    Integer userId = (Integer) map.get("id");
    List<Article> articleList = articleMapper.list(userId, categoryId, state);
    Page<Article> articlePage = (Page<Article>) articleList;

    pageBean.setTotal(articlePage.getTotal());
    pageBean.setItems(articlePage.getResult());

    return pageBean;
}
```

**设置分页参数**

**`PageHelper.startPage(pageNum, pageSize);`**：这是 MyBatis 分页插件 PageHelper 的方法，用于开始分页操作。它根据传入的 `pageNum`（页码）和 `pageSize`（每页大小）来设置分页参数。MyBatis 在执行后续的查询操作时，会根据这些分页参数对查询结果进行分页处理，它会自动修改查询 SQL 语句，添加必要的分页子句（如 MySQL 中的 `LIMIT` 和 `OFFSET`），从而实现分页查询。

**查询文章列表**

**`Page<Article> articlePage = (Page<Article>) articleList;`**：将查询结果 `articleList` 转换为 `Page<Article>` 类型的 `articlePage`。`Page` 是 MyBatis 分页插件提供的一个类，它封装了分页查询的结果，包括当前页的数据、总记录数等信息。由于之前调用了 `PageHelper.startPage` 方法设置了分页参数，所以 MyBatis 会自动将查询结果封装为 `Page` 对象，这里通过强制类型转换来获取它。

**设置分页对象的属性**

**`pageBean.setTotal(articlePage.getTotal());`**：将 `articlePage` 中的总记录数设置到 `pageBean` 的 `total` 属性中。总记录数是分页查询的关键信息，它可以帮助计算总页数等其他分页相关的信息。

**`pageBean.setItems(articlePage.getResult());`**：将 `articlePage` 中的当前页数据（即查询到的文章列表）设置到 `pageBean` 的 `items` 属性中，这样就把分页后的数据封装到了 `PageBean` 对象中，方便后续的使用和传输。

### 动态sql

在资源中创建相同结构的mapper文件夹，并在里面创建同名mapper的xml文件`XxxxMapper.xml`

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.example.mapper.ArticleMapper">
    <!--动态sql-->
    <select id="list" resultType="org.example.pojo.Article">
        select * from article
        <where>
            <if test="categoryId!=null">
                category_id=#{categoryId}
            </if>

            <if test="state!=null">
                and state=#{state}
            </if>

            and create_user=#{userId}
        </where>
    </select>
</mapper>
```

## 文件上传

### 本地文件上传

```java
@RestController
public class FileUploadController {
    @PostMapping("/upload")
    public Result<String> upload(MultipartFile file) throws Exception {
        // 文件保存在本地磁盘
        String originalFilename = file.getOriginalFilename();
        String fileName = UUID.randomUUID() +
                originalFilename.substring(originalFilename.lastIndexOf('.'));
        // 本地文件上传
        // file.transferTo(new File("E:\\JS\\javaTest\\files\\" + fileName));
        String url = AliOssUtil.uploadFile(fileName, file.getInputStream());
        return Result.success(url);
    }
}
```

### OSS

AliOssUtil.class

```java
package org.example.utils;

import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.PutObjectRequest;
import com.aliyun.oss.model.PutObjectResult;

import java.io.InputStream;

public class AliOssUtil {
    private static final String ENDPOINT = "https://oss-cn-beijing.aliyuncs.com";
    private static final String BUCKET_NAME = "blg-event";
    private static final String REGION = "cn-beijing";

    public static String uploadFile(String objectName, InputStream in) throws Exception {
        String url = "";

        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider =
                CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();

        // 创建OSSClient实例。
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
                .endpoint(ENDPOINT)
                .credentialsProvider(credentialsProvider)
                .clientConfiguration(clientBuilderConfiguration)
                .region(REGION)
                .build();

        try {
            // 填写字符串。
            String content = "Hello OSS，你好世界";

            // 创建PutObjectRequest对象。
            PutObjectRequest putObjectRequest =
                    new PutObjectRequest(BUCKET_NAME, objectName, in);

            // 如果需要上传时设置存储类型和访问权限，请参考以下示例代码。
            // ObjectMetadata metadata = new ObjectMetadata();
            // metadata.setHeader(OSSHeaders.OSS_STORAGE_CLASS, StorageClass.Standard.toString());
            // metadata.setObjectAcl(CannedAccessControlList.Private);
            // putObjectRequest.setMetadata(metadata);

            // 上传字符串。
            PutObjectResult result = ossClient.putObject(putObjectRequest);

            url = "https://" + BUCKET_NAME + "." +
                    ENDPOINT.substring(ENDPOINT.lastIndexOf("/") + 1) + "/" + objectName;
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }

        return url;
    }
}
```

## SpringBoot项目部署

### 导入插件

pom.xml

```xml
<build>
<plugins>
  <plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <version>3.4.5</version>
  </plugin>
</plugins>
</build>
```

执行maven的package生成jar包，终端执行

```cmd
java -jar xxx-1.0-SNAPSHOT.jar
```

### 属性配置

1. 项目的资源访问目录下的配置文件
2. jar包目录下的配置文件
3. 环境变量
4. 命令行参数

优先级从上往下变高

```cmd
--server.port=9999
```

在环境变量添加`server.port`

## 多环境开发



## WEB开发基础

### Controller

- @RestController

  将对象数据转换成json返回给服务器

- @Controller

  默认的控制器会跳转页面

### 路由映射

- @RestMapping

  负责url的路由映射，可以添加到Controller或者其他具体的方法上
  如果是在controller类上，则controller中所有的路由映射都会加上此映射规则。
  加在方法上只对当前方法有效
  **参数**
  value：请求url的路径，支持url模板、正则表达式
  method：http请求方法
  consumes：请求的媒体形式(Content-Type)，如application/json
  produces：响应的媒体形式
  params，headers：请求的参数及请求头的值
  **说明**
  @RequestMapping的通配符匹配非常简单实用，支持 `* ？**`等通配符
  符号`*`匹配任意字符，符号`**`匹配任意路径，符号`?`匹配单个字符。
  有通配符的优先级低于没有通配符的，比如`/user/add.json`比`/user/*.json`优匹配。
  有`**`通配符的优先级低于有`*`通配符的。

- @RequestParam

  idea里有示例

- @RequestBody
  132

- 常见错误

  - 405：请求错误

    例如接受的‘GET’请求，地址栏是‘POST’

## HTTP状态码错误

1xx：信息，通信传输协议级信息
2xx：成功，表示客户端的请求已成功接受
3xx：重定向，表示客户端必须执行一些其他操作才能完成其请求
4xx：客户端错误，此类错误状态码指向客户端
5xx：服务器错误，服务器负责这写错误状态码
