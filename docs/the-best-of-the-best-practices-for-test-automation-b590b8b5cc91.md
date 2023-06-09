# 测试自动化最佳实践中的“最佳”

> 原文：<https://medium.datadriveninvestor.com/the-best-of-the-best-practices-for-test-automation-b590b8b5cc91?source=collection_archive---------1----------------------->

[![](img/173cf818ee2f94232bf0789796e4d724.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/31d78f951fd737acde9e4623f1834fb6.png)

如果我要写测试自动化的好处，请放心，你会读到它提供的增强的可靠性，它的激光般的准确性，以及深远的覆盖面。当然，我肯定会强调它如何能够极大地提高产品质量，缩短上市时间，也许最有价值的是，它会带来很高的投资回报。

然而，我并不是在写[测试自动化](https://perspectives.mobilelive.ca/blog/test-automation-excuses)的好处，尽管当一切都像那样展开时，它们确实令人印象深刻。相反，我选择写一些比测试自动化给你的业务带来的好处更有价值的东西——以及如何实现它们。就像大多数做好的事情一样，它需要正确的程序、正确的策略，当然，还有“正确的”最佳实践。

[](https://www.datadriveninvestor.com/2019/02/12/ready-or-not-the-revolution-is-upon-us/) [## 不管准备好了没有，革命就在我们面前——数据驱动的投资者

### “对于技术如何影响我们的生活和重塑经济，我们必须形成全面的全球共识……

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/12/ready-or-not-the-revolution-is-upon-us/) 

今天，我们将深入那些最佳实践，这样您不仅可以从您的测试工作中获得最大收益，还可以交付最高的 ROI。

![](img/c4baa287e4200cf2c0fada240c8d6a93.png)

# 确定要自动化的测试用例

首先，您需要接受自动化所有测试是不可能的。我们知道，我们试过了。但是知道了这一点，选择自动化的测试用例就变得更加重要了。

本质上，测试自动化的真正价值来自于任何给定的测试可以重复多少次。如果一个测试只需要执行几次，最好还是手工测试。根据经验，频繁运行并需要大型数据集来执行相同操作的测试用例是自动化的理想候选。

下面是一些测试类型的完美例子，它们可以从自动化中受益匪浅:

*   容易出现人为错误的测试
*   跨多个版本运行的重复测试
*   需要大量不同数据集的测试
*   手动完成时需要大量精力和时间的测试
*   跨不同硬件、软件平台和配置运行的测试
*   手动运行根本不可能或不可行的测试

[![](img/0a183941cbc10e3c2338aa649b4273ea.png)](https://cdn2.hubspot.net/hubfs/1644951/mobileLIVE__Test%20Automation%20Guide%202019.pdf)

# 根据技能水平划分你的努力

虽然认为 QA 团队中的每个人都处于相同的技能水平是件好事，但事实是很少会这样。考虑到这一点以及测试创建是测试自动化的关键这一事实，根据您团队的技能水平和所选择的工具来相应地划分您的工作是至关重要的。请允许我详细说明。

如果您选择使用开源工具，那么您的自动化工程师必须拥有足够的编码技能来充分利用它，甚至完全利用它。然而，这并不是说初级工程师不能使用测试自动化。根据您选择的工具，比如某些专有的工具，所有技能水平的 QA 工程师都有能力在最少的培训或指导下创建测试脚本。

填补任何技能缺口或缺乏基础设施的另一条途径是将流程的某些方面外包给有技能和经验的合作伙伴。这可能包括从战略、概念验证、脚本开发、基础设施设置，甚至研讨会和实践培训的所有内容。

![](img/0d5dcdb74ce05b27afa81b8b981ab68f.png)

# 选择正确的测试自动化工具

有些人会说选择一个自动化测试工具对于测试自动化是必不可少的。我们认为选择正确的工具才是真正的不同。然而，快速的 Google 搜索会告诉你市场上有数百种不同的测试自动化工具可供选择。

那么你从哪里开始呢？

以下是选择适合您的工具时要考虑的一些基本准则:

**灵活性:**你的团队不太可能都处于相同的技能水平，这就是为什么你需要选择一个每个人都能使用的工具。例如，如果您缺乏编写自动化测试脚本的专业知识，您将希望确保该工具提供了一个替代方案，比如执行关键字测试的能力。

**可支持性:**可用的工具通常是平台和技术教条式的，这意味着您不会经常遇到支持多种平台和技术的工具。确定您正在测试什么以及跨什么操作系统，然后确定哪个工具最能支持您的工作。

可重用性:测试自动化最重要的好处之一是它能够重用测试，这就是为什么你需要选择一个工具来做这件事。它是否允许您创建不仅可重用，而且可维护的测试，更重要的是，抵抗应用程序中的 UI 更改？

![](img/72093efe569d97ce2ae2702726003367.png)

# 如果你想要好的测试，你需要好的数据

也许测试自动化最无聊和耗时的方面之一是测试数据的创建。可悲的是，它令人厌烦的事实丝毫没有降低它的重要性。

创建测试数据，更确切地说，良好结构化的测试数据，无疑是一项值得您花费时间和精力的任务。当您设置了高质量测试数据的基线时，在整个开发生命周期中编写自动化测试就变得容易多了。

当涉及到您的测试数据时，您可以实现的最佳实践之一是使用外部数据源。这背后的原因是，通过使用外部数据，它不仅使您的测试更容易维护，而且更重要的是，可重用。当这些完成后，您可以很容易地添加各种测试场景，通过新数据扩展数据文件，所有这些都不需要对原始的自动化测试进行任何编辑。

[![](img/0c8ef5ad5a6ff3009c400e898dacf3b3.png)](https://cdn2.hubspot.net/hubfs/1644951/mobileLIVE__Test%20Automation%20Guide%202019.pdf)

# 向左移动以获得最大结果

为了最大化您的测试自动化工作，您需要尽可能早地开始您的测试，并且根据需要尽可能频繁地开始；或者，正如许多人所知，你需要向左转。

[Shift-Left](https://www.eventbrite.com/e/meetup-test-automation-shift-left-to-get-it-right-tickets-59719482580) 运动是指测试人员和开发人员比以往更早地开始他们的测试工作。原因是当测试在项目生命周期中开始的越早，就会发现越多的错误和故障。像自动化单元测试这样的测试甚至可以在开发的第一天就开始，并用于逐步构建您的测试套件。不需要大量或复杂的解释就能认识到，当错误和故障被更早地检测到时，修复它们比在随后的生产或部署中要快得多，也便宜得多。

如果您希望生产更高质量的产品，减少上市时间，并获得更高的投资回报率，那么我会毫不犹豫地推荐测试自动化作为解决方案。然而，测试自动化的解决方案只有当它被正确地实现并使用最佳实践时才有价值。虽然不是每个业务都是相同的，它们对测试自动化的使用也不相同，但是前面提到的最佳实践都可以很容易地适应，来帮助您最大化您的自动化测试工作。

最初发布于[https://perspectives . mobile live . ca/blog/test-automation-best-practices](https://perspectives.mobilelive.ca/blog/test-automation-best-practices)