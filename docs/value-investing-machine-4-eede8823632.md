# 价值投资机器— 4

> 原文：<https://medium.datadriveninvestor.com/value-investing-machine-4-eede8823632?source=collection_archive---------8----------------------->

# 第 4 部分——使其成为产品

[第一部分——理解问题](https://medium.com/@vivekys/value-investing-machine-d2718d35d19b)

[第二部分——价值投资的深度强化学习代理](https://medium.com/@vivekys/value-investing-machine-2a-43ce2d05f2a2)

[第三部分——构建代理&现场实验](https://medium.com/@vivekys/value-investing-machine-3-4c1053221940)

第 4 部分—使其成为产品(当前文章)

在之前的文章中，我描述了投资组合管理问题，作为深度强化学习问题来解决它的数学结构，如何建立这样的模型以及实验这样的模型所需的工程系统。所有这些基本上都是为了给普通散户投资者打造一款产品。本文分享了这样一个产品的愿景。

[](https://www.datadriveninvestor.com/2019/02/08/machine-learning-in-finance/) [## 金融中的机器学习|数据驱动的投资者

### 在我们讲述一些机器学习金融应用之前，我们先来了解一下什么是机器学习。机器…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/08/machine-learning-in-finance/) 

对散户投资者来说，真正的挑战之一是管理储蓄账户和投资账户之间的流动性。与此同时，有必要以最低的风险和投资账户的低管理成本产生有意义的回报。有几种金融产品试图解决上述问题的一部分。但我认为它们都没有全面解决问题。我开始尝试模拟价值投资的定量模型，以构建一个解决上述问题的产品。我认为具有以下特征的产品会获得巨大成功。**请注意，很难验证这些特征是否能长期持续地得到满足。**以下是特点:

1.  3 个变量中有 2 个自变量。它们是年回报、提取(或 Cvar)和投资时间范围。客户可以指定 2 个变量中的任何一个(合理的值),投资组合经理在任何情况下都应该遵守它们。
2.  投资组合经理自动将储蓄账户中的多余资金(智能地基于客户的消费历史和未来预期)转移到投资账户。
3.  投资账户下的资产不一定仅限于股票，也不一定仅限于某个特定地区的股票。它可以是全球范围内满足客户期望的任何金融资产。

我希望有一天这样的产品能出现在市场上，让所有人都能买得起。

# 确认

我借此机会感谢 [Jairaj Sathyanarayana](https://www.linkedin.com/in/jairajs/) 帮助验证这项工作的数据科学方面， [Raj Desai](https://www.linkedin.com/in/raj-desai-321b8b8a/) 帮助建立一些工程系统。