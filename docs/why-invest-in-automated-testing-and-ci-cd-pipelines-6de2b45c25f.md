# 为什么投资自动化测试和 CI/CD 管道

> 原文：<https://medium.datadriveninvestor.com/why-invest-in-automated-testing-and-ci-cd-pipelines-6de2b45c25f?source=collection_archive---------3----------------------->

[![](img/82967fe390f4049455990ff71e958538.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/c4690a1379306b4ddf7b8027907efa3d.png)

(Source: [https://unsplash.com/photos/npxXWgQ33ZQ](https://unsplash.com/photos/npxXWgQ33ZQ))

你在研究自动化测试吗？它能为您和您的组织做些什么？或者实现这种自动化测试和 CI/CI 管道值得投资吗？在这篇文章中，我们将从某种高度来看自动化测试能为我们做些什么。

信不信由你，许多组织仍然没有在他们的软件开发过程中实现自动化测试。导致 QA 团队和工程团队之间的工作周转时间在今天的标准中效率低下，而其他组织正在努力使他们的应用程序能够受益于 CI/CD 管道中的自动化测试。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

以下是组织应该投资自动化测试和 CI/CD 管道的一些原因:

# 不容易丢失重要的回归测试用例

在软件工程中，缺陷修复、软件优化和新功能的开发对于使应用程序在生产中稳定、高效和可靠是至关重要的。由于我们经常处理代码变更，我们需要确保无论我们引入什么代码变更，我们都应该运行回归测试，以确保我们没有破坏任何东西。

在进行手动回归测试时，由于它是由一个人完成的，负责进行回归测试的人可能会错过或忽略重要的测试用例，如果不检查这些用例，可能会导致错误的应用程序更新或应用程序发布。或者有时之前报告并修复的问题可能会因为测试人员未能进行适当的回归测试而再次出现。但是当我们自动化测试时，我们减少了忽略重要测试用例的机会。

# 更高效、更主动

由于测试大部分是自动化的，如果不是完全自动化的话，QA 团队可以投入更多的时间来编写错误的测试场景，使应用程序更加可靠。

如果组织在他们的开发过程中建立一个 CI/CD(持续集成/持续交付)过程，他们将会更有生产力和主动性。假设工程团队使用 Git 作为他们管理代码库的方式，假设我们有一个开发分支和主分支。开发分支包含所有最新的特性、优化和 bug 修复，将在 Sprint *结束时发布(假设组织正在使用敏捷 Scrum)。*我们想要做的是，当有人打开指向开发分支的拉请求时，CI/CD 工具将运行 QA 团队在该代码基础上创建的回归测试，以测试该代码基础是否稳定，是否可以安全地合并到开发分支中。此外，当部署到生产时，我们想要做的是将开发分支合并到主分支中，并从主分支创建一个发布标签。我们希望从 CI/CD 工具中设置的是，当创建一个新的发布标签时，它将执行 QA 团队提供的所有测试。当所有测试通过时，它将创建应用程序的可部署状态，工程或开发-运营团队只需在生产中部署即可。

在生产环境中部署应用程序应该谨慎并按计划进行。我认为将构建部署自动化到生产环境有点太冒险了。我们想做的是通过使用像 Docker 这样的容器来简化部署过程。使用容器将确保我们的应用程序在生产中运行良好。

# 伟大的软件交付

如果您正在为您的客户开发软件，那么在我们的软件开发过程中实现自动化测试和 CI/CD 管道将会为组织和客户带来很好的软件交付体验。

这将对我们如何认真对待我们的软件交付工艺留下良好的印象。这会给人留下一个好印象，我们擅长我们所做的，我们是这个行业的专家，我们重视高质量的产品。

# 摘要

测试对于交付优秀的产品至关重要。我们在测试上投入更多是很重要的，因为我们不希望一个有缺陷的软件在生产中运行。这会让我们头疼，最重要的是我们的用户会受到影响。他们可能会觉得我们的软件不可靠，不稳定，选择不再使用我们的产品。从好的方面来看，如果我们聪明而努力地工作，我们会看到我们的用户使用并信任我们的应用程序，从而获得辛勤劳动的好处。