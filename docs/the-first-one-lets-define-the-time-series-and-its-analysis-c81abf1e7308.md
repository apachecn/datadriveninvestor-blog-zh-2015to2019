# 第一个——我们来定义一下时间序列及其分析！

> 原文：<https://medium.datadriveninvestor.com/the-first-one-lets-define-the-time-series-and-its-analysis-c81abf1e7308?source=collection_archive---------15----------------------->

![](img/6407dd9eaa1aa1471535ca1e967aa8cd.png)

source: [https://freedom.to/](https://freedom.to/)

## [1。第一个](https://medium.com/@venali/the-first-one-lets-define-the-time-series-and-its-analysis-c81abf1e7308) 2。[这一系列的温和开局](https://medium.com/@venali/a-gentle-start-in-this-series-time-series-and-its-analysis-bb0a67503d6e) 3。[逼近一个时间序列](https://medium.com/@venali/approximating-a-time-series-time-series-and-its-analysis-923aa81ca80a)

对我来说，时间序列很简单

> "在其结构中反映时间相关性的附加信息的数据."

让我们尝试检查四个著名平台的四个不同视角，并定义时间序列及其分析。

正如我常说的。数据科学的真正影响通过其货币价值或业务影响来衡量。

# 所以让我们来看看 Investopedia 是怎么说的

*[*来源*](https://www.investopedia.com/terms/t/timeseries.asp)*

*什么是时间序列？时间序列是按连续顺序排列的数字数据点序列。在投资中，时间序列跟踪选定数据点的运动，如证券的价格，在一段特定的时间内，定期记录数据点。没有必须包括的最小或最大时间量，允许以提供投资者或分析者检查活动所寻求的信息的方式收集数据。*

*了解时间序列时间序列可用于任何随时间变化的变量。在投资中，通常使用时间序列来跟踪一段时间内证券的价格。这可以在短期内跟踪，例如在一个营业日的整点的证券价格，或者在长期内跟踪，例如在五年内每个月的最后一天收盘时的证券价格。*

*时间序列分析时间序列分析有助于了解给定资产、证券或经济变量如何随时间变化。它还可用于检查与所选数据点相关的变化与同一时间段内其他变量的变化相比如何。*

*[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

时间序列预测时间序列预测使用有关历史值和相关模式的信息来预测未来活动。通常，这与趋势分析、周期性波动分析和季节性问题有关。和所有的预测方法一样，不能保证成功。* 

# *或者，让我们采取一个更一般的观点，用维基的方式来定义*

*[*来源*](https://en.wikipedia.org/wiki/Time_series)*

*时间序列是按时间顺序索引(或列出或绘制)的一系列数据点。最常见的是，时间序列是在连续的等间隔时间点取得的序列。因此，它是一个离散时间数据序列。时间序列的例子有海潮的高度、太阳黑子的数量和道琼斯工业平均指数的每日收盘价。*

*时间序列经常通过折线图绘制。时间序列用于统计学、信号处理、模式识别、计量经济学、数理金融学、天气预报、地震预测、脑电图、控制工程、天文学、通信工程，以及大量涉及时间测量的应用科学和工程领域。*

*时间序列分析包括用于分析时间序列数据的方法，以便提取有意义的统计数据和数据的其他特征。时间序列预测是使用模型根据以前观察到的值来预测未来值。虽然回归分析常用于检验一个或多个独立时间序列的当前值会影响另一个时间序列的当前值的理论，但这种时间序列分析不称为“时间序列分析”，它侧重于比较单个时间序列或多个相关时间序列在不同时间点的值。间断时间序列分析是对单一时间序列的干预分析。*

# *最后一个来自 Quora 的简短的问题*

*[*来源*](https://www.quora.com/How-do-I-learn-about-time-series-analysis-2?redirected_qid=1340201#!n=12)*

*时间序列是在一段时间内以规则的时间间隔测量的数据点序列。不规则数据不会形成时间序列。*

*它使用统计方法来分析时间序列数据，并提取关于数据的有意义的见解。*

*数据点是在一段时间内收集的。分析这些数据点(过去的值)来预测未来。很明显，它是依赖于时间的。*

## *虽然时间序列可能像 NLP 或 ML 中的任何其他领域一样是一个怪物，但本文和下文试图给出一个概述并进行足够的教育，以便在该领域中做高级的东西，并给出足够强的工作来建立/创建应用领域中可靠的真实世界用例。*

*一个美丽的开始是时间系列的 R 小书！ [*链接*](https://a-little-book-of-r-for-time-series.readthedocs.io/en/latest/index.html)*

*找到数据集的最佳位置，并把最佳算法与精确度联系起来: [*链接*](https://archive.ics.uci.edu/ml/datasets.php?format=&task=&att=&area=&numAtt=&numIns=&type=ts&sort=taskUp&view=table)*

# *信用*

*随着系列的进展，我将在索引中添加几篇文章，但首先是这个系列的一个温和的开始。该系列参考了几个数据源、软件包、研究论文、博客、书籍、vlog、实用建议、工业工作和个人经历。我感谢这一领域的每一个人，特别是我接触到的他们的工作使我能够把这些放在一起。所有的荣誉都属于外面的聪明人！*

****此外，这个系列是第一次有意识地努力建立自我证明的基础，而不期望在职业阶梯上获得赞赏。虽然每个人都生活在未知的奋斗和目标的发现中，但我个人认为，偷偷微笑一下，对在各种情况下做出的所有正确或错误的生活选择表示感谢是没问题的，因为否则你就不可能做出更好的选择。****