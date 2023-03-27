# 识别无效网站流量

> 原文：<https://medium.datadriveninvestor.com/identifying-invalid-website-traffic-f1ce32cbde7e?source=collection_archive---------36----------------------->

[![](img/919154f90999fba2aaf4bf14bb709e6a.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/a9cb1795cde0cc2e7e7d5e5b1be56eec.png)

## 太平洋时间 2018 年 12 月 18 日 18:00，我的博客成为垃圾邮件机器人攻击的目标..

*最初发表于*[*【millennialmoderator.com】*](https://millennialmoderator.com/identifying-invalid-website-traffic)*。*

我的网站请求率在 3 分钟内从平均 100/小时飙升到 2000/小时。根据谷歌分析，流量完全是无机的(0:00 花费在网站上)，99.99%的跳出率，我的网页没有一个增加了用户数量。由于这种无效的流量高峰，Google Adsense 完全关闭了我的 Adsense 帐户，我试图联系他们恢复的每一次尝试都被返回:

*在彻底检查您的帐户数据并考虑您的反馈后，我们的专家确认我们无法恢复您的 AdSense 帐户。*

我很容易受到一个神秘攻击者的攻击，被 Google Adsense 团队避开，我盈利的博客商业模式跌到了 0.00 美元。你可以在这篇关于媒体的文章中读到我是如何找到一个新的广告平台的。

![](img/b6332b6d5dd333cc188cf2974de74f5d.png)

# 什么是垃圾邮件？

在其所有的变体(电子邮件、表格、点击等)中，垃圾邮件是一种从广泛选择的个人中唤起预先思考的响应的乐观尝试。最常见的是，垃圾邮件试图以垃圾邮件、网站弹出窗口等形式收集人们的个人信息(信用卡、电话号码等)。在我的案例中，垃圾邮件流量(或机器人)在几分钟内成功地 ping 了我的网站数千次，最有可能的目的是让我陷入财务困境(AWS 的所有数据传输费用)，或者阻止我与谷歌的合作。谁知道呢，真的。一些垃圾邮件；比如时事通讯，可以被无限期地避免，但是其他的更狡猾，改变他们的外表来躲过安全协议，不被发现。

# 识别无效流量

起初，我不知道是什么导致了网络流量的急剧增加。第一个迹象实际上是来自谷歌的关于我的 Adsense 帐户被关闭的电子邮件，因为在这段时间我不在笔记本电脑旁，没有积极地监控我的网站。我立即去谷歌分析，看看我是否能识别这个流量峰值。我看到的第一件事是网站用户数量激增，今天我可以通过日期过滤来确认。

有趣的是，当我试图查看这些用户登录的页面时，没有任何数据。每页的用户数根本没有反映出流量的增加，这告诉我机器人正在向网站发送请求，而从来没有真正加载页面。绝对是我这边设计的一个[漏洞。我还能够从](https://www.amazon.com/gp/product/1491937017/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491937017&linkCode=as2&tag=aleksweyman-20&linkId=fa518860af3554b745a97444b8601b80) [AWS](https://millennialmoderator.com/how-to-use-amazon-web-services) 中的 CloudFront 分发控制台发现请求率的增加，我在那里处理我所有的托管需求。

![](img/cd14ef2e7513b5873e0828944a60d41e.png)

# 预防措施

我做的第一件事是在 AWS 方面设置了许多警报。Cloudwatch 是他们提供的警报服务，所以我设置了几个警报来通知我未来的无效活动。原来 Google Adsense 实际上有一个[表单，当你认为你的网站有无效流量时，你可以提交这个表单](https://support.google.com/adsense/contact/invalid_clicks_contact)。我想通过尽快通知他们，你向他们证明流量不是由你造成的，他们在评估你的账户是否需要被关闭时会考虑这一点。如果我早点知道这份表格，我会马上提交我的索赔。我想是吸取了教训。

在配置了大量警报之后，我转向我的 CloudFront 发行版来调节请求速率。因为我的[网站](https://millennialmoderator.com/website-hosting-on-s3-tutorial-low-cost)从未超过每分钟 200 个请求，所以我在那里设置了门槛，并祈祷它不会妨碍用户体验。从那以后，我提高了这个限制，以适应增加的(有机)流量。

当我转向 Google Analytics 上可能的安全措施时(因为 Adsense 控制台为我锁定)，我发现了一些有趣的事情，在进一步调查无效流量后，我能够确定网络来源不是别人，正是**亚马逊技术有限公司**经过一些研究并发现其他人也有[类似事件](https://www.statusbureau.com/blog/2017/04/analytics-bot-traffic-ashburn/)，这似乎是源于弗吉尼亚州阿什伯恩地区的已知 bot 垃圾邮件问题的来源。

![](img/04be7e25082d9b0216f4f7931d42a9d4.png)

阿什伯恩是整个亚马逊网络中最大的云计算数据中心之一的所在地。我推测他们的一个客户正在滥用硬件，发送 bot 流量淹没人们的网站。别担心，我已经就此向 AWS 滥用团队提交了索赔。

通过这次经历，我学到了很多关于我的网站的安全性，以及谷歌的无情本性(虽然我不怪他们)。我希望我的不幸能让你对如何更严密地监控你的资源有所了解，当然，也提醒你要认真对待安全问题。去[寻找新的广告平台](https://millennialmoderator.com/finding-alternatives-to-google-adsense)的旅程很艰难，但我猜黎明前总是最黑暗的。有评论或想法？在[推特](https://twitter.com/alekseyweyman)上让我知道！

标记为:[技术安全](https://millennialmoderator.com/identifying-invalid-website-traffic#)

*最初发表于*[*millennialmoderator.com*](https://millennialmoderator.com/identifying-invalid-website-traffic)*。*