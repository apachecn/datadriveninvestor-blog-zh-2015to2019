# 这种方式带来了一些邪恶的东西:保护您的 API

> 原文：<https://medium.datadriveninvestor.com/something-wicked-this-way-comes-securing-your-apis-85c850a662f9?source=collection_archive---------2----------------------->

[![](img/95a9a07783c75c7529565d11404d3697.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/d497c8b05b9d2e20268771adcd888835.png)

Source: Pinterest.com

一家公司现在运行的应用程序编程接口(API)的平均数量是 420 个。[据 Akamai 称，其作为 CDN 的流量中，超过 83%](https://www.akamai.com/us/en/multimedia/documents/state-of-the-internet/state-of-the-internet-security-retail-attacks-and-api-traffic-report-2019.pdf) 是 API 流量。事实已经不容忽视，如今互联网上超过一半的流量已经不再是人对应用的流量，而是应用对应用的流量。随着 5G 的兴起成为现实，更多的物联网(IoT)设备上线，这种流量将继续增长，而不是退潮。单一应用程序的日子也一去不复返了，因为它们开创了 API 背后的微服务的新时代，黑客们知道这一点。

“如果我要向一个敌对的民族国家建议如何让美国丧失能力，我会告诉他们先对付 API。”匿名的

[](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) [## 雅虎财经 API 的 6 个替代方案——数据驱动投资者

### 雅虎财务 API 是新的财务 API 万岁！雅虎财务 API 长期以来一直是许多公司的可靠工具。

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) 

不仅仅是小型企业的 API 遭到破坏。被攻破 API 俱乐部的不幸成员还包括[威瑞森](https://apisecurity.io/issue-26-verizon-routers-patched-api-vulnerability/)、[三星](https://techcrunch.com/2019/05/08/samsung-source-code-leak/)、[谷歌](https://apisecurity.io/issue-1-apistrat-cors-samsung-google-facebook-gitlab-apple/)、[脸书、](https://apisecurity.io/issue-1-apistrat-cors-samsung-google-facebook-gitlab-apple/) [苹果](https://apisecurity.io/issue-1-apistrat-cors-samsung-google-facebook-gitlab-apple/)、 [T-Mobile、](https://threatpost.com/t-mobile-alerts-2-3-million-customers-of-data-breach-tied-to-leaky-api/136896/) [万豪](https://krebsonsecurity.com/2018/12/what-the-marriott-breach-says-about-security/comment-page-1/)，不胜枚举。因此，如果这家价值数十亿美元的大公司能够雇佣跨越整个园区的开发人员和安全工程师，但似乎都做不好，那你还有什么机会呢？

我在这里告诉你你知道。您只需要认识到 API 是新的攻击面，并且您试图用来保护 API 的 Web 应用程序防火墙(WAF)就像试图用螺丝刀拔掉钉子一样。就是不行。

问题通常是 API 服务器(API 提供者)支持的内容和与 API 客户机(API 消费者)签订的合同允许的内容之间的差异。开发人员将密钥留在源代码中，并将其发布到源代码控制和存储网站，如 [Gitlab](https://devclass.com/2018/10/02/gitlab-api-flaw-security-updates/) 和[Github，这进一步加剧了这个问题，就在本周，三星](https://www.scmagazineuk.com/samsung-private-gitlab-tokens-exposed-including-source-code-credentials-secret-keys/article/1584224)就遇到了这种情况。

这些问题也延伸到移动应用程序的开发者，他们将 API 密钥、令牌和凭证硬编码到移动应用程序中，没有意识到这些应用程序可以使用免费的工具进行反编译，正如我自己的研究[报告中所证明的那样，该报告上个月与阿尔山科技](https://www.arxan.com/resources/video/vulnerability-epidemic-mobile-financial-apps)一起发布，随后在艾特集团发布。

事实是，除非开发人员停止犯诸如在可读源代码中硬编码密钥和令牌这样的错误，认识到 web 应用程序防火墙不是为询问 API 流量而设计的，而是使用 API 安全网关，执行 API 渗透测试，并利用静态代码和动态代码分析，否则情况会在好转之前变得更糟。

如果你需要一个 API 安全指南、新闻和漏洞信息以及这些漏洞的详细信息的一站式商店，请查看 [42 Crunch](http://www.42crunch.com/) 的人们在 [apisecurity.io](http://www.apisecurity.io/) 社区站点上创建的内容。

**分析师展望**

本月我将发布一份新的研究报告，内容涉及 API 安全市场的现状、参与者、问题和解决方案，以及如何使用这种新型工具来解决这个问题。欲了解更多信息，请访问艾特集团的我的研究[微型网站。](https://aitegroup.com/users/alissa-knight)

![](img/36e8caf8fd63116fbe553bcffb37840a.png)

那么你有什么看法？你认为为什么组织会不断地被他们的 API 攻击？你认为违规背后最大的原因是什么？你对 API 安全性有什么疑问？

请在下面的部分留下您的评论！

![](img/ac9cbdba4725e5633416bc4b1b63d69f.png)

喜欢和分享

像往常一样，如果你喜欢这篇文章，请点击“喜欢”来支持我，并与你自己的 feed 分享！这是你支持我和我继续研究的最好方式。如果任何人对这篇文章有任何补充或评论，请在评论区与下面的每个人分享！在我的主页[www.alissaknight.com](http://www.alissaknight.com/)、 [LinkedIn](http://www.linkedn.com/in/alissaknight) 上了解更多关于我的信息，在我的 [YouTube 频道](http://www.youtube.com/c/alissaknight)上观看我的视频博客，收听我每周的[播客片段](http://alissaknight.libysyn.com/)，或者在 Twitter 上关注我 [@alissaknight。](http://www.twitter.com/@alissaknight)

![](img/1b032f5550ca6f23269f5f56adf2359c.png)

关于我

我是 [Aite Group](http://www.aitegroup.com/) 的高级分析师，通过评估行业趋势、创建细分分类、确定市场规模、准备预测和开发行业模型，对影响金融服务、医疗保健和金融科技行业的网络安全问题进行重点研究。我通过公正、客观和准确的研究和内容开发，为这些行业提供网络安全市场的联合和定制市场研究、竞争情报和咨询服务。根据我对当今影响这些行业的当代网络安全问题的研究，我撰写研究报告和白皮书，并提供咨询服务，包括询问、简报、咨询项目、研究结果演示以及预约演讲，我经常在每年的网络安全会议、研讨会和圆桌会议上发表主题演讲。