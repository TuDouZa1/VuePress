---
title: SSM
createTime: 2025/07/08 17:03:15
permalink: /article/2kebrysw/
---
# SSM

> Spring+SpringMVC+Maven高级+SpringBoot+MyBatisPlus企业实用开发技术

## Spring

> 简化开发流程

### 创建Spring项目

新建Maven项目，修改Maven的镜像仓库

在pom.xml中配置Spring

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.2.10.RELEASE</version>
</dependency>
```



### IOC

> IOC容器集中管理Bean(类)，不用手动获取对象

#### 通过XMl配置Bean

- bean:创建bean
  - id:类名
  - class:类的位置
  - name:别名(用 空格 , ; 分割)
  - scope:bean是否为单例
  - factory-method:工厂创建类的方法名(getXxx)
  - factory-bean:bean工厂方法
  - autowire:一般使用 `byType` , 自动注入引用类型, 优先级低于手动写的注入，setter注入和构造器注入同时存在时会失效
  - init-method:Bean初始化后执行的函数
  - destroy-method:Bean销毁时执行的函数
  - lazy-init:控制bean延迟加载
- property:setter注入bean里的变量
  - name:变量名，集合注入时为集合类型名
  - ref:引用哪个bean
  - value:注入变量值
- constructor-arg:构造方法注入

集合注入就懒得写了（

```xml
<bean id="bookDao" class="com.example.ssm2.dao.Impl.BookDaoImpl">
</bean>
<bean id="bookDaoService" class="com.example.ssm2.service.Impl.BookDaoServiceImpl">
    <property name="bookDao" ref="bookDao"/>
</bean>
```

**加载properties文件**

懒得写了，看视频吧

**App**

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml"); // 创建IOC容器
BookDao bookDao = ctx.getBean("bookDao", BookDao.class); // 获取Bean
bookDao.save();
```



#### 通过纯注解配置Bean

- @Component(“”):定义Bean

  - Controller:表现层
  - Service:业务层
  - Repository:数据层

- @Scope(“”):bean是否为单例

- @Configuration:配置，代替xml文件

- @ComponentScan({“”, “”}):扫描Bean的范围

- @Import({“”, “”}):导入其他的配置

- @PropertySource(“”):导入properties文件

  - @Value(“”):注入常量

  - @Bean:配置第三方bean

    ```java
    @Bean
    public DataSource dataSource() {
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(username);
        ds.setPassword(password);
        return ds;
    }
    ```

  - @Autowired:自动注入，替代了setter

    - @Qualifier(“”):指定用哪个bean自动注入

```java
@Configuration
@ComponentScan("org.example")
@PropertySource("jdbc.properties")
@Import({JdbcConfig.class, MybatisConfig.class})
public class SpringConfig {}
```



**App**

```java
ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
BookDao bookDao = ctx.getBean(BookDao.class);
bookDao.save();
```

### JDBC

> 支持JAVA控制数据库

pom.xml

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.3.0</version>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>6.2.5</version>
</dependency>
```

class

```java
@PropertySource("classpath:jdbc.properties")

public class JdbcConfig {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String username;
    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource() {
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(username);
        ds.setPassword(password);
        return ds;
    }
}
```

**propreties**

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/abc?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=Asia/Shanghai
jdbc.username=root
jdbc.password=123456
```



### MyBatis

pom.xml

```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>3.0.4</version>
</dependency>

<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.16</version>
</dependency>
```

class

```java
public class MybatisConfig {
    @Bean
    public SqlSessionFactoryBean sqlSessionFactoryBean(DataSource dataSource) {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setTypeAliasesPackage("com.example.demo.account.domain");
        sqlSessionFactoryBean.setDataSource(dataSource);
        return sqlSessionFactoryBean;
    }

    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer() {
        MapperScannerConfigurer mapperScannerConfigurer = new MapperScannerConfigurer();
        mapperScannerConfigurer.setBasePackage("com.example.demo.account.dao");
        return mapperScannerConfigurer;
    }
}
```



### JUnit

> 让JAVA测试时也可以运行配置Spring

pom.xml

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>5.3.22</version>
</dependency>
```

class

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = SpringConfig.class)
public class UserServiceTest {
}
```



### AOP(注解)

> 面向切面编程，不惊动原始设计的基础上为其增加功能
>
> 将匹配上的Bean转换成代理对象

#### 基础配置

pom.xml

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.22.1</version>
</dependency>
```

class

```java
@Component // 声明为Bean
@Aspect // 启动AOP
public class MyAop {
    @Pointcut("execution(public void com.example.demo.service.BookService.update(int))") // 给那个函数增加功能
    private void pt() {}

    @Before("pt()") // 函数执行之前干嘛
    public void method() {
        System.out.println("hi aop");
    }
}
```

同时还要在config中加入`@EnableAspectJAutoProxy`

#### 切入点表达式

`execution`里可以用正则表达式

- *：一层任意字符

  ```java
  // 任意返回类型的example下的任意下的UserService的以find开头的方法，包含任意一个参数
  execution(public * com.example.*.UserService.find*(*))
  ```

- ..：任意层任意字符

  ```java
  // com下的任意的UserService.findById的任意个参数
  execution(public User com..UserService.findById(..))
  ```

- +：匹配子类类型

  ```java
  
  execution(* *..*Service+.*(..))
  ```

#### 通知类型

- @Before

- @After

- @Around(重点，常用)

  ```java
  @Around("FindPt()")
  public Object method(ProceedingJoinPoint pjp) throws Throwable {
      Object ret = pjp.proceed();
      return ret;
  }
  // 用ProceedingJoinPoint来获取原始方法的返回值
  ```
  
- @AfterReturning

- @AfterThrowing

#### 反射

```java
@Around("FindPt()")
public Object method(ProceedingJoinPoint pjp) throws Throwable {
    Signature signature = pjp.getSignature();
    String className = signature.getDeclaringTypeName();
    String methodName = signature.getName();
    Object ret = pjp.proceed();
    System.out.println(className + "." + methodName + "执行");
    return ret;
}
```

获取执行的对象信息

#### 通知获取数据

。。。



### Spring事务管理

#### 开启事务

1. 在要开启事务的功能的函数/类/接口上添加`@Transactional`

2. 在JDBC的config中设置事务管理器

   ```java
   @Bean
   public PlatformTransactionManager transactionManager(DataSource dataSource) {
       DataSourceTransactionManager ptm = new DataSourceTransactionManager();
       ptm.setDataSource(dataSource);
       return ptm;
   }
   ```

3. 在Spring Config开启Spring注解式事务驱动`@EnableTransactionManagement`

**如何工作的**

将所有的事务合并为一个事务，出现异常时同时回滚

#### Spring事务角色

- 事务管理员：发起事务方，在Spring中通常指代业务层开启事务的方法
- 事务协调员：加入事务方，在Spring中通常指代数据层方法，也可以是业务层方法

#### 事务相关配置

@Transactional有各种属性，事务只会在出现error和运行时异常才会回滚，其他异常不会回滚

```java
@Transactional(readOnly = true, timeout = -1) // 只读事务，永不超时
@Transactional(rollbackFor = {IOException.class}) // 设置IO异常也回滚
@Transactional(propagation = Propagation.REQUIRES_NEW)
```



## SpringMVC

### 创建SpringMVC

#### 配置tomcat

**tomcat7(JDK8)**

pom.xml

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>6.2.5</version>
</dependency>

<build>
    <plugins>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.1</version>
            <configuration>
                <port>80</port>
                <path>/</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

**tomcat10(SpringMVC6.0)**

*需要手动指定tomcat下载位置*

在pom.xml中加入`<packaging>war</packaging>`

pom.xml

```xml
<dependency>
    <groupId>jakarta.servlet</groupId>
    <artifactId>jakarta.servlet-api</artifactId>
    <version>5.0.0</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>6.2.5</version>
</dependency>
<dependency> // 启用导入json数据
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.18.3</version>
</dependency>
```

配置tomcat10

1. 在运行/配置中添加本地tomcat
2. 在pom.xml项目信息下添加`<packaging>war</packaging>`
3. 执行`mvn clean package`生成war包
4. war包移动到Tomcat 的 `webapps` 目录
5. 部署中点+号，选项目的war包路径，修改上下文路径为自己想要的
6. 启动tomcat

**初始化servlet容器**

ServletContainersInitConfig.class

```java
// 定义servlet容器启动的配置类，在里面加载spring的配置
public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
    // 加载springmvc容器配置
    @Override
    protected WebApplicationContext createServletApplicationContext() {
        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        ctx.register(SpringMvcConfig.class);
        return ctx;
    }
    // 设置哪些请求归springmvc处理
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
    // 加载spring容器配置
    @Override
    protected WebApplicationContext createRootApplicationContext() {
        return null;
    }
}
// 简化版
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    // 乱码处理
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter characterEncodingFilter = new CharacterEncodingFilter();
        characterEncodingFilter.setEncoding("UTF-8");
        return new Filter[]{characterEncodingFilter};
    }
}
```

SpringConfig.class

```java
// 创建springmvc的配置文件，加载controller对应的bean
@Configuration
@ComponentScan("org.example.controller")
@EnableWebMvc // 启动接收json功能
public class SpringMvcConfig {}
```

Controller.class

```java
@Controller // 声明为SpringMVC的核心控制器controller
public class UserController {
    @RequestMapping("/save")
    @ResponseBody // 设置controller的相应内容为当前返回值
    public String save() {
        System.out.println("user save ...");
        return "{'info':'springmvc'}";
    }
}
```

### 数据传递

**常规数据**

@RequestParam:用于查询参数

```java
@Controller
@RequestMapping("/user")
public class UserController {
    @RequestMapping("/save")
    @ResponseBody
    public String save(@RequestParam("name") String name, @RequestParam("age") int age) {
        System.out.println("name : "+name);
        System.out.println("age : "+age);
        return "{'info':'springmvc'}";
    }
}
```

**接收json数据转换成集合**

```java
@RequestMapping("/saveJson")
@ResponseBody
public String save(@RequestBody List<User> list) {
    System.out.println(list);
    return "{'info':'springmvc'}";
}
```

**按格式接收日期数据**

```java
@RequestMapping("/saveDate")
@ResponseBody
public String save(@DateTimeFormat(pattern = "yyyy-MM-dd")Date date) {
    System.out.println(date);
    return "{'info':'springmvc'}";
}
```

### REST风格

```java
@RestController // 相当于 @Controller + @ResponseBody
@RequestMapping("/users")
public class UserController {
    @RequestMapping(method = RequestMethod.POST)
    public String save() {
        System.out.println("users save ...");
        return "{'info':'save'}";
    }

    @RequestMapping(value = "/{id}", method = RequestMethod.DELETE)
    public String delete(@PathVariable(name = "id") Integer id) {
        System.out.println("delete " + id);
        return "{'info':'delete'}";
    }

    @RequestMapping(method = RequestMethod.PUT)
    public String update(@RequestBody User user) { // 记得为 User 类添加无参构造函数
        System.out.println("users update " + user);
        return "{'info':'update'}";
    }

    @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    public String getById(@PathVariable(name = "id") Integer id) {
        System.out.println("get id " + id);
        return "{'info':'getById'}";
    }

    @RequestMapping(method = RequestMethod.GET)
    public String getAll() {
        System.out.println("get all");
        return "{'info':'getAll'}";
    }
}
```

## SSM

### 创建SSM工程

pom.xml

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>6.2.5</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>6.2.5</version>
    </dependency>

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>6.2.5</version>
    </dependency>

    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.16</version>
    </dependency>

    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>3.0.4</version>
    </dependency>

    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <version>8.3.0</version>
    </dependency>

    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.20</version>
    </dependency>

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>jakarta.servlet</groupId>
        <artifactId>jakarta.servlet-api</artifactId>
        <version>5.0.0</version>
        <scope>provided</scope>
    </dependency>

    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.18.3</version>
    </dependency>
</dependencies>

<build>
    <finalName>SSM</finalName> <!-- WAR 包名 -->
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId> <!-- 自动部署 WAR 包 -->
            <artifactId>maven-war-plugin</artifactId>
            <version>3.3.2</version>
            <configuration>
                <outputDirectory>E:\software\JavaTools\apache-tomcat-11.0.2\webapps</outputDirectory>
            </configuration>
        </plugin>
    </plugins>
</build>
```

项目结构

- config
  - JdbcConfig
  - MyBatisConfig
  - ServletConfig
  - SpringConfig
  - SpringMvcConfig
  - SpringMvcSupport
- controller
  - interceptor 放拦截器
    - ProjectInterceptor

  - Code
  - Result
  - ProjectExceptionAdvice

- dao
- domain
- service
  - impl
- exception
  - BusinessException
  - SystemException

### 表现层与前端数据传输协议

Code.class

```java
package org.example.controller;

public class Code {
    public static final Integer SAVE_OK = 20011;
    public static final Integer DELETE_OK = 20021;
    public static final Integer UPDATE_OK = 20031;
    public static final Integer GET_OK = 20041;

    public static final Integer SAVE_ERR = 20010;
    public static final Integer DELETE_ERR = 20020;
    public static final Integer UPDATE_ERR = 20030;
    public static final Integer GET_ERR = 20040;

    public static final Integer SYSTEM_ERR = 50001;
    public static final Integer SYSTEM_TIMEOUT_ERR = 50002;
    public static final Integer SYSTEM_UNKNOWN_ERR = 59999;

    public static final Integer BUSINESS_ERR = 60002;
}
```

Result.class

```java
package org.example.controller;

public class Result {
    private Integer code;
    private Object data;
    private String msg;

    public Result(Integer code, Object data) {
        this.code = code;
        this.data = data;
    }

    public Result(Integer code, Object data, String msg) {
        this.code = code;
        this.data = data;
        this.msg = msg;
    }

    public Object getData() {
        return data;
    }

    public void setData(Object data) {
        this.data = data;
    }

    public Integer getCode() {
        return code;
    }

    public void setCode(Integer code) {
        this.code = code;
    }

    public String getMsg() {
        return msg;
    }

    public void setMsg(String msg) {
        this.msg = msg;
    }

    @Override
    public String toString() {
        return "Result{" +
                "data=" + data +
                ", code=" + code +
                ", msg='" + msg + '\'' +
                '}';
    }
}
```

### 异常处理

ProjectExceptionAdvice.class

```java
@RestControllerAdvice
public class ProjectExceptionAdvice {
    @ExceptionHandler(SystemException.class)
    public Result doSystemException(SystemException ex) {
        return new Result(ex.getCode(), null, ex.getMessage());
    }

    @ExceptionHandler(BusinessException.class)
    public Result doBusinessException(BusinessException ex) {
        return new Result(ex.getCode(), null, ex.getMessage());
    }

    @ExceptionHandler(Exception.class)
    public Result doException(Exception ex) {
        System.out.println("嘿嘿，异常你哪里跑！");
        return new Result(Code.SYSTEM_UNKNOWN_ERR, null, "嘿嘿，异常你哪里跑！");
    }
}
```



### 拦截器

SpringMvcSupport.class

```java
@Configuration
public class SpringMvcSupport extends WebMvcConfigurationSupport {
    @Autowired
    private ProjectInterceptor projectInterceptor;

    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/pages/**").addResourceLocations("/pages/");
        registry.addResourceHandler("/css/**").addResourceLocations("/css/");
        registry.addResourceHandler("/js/**").addResourceLocations("/js/");
        registry.addResourceHandler("/plugins/**").addResourceLocations("/plugins/");
    }

    @Override
    protected void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(projectInterceptor).addPathPatterns("/users");
    }
}

// 整合到SpringMvcConfig.class
@Configuration
@ComponentScan({"org.example.controller"})
@EnableWebMvc
public class SpringMvcConfig implements WebMvcConfigurer {
    @Autowired
    private ProjectInterceptor projectInterceptor;
    
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(projectInterceptor).addPathPatterns("/users");
    }
}
```

ProjectInterceptor.class

```java
@Component
public class ProjectInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle...");
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle...");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion...");
    }
}
```

## Maven

### 分模块开发

使用maven中的install能将工程内模块安装到maven的本地仓库内，然后在pom中导入即可实现分模块开发

### 依赖传递

依赖可以传递，相同的依赖，近的覆盖远的，新的覆盖旧的

### 可选依赖与排除依赖

**可选依赖（Optional Dependencies）**

目的：由依赖提供方（如项目B）决定是否传递某个依赖给下游项目（如项目A）

配置方式：在依赖声明中添加`<optional>true</optional>`标签

```xml
<dependency>
  <groupId>sample.ProjectB</groupId>
  <artifactId>Project-B</artifactId>
  <version>1.0</version>
  <optional>true</optional>  <!-- 标记为可选 -->
</dependency>
```

效果：若项目A依赖项目B，则项目A不会自动继承项目B中的可选依赖，需显式声明才能使用

**适用场景**

模块化功能隔离：例如项目B提供多个数据库驱动支持，但用户只需选择其一（如MySQL或Oracle），可将这些驱动设为可选依赖

避免冗余依赖：减少因传递性依赖导致的项目臃肿，例如热部署工具`spring-boot-devtools`常设为可选



**排除依赖（Dependency Exclusions）**

目的：由依赖使用方（如项目A）主动排除上游传递的某个间接依赖（如项目B依赖的C）

配置方式：在依赖声明中添加`<exclusions>`标签，

```xml
<dependency>
  <groupId>sample.ProjectB</groupId>
  <artifactId>Project-B</artifactId>
  <version>1.0</version>
  <exclusions>
    <exclusion>  <!-- 排除特定依赖 -->
      <groupId>sample.ProjectC</groupId>
      <artifactId>Project-C</artifactId>
    </exclusion>
  </exclusions>
</dependency>
```

效果：项目A完全排除项目B传递的依赖C，即使B本身依赖C

**适用场景**

解决版本冲突：例如项目A直接依赖C 2.0，但项目B传递了C 1.0，通过排除C 1.0避免冲突

兼容性问题：排除不兼容的第三方库，例如旧版日志框架或存在许可证冲突的依赖

### 依赖管理

1. 在父模块的 `<dependencyManagement>` 中声明依赖的 `groupId`、`artifactId` 和 `version`，子模块引用时无需重复指定版本，确保所有子模块使用同一版本。例如：

   ```xml
   <!-- 父模块 -->
   <dependencyManagement>
     <dependencies>
       <dependency>
         <groupId>org.springframework</groupId>
         <artifactId>spring-core</artifactId>
         <version>5.3.20</version>  <!-- 统一版本 -->
       </dependency>
     </dependencies>
   </dependencyManagement>
   
   <!-- 子模块 -->
   <dependencies>
     <dependency>
       <groupId>org.springframework</groupId>
       <artifactId>spring-core</artifactId>  <!-- 无需版本 -->
     </dependency>
   </dependencies>
   ```

   子模块若未显式声明版本，则自动继承父模块的版本

2. **避免依赖污染**

   `<dependencyManagement>`本身不会直接引入依赖到项目中，子模块需显式声明才能使用，避免了父模块中非必要依赖被所有子模块继承。

3. **解决传递依赖冲突**

   当依赖存在传递性冲突时（如模块 A 传递依赖 C 1.0，模块 B 传递依赖 C 2.0），父模块通过`<dependencyManagement>`声明版本后，子模块会优先使用该版本而非传递版本。

4. **简化子模块配置**

   子模块只需声明`groupId` 和`artifactId`，减少重复配置，提升可读性。例如：

   ```xml
   <!-- 子模块仅需声明依赖名称 -->
   <dependency>
     <groupId>mysql</groupId>
     <artifactId>mysql-connector-java</artifactId>
   </dependency>
   ```

### 聚合

> 聚合通过父项目的 `<modules>` 标签管理多个子模块的构建顺序，实现一键构建所有子模块。父项目本身不生成构建产物，仅作为构建协调者。

**父项目** 需设置 `<packaging>pom</packaging>`，并在 `<modules>` 中列出子模块路径：

```xml
<packaging>pom</packaging>
<modules>
    <module>../xxx</module> // 位置
</modules>
```

**统一构建流程**：通过 `mvn install` 一键构建所有子模块，无需逐个操作。

### 继承

> 继承允许子项目通过 `<parent>` 标签继承父项目的配置（如依赖、插件、版本等），避免重复配置。

- **父项目** 需设置 `<packaging>pom</packaging>`，并在 `<dependencyManagement>` 或 `<build>` 中定义公共配置。
- **子项目** 通过 `<parent>` 声明父项目，继承其配置：

```xml
<parent>
  <groupId>com.example</groupId>
  <artifactId>parent-project</artifactId>
  <version>1.0-SNAPSHOT</version>
  <relativePath>../pom.xml</relativePath>
</parent>
```

### 属性

1. **用户自定义属性**
   在`<properties>`标签中显式定义，用于集中管理版本号、编码格式等配置。例如：

   ```xml
   <properties>
     <junit.version>5.8.2</junit.version>
     <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   ```

   引用方式：`${junit.version}`

2. **内置属性**
   Maven预定义的属性，直接引用无需声明

   `${project.basedir}`：项目根目录（含`pom.xml`的路径）

   `${project.version}`：项目版本号

   `${maven.build.timestamp}`：构建时间戳（支持自定义格式）

### 多环境开发

1. 在`pom.xml`中为每个环境创建`<profile>`，并通过`<properties>`设置环境参数

   ```xml
   <profiles>
     <!-- 开发环境 -->
     <profile>
       <id>dev</id>
       <properties>
         <env>dev</env>
         <server.port>8080</server.port>
         <jdbc.url>jdbc:mysql://localhost:3306/dev</jdbc.url>
       </properties>
       <!-- 默认激活 -->
       <activation>
         <activeByDefault>true</activeByDefault>
       </activation>
     </profile>
     <!-- 生产环境 -->
     <profile>
       <id>prod</id>
       <properties>
         <env>prod</env>
         <server.port>8082</server.port>
         <jdbc.url>jdbc:mysql://prod-server:3306/prod</jdbc.url>
       </properties>
     </profile>
   </profiles>
   ```

2. **配置资源过滤**
   启用资源过滤以替换配置文件中的占位符

   ```xml
   <build>
     <resources>
       <resource>
         <directory>src/main/resources</directory>
         <!-- 开启过滤 -->
         <filtering>true</filtering>
         <includes>
           <include>*.properties</include>
         </includes>
       </resource>
       <!-- 按环境加载配置文件 -->
       <resource>
         <directory>src/main/resources/env/${env}</directory>
         <filtering>true</filtering>
       </resource>
     </resources>
   </build>
   ```

3. **激活Profile**

   命令行激活：`mvn clean package -P dev`**默认激活**：通过`<activation>`标签设置默认环境

### 私服

#### 安装nexus

到nexus目录下输入命令

```cmd
nexus.exe /run nexus
```

#### 访问

地址：`http://localhost:8081/`

| 仓库级别 | 英文名称 | 功能                    | 关联操作 |
| -------- | -------- | ----------------------- | -------- |
| 宿主仓库 | hosted   | 保存自主研发+第三方资源 | 上传     |
| 代理仓库 | proxy    | 代理连接中央仓库        | 下载     |
| 仓库组   | group    | 为仓库编组简化下载操作  | 下载     |

**本地仓库访问私服权限设置**

在maven的setting.xml中添加

```xml
<servers>
	<server>
      <id>deploymentRepo</id> // 写仓库名称
      <username>repouser</username>
      <password>repopwd</password>
    </server>
</servers>
```

地址设置，在setting.xml中

```xml
<mirrors>
	<mirror>
      <id>mirrorId</id>
      <mirrorOf>repositoryId</mirrorOf> // 直接写*就是全部
      <name>Human Readable Name for this Mirror.</name> // 可以省略
      <url>http://my.repository.com/repo/path</url> // 地址
    </mirror>
</mirrors>
```

工程上传到私服设置，在pom.xml中

```xml
<distributionManagement>
    <repository> // 发布版本
        <id></id>
        <url></url>
    </repository>
    <snapshotRepository> // 快照版本
        <id></id>
        <url></url>
    </snapshotRepository>
</distributionManagement>
```

配置完maven后运行`mvn deploy`上传到私服



