# 有幽默感的机器？

> 原文：<https://medium.datadriveninvestor.com/machines-with-a-sense-of-humor-69cd5e6c2ea5?source=collection_archive---------6----------------------->

[![](img/824a25f8c04a09706f3a32ca4b3097ac.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/5bc6b6dcab766bcd6d65bdb08783edcf.png)

Photo by [Dan Cook](https://unsplash.com/@dan_scape?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/laughing?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

如今，机器可以做一些令人惊叹的事情，但它们能知道什么是有趣的吗？为了回答这个问题，我参加了我的第一次数据科学竞赛，并在短短几天内获得了 67 名参赛者中的第二名！

我从大学开始就对人工智能和机器学习充满热情，最近我开始参加在线课程来培养我的技能。我已经在 Coursera 上完成了斯坦福大学教授吴恩达的[机器学习](https://www.coursera.org/learn/machine-learning)和[神经网络和深度学习](https://www.coursera.org/learn/neural-networks-deep-learning/)课程。这些课程真的很棒，我强烈推荐给任何人，但是我觉得家庭作业有点太多了。他们为你做所有的事情，除了一个空格，并准确地告诉你该在那个空格里填什么。我理解他们为什么这样做——让每个人都容易跟随，但我想做一个更自主的项目。

[](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) [## DDI 编辑推荐:5 本让你从新手变成专家的机器学习书籍|数据驱动…

### 机器学习行业的蓬勃发展重新引起了人们对人工智能的兴趣

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) 

因此，在开始该系列的下一堂课之前，我想花两天时间完成一个数据科学竞赛。我决定从 analyticsvidhya.com 的[笑话分级预测挑战](https://datahack.analyticsvidhya.com/contest/jester-practice-problem/)开始。给你一个训练数据集，其中有用户对笑话的评级，你的任务是预测用户有多喜欢一个他们以前没有看过的笑话。这种推荐系统是网飞、YouTube、亚马逊、Spotify 等大公司对机器学习的常见使用。这似乎是一个完美的起点，因为我可以应用我学到的一种叫做协同过滤的技术。

![](img/334c7e5d83565b003c4134570d7dc7a6.png)

Photo by [Franck V.](https://unsplash.com/@franckinjapan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/machine-learning?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

协同过滤是一种算法，其中我们学习固定数量的特征，每个特征代表底层数据的一些质量。对于笑话，一个特征可能对应于敲门式笑话，另一个特征可能是双关语，而另一个特征可能是攻击性笑话。这些特征是从用户偏好中自动学习的。品味相似的人会倾向于喜欢同一套笑话。基于此，我们可以了解到这些笑话一定有一些共同的特征。同时，我们也在了解每个用户的偏好。也许这个人喜欢双关语，但讨厌冒犯性的笑话。我们将相应地调整用户的参数权重。所以，我们正在同时学习笑话和用户的权重。我们学习一个笑话是否有一个特征(敲门-敲门笑话？)以及哪些用户同时喜欢哪个功能(讨厌敲门笑话)。这听起来很复杂，但实现起来相对简单。

![](img/73f14a42f0fff6085a04f9faa050a853.png)

Photo by [Ian Stauffer](https://unsplash.com/@ianstauffer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/celebrate?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

以机器学习课上的一个作业中的代码为例，我用 pandas 和 numpy 用 Python 重新写了一遍。当我运行完一个快速而肮脏的模型并给出预测时，我想做一个测试提交，看看我是否以正确的格式输出了预测。令我惊讶的是，在我第一次尝试时，我的名字出现在[排行榜](https://datahack.analyticsvidhya.com/contest/jester-practice-problem/lb)的 67 个名字中的第 3 个！！对于两天的工作来说还不错。当我稍微调整了一下超参数，我就能跑到第二名了！我的分数和顶解相差 0.01 以内，所以基本上是平手😂。我清理了[的代码，放在了 github](https://github.com/tonytonev/JokeRecommender) 上，如果你感兴趣的话可以欣赏一下。

这给了我很多信心，让我兴奋地继续做更多的项目，变得更好。