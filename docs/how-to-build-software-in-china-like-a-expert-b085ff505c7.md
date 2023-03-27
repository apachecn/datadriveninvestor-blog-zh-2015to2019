# 如何像专家一样在中国做软件？

> 原文：<https://medium.datadriveninvestor.com/how-to-build-software-in-china-like-a-expert-b085ff505c7?source=collection_archive---------1----------------------->

![](img/8b96d06297625c897e4df493f4438155.png)

“Spider-Man leaning on concrete brick while reading book” by [Raj Eiamworakul](https://unsplash.com/@roadtripwithraj?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

“中国是个黑洞！”在我说我要去中国做软件开发后，一个男人在一次会面中否认了。

他继续讲述他的想法是如何被窃取的，以及他的公司是如何在复制猫进入市场后破产的。

我很害怕，但我还是来到了中国。

快一年了，坦白说，没那么恐怖了。

不一样，但不恶毒。

这里有一些在中国或为中国观众构建软件的技巧。

# 按规矩办事

要在[长城防火墙](https://en.wikipedia.org/wiki/Great_Firewall)内玩游戏，你需要一个 [ICP](https://baike.baidu.com/item/ICP/4950300) 许可证，互联网内容提供商可以把任何网站放在公共互联网上。

如果不这样做，您的网站可能会被封锁。是的，它甚至不能加载。

# 告别你熟悉的 API

谷歌、脸书、Twitter，甚至这里的平台 Medium，都提供了某种 API 来加速我们的开发过程。

我们越来越喜欢他们的服务。当时，当我需要在网站中嵌入地图时。这是显而易见的:谷歌地图。

现在要在百度地图，Amap，QQ 地图，Mapbox，…

云提供商也是如此。AWS 有一个[中国版](https://www.amazonaws.cn/)，但是有些功能没有提供。

AWS 相关链接还得不断担心微信会不会屏蔽。即使你只是想要一个 S3 水桶的演示链接，微信可以说，“不，这是不合法的”，然后你又回到第一步。

# 你好腾讯微信

如果你做任何面向消费者的软件开发，都逃不过微信。微信每月活跃用户超过 10 亿，在中国移动互联网领域占据主导地位。

最常见的场景是用户想把 app(手机或网站)分享到微信。

刚开始的时候我想“哦，我就是加一些 meta 标签然后微信就接了是吧？”

不，你需要[微信的 JSSDK](https://medium.com/@davidyu_44356/why-do-we-need-wechat-js-sdk-b7b4ced39d29) 来让一个漂亮的卡片出现在消息线程中。

有一点要记住，开发者微信不是“弄个账号玩玩”那么简单。

你必须找到合适的客户。官方、订阅、服务或迷你程序。有开发用的沙盒账号，但是微信支付不能用沙盒账号测试。

大多数时候，你会发现自己在等待腾讯的批准，以激活一些功能，所以我建议你随时准备好你的中国公司信息，以使这个过程更加顺利。

# 不是所有东西都在堆栈溢出上

作为开发人员，我们经常复制错误信息并将其直接粘贴到 Google 中，然后 Google 先生提出了一个堆栈溢出解决方案。

当你在微信 SDK 中遇到错误时做同样的事情，往往会空手而归。(这就是为什么我写在媒体上，以提供更透明的信息)

同时，你可以使用百度或者 [SegmentFault](https://segmentfault.com/) 来找到你的答案。

# 大多数人不知道他们在谈论什么

每个人都可以阅读文档和微信的相关文章，但很少有人愿意自己通过试错过程来检验什么是可能的。

这就是为什么我们的老板只是追逐闪亮的物体。今年一直是微信小程序，微信的 app 内的 app。

每个人都想用迷你程序做点什么，因为，嗯，每个人都在做。

事实上，他们分不清网络应用和微信小程序的区别。

作为开发人员，我们需要通过掌握必要的知识来帮助他们做出更好的技术决策。

# 移动第一…只做移动版

[89%的人口使用手机](https://www.statista.com/statistics/278204/china-mobile-users-by-month/)。

我在中国的第一个网站，我们是从桌面版开始的。当我们查看分析时，每天只有 5 个人访问。

当我们开发手机版时，这个数字上升了 100 倍。

如果你建立了任何面向公众的东西，确保它很容易在手机上访问。

# 检查在有或没有 VPN 的情况下是否还能工作

VPN 在中国很常见。这是中国人与外界保持联系的方式。

防火长城是双向的。它可以拒绝访问外国网站，或者将连接速度降低到让你质疑生命存在的程度。

托管在中国的服务器在美国会很慢。选择正确的 CDN 对于一个全球可访问的网站至关重要。

# 知道你的坐标

GPS 坐标在中国是失真的。

以下是坐标系统:

[WGS 84](https://www.linz.govt.nz/data/geodetic-system/datums-projections-and-heights/geodetic-datums/world-geodetic-system-1984-wgs84)——谷歌地图用什么

[GCJ02](https://en.wikipedia.org/wiki/Restrictions_on_geographic_data_in_China) —腾讯地图/Amap 用什么

BD09 —百度地图用什么

帮助您进行坐标转换的库:

[](https://github.com/googollee/eviltransform) [## Google lee/evil transform

### 地球(WGS-84)和中国火星(GCJ-02)之间的运输坐标。—Google lee/evil transform

github.com](https://github.com/googollee/eviltransform) 

坐标测试网站:

[http://www.gpsspg.com/maps.htm](http://www.gpsspg.com/maps.htm)

# 结论

在中国做软件开发很有趣，因为这就像进入一个未知的领域进行探索。

如果你像我一样总是在学习，[点击此处](https://pages.convertkit.com/7f1dc85d44/61f5f55e74)获取我学习如何编码和日语的简明课程列表。