# 阻止无法检测的电子邮件病毒

> 原文：<https://medium.datadriveninvestor.com/stopping-the-undetectable-email-virus-44f460cbfffb?source=collection_archive---------14----------------------->

*增强企业安全性的简单策略，唾手可得，却常常被忽视*

![](img/4e670d580d64dcc3fb3599f3687fc756.png)

*(Photo: Shutterstock)*

在我的最后一次飞行中，当我站在机场安检线，漫不经心地看着安检过程——袋子、鞋子、笔记本电脑被匆忙放进托盘，放在传送带上，把所有东西都搬进 x 光机的黑色通道——我注意到 x 光操作员盯着多个屏幕，屏幕上有幽灵般的袋子轮廓，它们的内容显示为橙色和绿色的计算机突出显示的对象。我认为这个安全流程是公司如何保护自己免受外部电子邮件威胁的一个隐喻。在进入企业之前，电子邮件会通过系统筛选每封电子邮件及其内容。一旦检查到威胁，清除的邮件将被发送到用户收件箱。但这是一个不完美的比喻。机场和电子邮件安全流程有一个关键区别，即人。

在机场安检线，当检查包裹内容时，人与机器联合。对于每一台扫描袋子内容的机器，都有一名操作员在查看这些内容。由于机器能够识别关键物体，加上由大脑强大的模式匹配能力支持的人眼，为威胁检测创造了一个更强大的解决方案。

> 就像某种数字俄罗斯轮盘赌一样，如果它是一个被感染的文件附件，唯一的方法就是扣动扳机，或者在这种情况下，点击文件。

相比之下，几乎所有的电子邮件安全解决方案都仅仅依靠机器来扫描电子邮件及其内容以发现威胁。人类很少参与这个过程。机器扫描完成后，电子邮件及其附件将被转发给最终用户。现在，在组织的防火墙内部，最终用户只能在本地打开电子邮件及其附件。没有时间安全地检查里面的东西。就像某种数字俄罗斯轮盘赌一样，如果它是一个被感染的附件，唯一的方法就是扣动扳机，或者在这种情况下，点击文件。显然，这种模式并不奏效，正如每日新闻周期所证明的那样，充斥着通过头号攻击载体电子邮件( [1](https://gbhackers.com/malware-remote-access-trojan/) 、 [2](https://www.bleepingcomputer.com/news/security/new-threat-actor-impersonates-govt-agencies-to-deliver-malware/) 、 [3](https://brica.de/alerts/alert/public/1283880/government-raises-threat-level-on-undetectable-email-virus/) )传递的恶意文件所导致的不断的违规和勒索消息。如果机场安检和我们的“高级”电子邮件防御一样成功率很低，我们大多数人都会很乐意坐火车旅行。

[](https://www.datadriveninvestor.com/2018/09/22/infographic-journey-to-the-clouds/) [## 信息图:云之旅|数据驱动的投资者

### 聪明的企业领导者了解利用云的价值。随着数据存储需求的增长，他们已经…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2018/09/22/infographic-journey-to-the-clouds/) 

在一个我们指望计算机和人工智能算法来解决所有问题的时代，我们忽略了手边有一个经过良好测试的神经网络。事实上，它位于我们两耳之间。将人作为电子邮件安全解决方案的一部分的一种简单方法是，在本地打开文件之前，向用户提供文件的安全预览。通过提供安全的预览，企业安全可以利用人类的思维来检查文件的内容，然后将恶意代码直接释放到本地设备上。对于黑客来说，在一个名为“invoice.doc”的文件中创建并嵌入一个病毒，比编写一份对收件人有意义的实际发票要容易得多，也更容易扩展。

好消息是，可以通过许多不同的方式实现安全预览。一种容易实现的方法是将附件移动到一个单独的存储库中，并用一个链接替换它们，该链接使文件内容可以在 web 浏览器中查看。这几乎可以通过任何云存储服务来实现，如 Box、OneDrive、Google Drive 或 Egnyte。事实上，Gsuite 提供了大多数电子邮件附件文件类型的预览。挑战在于用户通常只是下载文件，然后在本地查看。赛门铁克的 [Email Security.cloud](https://www.symantec.com/products/email-security-cloud) 或 [mxHero](https://www.mxhero.com/) 等解决方案允许组织确保用户在下载附件之前先进行预览。MxHero 的解决方案甚至允许公司从现有的云内容平台上传文件，无论是 OneDrive、Box、Egnyte 还是 Google Drive。

![](img/f8c2df302e9b8db3cb1b1a6a3ae2fd19.png)

mxHero uploads and replaces attachments with cloud storage preview links. End users can safely preview files before downloading locally.

所以，下一次有人声称电子邮件病毒是“无法检测的”，让我们弄清楚——机器无法检测( [*政府提高了“无法检测”电子邮件病毒的威胁等级*](https://www.9news.com.au/national/emotet-government-raises-alert-level-on-dangerous-email-virus-hitting-inboxes/2402a731-4676-49b6-ae10-4de9a4ef79e2) )。当我继续阅读企业违规的新闻时，我觉得很讽刺的是，在许多情况下，问题可以通过一个简单的解决方案来避免，就在我们的眼皮底下，或者在这种情况下，在我们的耳朵之间。