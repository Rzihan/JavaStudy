# MAVEN

## 1、mevan介绍以及环境搭建

### 1.1、概念

Maven是基于项目对象模型(POM),可以通过一小段描述信息来管理项目的构建、报告和文档的软件项目管理工具。

### 1.2、maven的安装目录

*  boot目录包含一个类加载器的框架。
*  bin目录主要是一些运行的脚本。
*  conf是配置文件目录。
*  lib包含一些需要用到的类库

### 1.3、配置环境变量

* M2_HOME 值为maven的安装目录
* PATH的值 D:\apache-maven-3.2.1\bin

## 2、Maven的文件结构和第一个HelloWorld

### 2.1、文件结构

```
-src
	-main
		-java
			-package
	-test
		-java
			-package
	-resources
```

### 2.2、poe.xml的配置

```xml
<?xml version="1.0" encoding="utf-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
		 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		 xsi:schemaLocation="http://maven.apche.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.imooc.maven01</groupId>
	<artifactId>maven01-model</artifactId>
	<version>0.0.1-SNAPSHOT</version>
    
<dependencies>
	<dependency>
		<groupId>junit</groupId>
		<artifactId>junit</artifactId>
		<version>4.10</version>
	</dependency>
</dependencies>

</project>
```

* 其中groupId的值就是包名

### 2.3、几个简单的命令

* mvn compile 编译
* mvn test 运行测试
* mvn package 项目打包

## 3、maven的常见构建命令

```
mvn  -v 查看maven版本
	 compile 编译
	 test 测试
 	 package 打包

clean 删除target
install 安装jar包到本地仓库
```

## 4、maven自动建立目录骨架

```
mvn archetype:generate 按照提示进行选择
mvn archetype:generate -DgroupId=组织名，公司网址的反写+项目名字 
	-DartifactId=项目名-模块名
	-Dversion=版本号
	-Dpackage=代码所踩在的包名

* -DarchetypeCatalog=internal 解决卡顿的问题
```

## 5、maven中的坐标和仓库

```
坐标：构件
仓库：
	中央仓库：http://repo.maven.apache.org/maven2
	本地仓库：
更改仓库地址：<localRepository>D:\myFile\maven\repos</localRepository>
```

## 6、maven的生命周期和插件

### 6.1、完整的项目构建过程包括：

清理、编译、测试、打包、集成测试、验证、部署

### 6.2、maven生命周期：

```
clean 清理项目
default 构建项目
site 生成项目站点
```



