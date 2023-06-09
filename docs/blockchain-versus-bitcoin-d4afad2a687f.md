# 区块链对比特币？

> 原文：<https://medium.datadriveninvestor.com/blockchain-versus-bitcoin-d4afad2a687f?source=collection_archive---------22----------------------->

[![](img/b8ca0d52a6cc94ec0c319a9aab26aff6.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/306fd5a9dda3210f21280d5d77ce2fd5.png)

Photo by [André François McKenzie](https://unsplash.com/@silverhousehd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近有人问我，区块链和比特币有什么区别。我认为这个答案(出于普遍兴趣)在这里也是有意义的。我希望它有助于澄清那些仍然认为这是一个模糊的概念。

比特币是一种复杂的东西。这个项目最初是为了创造一种去中心化的货币，使任何人/任何东西都可以向任何人/任何东西支付，无论他们在哪里，并且没有银行(中央或地方)或政府的干预、控制或阻止。因此，这是一个社会项目。它最初是在一份白皮书中描述的，我鼓励你[在这里](https://bitcoin.org/bitcoin.pdf)阅读(或至少浏览)。

所以回到最初的问题……比特币背后的技术实际上是一个区块链。这是众多区块链中的一种。事实上，自 20 世纪 90 年代以来，区块链就已经以这样或那样的形式存在了……而比特币在 2008/2009 年的突然出现让它们突然变得非常受欢迎。

更准确一点来说，**比特币**其实是几样东西。

1.  **是一种货币**。一种加密货币。如上所述，旨在允许没有第三方控制的实体之间的交易。它内置了各种各样的安全、信任和去中心化的机制。
2.  **也是一个协议**。这是使用这种货币进行交易的方式。例如，它描述了与为您进行交易的机器进行对话的 API，它还描述了数据(用于识别发送者和接收者的地址)和交易消息的格式，以及您如何支付运行交易的费用，以及其他细节，如运行网络的机器如何为此获得报酬。
3.  它的核心也是一个网络。它建立在一个没有许可的区块链上(即，你不需要中央机构的批准来进行交易，只要你遵守规则、协议，并且有货币来进行你想做的交易)。网络的所有节点达成是否验证交易的决定的方式被称为**共识。**不同的区块链有不同的共识模型。比特币使用一种被称为“[工作证明](https://en.wikipedia.org/wiki/Proof-of-work_system)的共识模型，这是一种极其计算机密集型的模型，并在一种被称为 [hashcash](https://en.wikipedia.org/wiki/Hashcash) 的协议中使用，该协议由一位非常聪明的密码学家 Adam Back 于 1994 年发明，旨在防止垃圾邮件，比特币模型就是基于该协议。

另一方面，区块链(注意复数)是一个不断增长的庞大数据库家族，用于存储和处理事务。如果你愿意，它们是非常具体的焦点数据库(不像 SQL 数据库，你可以存储任何类型的结构化数据)。区块链有两大家族。有权限(只有有权限访问区块链的人/系统才能进行读取和/或写入)和无权限(任何人都可以进行交易，只要他们遵守协议)。区块链被称为“无信任”系统，因为您不需要信任任何单个节点就可以信任整个系统。事实上，区块链通常被设计为即使有相当大一部分节点是恶意的/受到威胁的(只要大多数参与的节点仍然没有受到威胁)，它们也能正常运行。这是一个伟大的元素。在比特币区块链中，有数十万个节点参与其中。因此，很难破坏整个比特币网络。网络上的交易被认为是非常可信的。

最后一个要素…当某些交易被执行时，一些区块链可以以可信的方式运行特殊的程序。这些项目被称为“T0”智能合同，由区块链基础设施运营。它们以可信的方式运行。你肯定知道，如果触发交易发生，程序将运行。套用阿尔伯特·爱因斯坦的话，智能合同*不仅仅是一个好主意……它是法律*。智能合约可以用来触发基于区块链交易的现实行动。这打开了一些真正奇特的应用程序，如工作流自动化，其中事务用于标记工作流中的一个步骤，执行的智能合约将触发工作流的下一个步骤的执行，所有这些都具有绝对的信任，如果一个步骤被事务标记为已完成，则绝对可以确定下一个步骤将由相应的智能合约触发。

根据您的使用情况，您将选择最适合您需求的区块链。在区块链问题上，没有“一刀切”的做法。有些应用使用智能合约，有些不使用。有些使用有权限，有些使用无权限。根据网络上的节点数量、交易速度、节点上的可用 CPU 能力，一些共识机制更适合特定的使用情形，而另一些则更适合其他使用情形——想想物联网设备，通常很小，具有很小的计算机能力，您不会将它们用于基于工作验证的区块链…

还有一个信息要素…区块链是一个存储交易的分布式数据库，或分布式分类账。因此，区块链通常被称为 DLT(分布式账本技术)。如今，DLT 在范围和类型上都有所增长。并不是所有的都是区块链…有些 DLT 是完全不同的。Hashgraph 是一种 DLT 技术，并不基于区块链。IOTA 网络(专为物联网应用设计，具有较小的计算能力)基于一种叫做 tangle 的东西，它是非区块链 DLT。而且还有更多，还会有更多。

最后，我要补充一点，大多数 DLT 都是开源的。这使得开发系统的安装变得容易，甚至可以部署大规模的应用程序。有一些专有的，但我倾向于支持开源的，因为对代码的完全访问允许快速发现错误，并且社区提供的补丁，正如开源的一般情况一样，往往会导致更好的代码质量和更快的修复。我鼓励你尽可能多地使用开源区块链。尝试构建应用程序。看代码。为这些区块链的项目做贡献。

[Wipro](https://www.wipro.com/open-source/) 是 [Hyperledger](https://www.hyperledger.org/) 项目的成员(该项目隶属于 [Linux 基金会](https://www.linuxfoundation.org/)，我们也是其成员)，以及专注于[以太坊](https://www.ethereum.org/)区块链的企业用途的[企业以太坊联盟](https://entethalliance.org/)(我们是其创始成员)。还有像[恒星](https://github.com/stellar)、[涟漪](https://github.com/ripple)、[宇称](https://github.com/paritytech/)(基于以太坊)、[科达](https://github.com/corda)、 [IOTA](https://www.iota.org/) ，当然还有[比特币](https://bitcoin.org/)……都试试吧。它们都是开源的，可以免费下载、使用和修改，以满足您的需求！

## 来自 DDI 的相关故事:

[](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) [## 为什么数据将改变投资管理——数据驱动的投资者

### 有人称之为“新石油”虽然它与黑金没有什么相似之处，但它的不断商品化…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) [](https://www.datadriveninvestor.com/2019/01/30/machine-learning-for-stock-market-investing/) [## 股票市场投资的机器学习——数据驱动的投资者

### 当你的一个朋友在脸书上传你的新海滩照，平台建议给你的脸加上标签，这是…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/30/machine-learning-for-stock-market-investing/)