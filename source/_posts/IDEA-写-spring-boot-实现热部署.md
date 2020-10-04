---
title: IDEA 写 spring boot 实现热部署
date: 2020-10-02 15:57:31
tags: 
- idea
- spring boot 
categories: spring boot 学习
comments: true
---

这里使用的是 devtools

<!-- more -->

## 引入依赖

在 pom.xml 中引入指定的依赖
![图片](img1.png)

## 修改配置文件

按下 <kbd>ctrl</kbd>+<kbd>shift</kbd>+<kbd>alt</kbd>+<kbd>/</kbd>，选择Registry进入配置界面

![图片](img2.png)

找到下图红框中的选项，打上勾

![图片](img3.png)

至此即可完成热部署的配置了，此后当修改类文件时，只需在运行情况按下 <kbd>ctrl</kbd>+<kbd>F9</kbd>即可
