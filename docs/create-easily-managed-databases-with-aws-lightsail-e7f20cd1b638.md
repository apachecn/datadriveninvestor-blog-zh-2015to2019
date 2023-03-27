# 使用 AWS Lightsail 创建易于管理的数据库

> 原文：<https://medium.datadriveninvestor.com/create-easily-managed-databases-with-aws-lightsail-e7f20cd1b638?source=collection_archive---------41----------------------->

![](img/0e1662af95ba4fbb7a55ddcc3710350b.png)

最近，亚马逊网络服务公司[宣布增加一项名为 AWS Lightsail](https://aws.amazon.com/blogs/aws/new-managed-databases-for-amazon-lightsail) 的服务。众所周知，Lightsail 是一种可以轻松创建服务器实例和管理网络操作的服务。令人兴奋的消息是，Lightsail 现在还提供了在几次点击之内创建完全托管的数据库的能力。

在自我维护的数据库上拥有一个完全托管的数据库会很方便，因为您不需要对实例本身进行任何维护。AWS 为您处理大部分事情，您只需要担心数据库中的实际数据。

[建立一个 Lightsail 数据库是一个快速而深思熟虑的过程。](https://lightsail.aws.amazon.com/ls/webapp/create/database)这归结于为您的数据库实例选择一个具有安全性、可用性和冗余选项的基本配置。每种配置都有固定的月价格，包括:实例、SSD 存储和数据传输。Lightsail 需要几分钟来创建数据库实例。之后，您可以连接、查看指标、日志和配置网络设置。
如果你想在 AWS 之外连接到你的数据库，你必须启用“公共模式”默认情况下，公共模式是禁用的，因此只允许来自同一 AWS 区域中的 Lightsail 资源的连接。如果启用了“公共模式”,任何拥有数据库用户名和密码的人都可以连接到您的数据库。通常，这不是您想要的，并且可能会带来安全风险。

默认情况下，通过 Lightsail 创建的每个数据库实例都有一个自动备份系统。数据存储 7 天，并为您提供时间点恢复选项。除此之外，Lightsail 允许您创建数据库的手动快照。

在撰写本文时，AWS 仅支持 MySQL 数据库引擎的最新两个版本。AWS 宣布他们将很快增加对 PostgreSQL 的支持。AWS Lightsail 数据库在所有支持 Lightsail 的地区都可用。

# 结论

如果您需要为测试或开发目的建立一个快速数据库，Lightsail 数据库可能会非常有用。它非常适合这类用例的需求。它成本低，安装非常快速和容易。
如果您有一个严肃的生产数据库用例，那么您最好使用 AWS RDS。托管关系数据库服务(RDS)为您提供了更多的功能，并且可以进行更详细的配置。然而，它有点贵，但回报也很多。