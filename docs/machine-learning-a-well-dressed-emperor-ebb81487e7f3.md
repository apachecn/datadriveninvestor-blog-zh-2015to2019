# 机器学习:衣冠楚楚的皇帝

> 原文：<https://medium.datadriveninvestor.com/machine-learning-a-well-dressed-emperor-ebb81487e7f3?source=collection_archive---------6----------------------->

## 机器学习不是魔术，但不要贬低它

![](img/224b97563c59b6d59fd6dfb8dcc21ece.png)

Photo by [Hitesh Choudhary](https://unsplash.com/@hiteshchoudhary?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/artificial-intelligence?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

今天看了[机器学习——皇帝穿衣服了吗？](https://medium.com/hackernoon/machine-learning-is-the-emperor-wearing-clothes-59933d12a3cc)作者[卡西·科济尔科夫](https://medium.com/u/2fccb851bb5e?source=post_page-----ebb81487e7f3--------------------------------)。虽然我很欣赏为机器学习提供易于阅读的介绍所做的努力，但这篇文章包含了一个我不能忽视的关键信息:机器学习只不过是通过看到人类必须提供的例子来学习给东西贴标签的想法。虽然这肯定是机器学习的一个巨大的子域(一个叫做监督学习的子域)，但机器学习还不止于此。因此，我担心 Cassie 对机器学习的观点过于狭隘，我提交这篇文章是为了给出一个不同的、更广泛的(不一定完整的)观点。

在[什么是机器学习？](https://medium.com/the-singularity/what-is-machine-learning-c0d85687a20f)我已经给出了机器学习的非正式定义:

> 当机器在一段时间内，在没有明确告诉它如何做的任务上变得更好时，机器学习就发生了。

[](https://www.datadriveninvestor.com/2019/02/28/4-books-on-ai/) [## 挑战你对人工智能和社会看法的 4 本书|数据驱动的投资者

### 深度学习、像人类一样思考的机器人、人工智能、神经网络——这些技术引发了…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/28/4-books-on-ai/) 

现在，这样的任务肯定是给东西贴标签。人们可以给计算机一些有猫和没有猫的图像，并告诉计算机哪些图像有猫，哪些没有。使用机器学习技术，计算机可以从这些例子中学习，并正确地给一个新的，看不见的图像贴上“猫”或“没有猫”的标签。这就是监督学习，似乎 Cassie 在她的文章中将机器学习等同于此。

然而，机器学习比“仅仅”监督学习更广泛。例如，强化学习是机器学习的一个领域，计算机可以从人类没有给出的“例子”中学习。例如，一台被赋予了 Connect Four 规则的计算机可以和自己玩一百万次 Connect Four 游戏。这样它就可以学着玩得更好。

> 计算机从自己生成的例子中学习。

我们必须告诉计算机，赢的情况是好的，赢之前的情况不太好(因为它们导致赢的情况)，等等。，但这只是一些基本规则:我们不会给计算机我们认为好的董事会状态的实际例子。我们告诉它，连续四个意味着赢(或输)，计算机将这一逻辑应用于它自己生成的棋盘状态(通过与自己对弈)。这同样适用于它产生的其他棋盘状态:它们越接近游戏中获胜的棋盘状态，它赋予该棋盘状态的分数就越高。这提供了额外的例子来学习。这样，计算机就可以从自己生成的例子中学习。

我的观点是:机器学习非常强大。虽然 Cassie 认为它非常有用，但她的文章似乎错过了一些重要的东西:机器学习的核心是在数据中寻找模式，这也是人类智能的核心。不，我不是说机器学习已经和人类智能平起平坐了。但我引用凯西的文章:

> "如果你期待魔法，那么，你越早失望越好."

当然，机器学习不是魔法，但人类的智能也不是。深度学习形式的机器学习显示出巨大的前景:例如， [DeepMind](https://en.wikipedia.org/wiki/DeepMind) 的 [AlphaZero](https://en.wikipedia.org/wiki/AlphaZero) (一种深度学习应用)现在正在教*美国*下棋。而且没错，AlphaZero 使用的是强化学习，而不是监督学习。