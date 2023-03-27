# 可穿戴设备和传感器数据的隐私(或者，缺乏隐私？)

> 原文：<https://medium.datadriveninvestor.com/https-medium-com-lucafoschini-privacy-of-wearables-data-parti-faf6a7e0c0e3?source=collection_archive---------1----------------------->

[![](img/3e48ba3d60b502e72db2aaa79ee26065.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/78a922b28f7c1772d33763ee599e55c6.png)

Photo by [Carlos Muza](https://unsplash.com/@kmuza?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# AI 可以通过挖掘他们的健身追踪器数据来暴露大量研究参与者的敏感健康信息吗？

最近的一项研究“[在大型国家体育活动数据集中重新识别个人的可行性，这些数据集中已使用机器学习删除了受保护的健康信息](https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2719130)”(Na 等人，JAMA Network Open 2018，2018 年 1 2 月 21 日)在主流新闻和社交媒体上引起了相当大的轰动。几个例子:

[](https://www.reuters.com/article/us-health-privacy/anonymous-patient-data-may-not-be-as-private-as-previously-thought-idUSKCN1OK24O) [## 匿名患者数据可能不像以前认为的那样隐私

### (路透社健康频道)-多年来，研究人员一直在利用大量的患者数据研究医疗状况…

www.reuters.com](https://www.reuters.com/article/us-health-privacy/anonymous-patient-data-may-not-be-as-private-as-previously-thought-idUSKCN1OK24O) [](https://www.dailymail.co.uk/news/article-6522835/Study-claims-hackers-able-match-identified-health-information-patient-identities.html) [## 研究称，黑客可以将“去身份化”的健康信息与患者匹配

### 新的 JAMA 网络开放研究能够使用人工智能成功匹配“去识别”Fitbit 数据…

www.dailymail.co.uk](https://www.dailymail.co.uk/news/article-6522835/Study-claims-hackers-able-match-identified-health-information-patient-identities.html) 

此外:

*   [可穿戴设备的聚合数据并不能完全隐藏个人身份](https://www.medpagetoday.com/primarycare/exercisefitness/77089)，*今日医疗*，2018 年 1 2 月 21 日
*   [我们的医疗保健数据不再是私人的:研究表明，机器学习可用于从身体活动数据中重新识别个人](https://hub.packtpub.com/our-healthcare-data-is-not-private-anymore-study-reveals-that-machine-learning-can-be-used-to-re-identify-individuals-from-physical-activity-data/)， *Packt Hub* ，2018 年 12 月 24 日
*   [人工智能的进步开启健康数据隐私攻击](https://news.berkeley.edu/2018/12/21/advancement-of-artificial-intelligence-opens-health-data-privacy-to-attack/) *伯克利新闻*2018 年 12 月 21 日 2018
*   [人工智能的进步威胁健康数据隐私:研究](https://www.theweek.in/news/sci-tech/2018/12/26/advances-in-ai-threaten-data-privacy-study.html)，*本周*，2018 年 12 月 26 日
*   [人工智能进步威胁健康数据隐私](https://www.sciencedaily.com/releases/2019/01/190103152906.htm)，*科学日报*2019 年 1 月 3 日
*   [可穿戴设备和移动设备中的人工智能威胁着健康数据的隐私:报告](https://www.gadgetsnow.com/tech-news/ai-in-wearables-and-mobiles-threatening-privacy-of-health-data-report/articleshow/67384683.cms)，Gadgets Now，2019 年 1 月 5 日
*   [人工智能的进步威胁健康数据的隐私](https://marketbusinessnews.com/artificial-intelligence-health-data/193677/),《市场商业新闻》，2109 年 1 月 6 日
*   [如何通过健身追踪器数据识别私人健康信息](https://medcitynews.com/2019/01/how-private-health-info-can-be-identified-through-fitness-tracker-data/?rf=1)，*医疗城新闻*，2019 年 1 月 31 日

在最近的事件中，强调了在大数据时代重新思考隐私的必要性(见最近的[哈佛商业评论评论](https://hbr.org/2019/01/privacy-and-cybersecurity-are-converging-heres-why-that-matters-for-people-and-for-companies)的概述)，预计这样的话题将得到主流媒体的大量关注。然而，许多人和许多报告对如何解释那等人的研究结果感到困惑。

在 Evidation，我们对类似于 Na 等人文章中讨论的数据进行了研究，包括 NHANES 数据集本身。基于这一经验，在接下来的系列文章中，我将尝试澄清 Na 等人的研究对以下问题的影响:

*   NHANES 研究参与者的隐私含义:**保持冷静，不要侵犯隐私。**
*   可穿戴设备数据和其他连续收集的时间序列数据的隐私含义:**侵犯隐私*将*可能发生。**
*   人工智能和机器学习在重识别攻击中的作用: **AI 在这里不是罪魁祸首，大(*高维*)数据才是。**

感谢任何反馈。欢迎对帖子发表评论或通过 Twitter @calimagna 发表评论。更多关于我的背景和研究的信息可以在[这里](http://lucafoschini.com/)找到。

# 第一部分:NHANES 参与者的隐私安全。(目前来说。)

让我们从 Na 等人的研究中使用的 NHANES 数据集的一些背景开始。这项研究查看了在美国疾病控制和预防中心(CDC)国家健康统计中心(National Center for Health Statistics)开展的[国家健康和营养检查调查](https://www.cdc.gov/nchs/nhanes/index.htm) (NHANES)背景下收集的可穿戴数据。

![](img/2bc1df919338a72175ffceb368179ce4.png)

The National Health and Nutrition Examination Survey (NHANES) is a program of studies designed to assess the health and nutritional status of adults and children in the United States. The survey is unique in that it combines interviews and physical examinations.

在 2003-2004 年和 2005-2006 年，NHANES 还收集了**身体活动监测(PAM)数据，包括 7 天内测量的 9601 名成人和 5030 名儿童的 1 分钟分辨率强度数据**。使用了 [Actigraph GT3X-plus](https://actigraphcorp.com/support/activity-monitors/gt3xplus/) 监视器。(此处[见](https://www.cdc.gov/nchs/data/nhanes/nhanes_11_12/Physical_Activity_Monitor_Manual.pdf)PAM 数据采集协议)。(对于那些对健康数据科学感兴趣的人，我在 Evidation 的团队与 UCSB 大学的 Alex Frank 教授合作，为 NHANES 2005 PAM 数据集创建了一个包含一些 ETL 脚本和探索的存储库。)

然后作者做了以下工作:

1.  **将 NHANES 数据分割**为数据集 **A** 和 **B.** 数据集 **A** 包含所有参与者的 PAM 和人口统计数据**周一至周三** *。*类似地，数据集 **B** 包含从**周四到周五**的所有参与者的数据。换句话说，就参与者而言， **A** 和 **B** 完全重叠，而就覆盖的时间间隔而言，它们完全不相交。
2.  **将数据集 **A** 和 **B** 上的**分钟级 PAM 数据聚合到 20 分钟的时间分辨率。
3.  表明作者在 **90+%** 的情况下(成人，85+%,儿童)的最佳算法可以通过仅查看参与者 20 分钟的累计身体活动和人口统计数据，将数据集 **A** 的参与者记录与数据集 **B 中的正确记录进行匹配。**

总之，聚合的身体活动和人口统计数据足以从数据集 **A** 和数据集 **B** 中重新识别参与者。

> 似乎被许多人忽略的要点是，所执行的重新识别完全包含在 ***匿名化的*** NHANES 数据集中。换句话说，该算法可以可靠地判断出 NHANES 参与者 0001337 何时在数据集 **A** 和 **B** 中是相同的，而不是参与者 0001337 是来自加州圣巴巴拉的 49 岁的阿达·洛芙莱斯。

同样值得注意的是，正如在回复这篇文章的的[后续社论中所讨论的那样，**大部分重新识别的准确性实际上来自人口统计数据，而不是活动数据。**引用回复:“从[Na 等人]文章中的表 3[第一列]中，我们看到两个队列(2003–2004 和 2005–2006)中仅人口统计学特征的成人再识别准确性超过 80%，而仅活动数据的准确性不到 7%。”](https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2719121)

总之，已经表明成功的重新识别被限制在 NHANES 数据集内的**，并且即使不使用活动数据，也可以实现，尽管精度较低。Na 等人的工作没有披露关于 NHANES 参与者的额外信息，这些信息还没有公开。**

我们可能会感到欣慰的是，数千名 NHANES 研究参与者的隐私并没有被这项研究的结果所侵犯。然而，正如我们将在本系列第二部分、**中看到的，这样的陈述只在此时此地**成立。重新识别是这种数据的固有风险，这种风险并不局限于特定数据集的边界内*。*从这个意义上来说，Na 等人将 NHANES 数据集分割成两个非时间重叠数据集**的过程混淆了这种数据**的真正问题，即如果攻击者*和*拥有时间重叠数据集，那么利用这种细粒度的时间序列数据，匹配过程将变得非常简单，并将产生几乎确定的重新识别保证。

这种时间重叠数据集被非预期的第三方获取的风险是我们未来必须不断防范的风险。从这个意义上说，NHANES 参与者的隐私，就像公开发布的数据集中的任何研究参与者的隐私一样，随着对手获得更多的数据和计算资源，正面临越来越大的风险。例如，如果艾达在 NHANES PAM 群组中，并在脸书上吹嘘她在研究期间的活动成就，她在脸书的朋友艾达的老板可能会使用 Na 等人的方法重新识别她，并了解她的[心理健康、性行为和酒精使用](https://wwwn.cdc.gov/nchs/nhanes/search/datapage.aspx?Component=Questionnaire&CycleBeginYear=2003)，这些也是 NHANES 研究的一部分。

随着最近 [FDA 推动使用真实世界的证据来支持监管决策](https://www.fda.gov/NewsEvents/Newsroom/PressAnnouncements/ucm627760.htm)(包括发布用于收集研究中数字数据的[应用](https://www.fda.gov/NewsEvents/Newsroom/FDAInBrief/ucm625228.htm))，以及最近[Fitbit 和 NIH](https://medcitynews.com/2019/01/fitbit-and-nih-boost-precision-medicine-research-partnership/) 的合作，以使 Fitbit 用户能够将其账户与[全美精准医学研究项目](https://allofus.nih.gov/)联系起来，研究中收集的数据越来越有可能直接来自来源，如消费者应用和可穿戴设备，其数据也可以由参与者(/消费者)通过其他渠道直接获得，例如例如，在研究过程中佩戴 Fitbit 的参与者可以在 Twitter 上分享他们的日常步骤成就，或者佩戴连续葡萄糖监测(CGM)设备的糖尿病研究参与者可以在 Instagram 上发布他们的 CGM 时间表的照片(前瞻性 [Tidepool](https://tidepool.org/) 的 [EULA](https://tidepool.org/legal/privacy-policy-2-0/) 中有一个例子)。如果研究人员将研究数据公之于众，任何人都可以将社交网络上发布的数据与研究中的数据联系起来，但与 Na 等人的论文不同的是，这一次**将数据与参与者的真实(在线)身份联系起来**。

这些风险似乎只是理论上的，但是正如我们将在[第二部分](http://https-medium-com-lucafoschini-privacy-of-wearables-data-partii-116fec6fbcf)中看到的，从计算的角度来看，这些攻击远非不切实际。随着时间的推移，随着更多数据的生成，风险也会增加。已经发布的数据集今天可能没有被重新识别的风险，但它们可能会很快被新的**非预期的推论** 所利用，这些推论是由在未来任何时间点变得可用的新数据实现的。

但是坏到什么程度呢？继续阅读[第二部分](https://medium.com/@lucafoschini/https-medium-com-lucafoschini-privacy-of-wearables-data-partii-116fec6fbcf)，了解如何量化重新识别的风险，以及围绕数据共享和面向未来的隐私保护方法开发的新隐私框架如何缓解这些问题。

## 来自 DDI 的相关故事:

[](https://medium.com/datadriveninvestor/why-data-will-transform-investment-management-4a60966c1c81) [## 为什么数据会改变投资管理

### 有人称之为“新石油”虽然它与黑金没有什么相似之处，但它的不断商品化…

medium.com](https://medium.com/datadriveninvestor/why-data-will-transform-investment-management-4a60966c1c81) [](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4) [## 数据科学和软件工程哪个更有前途？

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

medium.com](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4)