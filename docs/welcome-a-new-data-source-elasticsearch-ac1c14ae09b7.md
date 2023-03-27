# 欢迎一个新的数据源——弹性搜索

> 原文：<https://medium.datadriveninvestor.com/welcome-a-new-data-source-elasticsearch-ac1c14ae09b7?source=collection_archive---------23----------------------->

[![](img/c7718b5573b1836511e635ea89e33e28.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/d910b20c1e01d2ab54fab7f4beb0303d.png)

你可能已经注意到，今年充满了新奇的事物:*两个主要的发布版本丰富了新的用户界面、分析特性和安全改进。*

因为跟上大数据分析的最新趋势在不断发展的世界中至关重要，所以我们专注于扩展可以连接到数据透视表的数据源。

因此，我们很高兴推出用于弹性搜索的测试版 **Flexmonster 数据透视表&图表**。最终的稳定版本将在下一个主要的 2.7 版本中推出。很快就要发布了，请关注我们博客上的更新。

# 为什么这对你很重要

每个报告背后都有一个数据源。它是分析的基础。我们的主要目标是借助 Flexmonster 的搜索功能和分析功能，将您的网络报告体验提升到一个全新的水平。

很有前途的组合，不是吗？

# 为什么这对我们很重要

我们尽最大努力为您提供一流的弹性搜索数据分析体验，并帮助您将原始数据转化为极具洞察力的商业信息。这是迈向**大数据分析**的重要一步。

![](img/e5632d330d48f300e9bab129e1d2f502.png)

# 什么是弹性搜索

Elasticsearch 被誉为科技界最杰出的全文搜索引擎之一。此外，它是免费和开源的。Elasticsearch 是关于高性能搜索、实时可见性、可靠性和灵活性的。

世界上最大的公司采用 **Elasticsearch** 、 **Logstash** 和**Kibana**(**ELK**)**Stack**来获取商业智能、网站流量和客户支持。它的使用范围很广:医疗保健、教育、政府、电信行业的公司都在使用 ELK 进行搜索。更重要的是，Elasticsearch 作为实时分析的引擎，甚至为 NASA 的项目做出了贡献。

它的使用几乎无处不在——即使是现在，当你阅读这篇文章的时候，ELK 栈也在努力检测介质上的任何 DynamoDB 热点。

我们认为搜索的未来是弹性搜索——不管你从事什么行业。调查显示，它是十大最受欢迎的数据库管理系统之一。

# 为什么使用 Elasticsearch

随着企业规模的扩大，您的数据也在增加。为了不让你被它的数量淹没，Elasticsearch 帮助你存储数据，搜索数据并进行特别分析。此外，您可以使用它进行日志分析，以确定应用程序或服务器的问题。

作为一名开发人员，您可能会欣赏 Elasticsearch 的以下优点:

*   支持水平扩展的分布式特性
*   面向文档的存储实体系统
*   异常快速的查询执行
*   动态全文搜索搜索
*   RESTful API

还有更多。

关于用户体验优势，您肯定会喜欢 ELK 及其支持社区的丰富文档。

## 数据类型

Flexmonster 支持弹性搜索的核心数据类型，如**字符串**(所有维度均视为关键字)**日期**、**数字**、**布尔**和复杂类型:**对象**和**嵌套对象**。这就是为什么不需要担心数据的一致性和兼容性——flex monster 会自动处理数据类型。

# 为什么需要将 Elasticsearch 与 Flexmonster 结合使用

Flexmonster 为您提供了一个内置的 Elasticsearch 连接器，允许您从索引中探索数据，并通过可视化获得宝贵的见解。

# 如何开始使用 Elasticsearch 和 Flexmonster

在您的机器上安装了Elasticsearch 并连接到服务器后(有关更多详细信息，请参见[官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/6.2/install-elasticsearch.html))，让我们继续设置从 Flexmonster 到 Elasticsearch 的连接。

开始分析您的 Elasticsearch 数据只需要三个步骤:将组件嵌入到 web 项目中，从 Flexmonster 连接到您的索引，并使用 JavaScript API 配置报告。整个过程非常省时。在 [**Flexmonster 包**](https://www.flexmonster.com/download-page/?r=di) 中找到完整的指南。

# 安全性如何

Flexmonster 支持 HTTP 基本认证机制，该机制对从浏览器发送到服务器的索引凭证进行编码(但不加密)。此外，Flexmonster 是一个完全客户端的组件，它不会将您的数据存储在服务器上，因此，除了您之外，没有人可以访问您的数据。但是我们建议为您的 web 应用程序添加更多级别的保护。最佳实践包括:

*   启用 HTTPS 并将所有流量重定向到它。HTTPS 对数据进行加密，防止数据被截获后被检查。
*   为用户和用户组定义权利和权限
*   创建一个代理来检查来自 Flexmonster 的请求，并根据用户访问权限允许或拒绝这些请求
*   向请求添加自定义标头(访问令牌)以标识用户。

# 现场演示

通过 [**现场演示**](http://www.flexmonster.com/demos/connect-elasticsearch/?r=di) 获得第一手经验，了解 Flexmonster 的报告和可视化功能。

![](img/ca51d5016ec6a834dec1edb1d3a99d52.png)

# 认可和反馈

我们的客户是我们灵感的来源。

您的想法和我们将想法变为现实的坚持会产生协同效应。

率先测试和探索新测试版**flex monster&elastic search**的全部功能。选择 Elasticsearch 作为数据源，并[下载软件包](https://www.flexmonster.com/download-page/?r=di)以访问所有新功能。

请在下面的评论中告诉我们你对新数据源的体验。

您的测试和反馈将帮助我们改进测试版的功能。