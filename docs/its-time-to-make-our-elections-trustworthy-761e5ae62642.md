# 是时候让选举变得可信了

> 原文：<https://medium.datadriveninvestor.com/its-time-to-make-our-elections-trustworthy-761e5ae62642?source=collection_archive---------20----------------------->

[![](img/fda48e047dc085d50e33a1aeedb68901.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/31687e44f79b28d7a05c6b67b1f52b9f.png)

世界上许多国家的投票绝对是一团糟，即使是富裕的“自由”国家[如美国](https://www.washingtonpost.com/politics/broken-machines-rejected-ballots-and-long-lines-voting-problems-emerge-as-americans-go-to-the-polls/2018/11/06/ffd11e52-dfa8-11e8-b3f0-62607289efee_story.html?noredirect=on&utm_term=.df166ef808e4)，更不用说我们投票系统中现有的安全漏洞，如[一号](https://arstechnica.com/information-technology/2018/09/e-voting-researchers-warn-of-hack-that-could-flip-the-electoral-college/)，它可能允许“攻击者翻转选举团并决定总统选举的结果”**我们可以构建一个由*现有的*技术**组成的高级投票系统，它可以(相对)简单地运行，可审计，安全，并且比许多现有的系统更方便。

这可以通过结合修改后的区块链系统和现有的选举基础设施，在我们现有的基础上创建一个大规模改进的系统来实现。

这对用户的工作原理相对简单:

1.  登记投票。这可以使用现有的基础设施和方法来完成。(请注意，选民登记也可以得到改进，也许可以通过创建一个类似于汽车选民法案的围绕报税而建立的法案，但这是一个超出本文范围的主题)在登记时，您将收到一个与您相关的选民密钥，可用于以数字方式发送和签署您的投票。
2.  在选举日“投票结束”之前的任何时候，去投票网站(可能是像 vote.gov 这样简单的网站)投票。然后，您将使用您的投票人密钥签名并发送您的投票。请注意，这消除了提前投票和常规投票之间的差异——这是以相同的方式完成的，也可以在任何计算机上全天候完成。

就是这样。没有排队，没有旅行，没有时间限制——只是一种简单、方便的投票体验。

这很简单，对吗？后端也没那么复杂。创建后端所需的步骤概述如下:

1.  使用图灵完整区块链和权威证明(PoA)挖掘系统构建联邦区块链网络。图灵完备性表明以太坊的 PoA 版本是一个理想的选择。这不是尖端技术；甚至[微软也提供了现成的解决方案](https://azure.microsoft.com/en-us/blog/ethereum-proof-of-authority-on-azure/)。节点可以建立在位置良好并且已经数字安全的位置；一个潜在的候选人可能是在美联储的每个分支[放置一些节点](https://en.wikipedia.org/wiki/List_of_Federal_Reserve_branches)，这允许地理上的分散并且(我希望)已经有强大的数字安全措施。
2.  创建投票智能合同。这可能就像创建一个智能契约一样简单，只需存储足够大的字节数组，以保存给定选举中要发出的最大选票。
3.  创建前端。前端需要完成以下工作:

*   请个人填写适当的选票。有很多常规的方法可以做到这一点，只要考虑一下有多少个性化的在线调查平台。
*   把选票寄给区块链。这可以使用 Web3 来完成。

4.统计选票。这可以通过一个程序来完成，减少计票时间。

就是这样——这将需要一些时间和努力，但这并不是一个高度复杂的任务，以确保民主的基础。

**以下是好处:**

*   相对便宜——你只需要几台好电脑和几个工时。
*   减少漏洞——故障点的数量大幅减少，并且使用安全的以太坊(使用椭圆曲线加密技术),黑客攻击发生的几率大幅降低。
*   在选举日之前的几周内，每个人都可以全天候在家或在工作中投票。
*   一个好的用户界面可以让你的投票更容易理解和完成。
*   你可以在电脑的另一个标签中进行研究，同时按照自己的节奏完成投票。
*   易于审计—任何拥有计算机的人都可以全天候监控全国网络。
*   快速结果——几乎可以立即得到结果

澄清一些杂点和问题:

*   为什么是区块链？[区块链是可审计技术的巅峰](https://bitfury.com/content/downloads/bitfury_white_paper_on_blockchain_auditability.pdf)。
*   为什么是 PoA？[区块链试图一次性解决三个问题:去中心化、安全性、可扩展性](https://medium.com/@aakash_13214/the-scalability-trilemma-in-blockchain-75fb57f646df)。大多数人认为(考虑到目前的技术)这三件事情中只有两件可以一次性解决。BTC、ETH 和大多数加密货币选择安全性和去中心化作为主要关注点(研究重点是如何增加可扩展性)。PoA 网络选择安全性和可扩展性作为其关注点。鉴于政府选举本质上集中在某一点，使用一个提供可伸缩性和安全性的网络是一个合理的途径。
*   这怎么安全？它使用[椭圆曲线密码](https://arstechnica.com/information-technology/2013/10/a-relatively-easy-to-understand-primer-on-elliptic-curve-cryptography/)。