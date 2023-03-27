# 容器的安全问题

> 原文：<https://medium.datadriveninvestor.com/security-issues-with-containers-c253b43e4eca?source=collection_archive---------15----------------------->

可配置和版本化的容器即服务是一个新的现实。

忽视它们，后果自负。

我们将在这里讨论两种最流行的技术。

# 码头工人

**背景**

Docker 曾经是一场新的革命。

在撰写本文时，许多操作系统都可以运行 docker。

因此，我们可以在任何平台上以不变的**方式运行任何操作系统和应用程序。**

例如，我们的 Java 应用程序包堆栈可以是

> 我们的操作系统:MacOS
> 
> 我们的形象:阿尔卑斯山的爪哇[见[这里](https://hub.docker.com/r/anapsix/alpine-java/)和 dockerfile [这里](https://hub.docker.com/r/anapsix/alpine-java/~/dockerfile/)
> 
> 我们的应用:任何基于 java 的应用

现在我可以了

1.  创建上面的不可变图像
2.  在我们的 Mac 上运行并测试它
3.  我们把它上传到 DockerHub
4.  任何人都可以下载图像并获得完全相同的可重复结果。

这对任何工程师来说都非常方便。

**版本**

Docker 有一个 Docker 文件，可以帮助描述和构建图像。

因为它是文本文件，所以可以对其进行版本控制。

参见示例文档[此处](https://hub.docker.com/r/anapsix/alpine-java/~/dockerfile/)。

**码头工人的问题**

操作系统漏洞是不断被发现的。

在这里看看 2018 年的几个 Linux 漏洞

[https://resources . white source software . com/blog-white source/top-5-Linux-kernel-vulnerabilities-in-2018](https://resources.whitesourcesoftware.com/blog-whitesource/top-5-linux-kernel-vulnerabilities-in-2018)

其中一些比其他的更服务器，在上面的链接中，我们有一些可以导致拒绝服务攻击的东西。换句话说，如果恶意黑客利用该漏洞使您的服务瘫痪，您的服务可能无法访问。

**这跟 docker 有什么关系？**

由于我们的映像是不可变的，让我们想想，如果在操作系统或 JDK 中发现并修复了安全或其他漏洞，会发生什么？

我们的形象现在已经修复，但我确实需要修复漏洞

我们将需要保持我们的图像是最新的，或者换句话说，我们将需要在每次看到需要修复的漏洞时创建一个新的图像。

在这里详细阅读

[](https://sysdig.com/blog/7-docker-security-vulnerabilities/) [## Sysdig | 7 Docker 安全漏洞和威胁

### Docker 安全:安全监控和安全工具正成为现代 IT 世界的热门话题，因为早期…

sysdig.com](https://sysdig.com/blog/7-docker-security-vulnerabilities/) 

事实上，DockerHub 上的许多图像可能并不安全；-)

[](https://www.theregister.co.uk/2018/06/14/docker_security_dodgy_container_images/) [## 码头枢纽安全纠纷，狡猾的集装箱图像数据该死

### 周三在旧金山的 DockerCon 上，首席执行官史蒂夫·辛格强调安全性是 Docker 的核心原则之一…

www.theregister.co.uk](https://www.theregister.co.uk/2018/06/14/docker_security_dodgy_container_images/) 

# **Kubernetes**

**背景**

正如所见，docker 有助于创建部署我们的应用程序的映像。

如果我需要我们的应用程序进行扩展，该怎么办？我需要我们的应用程序的 10 个实例。如果我需要在不停机的情况下推出我们码头应用程序的新图像，该怎么办？如果我们的服务需要一个数据存储，一个特定的网络来与其他服务交流，发现新的服务。

Kubernetes 做了以上所有的事情，甚至更多。

此外，它从容器中抽象出硬件。不管我们是在 Oracle 硬件上运行，还是在 Amazon AWS 硬件上运行，还是在 Goggle cloud 硬件上运行，甚至是在定制的英特尔硬件上运行，都没有多大关系。

只要我们运行 Kubernetes，我们就可以使用相似的文件以完全相同的方式部署我们的应用程序。我说相似是因为云供应商之间有一些细微的差别，但是它们之间的差距并不是很大。

正如我们有一个 docker 文件一样，Kubernetes 有描述部署的 YAML 文件。因为它是文本文件，所以可以对其进行版本控制。看到下面一篇好文章:

[](https://www.mirantis.com/blog/introduction-to-yaml-creating-a-kubernetes-deployment/) [## YAML 简介:创建 Kubernetes 部署| Mirantis

### 在以前的文章中，我们一直在讨论如何使用来加速资源。到目前为止，我们一直在专门工作…

www.mirantis.com](https://www.mirantis.com/blog/introduction-to-yaml-creating-a-kubernetes-deployment/) 

Kubernetes 本身的一个很好的介绍:

[](https://www.infoworld.com/article/3268073/containers/what-is-kubernetes-container-orchestration-explained.html) [## 什么是 Kubernetes？解释了容器编排

### 容器的兴起重塑了人们对开发、部署和维护软件的思考方式。绘图…

www.infoworld.com](https://www.infoworld.com/article/3268073/containers/what-is-kubernetes-container-orchestration-explained.html) 

**Kubernetes 问题**

嗯，这和我们在软件的其他方面犯的错误是一样的。

例如:

1.  对于 MySql 服务器安装，保留相同的默认值
2.  将互联网路由器凭据保留为 admin/admin
3.  将安全摄像机凭证保留为管理员/管理员

这里有一篇很好的文章，详细介绍了 Kubernetes 在黑客方面的安全性。

[](https://techbeacon.com/hackers-guide-kubernetes-security) [## Kubernetes 安全黑客指南| TechBeacon

### Kubernetes 安全黑客指南在过去几年里，Kubernetes 在技术领域大放异彩…

techbeacon.com](https://techbeacon.com/hackers-guide-kubernetes-security)