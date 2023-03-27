# Java 持久性 API，JPA(第 1 部分)

> 原文：<https://medium.datadriveninvestor.com/java-persistence-api-jpa-part-1-f2685e348b8a?source=collection_archive---------8----------------------->

![](img/1b449943e9ff41d59065ba72b4eaac77.png)

所有技术中最关键的通用组件之一是收集、分析和服务数据的能力。从游戏、物联网、移动应用到企业解决方案的软件解决方案都有一个共同的组成部分；数据存储、管理和检索。

> 当我第一次开始学习代码时，我还不知道这可能会变成一种职业，我开始了第一个宠物项目，我称之为 iNBox ( [*)所有的代码仍然在我的 Github*](https://github.com/samuelowino) 上。我立即开始研究 iNbox——一种通用的消息传递解决方案——我突然意识到我需要存储大量的数据。

这种情况发生在所有的软件开发人员身上，我想，在我们职业生涯的早期，我们自然会被引导去学习特定的知识体系，而没有人真正告诉我们需要掌握这些知识或技能。

[](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) [## 6 雅虎金融应用编程接口的替代方案|数据驱动型投资者

### 对于许多数据驱动型投资者来说，雅虎财务应用编程接口一直是一个可靠的工具。许多人依靠他们的…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) 

使用企业 java，我们确实需要学习如何使用数据库——另一个庞大的知识体系值得拥有自己的系列文章。但是，在本文中，我们将研究一种允许我们忽略数据库解决方案提供者的解决方案(Oracle、Postgres、MongoDB 和数以千计的其他数据库发行版)。像 Hibernate 这样的框架已经通过对象关系映射(ORM)的概念解决了这个问题。

## JPA 与 Hibernate ORM 的关系

![](img/71026f670f3abf47eb8b07c5ac49b62a.png)

[Rick And Morty Season 4, Episode 3 Recap: Algorithmic Plot Twists Aplenty, Forbes](https://www.forbes.com/sites/danidiplacido/2019/11/25/rick-and-morty-season-4-episode-3-recap-algorithmic-plot-twists-aplenty/#1fec01214ce1)

JPA 提供了对特定 ORM 的抽象。它提供了由 ORM(在本例中为 Hibernate)实现的 API。JPA 是特定 ORM 的接口，它将把函数委托给底层数据库，例如 MySQL。

*使用 JPA 的优势在于，它允许您在不改变 api 代码的情况下* ***替换底层的 ORM*** *，更像是能够在不重新定义模式的情况下改变底层的数据库。*

这给我们带来了软件工程的一个重要原则，它启发了 JPA 和诸如 Hibernate 之类的 ORMs，即-**“关注点分离(SoC)原则”。—** SoC 是一种将计算机程序分成不同部分的设计原则，这样每个部分都解决了一个单独的**问题。**您的软件解决方案的组件应该彼此分离，因此具有最低级别的依赖性。

## **本系列报道的内容**

![](img/615dbe0e0dbf4f53b5f2a65b1b0c2808.png)

[‘Rick and Morty’ “Elon Tusk” finally explains a mysterious Elon Musk tweet](https://www.inverse.com/article/61202-rick-and-morty-elon-tusk-musk-season-4-episode-3-one-crew-over-the-crewcoo-s-morty)

Java Persistence API 为开发人员提供了一个对象/关系映射来管理 Java 应用程序中的关系数据。我们将在下一组文章中涵盖以下 JPA 的关键领域；

*Java 持久性 API 实体*

*实体继承*

*管理实体*

*查询实体*

*对象关系映射元数据*

## 进一步的信息

除了这一系列文章之外，您还可以在这些正式文档中找到更多关于 Java 持久性的信息。

[Java 持久性 2.1 API 规范](http://jcp.org/en/jsr/detail?id=338)

[Eclipse Link，GlassFish 服务器中的 Java 持久性 API 实现](http://www.eclipse.org/eclipselink/jpa.php)

[EclipseLink 团队博客](http://eclipselink.blogspot.com/)

[EclipseLink 维基文档](http://wiki.eclipse.org/EclipseLink)

支持我，看看我的小应用:[人生规划师](https://thelifeplanner.co)

干杯！