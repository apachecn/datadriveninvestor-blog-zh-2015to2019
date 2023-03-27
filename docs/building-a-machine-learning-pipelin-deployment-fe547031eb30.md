# 构建机器学习管道—部署

> 原文：<https://medium.datadriveninvestor.com/building-a-machine-learning-pipelin-deployment-fe547031eb30?source=collection_archive---------11----------------------->

欢迎回来！希望你喜欢前两篇关于构建机器学习管道的文章([第一部分](https://medium.com/datadriveninvestor/building-a-machine-learning-pipeline-exploration-and-data-processing-13b465e23898)，[第二部分](https://medium.com/datadriveninvestor/building-a-machine-learning-pipeline-modeling-3a5382412041)给错过前两篇的读者)。在本文中，我们总结了构建机器学习管道的理论之旅。下一篇文章将着重于构建概念证明。没有别的告别了，让我们开始吧！

现在我们有了数据和合适的模型，是时候让模型变得可访问和可用了。

![](img/d2a9de5fbc4ddd3eed10f21da088aa80.png)

概括来说，部署阶段包括两个方面

1.  部署到真实环境
2.  观察并改进模型

[](https://www.datadriveninvestor.com/2019/02/18/the-challenge-of-forex-trading-for-machine-learning/) [## 机器学习的外汇交易挑战|数据驱动的投资者

### 机器学习是人工智能的一个分支，之前占据了很多头条。人们是…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/18/the-challenge-of-forex-trading-for-machine-learning/) 

有几种方法可以部署您的模型。我们将很快介绍这些内容，但在此之前，请考虑以下内容:-

预测类型

1.  批处理—在这种情况下，模型可以作为后台进程，当数据在数据仓库中可用或上传到文件存储(如 Azure Storage Account 或 AWS S3)时触发。例如，报告或预测引擎通常不需要实时预测/分类。
2.  实时/按需—我们希望我们的模型能够根据输入提供实时预测。比如基于机器学习的推荐系统、面部识别、自然语言处理等。

观察和改进模型的能力

1.  能够检索和分析性能指标是确保您的模型满足用户需求并交付价值的关键。
2.  如果模型不是高性能的，那么需要一种相当简单的方法来测试、更新/替换模型，同时将停机时间和编程更改降到最低。可以通过路由输入数据来应用 A/B 测试原则，以生成潜在替代或下一代模型之间的比较指标。

根据我们正在处理的用例，可能适用一个或多个部署解决方案:-

1.  直接注入——如果您有一个定制的应用程序或者一个可以很容易地修改以合并新模块的应用程序(可能是一个移动应用程序),那么可以选择这个选项。将经过训练的模型作为组件直接注入到应用程序中，将允许您确保处理尽可能地接近用户交互和输入参数。最小化数据移动和减少延迟有好处，尽管代价是相互依赖和系统耦合，因为这种方法可能需要重新编码模型或提供包装器，以便将其作为应用程序的一部分嵌入。
2.  转换和导入-如果最终落脚点是可以导入使用 PMML 或 PFA 编码的模型的数据挖掘或分析引擎，那么将模型转换为可移植格式(如预测模型标记语言(PMML)或可移植格式分析(PFA ))可能是有意义的。这是我最不喜欢的选项。
3.  部署为服务——随着越来越多的应用程序迁移到云，通过 Google 的云 ML 引擎或 AWS SageMaker 部署您的模型为您提供一个按使用付费的可扩展堆栈。我的下一个博客系列实际上将是使用 AWS SageMaker 演示整个机器学习管道的概念验证。

现在就这样了。在过去的几周里，我们讨论了构建机器学习管道的三个阶段。每个阶段都同样重要，但一切都始于数据！如上所述，接下来是我们所学的所有概念的实际应用。