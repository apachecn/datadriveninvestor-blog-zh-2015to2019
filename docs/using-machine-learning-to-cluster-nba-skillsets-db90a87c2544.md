# 使用机器学习对 NBA 技能集进行聚类

> 原文：<https://medium.datadriveninvestor.com/using-machine-learning-to-cluster-nba-skillsets-db90a87c2544?source=collection_archive---------6----------------------->

[![](img/aac887fb28de43ffc16631ba895c8d8c.png)](http://www.track.datadriveninvestor.com/1B9E)

对于我的顶点，我的目标是基于高级统计重新分类玩家技能。我的顶点想法是基于我在 Alex Cheng 的 fastbreakdata.com 博客上看到的一个概念。亚历克斯认为斯蒂芬·谢伊非常擅长篮球分析。我买了谢伊的书，他称赞穆图·阿拉加潘，他说他是第一个公开提出篮球中的五个位置模型已经过时的人。

当你衡量今天的篮球时，你会发现这是真的。今天的比赛是关于进攻时的多功能性和空间能力，以及防守时的多功能性。比如看大前锋位置。密尔沃基雄鹿队在大前锋位置上首发扬尼斯·阿德托昆博，他是一个非常独特的球员，他选择主要通过运球攻击篮筐来进行比赛。在 2018-2019 赛季，詹尼斯 83%的投篮都在 2 分范围内。现在，看看同一支球队的尼古拉·米罗蒂奇，他大约 65%的投篮来自 3 分范围，35%的投篮来自 2 分范围。这两个球员都很擅长他们所做的事情，并且有着相似的高度，但是我们可以看到他们的比赛风格有很大的不同。

[](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) [## DDI 编辑推荐:5 本让你从新手变成专家的机器学习书籍|数据驱动…

### 机器学习行业的蓬勃发展重新引起了人们对人工智能的兴趣

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) 

我计划在这个项目中做的是使用 BeautifulSoup 收集网络数据，并检索 NBA 球员的统计数据。然后，使用无监督的机器学习方法 K-Means 和 DBScan 基于打法聚类球员。在对玩家进行聚类之后，我的计划是建立一个推荐系统，能够推荐与你选择的游戏风格相似的玩家。

![](img/f51e91f98cebf7cd5ced0a093e69bfdc.png)

Photo by [tommy boudreau](https://unsplash.com/@lenswithbenefits?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

对于这个项目，我的观众是任何对篮球分析感兴趣的人，或者只是对机器学习感兴趣的人。我的目标是，对篮球感兴趣的人可以更好地理解如何从整体上看待篮球。

当有人希望建立一个团队时，不一定要考虑“我需要多少个中锋？”更好地看看，我需要一个大的，可以完成周围的轮辋以及保护轮辋。或者我需要一个大前锋，可以为我的球队腾出空间，防守多个位置。NBA 前台现在欢迎数据科学社区的人，我认为这可能是一个有用的工具。

前台成员可以决定他们应该在自由市场追逐谁，他们应该交易谁，或者谁是他们当前团队潜在低估的人。例如，如果一个球队每场比赛只让一个人上场 15 分钟，但他们的打法和一个全明星球员相似，那么这个人可能就是我们在自由球员市场关注的对象。

![](img/c818759e07bf92ead62c2b70f84ed961.png)

Photo by [Luca Bravo](https://unsplash.com/@lucabravo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

到目前为止，在我的过程中，我使用 BeautifulSoup 从 Basketballreference.com 收集信息。我已经收集了 2017-2018 和 2018-2019 赛季的每场比赛统计数据、每 36 分钟统计数据以及高级统计数据。此外，我已经刮 G 联赛高级统计。我计划把 G 联赛的球员也加入到我的模型中。希望，这将给予这些球员很大的洞察力；有可能发现更多被低估的玩家或隐藏的宝石。最后，我收集了球员合同，我希望我们也能评估合同的价值。例如，如果某个球队明年买不起某个球员，可能需要替换他，那该怎么办？谁能以类似的方式填补这个空缺呢？

![](img/c04d458ab1b0e0051a820344ec8662d4.png)

Photo by [TJ Dragotta](https://unsplash.com/@tjdragotta?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我预计的一个障碍是清理数据的过程。这个数据集自然包含一些缺失的数据，因为可能有些球员在名单上，但没有参加任何比赛或尝试任何投篮。正确地输入这些丢失的数据将是一个障碍。我能看到的另一个障碍是找到我计划在建模过程中使用的正确特性。例如，我提到我收集了一大堆不同的篮球统计数据。我认为，确定哪些数据能最好地评价一名球员的比赛风格是一个潜在的障碍。到目前为止，我对每 36 分钟统计数据的理解对于在篮球比赛中打很多比赛的球员来说更准确。然而，对于不经常打比赛的球员来说，这会加重他们的统计数据，因此很难确定他们统计数据的真正意义。例如，如果你在一场比赛中打了 1 分钟，得到 2 分和 1 个篮板，即使样本量很小，你的 Per 36 也是非同寻常的。

这将是我第一个使用无监督学习方法和推荐系统的项目，所以这肯定是我计划在这个项目中改进的东西。我上面提到的另一件事是，我将致力于输入数据。有许多方法可以输入丢失的数据，这是我必须决定如何去做的事情。

我打过篮球，现在是它的超级粉丝。这个项目的一切都让我兴奋。能够对游戏有更强的理解，看到玩家怎么玩，和另一个玩家有多相似，是让我兴奋的事情。此外，潜在的使用推荐系统，我觉得将非常酷，纳入我的项目。我非常期待看到如何去做这件事。