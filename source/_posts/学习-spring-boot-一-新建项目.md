---
title: 学习 spring boot (一) 新建项目
date: 2020-09-30 20:27:41
tags: 
  - spring-boot
  - java
categories: spring boot 学习
comments: true
---
上来我直接列出 spring boot 的优点:

* 遵循"约定大于配置"的原则，简化了配置：
  * 牺牲了一定了灵活性，但是统一约定统一配置，适合整体管理
* 完全脱离 xml 配置，可以使用注解和 java config 进行配置
* 内嵌了 Servlet 容器，应用可以用 jar 包执行 (java -jar)
* 能快速构建项目、整合第三方类库，方便易用
* 提供了 starter POM，可以方便的进行包管理，简化包管理配置
* 于 spring cloud 相通，spring boot 是目前 java 体系内实现微服务的最佳方案
<!-- more -->

IDE当然是 IDEA 啦，不用Eclipse哈。

## 新建项目

点击新建项目，记得选择 Spring Initializr

![图片](img1.png)

![图片](img2.png)

然后进入依赖选择，这里选择最基本的 Spring Web 了，其他的以后再讲

![图片](img3.png)

创建完之后，选择左边的项目目录，下图中高亮的几个文件可以删除，因为在使用 IDEA 这个编辑器，我们可以通过右边栏有个专门管理 maven 的模块使用

![图片](img4.png "可以删除的文件")

![图片](img5.png "maven 模块")

在 pom.xml 文件中，我们可以看到刚刚勾选的依赖 spring-boot-starter-web 已经导入到项目中了

![图片](img6.png "spring-boot-starter-web")

至此项目创建完成

## 编写一个简单的 controller

 <kbd>Alt</kbd>+<kbd>insert</kbd> 或者右键选择 New，创建一个 controller 文件夹，并用同样的方法创建一个 HelloController.java 在该文件夹下

![图片](img7.png "创建文件夹和文件")

给 HelloController 类加上注解 @RestController，并且编写一个 hello 方法，该方法拥有一个 name 参数 并返回 hello world 和 name 的组合，并给该方法加上一个对外服务的路径 @RequestMapping("/hello")，这样一个简单的 spring boot 的服务接口就完成了

![图片](img8.png "添加注解和方法")

## 显示效果在此

![图片](img9.png "效果")

![图片](img10.png "效果2")

## 项目结构

``` html
first
├─.idea
│  ├─codeStyles
│  └─libraries
├─.mvn
│  └─wrapper
├─src
│  ├─main
│  │  ├─java
│  │  │  └─com
│  │  │      └─pjboy
│  │  │          └─first
│  │  │              └─controller
│  │  └─resources
│  │      ├─static
│  │      └─templates
│  └─test
│      └─java
│          └─com
│              └─pjboy
│                  └─first
└─target
    ├─classes
    │  └─com
    │      └─pjboy
    │          └─first
    │              └─controller
    ├─generated-sources
    │  └─annotations
    ├─generated-test-sources
    │  └─test-annotations
    └─test-classes
        └─com
            └─pjboy
                └─first
```