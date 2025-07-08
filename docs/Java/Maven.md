---
title: Maven
createTime: 2025/07/08 17:03:15
permalink: /article/orvw2pve/
---
# Maven

> 标准化的项目结构，标准化的构建流程，方便的依赖管理。

## 下载和配置

[Download Apache Maven – Maven](https://maven.apache.org/download.cgi)
在环境变量中新建`MAVEN_HOME`并加上路径，在Path里添加`%MAVEN_HOME%\bin`
在`cmd`中输入mvn -version验证

**修改maven本地仓库位置**
在maven的`conf`文件夹下的settings.xml文件中找到`localRepository`添加类似这样的，并创建`mvn_resp`文件夹

```xml
<localRepository>E:\software\JavaTools\apache-maven-3.9.9\mvn_resp</localRepository>
```

**配置阿里云私服**
阿里云私服官网：[仓库服务](https://developer.aliyun.com/mvn/guide)

**IDEA导入maven项目**
在IDEA中，选择File-Open-Project，选择pom.xml文件即可。

## Maven坐标

> 资源的唯一标识

groupld：定义当前Maven项目隶属组织名称（通常是域名反写，例如：colm.baidu)
artifactId：定义当前Maven项目名称（通常是模块名称，例如order-service、goods-service)
version：定义当前项目版本号

## Maven的生命周期

clean：清理项目
default：默认的生命周期，相当于clean、site、validate、compile、test、package、verify、install、deploy。
site：生成项目报告
compile：编译项目
test：测试项目
package：打包项目
install：安装项目
deploy：部署项目
**执行后面的命令会自动执行前面的命令**

## 依赖管理

### 依赖配置

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>
```

**导入本地没有的依赖**
访问：[Maven Repository: Search/Browse/Explore](https://mvnrepository.com/)
**IDEA搜索自动导入**
alt + insert

### 依赖范围

`<dependency>`里的`<scope>`标签
scope：依赖的范围，可选值有compile、test、provided、runtime、system、import。
compile（默认）、test、provided(主程序，测试时运行)、runtime(测试，打包时运行)、system。