# 创业成长的烦恼:质量控制

> 原文：<https://medium.datadriveninvestor.com/startup-growing-pains-quality-control-dca84b4980ff?source=collection_archive---------10----------------------->

[![](img/b2f394b4538ffa1249a9a135ea85e615.png)](http://www.track.datadriveninvestor.com/1B9E)

## 如何验证软件质量以推动产品成功

![](img/a716665ad6a9c606dd23d331a9e46c83.png)

Photo by [Sarah Kilian](https://unsplash.com/@rojekilian?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

初创公司早期的许多时间都花在了通过迭代定义产品、创建概念验证原型和收集用户反馈以确定产品是否适合市场上。

随着时间的推移，原型被改进，它们最终需要融合和成熟，成为人们可以支付和使用的实际产品。在这一阶段，出现了额外的需求，例如对稳定性、健壮性和响应性的需求，而不考虑用户群的负载和异构性。

接下来发生的就是人们通常所说的*产品化:*一种重构/重写练习，采用现有的代码库，并使其符合这些新的需求，这样就可以创建一个可销售的产品。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

一旦产品准备好了，就需要验证这些要求，以证明它确实可以销售。这种认证也不仅仅是一次性的活动，它是一个随着产品的增长和扩展而持续进行的过程。

在我们的精益创业中，我们可以使用什么流程来持续执行这种验证？质量控制，更具体地说，它的工程驱动版本被称为质量工程。

# 什么是质量工程？

![](img/c0e36c691a53d6a651369b61d58c6143.png)

Photo by [Dawid Małecki](https://unsplash.com/@djmalecki?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

质量工程(QE)是通过使用独立的工具和自动化来确保软件质量的实践。这些用于减少质量保证团队需要执行的手工工作，反过来导致被测试系统的更大或更好的覆盖。

可以使用各种工具来测试代码库的不同功能方面，例如用户交互、API 响应和错误条件。其中一些工具是图形化的(基于 UI)，而其他工具需要一些编程知识，因为它们依赖脚本来执行工作。

此外，像传统的质量保证一样，QE 还可以覆盖功能测试以外的问题，如性能和安全性，再次通过专门的软件工具，这些工具很容易在网上找到。

QE 也可以参与单元测试，或者作为工程资源稀缺时的“应急”措施，或者作为让新加入者熟悉产品功能的培训机会。然而，这并不能替代最佳实践，例如测试驱动开发，无论如何都应该执行测试驱动开发，以降低代码更改期间引入 bug 的风险。

# QE 发生在什么时候？

![](img/6c13928cc7ae83ba5a7490c15e90960d.png)

Photo by [Alvaro Reyes](https://unsplash.com/@alvaroreyes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一般来说，QE 活动与 sprint 中的软件实现并行运行，具体来说:

*   在计划期间: QE 评审功能需求，以便准备一个测试计划和一组测试脚本
*   **在实现期间:** QE 在代码开发的同时实现测试计划及其脚本，留意可能出现的变化，并相应地调整计划
*   **实现后:** QE 对发布候选进行测试，如果所有测试都令人满意，则认证代码发布

这最后一步显然是最耗费资源的，因此，假设 QE 团队的规模合理，它可以与下一个 sprint 的计划阶段重叠。否则，软件开发工程师可以在实施结束时帮助执行测试，以更长的冲刺周期为代价，减少 QE 的专门人员。

当使用这种策略时，通常好的做法是轮换工程师，这样他们就不会直接测试他们自己编写的代码，从而避免测试偏差。

# 为什么 QE 很重要？

![](img/6d288c9d7f4ad8cd97f54ef4c6a14b1f.png)

Photo by [Tim Gouw](https://unsplash.com/@punttim?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

QE 团队的任务是从技术角度证明正在生产的软件适合发布。在实践中，这转化为降低发布后用户群的意外和异常的风险，这些意外和异常可能导致业务损失和/或对公司声誉的损害。换句话说，它帮助你晚上睡得更好。

尽管通常在软件开发团队和它的过程上花了很多心思来实现良好的速度，但是缺乏良好的质量控制真的会使所有这些努力无效，因为需要快速解决的意外错误会抛弃任何先前的开发计划，并使团队的速度停止。

此外，在变革管理的背景下，QE 可以提供很大的帮助。当好的自动化脚本就位时，可以快速准确地评估和验证代码库变更的影响，从而简化管理和交流这些变更的过程。

到目前为止，我们已经将质量工程视为一套帮助我们确定我们的软件是否可以发布的实践。现在让我们看看 QE 的人员方面，以便我们可以开始建立我们的团队。

# 质量工程师的简介

![](img/29c93073360f9737484ae3b2b9b9e773.png)

Photo by [Arif Riyanto](https://unsplash.com/@arifriyanto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一个质量工程师通常是一个非常注意细节和有好奇心的人。他们不太关心架构/软件设计，他们更关心的是理解一些东西是如何工作的，以及他们如何利用它来实现与预期不同的行为。

因此，他们解决问题和排除故障的技能实际上非常类似于软件开发工程师的技能，尽管他们以不同的方式应用。

反过来，他们编写的自动化脚本在遵守编码标准和最佳实践方面可能会遇到松散的情况，因为他们的目的只是在受控环境中执行特定的活动。

这有点自相矛盾，因为这些脚本的目的恰恰是暴露测试主题中有时引入的错误情况，正是因为对编码标准和最佳实践的不良坚持。这可能是软件开发工程师在审查质量工程代码时最头疼的问题。

创造力对于质量工程师来说也扮演着重要的角色，尤其是在功能测试的环境中，因为自动化测试需要模拟现实世界中不同用户的不可预测的行为。

# 建立你的 QE 团队

![](img/80bf4955c56ad0577fbd627ec8f1d397.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

招聘并不是建立 QE 团队和实施其实践的严格必要条件。否则，我们不会在精益创业的背景下谈论它。

考虑到质量和软件开发工程师档案之间的重叠，我们可以通过在软件开发团队中轮流分担 QE 的职责来开始。与此同时，我们可以开始寻找一位 QE 经理来进一步发展，或者在团队中物色一个人来担任这个角色。

注重细节的高级工程师或首席工程师是这个职位的理想人选，因为他们可以专注于大局，处理运营问题，同时将脚本任务委派给被分配轮流履行 QE 职责的工程师。

就过程的实现而言，良好的第一步是选择质量工程的一个特定方面，并将其作为工程团队工作的软件开发“项目”来构建。

这可能意味着，例如，在 web 应用程序的情况下，通过 [Selenium](https://www.seleniumhq.org/) 实现登录屏幕的自动化功能测试，或者打包自动化单元测试，以便它们可以通过直接来自 CLI 的单个命令来执行。当实现一个持续集成系统来直接验证对代码库所做的更改时，这在以后也会变得很方便。

# 包扎

![](img/cbd3afcb695f609cb00e52f62c0bd0fd.png)

Photo by [Jesus Kiteque](https://unsplash.com/@jesuskiteque?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这个简短的介绍中，我们看到了质量工程如何在软件产品/服务交付给客户之前帮助确保构建质量。这类似于传统 QA 团队所扮演的角色，但由于使用了工具和自动化，人员参与更少，效率更高。质量工程涵盖的常见测试方面包括:

*   **用户交互:**模拟最终用户在软件/服务中采取的步骤，并期待意想不到的结果
*   **API 验证:**确保对 API 的更改不会破坏现有的消费者代码
*   **弹性/可靠性测试:**模拟成千上万的用户同时使用系统
*   **稳定性测试:**确定应用程序在面对意外输入时是否会崩溃，通常通过用户界面上的随机点击来模拟
*   **性能测试:**收集与一组预先确定的用户步骤的执行相关的指标
*   **回归测试:**每当一个新的构建可用时，运行以上所有的测试，并将结果与之前的运行进行比较，以确保现有的功能没有被破坏或者被无意中改变

我们还看了质量工程师与软件开发工程师的区别，这在两个方面帮助了我们:

*   在短期内，它允许我们建立团队，而不必出去立即招募专门的资源
*   从长远来看，它有利于通过挑战一些来自更传统背景的开发人员对从事质量保证工作的人的偏见来创建一个更有凝聚力的团队，尽管这些误解可能是不公平的

最重要的是，我希望这篇文章能提高人们对结构化质量控制实践的好处的认识，不管创建它的团队有多大，只要涉及到面向客户的产品。这不仅适用于基于软件的产品，也同样适用于客户参与网站和应用程序。

毕竟，这是领导对你的品牌的第一次审视。如果他们只是因为用户在注册你的时事通讯时输入了一个比平常更长的电子邮件地址而崩溃，那么你的公司和产品会有什么样的形象呢？

谢谢你坚持到最后。我希望你喜欢这篇文章，如果需要的话，我会很高兴参与这个话题的进一步讨论。请在下面分享你的经历和想法，我会非常乐意继续对话。

同时，祝你一路顺风，继续做好事！