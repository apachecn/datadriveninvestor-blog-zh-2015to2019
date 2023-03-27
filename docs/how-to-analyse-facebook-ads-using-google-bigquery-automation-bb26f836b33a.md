# 如何使用 Google BigQuery Automation 分析脸书广告

> 原文：<https://medium.datadriveninvestor.com/how-to-analyse-facebook-ads-using-google-bigquery-automation-bb26f836b33a?source=collection_archive---------5----------------------->

脸书广告是当今成功的数字广告形式之一，目前有超过 700 万广告客户在该平台注册。此外，67%的数字营销人员认为脸书是他们业务的首选社交媒体渠道。根据 [2019 社交媒体营销](https://medium.com/@JBBC/10-key-findings-from-the-2019-social-media-marketing-industry-report-9ffb95b33926)报告，脸书是 72%的 B2C 营销公司和 43%的 B2B 公司的首选广告渠道。

![](img/2a8bb4a40a23af72a6cc7b11daec4092.png)

无论是单个(或多个)商业广告还是整个广告活动，脸书广告都在为 B2B 和 B2C 营销者创造价值。除此之外，脸书广告数据是商业决策的丰富分析和洞察力的宝贵来源。然而，如果没有合适的自动化工具，处理脸书数据可能是一件耗时且昂贵的事情。这就是脸书广告对 BigQuery 自动化起着至关重要作用的地方。

作为一个数据仓库解决方案， [Google BigQuery](https://cloud.google.com/bigquery/) 通过其快速执行的类似 SQL 的查询引擎实现大数据查询，该引擎可以处理数 Pb 的数据。

[](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) [## 为什么数据将改变投资管理|数据驱动的投资者

### 有人称之为“新石油”虽然它与黑金没有什么相似之处，但它的不断商品化…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) 

在接下来的章节中，我们将评估脸书广告分析如何与谷歌 BigQuery 整合，以及脸书广告如何为 BigQuery 自动化带来商业利益。

# 什么是脸书广告分析？

作为一家企业，你可以依靠脸书广告建立一个在线品牌，为你的商业网站增加流量，甚至鼓励转化。想知道你最近的脸书广告活动是否成功吗？您可以依靠脸书广告分析公司，该公司拥有一套专门为广告相关洞察而设计的关键指标和 KPI。

![](img/301123a8bad8328ccaeaf36cb2d277e2.png)

无论是单个(或多个)商业广告还是整个广告活动，脸书广告都在为 B2B 和 B2C 营销者创造价值。除此之外，脸书广告数据是商业决策的丰富分析和洞察力的宝贵来源。显而易见的下一个问题是如何以及为什么将脸书分析整合到 BigQuery 中。

借助合适的工具，可以使用脸书广告洞察 API 轻松检索脸书生成的数据。除了快速高效之外，Google BigQuery (BQ)还能从标准的 SQL 查询中获得准确的结果。

在下一节中，我们将看到脸书广告如何在 BigQuery 自动化中发挥重要作用。

# BigQuery Automation 的脸书广告是什么？

脸书广告到 BigQuery 自动化流程是一个自动化的 BigQuery 作业，旨在保持脸书广告数据的新鲜和更新。通过使用数据字段的自动增量，您的开发人员可以编写脚本来集成 BigQuery 和脸书数据。

此外，您可以将这些自动化脚本配置为作为 cron 作业运行(或持续运行),以便从社交网络平台检索新的脸书数据。

![](img/d60a91bab24e111d84bbaccb391fb056.png)

## 脸书广告数据自动传输到 BigQuery 有什么帮助？以下是一些好处:

*   自动化节省时间，特别是对于资源有限的公司。
*   即使您的脸书数据量随着时间的推移不断增加，扩展也更加容易。
*   通过集成多种营销和 CRM 工具，BQ automation 的高级分析可用于构建高效的数据仓库。
*   自动化流程比需要人工干预的手动方法更有效。
*   有了高效的数据基础设施和仓库，可以通过预测数据建模或自然语言处理来促进业务增长。

这是一个典型的电子商务案例研究，非常适合用 BigQuery 分析脸书广告:

*   客户端的目标是每天提取 [MySQL](https://www.mysql.com/) 数据库表(包含 WooCommerce 数据)并将它们移动到 Google BigQuery 仓库中。

Google BigQuery 被选中从关键的脸书广告指标中提取见解，包括特定于活动的指标和广告集。

*   BigQuery 数据库表也必须兼容，才能在 [Google Data Studio](https://datastudio.google.com/) 仪表板上使用。
*   必须创建自动化的 BQ 脚本，以便每天对脸书数据执行。
*   最后，Data Studio 仪表板数据必须简化数据可视化以及对日常电子商务活动和广告支出的理解。

# 脸书 Ads to BigQuery Automation 是如何工作的？

作为一名数据分析师，你可以使用像脸书性能 API 或 Ads Insights API 这样的 API 提取任何脸书广告数据。这些易于使用的 API 可用于各种功能，包括创建广告和从广告中提取数据。

在将脸书数据加载到 BigQuery 之前，请确保 CSV 或 JSON 数据格式支持该数据。

您还可以借助以下任何数据源，将脸书广告的数据自动加载到 BigQuery:

## 谷歌云存储

BigQuery 支持从云存储中加载各种格式的数据，包括 Avro、CSV(默认)、JSON 和 ORC。您可以直接使用 Google 控制台来执行加载。

## 发布请求

另一种选择是使用 JSON APIs 直接发布数据。脸书性能 API 在将数据加载到 BQ 数据仓库和从中提取数据方面起着至关重要的作用。例如，您可以使用 CURL 或 Postman 工具执行 HTTP POST 请求。

接下来，我们将看看脸书广告给 BigQuery 自动化带来的一些商业好处。

# 脸书 Ads 给 BigQuery Automation 带来的商业利益

BQ automation 允许企业在几分钟内传输其脸书数据以供 BQ 处理。以下是 BQ 自动化的一些其他业务优势:

## 简化 Google BQ 上的数据复制过程

传统的 ETL(提取、传输和加载)工具已经不足以在 BigQuery 上复制大数据。这是因为 ETL 代码编写非常耗时，实现起来非常昂贵，并且需要专业技术知识。作为一个商业企业，您可以将资源集中在数据集成的价值上，而不是编写和修改 ETL 代码程序。

与 ETL 相比，BQ 自动化工具在执行数据复制时速度更快。因此，商业企业可以通过更快的决策执行脸书洞察和转换。

## 支持将数据直接传输到 BigQuery

通过 BQ 自动化和与脸书的集成，您可以直接将广告数据提取到 BQ。此外，支持 BQ 的数据仓库可以存储万亿字节的数据，这些数据可以放入任何 R 编程或 Python 工具中。

## 获取更新的脸书广告数据。

由于自动化的 BQ 脚本，您可以轻松地从脸书平台检索新的(或最新的)数据。这比在 BQ 仓库上复制整个数据块(或记录)更有效，后者是一个更长、更耗费资源的过程。

## 将 BigQuery 连接到其他数据源

BigQuery 自动化工具允许您的数据分析师访问其他数据源，包括数据库系统和 SaaS 工具。例如，像 Stitch 这样的 BQ 自动化工具允许你将你的分析连接到像亚马逊 S3、BigCommerce 和 Campaign Monitor 这样的数据源。

# 结论

在最有效的数字广告模式中，脸书广告也是一个丰富的数据仓库，帮助企业了解客户行为和其他趋势。如本文所强调的，在 BigQuery 中使用数据分析带来了许多运营业务优势。

随着脸书广告的出现，到 BigQuery 的自动化进程，数据分析师和科学家已经可以访问更新的脸书广告数据。这反过来增加了数据驱动的洞察力的价值，从而带来竞争优势。

作为数据分析和商业智能(BI)解决方案提供商，Countants 为其全球客户提供优质的 BigQuery 服务。该公司凭借其在云计算解决方案方面的技术专长，通过[数据分析](https://www.countants.com/blogs/business-benefits-of-cross-domain-tracking-using-google-analytics/?utm_medium=social&utm_source=Medium&utm_campaign=Traffic)和[数据可视化](https://www.countants.com/blogs/data-visualization-how-it-is-going-to-evolve-into-the-future/?utm_medium=social&utm_source=Medium&utm_campaign=Traffic)为客户提供价值。

您是否希望利用从脸书广告数据中提取的宝贵见解？然后是时候访问我们的[网站](https://www.countants.com/?utm_medium=social&utm_source=Medium&utm_campaign=Traffic)并与我们取得联系了。