# 情感分析——了解用户意见

> 原文：<https://medium.datadriveninvestor.com/sentiment-analysis-know-the-user-opinion-90d711a81b54?source=collection_archive---------6----------------------->

曾经有一段时间，人们不得不通过手动流程或收集反馈表或类似旧时代的东西来与客户交流客户反馈，现在客户使用社交媒体来分享他们的体验。

**TL；博士:你可以从这里获得代码→** 、http://bit.ly/2QzE8xt[和](http://bit.ly/2QzE8xt)

![](img/7e340c14135eb692aabf216a6f0a127a.png)

Photo by [freestocks.org](https://unsplash.com/@freestocks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

您必须向客户寻求反馈，然后采取行动加以改进的日子已经一去不复返了。我们以一家餐馆为例。去那里参观的人会拍下照片，并在 Instagram、twitter 或 facebook 等一些平台上分享。他们过去常常分享他们对餐馆的想法，如果体验是 ***愉快的*** 还是 ***可怕的*** 。大公司使用用户分享的数据来分析分享他们想法的人的情绪。

[](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) [## DDI 编辑推荐:5 本让你从新手变成专家的机器学习书籍|数据驱动…

### 机器学习行业的蓬勃发展重新引起了人们对人工智能的兴趣

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) 

该公司可以使用同样的工具来帮助他们分析客户的情绪。他们会密切关注给他们贴标签的社交媒体，关注那些有着糟糕体验的人，并立即采取行动解决客户问题。

在这篇文章中，我将讨论使用社交媒体进行情感分析以及如何使用 Python 处理这一话题。

作为公司，成功和失败直接取决于他们的客户。因此，如果客户喜欢公司的产品，这就是成功，如果不喜欢，公司需要进行一些改进。因此，为了知道客户是否喜欢你的产品，公司需要分析他们的客户。该公司可以做的事情之一是对其客户进行情绪分析。这时，客户的情感分析就派上了用场。

## **什么是情感分析？**

![](img/51bb1d5b3a450092761956317466d757.png)

Photo by [Obi Onyeador](https://unsplash.com/@thenewmalcolm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

情感分析是对观点进行计算处理，以便对其进行识别和分类。他们用一段文字来判断作者的态度，或者说顾客对产品的态度是消极的、积极的还是中立的。

作为个人，我们在购买之前会分析产品的评论或者说产品评论。但是作为一家公司，他们有许多客户，如果手动进行分析，他们需要很多时间。在那里，他们必须使用情感分析来在短时间内分析数据。

## **情感分析是如何工作的？**

情感分析的过程是一步一步来的。

1.  ***标记化:*** 这是情感分析的第一步，会把句子分割成一段一段的标记(分割成词)。
2.  ***移除特殊字符:*** 在这一步中，它将从令牌中移除所有的特殊字符。比如'，'，'？'、' { '、']'等。
3.  ***停用词的删除:*** 在这一步，我们要从数据中删除所有停用词。像过去、现在等。
4.  ***剩余单词的分类:*** 在这一步，我们要做的就是将剩余的令牌分类为正面、负面或中性，并给出一定的分值。
5.  ***应用监督机器学习算法:*** 这一步，我们要在已经有的数据上训练 ML 模型，并在一些句子上进行测试。因此，在这个过程中，模型的准确度分数越高，句子的分类就越好。
6.  ***计算极性得分:*** 在这一步，我们要计算最终的极性得分。如果极性得分“等于 0”，则为“*”；如果“大于 0”，则为“**正**”；如果“小于 0”，则为“**负**”1。*

*在 python 中，为了简化这个过程，有一个名为 TextBlob 的库，它将帮助我们识别人们的情绪。*

*[sentiment_analysis_textblob](https://gist.github.com/jayeshmanani/4c36f6bb639b9840532abd17bdb09251)*

*TextBlob 是一个你可以用来分析人的文字表达的情绪。你只需要使用终端中的语句来安装它*

> *pip 安装文本 blob*

*然后你必须在文件中导入它。使用语句。*

> *从文本 Blob 导入文本 blob*

*然后你只需要用语句检查极性。*

> *TextBlob("SomeText ")情绪.极性。*

*分数将被打印出来，你可以检查它是 0，大于 0 还是小于 0。相应地，你可以检查它的极性。*

*我希望你能从中学到一些东西，并使用情感分析来检查各种文本数据的情感。*

*建设性的反馈会很有价值。*