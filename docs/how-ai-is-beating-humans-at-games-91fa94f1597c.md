# 人工智能如何在游戏中击败人类

> 原文：<https://medium.datadriveninvestor.com/how-ai-is-beating-humans-at-games-91fa94f1597c?source=collection_archive---------10----------------------->

## 理解用于人工智能的强化学习和深度 Q 网络(DQN)的基础

你可能听说过 AI 的其他应用，比如模式识别(检测癌症等。).所有这些应用都依赖于监督学习，即给计算机一个带标签的数据集(它知道那是对的和错的)。这些应用程序很棒，但也有一些缺点。由于他们是在数据集之外接受训练的，他们将简单地识别模式并加以利用，而不是探索人类没有的地方。

![](img/4bec6c7a9abfa5853307f96173d5521e.png)

Some of the places where reinforcement learning is being applied today. Currently, it is mainly deployed in smart robotics and games. Credit: [Andrej Karpathy](http://karpathy.github.io/2016/05/31/rl/)

这就是强化学习的用武之地。它既不是有监督的，也不是无监督的学习；它是人工智能的子集。强化学习依赖于一个对人类来说非常直观的概念——**试错**。通过提供奖励来强化积极的行动和行为。大多数情况下，计算机试图做的就是在任何给定的情况下最大化奖励

这种人工智能的方法不是在监督或无监督学习下考虑的，而是它的范式。目前，深度学习(使用神经网络)已经得到了所有的关注；但是，它需要一个带标签的数据集。这可能会有问题，因为对于特定的人工智能应用程序来说，很难获得足够大的高质量数据集。这使得它非常适合 RL，因为它不需要关于其环境的任何过去的信息。

[](https://www.datadriveninvestor.com/2019/02/19/artificial-intelligence-trends-to-watch-this-year/) [## 今年值得关注的 5 大人工智能趋势|数据驱动的投资者

### 预计 2019 年人工智能将取得广泛的重大进展。从谷歌搜索到处理复杂的工作，如…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/19/artificial-intelligence-trends-to-watch-this-year/) 

我发现 RL 令人兴奋的原因之一是因为它在人工通用智能方面的发展。目前 AI 的大部分应用都是指狭义的 AI。这意味着人工智能只擅长做特定的任务。虽然这看起来很棒，但这与实现科幻电影中的 AGI 相去甚远。然而，由于 RL 的本质，它被认为是实现 AGI 的最佳方法之一，因为它模仿了人类的一般学习方法。

假设您正在播放一个看起来像 Packman 的全新视频。当加载游戏时，你变得特别不耐烦，只是跳过显示游戏规则和对象的屏幕。你刚刚在第一轮游戏中加载，但你不知道该怎么办。

![](img/88a292be1eb8c2759c9ad26ddbac482b.png)

除此之外，在顶端有一个分数，并且你正在努力得到可能的最高分。你不知道该怎么做。所以你开始四处走动。你突然被鬼撞了，你就失分了。现在你知道你可能不想接近鬼魂。然后你遇到几个硬币，你看到你的分数迅速增加。现在你知道你需要得到尽可能多的硬币而不被鬼抓住。所以你开始这样做。您可以获得最大数量的硬币。然而，你注意到在游戏区的另一边有一个像门一样的装置。所以，除了利用所有的硬币，你还应该探索那扇门。

# 强化学习的组成部分

我上面提到的系统是模仿强化学习的。所有强化学习系统都由 4 个基本要素组成:

*   一个**代理**(你):被放置在一个环境中，并试图最大化报酬
*   一个**环境**(游戏等级):这些作为代理能做什么和不能做什么的界限。
*   一个**策略**(大脑)它通过检查各种可能性来定义代理在特定状态下的行为
*   A R **ewards 函数**:它设定正在进行的学习的目标。它会给予一定数量的奖励。如前所述，代理人的目的是立即最大化报酬。
*   一个**价值函数**:虽然一个奖励函数对于指导短期行动是非常好的，但是价值函数有助于长期优化。它试图找出从长远来看什么行为会产生最高的回报。
*   一个 **Q 值函数**:它可以被认为是价值和回报函数的组合。基于所选择的动作，它确定哪个状态具有最佳 Q 值(长期回报)。
*   A **型号**:型号和环境不同？

![](img/1e2eeb182bd8f19863e45b814ef54024.png)

# 一切都是数学题！

虽然将代理人经历的奖励和状态概念化可能很容易，但认识到这是一个复杂的数学问题是至关重要的。强化学习的整个过程统称为**马尔可夫过程**，可以分解为马尔可夫奖励过程、贝尔曼方程、马尔可夫决策过程。

警告:了解 RL 是如何工作的并不是这篇文章或项目的后续部分所必需的，但是它为深入研究 RL 打下了坚实的知识基础。

## 马尔可夫性质

马尔可夫属性表明:

> 鉴于现在，未来独立于过去

这一点很重要，因为一旦代理知道了环境的当前状态，它就可以丢弃关于过去的所有信息(内存效率更高)。任何具有马尔可夫性质的状态都被认为是马尔可夫状态。从那里，**转移函数**表示给定当前状态的未来状态的概率分布。

## 马尔可夫过程

马尔可夫过程只是指不依赖于先前状态，而是依赖于具有马尔可夫特性的状态的过程。马尔可夫过程被定义为(S，P ),其中 S 是状态空间，P 是马尔可夫状态的转移函数。

![](img/611fd11de6af4b8a4da850814418c409.png)

A visualization of a Markov Process

## 马尔可夫奖励过程(MRP)

这是一个马尔可夫过程，它基于是另一个马尔可夫过程的序列来确定累积的奖励量。MRP 的定义类似于马尔可夫过程，但有更多的参数:

(法国、巴西、𝛾).除了 s 是状态空间，p 是转移函数，r 是奖励函数，它定义了代理将获得的即时奖励的数量，𝛾是折扣因子。折扣系数告诉代理如何评估当前和长期奖励。例如，值 0 使代理仅针对短期奖励进行优化，而因子 1 使代理最大限度地强调长期奖励

## 贝尔曼方程

为了最大化在特定状态下给出的奖励的总和，代理必须知道函数的最优值，以获得所有可能奖励的最大总和。为此，我们可以使用贝尔曼方程来计算每个给定状态的值函数。它被进一步分解为即时价值回报(忽略贴现因子)和贴现价值函数(包括贴现因子)

直接实现贝尔曼方程是非常低效的内存，因为计算的复杂性线性增加。这对于大多数小型 MRP 来说是没问题的；然而，其他方法，如动态规划，蒙特卡罗和时间差异学习，用于可扩展和有效的解决方案。

## 马尔可夫决策过程(MDP)

马尔可夫决策过程(MDP)可以被看作是一个由马尔可夫状态组成的环境中涉及决策的 MRP。因为 RL 的目的是最大化 MDP，所以在此实施贝尔曼方程。MDP 被定义为具有输入(s，a，p，r，𝛾)的函数，其中 a 被定义为行动的有限选项(在 MRP 中描述了 s，p，r 和𝛾)。首先，MDP 产生一个价值函数，输出集合中任何行动的预测回报。

![](img/ae8d5e63415053b7d3e2ce3b03970e9b.png)

An imaginary student’s MDP with actions. (Credit: David Silvers)

## 而且不止于此

虽然我们已经介绍了 MDP 的基本知识，但 MPs 中还有许多其他过程，如贝尔曼最优方程、最优状态值函数、最优行动值函数和总体最优策略。

> 查看理查德·萨顿的《强化学习简介》，更深入地了解马尔可夫过程

# q 学习

Q-Learning 是一种流行的 RL 算法，用于各种问题。它不同于其他算法，因为它是一个非策略算法。这意味着它独立于主策略，只接受中央策略的操作。

一旦它接收到一个动作，它就试图优化 Q 值。这被称为贪婪算法，因为它只是试图最大化一件事，Q 值。

# 深度 Q 学习

事实证明，实际实现 Q 学习算法有其不利之处。最大的缺点是缺乏通用性。换句话说，代理人不知道在一个看不见的状态下做什么，即使它与已知状态非常相似。

## 有什么解决办法？

神经网络。使用深度神经网络来实现该算法，以增加代理的泛化能力。神经网络的结构相对简单。在这种情况下，您可以将游戏帧输入卷积层以进行边缘识别。然后，一系列完全连接的层可以获取该信息，并输出环境中所有可能行为的 Q 值。

![](img/531148e4a88456fb398fe2bf26a20a3d.png)

Google Deepmind’s DQN architecture.

此外，dqn 采用两种技术来最大化其性能:

1.  **体验回放**:由于普通的神经网络或 CNN 很难处理像视频游戏帧这样高度相关的数据，这通常会导致性能下降。为了抵消这一点，我们可以在一个图像池中存储体验，并在过渡期间重放体验。
2.  **单独的目标网络**:由于神经网络是如此复杂的网络，所以在策略和价值网络之间可能会有很多波动。为了避免这种波动，策略网络的权重取决于价值网络的权重，这使得代理每走 *n* 步就有一个更稳定的学习过程(即时更新会使代理更关注短期回报)

对于所有的数学迷来说，DQN 算法的伪代码应该是这样的:

![](img/80c676faf19ab16636a0c6b55908607e.png)

Credit: Richard Sutton

# 我们来了，乓

![](img/fee7e09bfa6a1c5e00c14b403c151b82.png)

现在我们知道了强化学习和深度 Q 网络的基础知识，我们可以尝试一下游戏机器人。为此，我将 OpenAI 的健身房库用于 pong 环境和代理。然后我将 Pytorch 用于神经网络和其他标准数据科学库。

为此，我将 OpenAI 的健身房库用于 pong 环境和代理。然后我将 Pytorch 用于神经网络和其他标准数据科学库。

> 注 *:* *一个 RL 代理需要很长的时间来训练并达到最佳性能水平(我的机器人在 1000 多场游戏中处于负奖励区* *😬).为了帮助您跳过所有的计算时间和资源，您可以为 DQN 导入现有的重量和大小。然而，对于像 m* e 这样的人来说，看着你的机器人从-21 到+18 是一种令人回味的经历。

![](img/7975f865e48ac33a8a97b72034db18df.png)

The approximate performance of my bot based on another similar bot. Credit: MinPy

# TL；速度三角形定位法(dead reckoning)

> 强化学习是一种依赖于试错的机器学习，它试图最大化给定的回报
> 
> 马尔可夫过程被用来把这个学习问题转化成一个有许多组成部分的数学问题。
> 
> 深度 Q 学习使用神经网络作为其架构，并被用于开发神级 Pong bot

如果你喜欢这篇文章，请随意分享👏并在评论中评论你的想法！如果你想了解涵盖从自我成长到机器学习等方方面面的新文章，请关注我的 Medium。

*我会* ***喜欢*** *去认识新的人，与他人交流，谈论*任何事情*。欢迎通过我的 LinkedIn 或电子邮件联系我:*[【mehta.r.jatin@gmail.com】T21](https://mailto:mehta.r.jatin@gmail.com/)*！*