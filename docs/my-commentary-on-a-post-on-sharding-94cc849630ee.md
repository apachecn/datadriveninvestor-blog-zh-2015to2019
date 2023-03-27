# 关于分片的观点

> 原文：<https://medium.datadriveninvestor.com/my-commentary-on-a-post-on-sharding-94cc849630ee?source=collection_archive---------14----------------------->

[![](img/b20a0eab3bb62531f680ae2f41cc2cd1.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/fe8ead7cd970c5c92491b307f97dfc67.png)

发布这篇文章的网站没有添加评论的方法。我把它们放在这里。这篇文章提出了一些限制性的假设，我们刚刚花了一年的时间来消除这些假设。

我的评论是指 Cointelegraph 上的以下帖子:

[](https://cointelegraph.com/explained/sharding-explained) [## 解释说

### 1.分片是数据库分区的一种形式，也称为水平分区。这个过程包括分手…

cointelegraph.com](https://cointelegraph.com/explained/sharding-explained) 

对 Cointelegraph 上这篇文章的评论:这是对分片的一个相当好的描述，但有几个例外。

首先，它假设通过分片，工作证明的哈希能力被稀释了。只有当共识算法以这种方式工作时，情况才会如此。

我们有一个替代模型，可以在不稀释 hashpower 的情况下实现分片，从而保持相当于非共享单链的安全性。因此，我们帮助解决了三难中的一个方面，即安全性。

其次，它假设主要的编程模型是智能合约和 altcoin 令牌。从这个角度来看，将智能合约放在碎片上确实有意义，但是智能合约的吞吐量仍然受限于碎片的吞吐量。因此它仍然是序列化的。这比将所有智能合约序列化在一起要好，但仍然是有限的。

我们有一个替代模型，它消除了智能合同序列化，允许吞吐量随帐户数量而扩展，而不受智能合同序列化的限制。因此，我们帮助解决了三难困境的另一面，可伸缩性。(去中心化，第三方用开放的、无权限的全球点对点模式解决)。