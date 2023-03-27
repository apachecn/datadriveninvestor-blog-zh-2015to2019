# 逃离系统管理员的苦差事，成为一名开发运维工程师

> 原文：<https://medium.datadriveninvestor.com/escaping-the-windows-sysadmin-grind-and-becoming-a-devops-engineer-f366b76093ad?source=collection_archive---------4----------------------->

![](img/fd7632a00f392dc9e7dfed47892a94e7.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 从你目前的角色开始

首先，请注意，任何人都可以在其当前角色中开始使用 DevOps 工具和方法。仅仅因为你的工作描述中没有“DevOps”这个词，并不意味着你必须转换角色。为什么？ **DevOps 是一套做法；**不是职称。DevOps 是关于在开发人员和操作人员之间架起一座桥梁，并确保您所负责的产品在开发、构建、测试、部署和支持的整个生命周期中平稳过渡。

“好吧，可以，但我是系统管理员。我负责管理核心基础设施。我不是开发人员，此外，我知识不够//我太忙//管理层永远不会同意改变我们所有的实践和程序//[在此插入原因]，”你可能会说。*这正是我所想的*——我永远不会有机会进入以开发项目为导向的职业，因为我没有做任何被认为是坚持开发项目实践的事情。

[](https://www.datadriveninvestor.com/2019/03/26/agile-management-the-good-the-bad-and-the-downright-ugly/) [## 敏捷管理:好的、坏的、丑陋的|数据驱动的投资者

### 公司不断重塑自己，以获得或保持竞争优势和市场份额。这是…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/26/agile-management-the-good-the-bad-and-the-downright-ugly/) 

在这篇文章中，我希望向你展示的是你可以从现在的职位上开始做的一系列事情，这些事情会给你在职业生涯中做出真正改变所需的技能和心态。

# 1.找到你的老师

![](img/d3291e345521bf63800f69eabc7f2135.png)

Chalkboard and Macbook Pro not required. Photo by [jose aljovin](https://unsplash.com/@josealjovin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

找一个在以下任一方面有所了解的人:

*   Linux (CentOS/RHEL，Ubuntu)和 Bash
*   计算机编程语言
*   红宝石
*   去
*   …甚至是 PowerShell(稍后将详细介绍)

这可以是你团队中的一员，你组织中的一个单独的团队，甚至是工作之外的朋友或同事。尽可能多地和他们坐下来，一起进行结对编程，这是你的使命。在线观看培训视频和阅读所有你能找到的奥赖利出版物都很好；当两个人坐下来一起做某件事时，才是真正的学习。

一旦你有了这些知识，你就可以…

# 2.自动化、迭代和构建投资组合

![](img/a914d3a24652e5ed19ee3a10be8a8108.png)

Photo by [Christina @ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

找到你讨厌的事情，然后*自动将它们遗忘*。这是你开始建立你的 DevOps 印章的地方，从识别一个潜在的工作的早期阶段，把它分解成它的组成部分，开发一个解决方案(自动化！)，部署它，最后支持它。

一旦你自动化了这个小的(或者希望是非常大的)麻烦，清理你的代码并把它推给 GitHub。“我还不知道如何使用 Git，”你可能会说。现在正是你一石二鸟的绝佳时机。您将在实践中学习 Git，从简单的推和拉代码开始。最终，你会有一大堆工作来证明你知道如何写代码，并且能够创造性地思考。

下面是我几年前做的一件事的例子。我厌倦了在 AD 和 Exchange 中手动禁用用户。这个脚本——以及嵌入我们自动化平台的一项更大的工作——将一个通常需要几个小时的任务简化为一个按下按钮就可以启动的任务，完成后向我们发送电子邮件，并自动通知客户端用户 X 已经*崩溃*。

当你在做这件事的时候，衡量一下你的自动化在减少工作时间或防止支持票方面的影响。这将为你的简历提供证据，证明你所采取的措施和编写的代码对你的组织产生了真正的影响。

最后，不要只是写一个快速的 Python/PowerShell 脚本来做一些*稍微不那么痛苦的事情*。绝对驱动你的心和灵魂去学习如何用适当的日志记录、错误处理和报告来写东西，这样你就可以衡量它有多有效。这会让你成为一名更好的工程师，你未来的自己也会因此而感谢你。

![](img/8843206ecbb55da1357f574f8e0b3ed4.png)

These are the kinds of graphs you’ll want to show to the higher-ups when you describe how effective your “start the coffee machine before I get out of my chair” script is. Photo by [Isaac Smith](https://unsplash.com/@isaacmsmith?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 3.学习配置管理工具

如果你的组织愿意尝试厨师、Ansible 或木偶之类的东西，成为支持这种改变的人。如果您的组织已经在使用一些工具来管理您的服务器/工作站的状态(网络安全管理软件产品、Kaseya 或其他工具)，那么学习如何使用 Chef/Ansible/Puppet 并让它配置您自己的工作站或测试机器。将您编写的任何内容推送到 Git，并不断完善它，直到您自动化了想要配置的每一个细节。如果你正在使用 Chef，如果你学会了如何配置 Chef 服务器并把你的食谱推给它，你会得到额外的奖励！

如果你想试试 Ansible，这里有一些小东西，比如配置 Linux 系统:

```
- hosts: webServers
  remote_user: root
  tasks:
    - name: ensure packages are installed
      yum: name**=**{{item}} state=latest
      with_items:
        - python-psycopg2
        - git
        - httpd
    - name: Add user 'jackmo' with uid 1040 and primary group 'admin'
      user:
        name: jackmo
        comment: Jack Morris
        uid: 1040
        group: admin
```

既然您已经花了一些时间来自动化一些任务，那么您应该更熟悉编码、Git 以及思考如何通过代码而不是 GUI 来解决问题。

一旦您体验并学会了如何使用这些配置管理工具之一，您就可以尝试将它引入您的组织。最起码，对于小的、重复的、具体的任务，看看是不是值得考虑的事情。如果这是你的公司不愿意做的事情，那也没关系——找一些可以自动化的小工作，写一些可行的剧本/厨师食谱，在你自己的时间里实现自动化，然后把它放到你的文件夹里。也许有一天他们会改变主意。如果他们这样做了，那么所有的代码都已经写好了。如果他们不这样做，你可能会发现你的代码在另一个雇主那里很有用。谁知道呢！

# 4.和 QA 团队交朋友

![](img/9d351f1f62135c98e885a430ce0273da.png)

Don’t forget to bring these with you! Photo by [Tu Trinh](https://unsplash.com/@tutrinh?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

以 DevOps 的方式工作意味着您将经常与性能测试人员、安全工程师和 QA 分析师坐在一起，以自动化的方式解决部署、安全缺陷和运行单元/浸泡/性能测试的问题。我全心全意地建议坐下来，学习他们做什么和他们使用什么工具。举例来说，你不需要学习 JMeter 是如何工作的，但是知道你的 QA 团队如何使用它，以及他们是否自动化了他们的任何测试是有帮助的。如果他们使用自动化，尽可能多地了解他们是如何做的，他们遇到了什么陷阱，以及他们背后的思维过程。

虽然这个任务更多的是一个事实调查任务，但是它将让您接触到(希望)新的信息和一个通常直接集成到 DevOps“团队”中的领域。更重要的是，这是你练习理解另一个团队如何工作的 DevOps 艺术的地方。很多时候，你的工作会与这个团队发生交叉，为了能够有效地理解这个问题，你需要知道他们是如何运作的。

# 5.和开发者交朋友

![](img/d8236f0dafdf58ccfd0a598df59f9a57.png)

Photo by [Nathan Dumlao](https://unsplash.com/@nate_dumlao?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

好吧，这不是列表中的第一个原因是因为你不可能概念化整个应用程序是如何编写、构建、测试、打包和部署的，除非你理解如何:

1.  读取代码
2.  写代码
3.  商店和版本代码
4.  部署代码

我在这里可能是错误的，但是我认为在试图理解 Jenkins 管道之前，最好对基础知识有一个很好的理解，该管道构建 Maven 项目并将其部署到 spot EC2 实例以进行集成和性能测试。

再说一次，这是你坐下来学习另一个团队如何工作的机会。这是至关重要的:了解另一个团队是如何运作的——以及该团队与 QA 或变更管理之间的交接点在哪里——是 DevOps 世界中的正常现象。这些交接点可能是您的自动化工具、脚本和管道发挥关键作用的地方。你将被期望扮演一个“胶水”的角色，把所有的东西粘在一起。为了有效地做到这一点，你必须了解所有组件是如何相互作用的。

# 6.申请一个初级职位，放手一搏

好吧，我知道我说过 DevOps 不是一个角色，但这并不妨碍人们在工作论坛上发布类似“初级 DevOps 工程师”的职位这很好——只要你知道 DevOps，根据定义，不是一个角色，而是一套实践，你就很好。

申请一个适合你的初级 DevOps 工程师角色。即使你的大部分经验是自动化 Windows 任务，这也会成为你下一份工作的桥梁，并表明你愿意尝试新事物。它还会让你接触到更多的技术，扩大你的投资组合，甚至进一步扩大你的职业网络。所以走出去，去争取吧！

![](img/a493d91426174167e6fbc25c1a9b5501.png)

Photo by [Nathan Ziemanski](https://unsplash.com/@nathanziemanski?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)