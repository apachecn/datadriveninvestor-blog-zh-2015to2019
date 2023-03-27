# Concourse(不)什么时候适合你？

> 原文：<https://medium.datadriveninvestor.com/when-is-concourse-not-for-you-cbb33649d5e0?source=collection_archive---------6----------------------->

[![](img/25a862897bece73b27ad82310615787c.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/6506ccbf9c86aadc3abc61bdeab4f791.png)

Photo by [tian kuan](https://unsplash.com/@realaxer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# **TLDR；**

与詹金斯相比。

*   没有重复构建(但有解决方法)
*   管道是静态的，由管理员应用。
*   一个管道，一个分支。
*   复杂和多源或依赖是可能的。

—

# 自带构建工具

我喜欢在容器上运行资源和任务的 Concourse 概念。它解决了我在使用 Jenkins 时遇到的管道可移植性问题。作为用户，我不再需要依赖 CI 管理员来安装插件。我可以从管道代码本身控制构建的每个方面。这也可能意味着更多的团队可以使用相同的 Concourse 安装。

concourse 中的每种资源都提供 3 种功能:检查、进入和离开。它可以是任何东西。例如:源存储库、s3 存储、电子邮件通知系统。

[](https://www.datadriveninvestor.com/2019/03/26/agile-management-the-good-the-bad-and-the-downright-ugly/) [## 敏捷管理:好的、坏的、丑陋的|数据驱动的投资者

### 公司不断重塑自己，以获得或保持竞争优势和市场份额。这是…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/26/agile-management-the-good-the-bad-and-the-downright-ugly/) 

# 管道基本

当我开始使用 Concourse pipeline 时，我有一套假设，认为它将类似于 Jenkins 所拥有的——除了容器原生部分。只是最近我才注意到它有另一个根本的不同。

在詹金斯，CMIIW，来源是核心。其他一切都建立在与源头的互动之上。应用于源的管道。这使得在树枝上工作变得很自然。一旦构建开始，无论何时我们引用源代码，它都将使用相同的版本。构建作业本身将保留该版本，因此以后可以在完全相同的版本上重新构建。

这不是 Concourse 所能提供的。源代码是一种资源。资源有版本。然而，没有分支的概念。因此，处理拉取请求有时会很困难。如果每个建筑都是绿色的，就不会有任何问题。但是有时由于依赖关系的变化，您会得到不稳定的构建或者只是想要重新构建。

Jenkins 和 Concourse pipeline 也有根本的不同。在詹金斯，管道是来源的一部分。而在 Concourse 中，管道是一个独立的实体，可以与代码交互。在詹金看来，这更像是一份工作。

必须在运行管道之前应用管道。在 Jenkins，管道就像作业开始时运行的脚本。当您将更新应用到管道时，所有生成都将使用它。它不能与源代码一起发展。

# 高级管道

因为管道不是代码的一部分，所以您可以构建一个跨越多个存储库的管道。

你可以从引入 10 个存储库开始，用它做一些事情。将工件(使用外部存储)传递给下一个作业。再拉不同的 10 件事等等。

可以定义作业依赖关系，因此您可以将作业设置为仅在 10 个不同的作业无错误运行时运行。

我仍然记得在詹金斯联系工作有多难。

# 秘密

Jenkins 附带电池。秘密管理与安装捆绑在一起。相比之下，默认情况下，concourse 只会给你提供在其上构建东西的基础设施。您需要自己带来秘密管理—这意味着存储和 UI。Concourse 实际上并没有将 secret 视为 secret，它只是由外部保险库提供的参数。

# 作业参数

在 concourse 中，作业由任务组成。任务可以定义其所需的参数。默认情况下，它将从外部 vault 中提取参数值。如果我们要手动触发作业，我们必须指定每个参数的值。

# 那么，是给我的吗？

是的，它符合我的需要。我想要基础设施的可移植性和可重复性。我能够使用 Docker 设置 Concourse 并要求保险库。然后，添加一个非容器工作器来在 macOS 上运行任务。我不需要处理任何插件。我可以获取任何我想要的资源，并将其添加到任何需要它的管道中。其余的是外壳脚本。

你可以用任何你想要的语言构建你自己的插件——只需发布一个 Docker 图片。很容易找到要挂钩的扩展点。