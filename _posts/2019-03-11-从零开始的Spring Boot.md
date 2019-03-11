---
layout: post
title: 从零开始的spring boot
category: spring boot
tags: [spring boot]
---

现如今，你要是不会`Spring Boot`你都不好意思说自己是做Java开发的，`Spring Boot`已然成为每个Java程序员必学的一项基本功。

## 快速入门
### 开发环境
首先我使用的开发工具是[IntelliJ IDEA](http://www.jetbrains.com/idea/download/#section=windows)，非常好用的集成开发环境。IntelliJ在业界被公认为最好的java开发工具之一，尤其在智能代码助手、代码自动提示、重构、J2EE支持、Ant、JUnit、CVS整合、代码审查、 创新的GUI设计等方面的功能可以说是超常的.

### 构建Maven项目
在IDEA中分为`Project`和`Module`，`Project`类似于Eclipse的workspce，`Module`类似于Eclipse的`project`,所以我们先创建好`Project`，之后选择`File->New->Module`，选择`Spring Initializr`，然后Next，在本次开发中，设置`Group`为`com.example`，`Artifact`为'demo',其他为默认选项，一路Next知道建立完成，此时项目结构如下所示
![](https://raw.githubusercontent.com/MGXT/repository/master/spring/92SES887TFXI5.png)
