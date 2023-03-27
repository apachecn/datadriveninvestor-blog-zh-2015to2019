# 我如何使用这个免费的 API 来寻找被低估的股票

> 原文：<https://medium.datadriveninvestor.com/how-i-use-this-free-api-to-find-undervalued-stocks-6574b9a3f2fe?source=collection_archive---------3----------------------->

![](img/8f748d21e77f701d9fcef983c96efa15.png)

我最近推出了 [TenQuant.io](https://www.tenquant.io) ，为投资者和使用技术推动投资决策的基金提供关于未覆盖股票的准确数据。我对彭博终端缺乏我跟踪的股票的基本面数据感到失望——尽管价格数据是无与伦比的——也不想花钱获取不关注小盘股的专有数据集。目前它是完全免费的，可以访问大量的历史数据和当前的基本面。

在本教程中，我将教你如何使用 Python 的 requests 和 JSON 库在我的 API 中搜索纳斯达克上未被覆盖的股票。我最喜欢的寻找被低估公司的方法是本杰明·格拉哈姆的净流动资产价值公式，或称净净值，因为它完全基于规则，最适合小投资者，而不是机构。

[](https://www.datadriveninvestor.com/2019/02/28/the-rise-of-data-driven-investing/) [## 数据驱动投资的兴起|数据驱动投资者

### 当 JCPenney 报告其 2015 年 2Q 的财务结果时，市场感到非常震惊。美国零售巨头…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/28/the-rise-of-data-driven-investing/) 

这个公式实质上是以如此低廉的价格购买一组股票，以至于如果这些股票今天被清算，其运营业务和长期资产将变得一文不值，那么它们的售价将低于它们的价值。

![](img/7b44b5c45dd5a1a2a0526e292466db40.png)

Benjamin Graham, the father of value investing.

本质上，你拿股票的流动资产，减去所有负债和优先股，以获得净流动资产价值。对一些人来说，这可能是负面的，因为现金少而债务高。对其他人来说，这可能是积极的，但理论上，一家公司永远不应以低于其流动资产净值的价格出售。事实上，市场并不是完全有效的，尤其是在小盘股领域，这就提供了一个机会。

投资到此为止。让我们来看看代码。

首先启动您最喜欢的 IDE 并导入必要的库:

```
import requests
import json
```

请求库允许 Python 程序与网站和基于 web 的 API 对话。它在许多应用程序和脚本中使用，并且在很大程度上非常直观。

JSON 库使我们能够使用 JavaScript Object Notation，或 JSON，这是一种在计算机之间发送数据的标准。你访问的几乎每一个网页都会用到它，能够将它从 JavaScript 对象转换成我们可以处理的数据在这里是至关重要的。

接下来，从 [TenQuant.io](https://www.tenquant.io) 获取一个 API 密匙，并将其插入此处:

```
base_url = '[https://api.tenquant.io/balancesheet?key=[YOUR KEY HERE]&ticker={TICKER}'](https://api.tenquant.io/balancesheet?key=HSAUERS25&ticker={TICKER}')
```

在我们使用这个 API 之前，我们需要获得一个股票列表来进行搜索。你可以从 Nasdaq 这里(FTP://FTP . Nasdaq trader . com/symbol directory/Nasdaq listed . txt)下载它们，或者使用我在 API 上内置的行情列表:

```
ticker_list_url = '[https://api.tenquant.io/res/nasdaqlisted.txt'](https://api.tenquant.io/res/all.txt')
tickers = requests.get(ticker_list_url).text.split('\n')
```

这段代码向 API 请求一个 tickers 列表，然后将它转换成一个 Python 列表，并按每一个新行进行拆分。这仅使用了请求库和 Python 的内置数据类型方法。

让我们初始化一个地方来存放我们发现的被低估的股票:

```
netnets = []
```

Python 有一个独特的 for-each 循环，允许您遍历列表中的每个元素，而不是通过索引进行搜索。让我们在报价器中搜索被低估的股票:

```
for ticker in tickers:
  print(ticker)
```

现在，在这个循环中从 TenQuant API 获取它的基本数据:

```
 balance_sheet_json = requests.get(base_url.replace('{TICKER}', ticker)).text
```

将其转换为 Python 字典，以便我们可以更轻松地使用它:

```
 balance_sheet = dict(json.loads(balance_sheet_json))
```

该语句确保 API 不会返回某种错误。这通常是由股票交易列表中的错误数据或一段时间没有提交文件的公司引起的，但我们不希望在发生这种情况时中断程序。

```
 if 'error' in balance_sheet.keys():
    continue
```

从股票的资产负债表中获取一些基本数据:

```
 current_assets = balance_sheet['currentassets']
  total_liabilities = balance_sheet['liabilities']
  preferred_stock = balance_sheet['preferredstock'] sector = balance_sheet['sector']
  market_cap = balance_sheet['marketcap']
```

过滤掉医疗保健/生物技术股票，因为它们通常具有烧钱和投机的特点:

```
 if sector != 'Healthcare':
```

计算股票的净流动资产价值，或大甩卖清算价值:

```
 ncav = current_assets - total_liabilities - preferred_stock
```

只搜索净资产值比当前市值至少高 35%的股票:

```
 if ncav > market_cap*1.350:
      print('Net-net found: ' + ticker)
```

将它与可比数据一起添加到我们的列表中，以便我们可以一次看到所有数据:

```
 netnets.append({'ticker': ticker, 'ncav': ncav, 'marketcap': market_cap})
```

最后，打印出结果。这部分超出了我们的 for-each 循环:

```
for stock in netnets:
  print(stock)
```

试一试你的程序吧！这里有一个提示:用它来搜索不仅仅是纳斯达克上市的股票，因为 API 支持任何在 SEC 备案的公司(甚至外国公司！)如果你需要任何帮助或者只是想谈谈编程和投资，请随时给我发电子邮件。

[](https://www.datadriveninvestor.com/2019/09/01/data-structures%e2%80%8a-%e2%80%8aarray/) [## 数据结构-数组|数据驱动的投资者

### 现在，我们将开始讨论数组，它是我们可以处理的最简单的数据结构。数组是用来存储…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/09/01/data-structures%e2%80%8a-%e2%80%8aarray/)