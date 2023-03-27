# 寻找与熊猫的晚餐

> 原文：<https://medium.datadriveninvestor.com/finding-dinner-with-pandas-e517b1c1dcdb?source=collection_archive---------15----------------------->

使用熊猫查看、过滤和搜索数据的教程

大家好！今天我要讲的是*熊猫* Python 库。没错，就像可爱的动物。

![](img/6c953b0efc1da6e21caa2c7168998995.png)

嗯，不太好。 *pandas* 是“Python 数据分析库”的缩写。这是一个非常有用的库，特别是对数据专家来说。根据[文档](https://pandas.pydata.org/pandas-docs/stable/)， *pandas* 是一个开源库，为 Python 语言提供易于使用的数据结构(以一种叫做 dataframes 的结构化表格格式)和数据分析工具。

好吧——那么，为什么要用*熊猫*？

如果你想用 Python 代码探索数据，使用 *pandas* 。*“它是对现有科学 Python 堆栈的有力补充，同时实现并改进了其他统计编程语言(如 r)中的各种数据操作工具。”* [1]

酷，让我们来看一个例子。首先，我们需要导入一些数据。我将使用从 Kaggle 找到的关于食谱的数据集[这里](https://www.kaggle.com/shuyangli94/food-com-recipes-and-user-interactions#RAW_recipes.csv)。这套包括 180，000+食谱和 700，000+食谱评论，涵盖了 Food.com 18 年的用户互动和上传。

[](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) [## 成为数据科学家所需的 8 项技能|数据驱动型投资者

### 数字吓不倒你？没有什么比一张漂亮的 excel 表更令人满意的了？你会说几种语言…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) 

下载数据并确定 RAW_recipes.csv 文件的路径。导入必要的模块(熊猫)和数据。将数据存储在 *pandas* dataframe 中——表格格式的数据。

让我们看看文件的形状…

…好的。有 231637 行数据(想想:231637 个食谱)。这有很多食谱，所以让我们只看数据的一个子集。

假设我只想要前 5 个食谱的信息。

*(注:可在 food.com*[*搜索页面*](https://www.food.com/search/) *输入“id”栏中的值，以找到完整的配方！)*

这也可以用 loc 函数来完成，它通过标签选择数据帧的一部分。行由索引(本例中是一个整数)标记，列标签只是列名。

我们也可以只选择几列。

还有一个名为 iloc 的函数，它可以返回相同的视图，但在实现上与 loc 函数不同。loc 选择标签，iloc 选择数字(整数)，特别是行号和列号。

让我们按“分钟”来筛选数据，找出能在 30 分钟或更短时间内做出的食谱。我将在这个过滤器中添加 count()，这样我们就可以看到返回了多少个食谱！

231637 种食谱中的 99052 种！

让我们用 loc 方法重写前面的方法。

注意，两种格式的输出是一样的。

想象一下，我的朋友做了[早餐披萨](https://www.food.com/recipe/a-bit-different-breakfast-pizza-31490)，准备只花了 25 分钟，而不是 30 分钟。我们可以将数据框中的 30 分钟改为 25 分钟。

一个警告？这是什么怪异的行为？这是 SettingWithCopyWarning —标记潜在的令人困惑的“链式”分配。它警告您的代码可能没有按预期执行。无视这一警告是**的不良做法**！

只需使用 loc 将链接的操作合并成一个操作，并消除警告。

等等，loc 做了什么第一个方法没有做的事？

要回答这个问题，要明白熊猫可以返回一个视图或一个副本。当您进行链接时(像上面的代码那样连续使用多个索引操作)，将返回数据帧的副本，其中包含:

然后在副本上执行第二操作。新值 25 未在原始数据帧中设置。*(查看原始数据帧，30 没有被替换！)*

我对这个数据集很感兴趣，因为我想找到无麸质食物的新配方——比如无麸质面包、甜点和砂锅菜。晚餐吃点东西。为此，我可以在“名称”、“成分”和“描述”列中搜索关键字。

使用。我看到有 1256 种食谱被标为无麸质。有多少能在 30 分钟或更短时间内完成？试着自己编码吧！

有问题吗？在评论里说吧。

来源:

1.  麦金尼韦斯。“pandas:用于数据分析和统计的基础 Python 库”。检索自:[https://www . DLR . de/sc/portal data/15/Resources/doku mente/py HPC 2011/submissions/py HPC 2011 _ submission _ 9 . pdf](https://www.dlr.de/sc/Portaldata/15/Resources/dokumente/pyhpc2011/submissions/pyhpc2011_submission_9.pdf)