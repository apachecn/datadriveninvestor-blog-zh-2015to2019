# 精确度、召回率和相关性

> 原文：<https://medium.datadriveninvestor.com/precision-recall-and-relevance-1d7ced4cacb5?source=collection_archive---------0----------------------->

"*你的回答有多贴切？* "
问一个简单的问题，但想出答案却很容易让你掉进兔子洞。不过，在我们往下说之前，让我们先看看“*相关的*”实际上是什么意思。

> **相关性**是指一个主题与另一个主题相关联，在考虑第一个主题时，考虑第二个主题是很有用的
> ——[维基](https://en.wikipedia.org/wiki/Relevance)

或者，换句话说，*相关性*完全是关于*联系*，在想法、概念、话题、交流等等之间。简而言之，当我们想知道*与*某件事有什么关联时，我们实际上问的是*如何将*与你感兴趣的其他事联系起来。

![](img/add3fc6701780b43f4a5c9d0f32917b1.png)

当我们开始考虑回答的准确性时，相关性就变得很重要了。比如说我们说的是猫(因为，*猫！*)。如果你问我发了多少张猫的图片，我回复 ***211*** (注:不是准确数字)，那你怎么衡量我的准确性？
嗯，有很多种方法，但在这种情况下，让我们把重点放在*精度*，和*召回*。

![](img/ac9ab9e8853091614c648dffdb07780b.png)

*精度是对我的反应的*质量*的衡量，即我的反应有多少是正确的。如果你看了 ***211*** 的推文，说“****200****这些都是猫，但是* ***11*** *这些都是披萨的图片！*”，那么我的*精度*就是`200/211`。(我的 211 个项目中只有 200 个是猫)
简而言之，把*精度*看作是对*选择的*项目中有多少是*相关的*(在数学中— `Precision = True Positives / (True Positives + False Positives)`**

*****回忆*** ，OTOH，是衡量我反应中*量*，即我与*实际*答案的接近程度。如果你看了我所有的推文，发现了 727 张猫的照片(出于某种原因，我没有数出来🙄)，那么我的*回忆*就是`200/(727+200) = 200/927`(我的 211 只中有 200 只是猫，另外还有 727 只猫我没数)
简而言之，把*回忆*看成是对*相关*项中有多少被*选中*(数学上— `Recall = True Positives / (True Positives + False Negatives)`**

***精度*和*召回*在机器学习中[可笑的相关(毕竟曾经在模式识别中巨大……)。关于这方面的更多信息，](https://towardsdatascience.com/beyond-accuracy-precision-and-recall-3da06bea9f6c)[看看维基页面](https://en.wikipedia.org/wiki/Precision_and_recall)，然后谷歌一下…**

***(* [*这篇文章也出现在我的博客上*](http://dieswaytoofast.blogspot.com/2018/07/precision-recall-and-relevance.html) *)***