# Python 2 EOL —现在怎么办？

> 原文：<https://medium.datadriveninvestor.com/python-2-eol-now-what-e48fb2efca3c?source=collection_archive---------14----------------------->

![](img/9f12a03aa15ecb3c5f9cdd249e983d67.png)

Python 2 — The Time is Running Out

如果您和大多数 Python 开发人员一样，那么您已经使用 Python 2 很多年了。现在，随着 Python 软件基金会宣布 Python 2 的生命周期结束(EOL)，核心开发团队将从 2020 年 1 月 1 日起不再支持、更新或提供 Python 2 的新版本。

作为一名开发人员，您可能更喜欢采用 Python 3，但是出于各种原因(公司政策、资源缺乏、法律限制、合同义务等。)，在可预见的未来，您的组织可能会在 Python 2 上维护现有的应用程序(甚至继续使用 Python 2 开发)。那么你能做什么呢？

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

# Python 2 EOL 的影响

你的 Python 2 应用程序将持续运行到 2020 年 1 月 1 日——它们不会自毁——但随着时间的推移，它们会变得不那么可靠，也更容易受到攻击，因为会出现错误、安全问题和 CVE。一些需要考虑的事情:

*   Python 2 核心团队不会对 Python 2 解释器或 Python 2 标准库提供官方支持。此外，[不保证](https://discuss.python.org/t/packaging-and-python-2/662/98)Python 打包权威机构(PyPA)或 Python 包索引(PyPI)将在 EOL 日期后的任何时间内继续支持 Python 2。
*   开发 Python 2 和 Python 3 版本包的社区开发人员将降低开发 Python 2 代码的优先级。事实上，许多作者已经表示，他们在[流行的 Python 2 包](https://python3statement.org/)上的所有工作将在 2020 年被放弃，只支持 Python 3 的开发。
*   现在提供 Python 2 发行版的供应商(比如 Linux 供应商、Docker、云供应商等)可能会逐渐停止对 Python 2 的支持。虽然 Python 2 产品不太可能在 2020 年 1 月 1 日从目录中消失，但随着时间的推移，它们的支持范围可能会变得有限。

例如， [AWS 的 Lambda 支持页面](https://docs.aws.amazon.com/lambda/latest/dg/runtime-support-policy.html)声明不推荐使用的运行时不能用于创建新函数，但仍然可以用于处理调用事件。

# Python 2 EOL 支持选项

如果您不愿意或不能将 Python 2 应用程序迁移到 Python 3，那么未来并不像您想象的那样不稳定。IT 领域充斥着操作系统的部署(有人知道是 Windows XP 吗？)、应用程序(如 Internet Explorer 6，它顽固地拒绝消亡(T1)以及各种技术栈的旧版本(COBOL、Java 等)，这些技术栈已经正式过时，但仍在继续使用。

在每种情况下，组织通常采用两种常用策略之一:

*   **自己支持它** —如果你已经使用 Python 2 很多年了，你应该熟悉如何支持你自己的 Python 2 代码。但是，这种自助支持通常仅限于调查新出现的错误/漏洞，并在必要时应用官方更新或升级。当您需要修补/升级不是您自己创建的包，测试它的依赖项，甚至更新那些依赖项时，情况就不同了。
*   **寻找商业供应商** —在某些情况下，您可以从第三方商业支持供应商处购买扩展支持。ActiveState 就是一个很好的例子。

# Python 2 的自我支持与商业支持

如果您自己决定支持 Python 2，那么您应该考虑许多选项，包括:

*   **内部 Python 2 专家**——成为组织中专门的 Python 2 专家是一个有价值的(尽管有限)职业发展。或者，您可以建议从社区中雇佣一名 Python 2 专家。不幸的是，不能保证这些专家不会离开组织，而且随着 Python 2 的老化，雇佣替代者会越来越难。
*   **外包** —传统的咨询公司总是愿意承担您的 Python 2 支持和维护工作，允许您转移到更新的技术栈，在那里您可以为组织增加更多价值。当然，随着 Python 2 专业知识的逐渐枯竭，外包费用可能会变得非常昂贵。
*   **赞助** —就像组织可以赞助开源作者通过 [OpenCollective](https://opencollective.com/) 这样的服务开发当前技术一样，赞助 Python 2 作者继续维护您需要的一两个关键包也是可能的。不幸的是，如果您的应用程序有几十个关键包，这样的解决方案根本无法扩展。

或者，ActiveState 在停产日期之后为 Python 2 提供商业支持，在社区支持到期后为您的 Python 2 应用程序提供安全修复。点击阅读更多关于该产品的信息[。](https://www.activestate.com/resources/datasheets/python-2-eol-commercial-support/)

# Python 2 EOL 调查

随着 Python 2 即将于 2020 年 1 月 1 日停产，了解企业如何为这一变化做准备比以往任何时候都重要。考虑到这一点，ActiveState 目前正在进行一项 [Python 2 寿命终止(EOL)调查](https://www.surveymonkey.com/r/XH9CQCJ)。

任何编码、测试、部署、运行、管理或使用 Python 2 应用程序的人都可以完成，所有参与者都将收到一个调查结果的链接。