# 即将到来的人工智能冬天

> 原文：<https://medium.datadriveninvestor.com/the-oncoming-ai-winter-8f7c88b962a2?source=collection_archive---------13----------------------->

![](img/7667d893f4a982f03607cd04d7489576.png)

就在大约一个月前，AI 在游戏领域获得了另一个奖项，他在 5v5 Dota 2 的三轮比赛中击败了一队高排名玩家。虽然去年同一支球队的一个机器人能够在 1v1 比赛中击败职业选手，但 OpenAI 的新 5v5 机器人，恰如其分地命名为 OpenAI Five，是一个更大的成就(OpenAI 的 Dota 团队，2018)。在每一方增加 4 个游戏会给游戏增加巨大的复杂性，团队合作的新方面出现了。科技领域的许多领导者，如比尔·盖茨，称赞这项成就是人工智能历史上的一个标志。(克利福德，2018)。

OpenAI Five 使用了一种称为强化学习的技术，这是人工智能的一个专门分支，已被证明特别适合游戏场景。与 AI 的其他子领域不同，强化学习使用奖励系统来训练代理(如 Dota 2 bot)。这个奖励系统的功能类似于训练一只狗或一个新生儿学习新行为的方式。当触摸一个热的炉子时，你会以疼痛的形式收到一个负面的奖励，让你想要停止触摸热的东西。当你做了好事，你可能会收到父母的礼物，鼓励你更多地表现出同样的行为。类似地，Dota 2 中的机器人可能会在输掉游戏时获得负奖励，而在赢得游戏时获得正奖励。

OpenAI Five 并不是唯一的成就，而是许多游戏人工智能系统中的一个。利用强化学习的第一个重大游戏成就出现在 20 世纪 90 年代初，当时 Gerry Tesauro 创建了一个可以与职业玩家竞争的双陆棋机器人(Teasuro，1995)。1997 年，国际象棋世界冠军被 IBM 的深蓝击败，深蓝基于一种算法来快速搜索可能的结果并预测对手的棋步(皮赫，2013)。在沉寂了 19 年之后，2016 年，DeepMind 凭借 AlphaGo 震惊了世界，alpha Go 是一种人工智能，击败了当时的世界围棋冠军。围棋比国际象棋有大约 1054 种可能的棋盘布局，是一种极其复杂和困难的游戏。甚至当时的冠军李·塞多尔(Lee Sedol)也预计 AlphaGo 会轻松获胜，以 4 比 1 或 5 比 0 结束(李，2016)。仅仅一年后的 2017 年，一个更新的版本 AlphaGo Zero 以 100 比 0 击败了 2016 年的版本(2017 年的银牌)。随着 OpenAI Five 在一年后问世，玩游戏的人工智能似乎正在不可阻挡地超越人类。但所有的成功都回避了一些问题:为什么玩游戏的人工智能突然复兴了？为什么效果这么好？而且还会这样继续下去吗？

强化学习实际上并不是近年来蓬勃发展并取得如此快速成功的唯一人工智能领域。相反，包括强化学习在内的深度学习领域一直在改善从语音识别(就像你可能使用 Siri)到物体检测(就像在为无人驾驶汽车开发的软件中使用的那样)的任务。人工智能热潮始于 2012 年的 ImageNet 竞赛，各队竞相开发能够检测给定图像中存在什么的程序。虽然多年来在这个问题上的成功进展缓慢，但 2012 年比赛的获胜者击败了之前约 9%的错误率，通过使用深度学习，准确率从 75%提高到 84%(Gershgorn，2017)。然而，深度学习的发明并不是人工智能繁荣的唯一原因，因为深度学习技术在 20 世纪 50 年代就已经被发明，但从未被大量使用。真正改变的是对大量格式化数据的访问和速度快得多的硬件，这些硬件可以建立更大更快的深度学习模型。虽然软件在当前的人工智能时代发挥了重要作用，但它不是最初革命的原因。

继 2012 年的最初飞跃之后，软件在开发中发挥了更大的作用。从那以后，出现了大量经过修改的软件来增强深度学习的能力，并且创建了许多在某些任务上工作得特别好的模型。随着软件的主要改进，ImageNet 比赛于 2017 年结束，当时人工智能在图像检测方面超过了人类，准确率达到 97.3%。

展望未来，软件、硬件和数据最有可能成为人工智能发展的支柱，但也就是说人工智能的发展不会放缓，甚至不会达到极限而停止。互联网上的数据比以往任何时候都更容易获取。特别地，对于深度学习中最流行的任务，存在公共数据集。像 Kaggle 和 Google 这样的平台甚至有允许你搜索数据集的功能。数据集的创建也可以通过使用像亚马逊的 Mechanical Turk 这样的软件来有效地完成，这是一个用于标记数据的众包平台。对于大多数任务，缺少数据不再构成威胁。虽然自 1965 年以来，硬件的效率每两年翻一倍，但新的数据似乎表明，当前的硬件生产技术正在达到其最大容量，因为零件在物理上不可能变得更小(Simonite，2017)。

幸运的是，软件一直在进步，但没有最近在该领域取得的成就让一些人思考的那么快。OpenAI 使用了 LSTM，这是一种自 1997 年就已经存在的深度学习模型(Hochreiter，1997)。为了实现他们的结果，OpenAI Five 使用了 128，000 个 CPU 核心和 256 个 GPU 来训练其机器人(OpenAI，2018)。一台普通的电脑只有 2 个 CPU 和 1 个 GPU。这些机器人训练了几个月，每天收集大约 900 年的经验。AlphaGo Zero 使用了相当数量的计算能力来实现其结果。这种情况使得没有一台巨大的超级计算机就不可能取得这样的成就。随着传统硬件达到其计算极限，这种超级计算机系统不太可能以一致的速度扩展。深度学习肯定会继续在许多领域取得成功，但如果没有新的革命，深度学习可能会停滞不前，引领世界进入下一个人工智能冬天。

# 来源

c . Clifford(2018 年 6 月 28 日)。比尔·盖茨表示，来自埃隆·马斯克支持的非营利组织的游戏机器人是人工智能领域的“巨大里程碑”。检索自[https://www . CNBC . com/2018/06/27/bill-Gates-open ai-robots-beating-humans-at-dota-2-is-ai-milestone . html](https://www.cnbc.com/2018/06/27/bill-gates-openai-robots-beating-humans-at-dota-2-is-ai-milestone.html)

格什高恩博士(2017 年 7 月 26 日)。这些数据改变了人工智能研究，也可能改变了世界。检索自[https://qz . com/1034972/the-data-that-changed-the-direction-of-ai-research-and-possible-the-world/](https://qz.com/1034972/the-data-that-changed-the-direction-of-ai-research-and-possibly-the-world/)

Hochreiter，s .，& Schmidhuber，J. (1997 年)。长短期记忆。*神经计算，* *9* (8)，1735–1780 年。doi:10.1162/neco

克里斯皮赫。(2013).深蓝色。从 http://stanford.edu/~cpiech/cs221/apps/deepBlue.html[取回](http://stanford.edu/~cpiech/cs221/apps/deepBlue.html)

李世石确信他将在中国古代围棋比赛中击败艾。(2016 年 2 月 22 日)。检索自[https://www . daily mail . co . uk/science tech/article-3458081/Human-champion-certain-hell-beat-AI-ancient-Chinese-game.html](https://www.dailymail.co.uk/sciencetech/article-3458081/Human- champion-certain-hell-beat-AI-ancient-Chinese-game.html)

OpenAI。(2018 年 9 月 11 日)。打开五号门。从 https://blog.openai.com/openai-five/[取回](https://blog.openai.com/openai-five/)

OpenAI 的 Dota 战队。(2018 年 8 月 31 日)。OpenAI 五项基准测试:结果。从[https://blog.openai.com/openai-five-benchmark-results/](https://blog.openai.com/openai-five-benchmark-results/)取回

silver d .，Schrittwieser j .，Simon Yan k .，Antonoglou I .，Huang a .，Guez a .。。哈萨比斯博士(2017 年 10 月 18 日)。在没有人类知识的情况下掌握围棋。从 https://www.nature.com/articles/nature24270[取回](https://www.nature.com/articles/nature24270)

t . simonite(2017 年 2 月 06 日)。计算机行业创新的基础正在动摇。有什么可以替代？检索自[https://www . technology review . com/s/601441/Moores-law-is-dead-now-what/](https://www.technologyreview.com/s/601441/moores-law-is-dead-now-what/)

特索罗，杰拉尔德。(1995).时间差学习和 TD-Gammon。(未注明)。从 http://www.bkgm.com/articles/tesauro/tdl.html[取回](http://www.bkgm.com/articles/tesauro/tdl.html)