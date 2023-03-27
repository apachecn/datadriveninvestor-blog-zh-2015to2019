# 机器学习有什么不同？(以及为什么更好。)

> 原文：<https://medium.datadriveninvestor.com/how-is-machine-learning-different-and-why-it-is-better-d5671b52dd65?source=collection_archive---------5----------------------->

![](img/20373b716472ef07eb1f875497cf934d.png)

Photo by [Ash Edmonds](https://unsplash.com/@badashproducts?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

认知状态:不够资格和过于固执己见。

**TLDR** : ML(机器学习)从数据中学习(类似于统计学)，而传统方法(专家系统)是手工定制的。在实践中，ML 优于专家系统。

一般外行人对人工智能的概念实际上更接近于专家系统。(虽然我怀疑随着 ML 在媒体上越来越受欢迎，这种情况正在慢慢改变。)在这篇文章中，我将通过多个例子来展示不同专家系统和 ML 的区别。

(从技术上讲，专家系统和 ML 都是 AI。然而，如今，在 2011 年前后，大多数专家不再认为专家系统是 AI，而是 ML。[这就是为什么我更喜欢 ML 这个术语而不是 AI](https://medium.com/datadriveninvestor/ai-by-any-other-name-would-be-much-better-b42dd8a77c88) 。)

# 一个漂亮的计算器。

*(只是一点有趣的历史。你可以跳过这一节)*

![](img/ecb2e623daf56e674ee3a5a8af7f5e8e.png)

The earliest computers were just glorified calculators. Photo by [Charles Deluvio 🇵🇭🇨🇦](https://unsplash.com/photos/zGn2cg9qBvU?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/scientific-calculator?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

第一台计算机只不过是一个美化了的计算器。如果你想快速地多次做同样的计算，计算机是个不错的选择。你只需编写一次代码，它就会为你完成计算。希望比人类更快，更便宜，更准确。

(关于“男人”那部分我是开玩笑的。曾几何时，电子计算机的性能和准确性与人类计算机不相上下。是的，即使是最早的电子计算机也有缺陷和错误。是的，“计算机”一词最初指的是进行数学计算的人。这些人类电脑中有许多是女性。我至少看了一部关于它的电影。)

美化了的计算器有用的实际历史例子:炮兵射表。在第一次世界大战的堑壕战中，火炮是一件大事。然而，瞄准火炮并不容易。你需要解决一个微分方程，同时考虑到以下因素:敌人有多远，高度差，你使用的子弹类型，科里奥利效应，空气摩擦，风。让炮兵队每次设置都解这个方程是不现实的。你需要教寿命很短的士兵高等数学。另一个选择是尝试和错误。不幸的是，这将浪费大量的弹药和时间(曳光弹对此很有用)。希望有经验的士兵能有更好的猜测。

还有更好的解决办法:[射表](https://apps.dtic.mil/dtic/tr/fulltext/u2/826735.pdf)。基本上，事先做好数学计算，所以战场上的士兵只需要在几个表上找到相关的数字，然后进行简单的计算。然而，需要做的数学工作非常多。这就是计算机出现的地方。解一个微分方程可以转化为做一系列的计算，而这些计算又可以转化为计算机的指令。这就是被美化的计算器的优势所在。事实上，最早的计算机之一，叫做 ENIAC，就是这样做的。

> 一个熟练的人用一个台式计算器可以在大约 20 小时内计算出一个 60 秒的轨迹；Bush 微分分析仪在 15 分钟内产生相同的结果；但是 ENIAC 只需要 30 秒，比飞行时间还短。来自: [ENIAC:军队支持的革命](http://ftp.arl.mil/~mike/comphist/96summary/index.html)。

这在解开纳粹密码之谜、制造核武器和将人送上月球方面继续发挥着作用。在此期间,“编程”一台计算机实际上就是修补物理线路，这是一个非常乏味的过程。

![](img/71fe38955eacd88b0353290fa8e51533.png)

With calculators less powerful than most of today’s smart phone, we went to space. Photo by [SpaceX](https://unsplash.com/photos/-p-KCm6xB9I?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/rocket?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 专家系统

当编程变得更容易，计算能力增加时，关于“聪明/智能”计算机的理论想法变成了现实。如果你能把人类的“思维”分解成一套计算机指令，你就能拥有一个专家系统。这些程序被认为是“智能的”,因此是第一代人工智能。

例如:井字机器人。一个 3x3 井字游戏可能只有有限的几个游戏。有两种方法可以制作井字游戏机器人。首先，你可以编写一系列的“如果敌人移动到这里，那么我就移动到这里”来涵盖所有可能的场景。另一种方法是“蛮力”。计算机可以模拟所有可能的合法行动，并选择一个能确保胜利的行动。

例子:象棋机器人。国际象棋对于专家系统来说更难。有这么多合法的举动，这么多的可能性。有太多的计算来找出所有可能的移动。那时的计算机(甚至可能是现在？)没有足够的力量来检查它们。所以如果他们想制造一个象棋机器人，他们必须更聪明。为了解决这个问题，他们请来了象棋专家。同样，像井字游戏一样，有两种方法来处理这个问题，最终结果是两者的结合。

![](img/72f13120730bc673d867b93df6982a41.png)

The earliest chess bots are just wisdom of chess experts written as instructions for machines. Photo by [rawpixel](https://unsplash.com/photos/or9ZQ9Y4VAw?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/chess?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

第一种方式是一系列“如果那么”来涵盖很多典型场景。基本上就是把国际象棋的开局转化成计算机的指令。第二种“暴力”方法是不可行的，所以他们必须更加聪明。

专家们已经发展出一套智慧，给每一件作品赋予一个数字值。例如，棋子的值为 1，皇后的值为 9。还设计了更复杂估价系统:

> 棋子的位置也有很大的不同，例如靠近边缘的棋子比靠近中心的棋子价值低，靠近晋级的棋子价值高得多，控制中心的棋子价值高于平均水平，被困住的棋子(如[坏主教](https://en.wikipedia.org/wiki/Bad_bishop))价值低，等等。来自[同一个维基链接](https://en.wikipedia.org/wiki/Chess_piece_relative_value#Standard_valuations)。

提前 50 步进行野蛮的搜索来看谁会赢是不可行的。然而，只需提前 5 步进行野蛮搜索，看看谁将获得最多的总碎片值是可行的。(由于我资历不足且过于固执己见，本段中的所有数字都是虚构的)。这方面最著名的例子是[深蓝击败了当时的世界冠军(查看维基链接中的非虚构数字)](https://en.wikipedia.org/wiki/Deep_Blue_(chess_computer))。

这是专家系统的标志:

1.  召集专家达成共识
2.  根据共识制作流程图
3.  在机器上实现流程图

# 复杂的算法

为了说明我是多么的不合格，我将随意地把一些不同的算法归为一类，这个类别的名字叫做:复杂的算法。

有些问题需要的不是特定主题的专业知识，而是聪明算法的发明。这些问题的例子包括:解决一个迷宫，排序大量的数字，寻找最短的路径。不幸的是，我不能给门外汉解释这些算法的工作原理，因为它们本质上是非常技术性的。然而，这些算法与专家系统相似，从某种意义上说，一旦它们被制造出来，就不能再改进了。

![](img/6fbab526858410664ca8bc6340830129.png)

Invention of clever algorithm, like Google’s PageRank, can make machine appears smart. Photo by [Markus Spiske](https://unsplash.com/photos/70Rir5vB96U?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

一个最好的例子就是 PageRank，Google 第一次迭代背后的算法。拉里·佩奇和谢尔盖·布林没有让一群互联网专家想出搜索网页的方法，而是把 PageRank 作为他们博士论文的一部分。

# 下一步是什么？

让我们回到象棋中的蛮力。如果有足够的处理能力，机器可以模拟所有可能的游戏，并且 100%获胜，就像人类可以玩井字游戏一样。然而，可用的处理能力往往远远小于我们试图解决的问题，因此，非常简单的算法，如蛮力搜索(和[贪婪](https://en.wikipedia.org/wiki/Greedy_algorithm))通常不会给出最佳答案。

一组人类专家(通常是主题专家、数学家和计算机科学家的组合)可能会聚在一起，提出比简单的野蛮搜索更好的解决方案。然而，在处理难题(比如象棋)时，我们离获得最佳解决方案还非常遥远。

更重要的是，我们的算法不能超出人类想象力、创造力和偏见的能力。机器能想出比人类更好的算法吗？

# 人类学习:统计学

在我们讨论机器学习之前，让我们先多思考一点人类的学习(阅读:认识论)。学习是一个自然的过程，我们从经验中获得。也是一个主观的过程；不同的人可能从相同的经历中得出不同的结论。但是一定要这样吗？有没有可能构建一个客观的学习框架，这样，当给定相同的数据时，人们总是会得出相同的结论？是的，答案是，统计学。

例如:井字游戏。让我们收集一千个井字游戏。然后，我们可以从这些数据中进行统计。例如，平均而言，第一步应该在中心、侧面还是角落？

比如:象棋。棋子值由象棋专家在专家系统框架下确定。专家之间确实存在一些分歧。但我们总是可以收集一百万盘棋，让统计学家，而不是象棋专家，来对棋子进行更客观的估价。

事实上，统计学是机器学习的最简单版本。许多机器学习课程和教科书都是从线性回归开始的。许多研究也使用线性回归作为基线比较。

对于那些不熟悉线性回归的人。简单地把它想成一个有输入和输出的数学等式，例如 y=2x+3。你输入 x 的值，比如 5，它会输出 y 的值，比如 13。

更复杂的版本将接受当前棋盘位置作为输入，每个棋子的值作为输出。现在，有许多可能的方程可以使用，线性只是其中之一。(多项式，如果你知道是什么，那就是另外一个。)

# 最后，机器学习

机器学习就像另一类“方程”(正式名称为模型)，但更好。常见渗入主流媒体的模型有:trees 和 ANN(人工神经网络)。树的改进版本被恰当地称为随机森林，而人工神经网络的改进版本是现在著名的深度学习。

这是我能想到的对机器学习最好的类比。它既不做任何神奇的事情，也不模拟人类的思维或智力。它基本上是运行一组指令来对任何给定的数据执行非常复杂的“统计”。

![](img/33bbb86cbc8809d1f5b9525a544873af.png)

If human can learn from any arbitrary data by using statistics, so can machines. Photo by [William Iven](https://unsplash.com/photos/jrh5lAq-mIs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/chart?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

说到这里，结果还是很惊人的。在许多不同领域，从识别人脸到将语音转换为文本，它可以做出比我们所知的任何传统统计更准确的预测。很多时候，胜过人类专家。

它并非没有弱点，我将在另一篇文章中讨论。