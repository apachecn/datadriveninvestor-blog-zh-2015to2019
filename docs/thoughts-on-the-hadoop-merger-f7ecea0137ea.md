# 关于 Hadoop 合并的思考

> 原文：<https://medium.datadriveninvestor.com/thoughts-on-the-hadoop-merger-f7ecea0137ea?source=collection_archive---------16----------------------->

最近，Hortonworks 和 [Cloudera](https://medium.com/u/89133b725092?source=post_page-----f7ecea0137ea--------------------------------) 都宣布了一项[合并](https://www.cnbc.com/2018/10/05/cloudera-ceo-on-hortonworks-merger-could-be-oracle-of-the-future.html)，这在上周震动了大数据和技术领域——我承认这是我没有预料到的举动。鉴于 Hortonworks 一直站在开源和 Cloudera 的支柱上，坚持企业就绪和受支持的模式，这两个 Hadoop 巨头似乎无法找到共同的战略基础，尽管他们吹嘘自己的核心功能是相同的。然而，剥开表面，这看起来比我原来想象的更有意义。

**转向开源**

Hortonworks 长期以来一直支持开源社区，并致力于在新组件可用时将其集成到 GA 版本中，而 Cloudera 采取了更保守的方法。如果合并导致新公司采用开源方法，许多客户将获得可用技术的大幅升级，并可能满足现有客户希望转向更开放平台的需求。

**单个低延迟查询和执行选项**

从这个角度来看，在 Tez 和 LLAP 的 Hortonworks 以及 Cloudera 的 Impala 和 Kudu 的合并中，有许多选择。迄今为止，Tez 和 Impala 一直是天然的竞争对手，Hortonworks LLAP 技术为 Hadoop 平台带来了 ACID 合规性。当然，它们在未来的平台上都有一席之地，然而哪一个会胜出呢？我猜这三者的某种组合将最终带来 ACID 遵从性和低延迟查询访问。现有客户转移到新平台所需的任何叉车都是一个问题。有多少顾客依赖 Impala 桌子？LLAP 表？没有技术开发中心就无法在特定服务水平协议下执行的处理？Tez 在开源社区中的路线图是什么，最近提交的数量是多少？Kudu 被很多客户采用了吗？他们的用例能容易地移植到 LLAP 表上吗？

这些问题的答案以及仔细的技术差距分析将推动决策。我预测 LLAP 和 Impala 将以某种混合的方式继续存在，随着平台继续向 Spark 计算和流媒体架构迁移，Tez 将逐渐淡出市场。

**走向流媒体平台**

我认为合并的一个直接好处是，现有的 Cloudera 客户将获得基于 Apache NiFi 的 Hortonworks DataFlow ( [HDF](https://hortonworks.com/products/data-platforms/hdf/) )的功能。这款功能极其强大的工具为 Hadoop 生态系统带来了实时和流媒体功能，并有助于通过两个平台都支持的开源 Kafka 抽象出一些编排流媒体管道的复杂性。

此外，Hadoop 平台作为一个整体，迫切需要跟上许多客户对实时平台的需求。此次合并将为两家公司提供一个机会，整合他们的人才基础，努力将 Hadoop 产品扩展到不仅仅是 HDFS 和批处理分析，将我们在过去 10 年中所熟知的 Hadoop 平台带入下一个阶段。

**改变 Hadoop 商业模式**

最后，Hadoop 在很大程度上是一种本地批量分析解决方案。虽然有希望扩展到云，在分布式低成本平台上实现实时和低延迟的数据访问，但这对大多数客户来说还没有成为现实。希望 Hortonworks 和 Cloudera 能够在这次合并中走到一起，解决这些问题，将“Hadoop”再次带到大数据技术领域的前沿，并使该平台超越其最初的意图。

在接下来的几天、几周和几个月里，我们肯定会密切关注此事…

*更多大数据思想和文章，关注我*[*Twitter*](http://www.twitter.com/geoffbaird_)*@ geoffbaird _*