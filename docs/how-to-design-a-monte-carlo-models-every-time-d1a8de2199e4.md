# 如何每次都设计一个蒙特卡洛模型

> 原文：<https://medium.datadriveninvestor.com/how-to-design-a-monte-carlo-models-every-time-d1a8de2199e4?source=collection_archive---------5----------------------->

每次你想运行蒙特卡洛模拟时，请遵循以下步骤

![](img/0d03568e3ebb5ba4da3db4a0ac53b7e4.png)

Photo by [Luke Chesser](https://unsplash.com/@lukechesser?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/analytics?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

最初是在 20 世纪 40 年代为分类研究而设计的，这种流行的模拟技术对许多样本进行统计分析。由于计算机的限制，早期的应用很少。然而，现在任何拥有笔记本电脑的人都可以使用它。

当你想到我们可以应用于随机模型的应用范围时，我们现在可用的计算能力是惊人的。医疗保健、金融、国防、商业，凡是你能想到的，都有办法用蒙特卡洛来研究。

[](https://www.datadriveninvestor.com/2019/02/28/descriptive-vs-inferential-statistics-whats-the-difference/) [## 描述性统计和推断性统计有什么区别？数据驱动的投资者

### 描述性统计和推断性统计是统计分析的两大分支。根据定义，描述性的…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/28/descriptive-vs-inferential-statistics-whats-the-difference/) 

当您有可变性并对预期行为做出假设时，请使用此模型类型。模拟模型通常会反复运行多次，以得出描述结果的平均值。当你没有一个函数方程，并有可变性使用蒙特卡罗模拟方法。

但是你需要知道正确的步骤。

假设你正在关注比特币的价格，你想创建一个交易模型。请遵循以下步骤:

***1。用概率分布识别基本状态变量和随机变量。***

基本变量是模型的基础。你现在有什么假设？然后用概率来定义你的变量，我们可以用随机样本来测试。

***2。识别导出的状态变量及其函数形式。***

派生状态变量被定义为随机试验的结果。如果观察到某个概率，模型的结果是什么？例如，你有买入或卖出信号吗？

***3。确定所需的样本数或其他收敛标准*或**

这是一个定义使用结果所需的置信度的过程。参考中心极限定理来确定你需要的样本数。这可能是一个重要因素，例如 100 个样本或 10，000 个样本。

***4。对于每个示例，生成随机变量，组成并记录上面 3 中确定的试验次数的导出状态变量结果。***

***5。根据结论计算并可视化统计数据。***