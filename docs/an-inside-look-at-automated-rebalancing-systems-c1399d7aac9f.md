# 自动再平衡系统的内部观察

> 原文：<https://medium.datadriveninvestor.com/an-inside-look-at-automated-rebalancing-systems-c1399d7aac9f?source=collection_archive---------14----------------------->

杰拉德·迈克尔

![](img/4e3a5f4b3f94a967bee2e59c162f1f6e.png)

*我们做什么以及如何做。*

我们写这个博客已经一年多了。您现在可能已经知道 Smartleaf 提供了一个用于自动化定制和税务管理的系统，但我们从未真正解释过我们的系统是如何工作的，或者我们与其他解决方案有何不同。我们认为我们现在应该这样做。

我们认为，我们用来实施自动再平衡的基本方法是非常通用的。不是说所有的再平衡系统都是按照我们的方式构建的(它们不是)。但是从某种意义上来说，任何实现高级定制和税务管理自动化的系统都必须以同样的方式做事。换句话说，我们不认为对我们方法的描述是真正关于我们自己的。它是关于复杂投资组合的自动再平衡需要什么，不管是谁做的。称之为构建复杂投资组合自动再平衡系统的指南。

为什么自动再平衡很有趣？因为高度定制、税收优化的财富投资组合管理正在成为“赌注”，这意味着你不会为此获得报酬，但如果你没有它，你将处于竞争劣势。实施它将改变你的组织和你的客户体验(特别是，它将促使顾问专注于财务规划并充当“生活教练”)。

(我们之前在这里写过自动化再平衡对财富管理行业的影响:[什么是再平衡自动化？、](https://www.smartleaf.com/our-thinking/smartleaf-blog/implications-of-rebalancing-automation-part-1) [再平衡自动化会改变你的工作，](https://www.smartleaf.com/our-thinking/smartleaf-blog/implications-of-rebalancing-automation-part-2) [合规可以自动化吗？，](https://www.smartleaf.com/our-thinking/smartleaf-blog/can-compliance-be-automated) [停止。是时候重新思考再平衡了，](https://www.smartleaf.com/our-thinking/smartleaf-blog/forget-what-you-think-you-know) [自动化再平衡:投资者为何关注。](https://www.smartleaf.com/our-thinking/smartleaf-blog/why-investors-care))

我们的方法可以被有效地(如果不恰当地)描述为协作的、整体的、优化的、基于模型的、参数化的、程序化的和无套的。或者简称 CHOMPPN。(我们知道。我们的市场部正在努力。)更准确地说，我们的系统(以及我们认为的任何其他能够自动化复杂投资组合再平衡的系统)的关键架构元素是:

*   协作投入
*   整体优化分析
*   基于模型的智力资本
*   参数化定制
*   程序化工作流程
*   无套账户

让我们一次看一个。

# 协作投入

传统上，投资组合管理是一种孤狼式的活动，每个顾问负责管理他们账户的所有方面。

在自动化系统中，项目组合管理是协作的。这是三个小组的共同努力:投资政策委员会、顾问和临时经理。这些术语描述的是角色，而不是个人。这些角色可以全部由一个人承担，也可以分布在三个小组中，而且每个角色本身还可以细分。)

*   投资政策委员会负责研究和尽职调查，创建专有模型，创建公司的战术和战略资产分配建议，设置资产分配修改的合规限制，为每个资产类别选择推荐和替代模型，以及设置资产类别漂移限制。
*   顾问负责帐户设置，为每个客户设计定制的解决方案(用一组参数表示)。定制包括选择适当的风险类别、修改资产分配、修改每个资产类别的产品选择、设置税务管理偏好、设置现金管理偏好、输入约束等。
*   覆盖经理负责在所有账户中执行顾问和投资政策委员会的联合指示。

以这种方式使项目组合管理成为一种协作的努力，使得每个人或者团队能够专注于他们最擅长的事情。至关重要的是，它让顾问能够委派投资组合再平衡的日常任务，并花更多时间与客户和潜在客户相处。结果是更高的效率和机会，同时为客户提供更高水平的定制和税务管理。

# 全面优化的分析

大多数项目组合管理系统是“向前行动的”这意味着他们的工作是帮助经理实施一系列离散的行动，如战术性资产分配、模型中的证券互换、现金提取等。对于每个再平衡，大多数系统的基本思想是实现这些操作，尽可能少做其他事情。这些系统也可以支持“总体再平衡”，但通常不是以特别税收或费用有效的方式，除非有人工干预。

虽然“行动推进”工作流程的概念听起来很合理(甚至令人兴奋)，但它会给顾问和他们的客户带来不良后果。这些工作流程往往会产生一种环境，在这种环境中，每天都不同程度地成为损失收获日、漂移合规日、模型变更日等。也就是说，顾问最终只能被动地(在一天内尽可能多地)解决某项投资和交易政策的某个方面，同时努力确保他们的行动不会与同一政策的其他方面发生冲突。一天或一年中没有足够的时间让这个过程适用于每个投资者账户。

有了自动化系统，所有这些再平衡“触发器”(战术性资产分配变化、股票互换、套现请求、漂移、损失收获等)。)合二为一。在每一次分析中，系统都会在需要或合适的时候做所有这些事情。每次都是。每天都是。

这种方法使顾问和财富管理公司能够主动实施其计划的各个方面。不是“模型改变日”、“损失收获日”、“模型 7 再平衡日”，每天都是“让投资组合更好的一天”。

这种方法的结果是更低的漂移(投资组合与其目标之间的回报率差异)和同时更低的税收。这是可能的，因为系统在适当的时候采取行动——有时比传统方法更早(因为系统每天都在分析)，有时更晚(例如，推迟销售，直到短期收益变成长期收益)。

你能创建一个不完整或优化的自动化系统吗？我们对此表示怀疑。至少在税收管理或风险控制水平上是不同的。非整体性的再平衡(一次实施一项行动)不必要地放弃了改善税收和/或风险的机会。试图用一系列规则复制一个优化器的逻辑很快变得势不可挡；规则变得太复杂，无法处理你可能遇到的所有可能的权衡情况组合。

# 基于模型的智力资本

“基于模型的智力资本”是“持股、资产配置和交易信息的参数化投入”的另一种说法它是参数化定制的表亲，我们将在下面描述，并且它对于支持自动化是必要的。另一种方法是建立买入清单和资产类别分配范围，以及人工选股和交易。

我们系统中的每个投资组合都遵循一个或多个模型的混合(加权证券列表)。如果投资组合经理或公司希望在多个投资组合中交换股票，这样做的主要机制是调整模型中证券的权重。战术性资产配置通过改变我们称之为“目标模板”的资产类别权重来表达目标模板还包括对资产分配修改的固定限制和对资产类别漂移的固定限制。

# 参数化定制

对许多顾问来说，“定制化”意味着根据每个客户的需求量身定制的一次性、逐个交易的决策。

自动化系统不是这样做的。自动化系统将定制需求和偏好存储为描述应该如何管理每个投资组合的参数。这包括税务管理偏好、资产分配修改、产品替代、SRI 筛选等。

然后，这些偏好和约束会自动合并到每个分析中。

使用这种方法，实施税务管理或定制不需要额外的步骤。而且税务管理和定制的增量成本被有效地降低到零，这导致了一个重要的和有些违反直觉的效果。当你提供免费的东西时，人们会消费更多。定制和税务管理没有什么不同。当你把它的成本降低到零，顾问会消耗更多的成本。也就是说，当企业将定制参数化并将这些参数纳入每项分析时，它会导致客户投资组合的定制和税务管理水平大幅提高。

而且，并非偶然地，它也有助于遵从。没有客户请求丢失便利贴。一旦一个请求进入系统，它将被包含在每个分析中。投资组合不需要超过一个工作日不符合规定。

# 程序化、统一的日常工作流程

一个自动化系统每天分析每个投资组合，并生成遵循投资者、客户和投资政策委员会联合指令(即参数)的交易。然后，公司可以应用过滤系统来选择他们想要交易的投资组合。

这本身并不罕见。与众不同的是，公司可以每天应用相同的工作流程，相同的过滤器。

每天都有相同的工作流程并不意味着每天都交易所有的账户。这仅仅意味着对交易有统一的标准。对于我们的大多数用户来说，交易账户有两个基本原因:

*   账户需要进行交易以符合一项或多项指令(如提取现金请求或一些其他约束)。
*   对账户的分析显示，一组交易的净收益(即收益，如漂移减少，减去成本，如税收和佣金)高于某个阈值。

这个基本的两步工作流程每天都应用于每个客户。但是个别公司可以并且愿意定制这个工作流程，以适应他们每个投资项目的细节。

传统的再平衡系统旨在促进实现一系列请求，如股票互换。在任何给定的一天完成什么将取决于顾问选择实现的请求以及它们的执行顺序。

相比之下，程序化方法的目的不是实现特定的交易，而是实现特定的程序和政策。

# 无套资产

许多系统将持有分成多个套(也称为分区或子账户)，每个模型一个套。我们不这样做，因为袖子是昂贵的操作和干扰最佳的风险和税收管理。你可以在之前的几篇文章中读到我们对袖子的思考:[袖子终极指南，第一部分](https://www.smartleaf.com/e1t/c/*W4RZ4lG7wNvB9N35bZFkhgkNj0/*MWGhhSgG_LwN14qYV85fmj40/5/f18dQhb0SnG-9jx95gW8RzwBz7t5LzlW12xF5W8pTgPFW3LZc7M6gzNFPW2K4R9r8ZkD0BN7sr5FcKzm3-W2_Z2W-5mZ50NW8W2c9l2MmTZXW6wCVc-8_7FpdW2Hv0M997z1HfW6Rgn-f5DjQT_W6bW6V35CbYnPW1nY8c325NMP1W6b-LdD1nrCGBW51LTg55DHNj2W1mc1q58wXNtsW2z8SPy1xbS-NVYwlHF19jypgVqRX8t1VJH71W4c2Rr971B_trW1x4lQB6G8-RxW9dH8_66V4mfxW1G1CW52P2TFTW1VJryk5lX8fqW13bD4h6dkl-ZW7tVCjH5Ym74rW4NBgHH49YtCTW7vB7fD1GwyyYW55lWTz7Lc_3-VnL_0C2MJys0W1C5Cfx77gFx3W1hNG872PGS2FN30XZV-4RHkRW7LF8D-2sxDXsW57f6Bs775lwXW14LjL04fsZm-W6YtTf88nDXWqW38L9ry7pF69GW73R1h2224m2ZW1kwZ_w1V3YvJN7kLn_Z10N9FW5xftxg8Nhx4fN83rSgtdnDGfW3_jN0w841Q0dW38YPyw5CNSrnMmRw0WdXyXbTjkRm6vfdn0103)和[第二部分](https://www.smartleaf.com/e1t/c/*W4RZ4lG7wNvB9N35bZFkhgkNj0/*W947W942ytX45W8C2zNM1c761d0/5/f18dQhb0S5pT1QgjpYTy8Xr1tY4VQN5WLDvCQyrnMVWHjPK40mZ4bW60JW3W2lSW3-W6PhcMC8q8RQQW5p6bgz25mT_zW5KkPwQ12slbjVSQ-d88zZyM5W48Xw8c4QprTGW4rZyXx12QzdLW94F9L46xCdYgW1CgFhR6RQxY8W96bsVq5XZq6mW78PGQ_59_3LwVG1F6V70ZMFLN7XBzqck-GPKW1G8zQL8v6TfKMdS0RFpLcHJN8zbSb6Nn8zLW1Nrn5G3TlFD3VvvmdK2sXWvhW1-WsFy58f6H2W6svMhN3Qt2YJN534J5C6nllPW5xbB0q1cLThSW7hf5Yy7D9T1NW9f_8S53CNw32N4ftNJynbdWRVf46P78GPDScW7ldg5k7djFSGW1HgQ7x1z1G9PVJJMPW3w76r9W59DZFX4hzBcLW7t-mdp7jWZRtW14FKTT3G3WCnN7M1vF0RQDYzW39Q_yz40L1_DN3-fhqLTV3zrW2-dvcw7qk-FtW6mK7rt8ZxjkLW1pppjF31Kj0-W20YTJ95mwBQZW4FqC3d4zmK93W7VlYrk4ZPcfDW9gNy7p8X1FcvW1ksVph6Wyh5CW5B5W1b4Pt_qW0)，[选择再平衡系统指南](https://www.smartleaf.com/e1t/c/*W4RZ4lG7wNvB9N35bZFkhgkNj0/*W1595Tr2MBF82Vn_w0_5jbXc30/5/f18dQhb0SfHv9c-lR0W8j18hL5D47MtW234jd_7vBFHHW7tWqhv6GvqgMW5q9cPw8yym7NW5yMltN1p88LvW5_VJfB1nPLDMW8sZ4-t5vLLS4W3K4q-_8D9RnHW5nY8r98ZyZJXW2Mnlh04hrxPkW5nrYy555fMLYVKpjkH5n9_G4W8WBFpz8htXy8W7N0xw05mNLNvW7bqTzM7vp5SXW5m8s7M8YwCWfW1h4F6f1xbS-NVYwlHF19jypgW6T53N31VJH71W4c2Rr97Mv86WW49z-4P2MV0XLVbG0m98W1JLSW2KSxqc4FW6BVW1QjhXf1txG9NW6GsfdK8XNh8_W7J_sPh7rFbtxW49hlXZ1KkvR0Vml-Vw1VcwZkW4fMQhM1_TBF5N7Tk5mxkJ87dW48hY3v57jfKHVyJLDn45yG4KW47lbHQ2JB-C3W7k9_0j6fPjqPN6kMvrzwLvvlN6KtdwwtyKkyW1GGZbq1HRpBrW5HFKKT13dJDnN1zW062zD-dgW1tnvdk9dCW96W8lwygZ10QcR6VsjV005XThvKW4G21F378bkLSVVpxCB4CsDqMW935M8051xYt9W7yTgfY1NwBMnF1MVsRjC__Lf2y9tqW03)，以及[不要把个人投资者当成机构](https://www.smartleaf.com/e1t/c/*W4RZ4lG7wNvB9N35bZFkhgkNj0/*W5vKw7K6R5CbgW8ZKtbv7WWG700/5/f18dQhb0SfHv9c-lR0W8j18hL5D47MtW234jd_7vBFHHW7tWqhv6GvqgMW5q9cPw8yym7NW5yMltN1p88LvW5_VJfB1nPLDMW8sZ4-t5vLLS4W3K4q-_8D9RnHW5nY8r98-2Q3pW2KWRYT2_YRXTW1Ww7d67qXTdYVKntjk4chYmXW4KyFbN5C9g4yW5DQqWp90G7thN8S3yR5bY02SW4s7XyV96B573W1nk4sT2mqhcHN55ks-lrllPKW53hh3V67b7w6W7hYCG43N1Lh3W5FqWfs64jzh4W7-JXR61k3jnvW7vRbb18617vHW7bdNkZ2hBQwBW1MqhJK7ldyjxW608ynQ7sSTRPW1xsNq-1smZyyW1fnWy_7VPshQW83JXPD6TFlqTW21dSH46cHyQtW6Tv26T6tDBy8W1V4XLP25ZZ4yW7l793l1D5wkJW1D3qNV1V-bB2W23VT3Y779YHxW24bw3n7TCbqBW2Qn0lk81yxvWW3bwBC93Y196jN6Mn8nHVR6H2W4q1Pz42x2cJ8W1SPFdS573tWwVj8tbN480YYsW97g7Px7sDfy-W43MFcT89WwFZW72y65S3DDJ6zW5R8Z1R5_5dj9w3xWwfq2vsf6LSbQB02)。

所以，你有它:CHOMPPN:协作的，整体的，优化的，基于模型的，参数化的，程序化的和无套的再平衡。简单。(我们市场部还在做。)

关于这个话题的更多信息，请查看[什么是再平衡自动化？](https://www.smartleaf.com/our-thinking/smartleaf-blog/implications-of-rebalancing-automation-part-1)