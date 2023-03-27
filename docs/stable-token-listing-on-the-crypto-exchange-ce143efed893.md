# 加密交换上的稳定令牌列表

> 原文：<https://medium.datadriveninvestor.com/stable-token-listing-on-the-crypto-exchange-ce143efed893?source=collection_archive---------20----------------------->

[![](img/b80f7627d6b1fccd43e0aa4ade5f57f2.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/f3a5d9eb6f67ef61d9d0fc601b439a2a.png)

*Image courtesy of Loveluck at FreeDigitalPhotos.net*

我每天至少会从专门从事招募工作的密码交易所或经纪人那里联系到一次。

在特别报价 BS …我们通常来 ERC20 代币和交换技术能力列出稳定代币。

> 对于大多数加密交换来说，稳定令牌似乎是未知领域。

# 如何稳定代币/硬币应该上市？

**让我先做一个比较，这样事情就清楚了……**

如果你出国旅行到使用外币的国家，你可以在银行购买所需的货币。他们对每种货币都有固定的汇率，你只能决定买入或卖出。例如，100 欧元你将得到 115 美元。**美元的价格**不可以讨价还价。如果你带着 100 瑞士法郎去银行，你将得到 101 美元。

*是的，我知道如果你有机会进入外汇市场，你可以尝试让你的钱得到更多。我也确信乔治·索罗斯还有更多外汇锦囊妙计，但这是题外话。*在银行，当天当场，你作为小客户是拿不到差价的。**

**现在是技术说明……**

愿意将 stable token 与 ETH 和 BTC 列为一对的交易所必须拥有关于欧元汇率、美元汇率、BTC 对美元、BTC 对欧元、ETH 对美元和 ETH 对欧元的实时输入数据。**sc ctn 对欧元的汇率是固定的**所有其他汇率 SCCTN/ETH 和 SCCTN/BTC 需要根据 ETH/USD、BTC/USD 和 USD/EUR 的输入数据实时计算。

*第二步！需要采用的交易:*

*   对于以市场价格提供购买或出售的交易所，上述汇率必须成为市场价格，并且需要禁用其他选项。
*   对于任何价格的交易所报价购买——需要禁用价格设置——系统需要使用上述价格。应该只允许交易者输入购买量或销售量。

**借口和解释**

在 coinmarketcap.com，USDT 是一种稳定的硬币，它的价格并不总是 1 美元。这是正确的，但是，价格差异是 USDT 在瑞士联邦交易所或 BTC 或任何其他加密货币中交易的直接后果，它是在 T1 时间交易的，交易所在 T2 时间向 Coinmarketcap 报告，Coinmarketcap 在 T3 时间计算利率。因此，1 美元与 Coinmarketcap 上显示的汇率之间的差异与时间 T1 + (T3-T1)内 ETH 或 BTC(或其他用于购买 USDT 的加密货币)的价值上升或下降完全相同。

因此，在任何给定时间，由于 ETH 或 BTC 在 T1 + (T3-T1)的上涨或下跌，SCCTN 在 Coinmarketcap 上具有不同于 1 SCCTN = 1 欧分的汇率是完全可以接受的。 ***但是 Coinmarketcap 汇率(T3)不能成为 1 SCCTN 在时间 T1 时在交易所上不值 1 欧分的借口。***