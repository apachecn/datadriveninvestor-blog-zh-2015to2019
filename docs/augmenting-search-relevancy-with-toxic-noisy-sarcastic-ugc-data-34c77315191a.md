# 大规模解决 UGC 搜索相关性的词汇袋？

> 原文：<https://medium.datadriveninvestor.com/augmenting-search-relevancy-with-toxic-noisy-sarcastic-ugc-data-34c77315191a?source=collection_archive---------16----------------------->

*从喧闹、讽刺的&或许有毒的用户生成内容(ugc)和单词袋模型看大规模增加搜索相关性的可能性。*

![](img/de73f51c769307783102eb9fe48285b1.png)

bag-of-words ? huh!

```
**Note:** *The challenge of tackling Relevance at Scale with noisy ugc data is largely generalized for the sake of blog post*
```

比方说，你正在为一个网站管理搜索平台，比如 Youtube、Reddit 甚至脸书。并且您希望加入评论数据来增加用户帖子的可发现性。

考虑一个例子，其中站点 ***的用户张贴了他们自己的图片*** ，标题如下

> “下周结婚。自从我订婚以来，体重明显减轻了。”(帖子附有自己的前后照片)

用户社区对该帖子的评论示例如下面的代码片段所示(*下面的示例仅受到非常轻微的* *级噪声*)

***通常的*** 方法是将帖子中的评论编入索引，作为额外的可搜索元数据(在大规模平台上，通常有数百万用户帖子中的数十亿条评论)。

***问题解决了？*** 可能是也可能不是！

然而，挑战在于评论这样嘈杂的数据很难用通常的算法相关性产生价值。当 Youtube 遭受评论的毒害时，Reddit 的主要特征是其用户讽刺的&怪圈行为。这为 ***与带有噪声的 ugc 数据*** 的规模相关性提出了一些独特的挑战。

然而与此同时，他们拥有 ***非常有价值的*** 相关术语，这些术语可以帮助帖子被发现，否则这些帖子可能会被某些关键字搜索遗漏。

```
**In Short:** When indexed, comments as searchable meta data has the potential to cause significantly more false positives than true positives. In other words increases recall many times over precision besides more importantly slowing down search performance overall.
```

我们如何**减少噪音&从这样的数据中提取相关术语**？我们需要在不损失精确度的情况下解决召回增加的问题。

> 我想讨论的方法之一是 ***袋字*** 模型(*这绝不是解决*的唯一方法。)

B***ag-of-words***是 **NLP** 中最简单但也是使用最广泛的技术之一。对于任何基于文本的问题，这是一个很好的开始方法。

**![](img/98d9ecb093b2e2e86ba8557146636eb2.png)**

**this is wall-of-words! not bag-of-words**

**一般处理步骤:*清理* *停用词* *标记化* *词干化* *矢量化***

***“如果你觉得***模型很新，那么有很多很棒的在线资源可以阅读****

***在这种情况下，我们实现了单词袋 模型的 ***变体，它的不同之处在于，在矢量化步骤中，我们将每个评论视为一个独立的文档。******

***换句话说，我们为每个帖子构建一个简单的 ***流内存 tf-idf 索引*** ，完全由与该帖子相关的评论组成。一旦完成该索引中的每个术语，我们就针对该索引运行查询，以计算该术语的*tf-idf* 得分，并且结果是基于与该帖子文档高度相关的 *tf-idf 得分*的前 N 个术语。***

***构建一个内存中实时的**TF-IDF*基础索引相对容易在 stack 上实现像***Apache Solr****&****Apache Spark。*******

> ****有很多很棒的在线资源可以了解经典的 ***tf-idf*** 相似性。在这种情况下 *tf-idf 得分* 简单计算如下:
> tfidf(t，D，D) = tf(t，D)。idf(t，D)****

****一旦我们有了前 N 个术语，我们可以简单地将它们作为该帖子的额外可搜索元数据编入索引，可能是在一个多值字段中，并根据您的整体相关性需求对其进行加权。****

****示例*词汇袋*TF-IDF 得分排名前 N 的术语:****

******可能的搜索匹配:******

```
**amazing weight loss
wedding transformation
keto weight loss
..{more}..**
```

****您将会看到上面的片段中列出的一些查询，这些查询可能是由*单词袋*模型为该特定帖子的用户评论输出而生成的顶级术语。****

****与其他元数据属性相比，这可以被加权为更高或更低，这取决于整体相关性需求。****

```
****Note:** With *bag-of-words* model since its a decomposition of text that ignores the context of these terms we won’t be able to do ***phrase-matching***. (*You can force all terms to be present to be considered a match but still its not quite the same*)**
```

****就准确性而言，与任何模型一样，取决于您如何实现模型，它有可能丢弃一些高度相关的术语，同时在不同程度上包含一些不太相关的术语。****

****![](img/76cead19fd6568297bd21defc66a7ca8.png)****

****tuning****

****有多个参数可用于执行若干启发式评估:

*最小值-TF* *最大值-IDF* *长度过滤器* *接合过滤器* *深度过滤器*****

# ****超越*文字袋*型号:****

****以上是我们可能探索的一种方法，但还有更高级和复杂的方法:
*·短语提取。
统计学上不太可能的短语。
·n 元模型。
……还有更*****

****在接下来的文章中，我将谈论我们如何在生产中实现这一点，以及我们如何测量性能。希望这篇文章对你有用！喜欢听你的反馈。****