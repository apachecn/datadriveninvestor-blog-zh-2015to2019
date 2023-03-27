# 用于数据分析的必备 R 包(库)

> 原文：<https://medium.datadriveninvestor.com/must-have-r-packages-libraries-for-data-analytics-5a7a40dcc29?source=collection_archive---------29----------------------->

![](img/4ceb85b8a429cf65fc894fe977461072.png)

TL；DR: **如果你是一名数据科学家/分析师，这些是你必须拥有的 R 包:** tidyverse (ggplot2，dplyr，readr 等)，xml2，caret，sqldf，tseries，zoo，forecast，randomForest，tree，gam，e1071，xml2，ggmap，caret，pls，plotly。

我非常喜欢 R，也非常喜欢使用 RStudio，它是 R 的集成开发环境。

# 为什么我这么爱 R？

我喜欢它主要是因为它是开源的，这意味着有一个强大的开发人员社区不断改进现有的功能并发布新的功能。这也意味着，作为一名数据科学家/分析师，你可能需要的几乎所有东西，都有一个由这个令人敬畏的社区的成员创建的包(又名库)。

据推测，如果你是一名数据科学家或即将成为一名数据科学家，你已经知道所有这些。但是，这并不意味着您知道所有可用于您的服务的软件包。

所以这里列出了我最喜欢的 R 包，并简单介绍了它们的功能。**请留言分享你喜欢的套餐。**总是乐于学习和尝试新的 R 库。

# 用于数据分析的必备 R 包

*   **tidyverse:** 这是一个为数据科学设计的 R 包集合，包含:
    **ggplot2:** 用于数据可视化
    **dplyr:** 用于操作(例如选择、过滤、子集等)。)数据帧
    **readr:** 要导入 csv 或 tsv
    ****string:**要操作字符串
    您可以运行 install.packages("tidyverse ")来安装所有这些包以及这里没有列出的一些其他包。**
*   ****sqldf:** 对 R 个数据帧运行 SQL 语句— **是！****
*   **用于处理时间序列(ts)对象，对于金融数据分析也非常方便**
*   ****zoo:** 处理不规则(以及规则)的时间序列对象**
*   ****预测:**用于时间序列预测，例如使用 ARIMA**
*   ****随机森林:**用随机森林进行分类和回归**
*   ****树:**适合分类和回归树**
*   ****gam:** 建立包括非线性平滑函数的广义加性模型，以更好地解释/拟合数据**
*   ****e1071:** 包含各种统计方法**
*   ****xml2:** 解析和处理 xml 文件**
*   ****ggmap:** 使用 ggplot2 框架绘制有用的地图**
*   ****插入符号:**训练回归和分类模型以获得更好的预测(包括特征选择)**
*   ****pls:** 执行多元回归方法，包括主成分回归**
*   ****绘声绘色:**制作互动图形**

**一些软件包可能有重叠的功能，但我认为它们中的每一个都有独特的价值。**

# **安装所有软件包**

**您可以运行下面的代码来安装所有这些包。**

```
install.packages("tidyverse")
install.packages("xml2")
install.packages("caret")
install.packages("sqldf")
install.packages("tseries")
install.packages("zoo")
install.packages("forecast")
install.packages("randomForest")
install.packages("tree")
install.packages("gam")
install.packages("e1071")
install.packages("xml2")
install.packages("ggmap")
install.packages("caret")
install.packages("pls")
install.packages("plotly")
```

**【gulsahsemiz.com】最初发表于[](http://gulsahsemiz.com/must-have-r-packages-libraries-for-data-analytics/)**。****