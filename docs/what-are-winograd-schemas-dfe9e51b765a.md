# 什么是 Winograd 模式？

> 原文：<https://medium.datadriveninvestor.com/what-are-winograd-schemas-dfe9e51b765a?source=collection_archive---------12----------------------->

[![](img/e2cbc822a2bedfe54be48f1b1387f52b.png)](http://www.track.datadriveninvestor.com/ExpertViewTeali1)![](img/10e22097f9563e47682a9e3bbfc8e690.png)

Photo by [Franck V.](https://unsplash.com/photos/JjGXjESMxOY?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/artificial-intelligence?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

图灵测试测试机器是否能表现出与人类相当或无法区分的智能行为。有了 [Google Duplex](https://www.youtube.com/watch?v=D5VN56jQMWM) 替你打电话，通过图灵测试，就能说机器真的智能了吗？当然，它确实将人工智能带到了一个全新的水平，但图灵测试并不是判断机器智能的理想方式。

[威诺格拉图式挑战赛](http://commonsensereasoning.org/winograd.html) (WSC)是一项通过 ***常识推理*** 的机器智能测试。

它是图灵测试的一种替代方法，提供了多项选择，采用了非常具体的结构问题:它们是所谓的 Winograd 模式的实例，以 Terry Winograd 教授的名字命名。

考虑下面的句子:

> 市议员拒绝给示威者发放许可证，因为他们[害怕/主张]暴力。

“害怕”和“提倡”的选择把图式变成了两个实例:

1.  市议员拒绝发给示威者许可证，因为他们害怕暴力。
2.  市议员拒绝发给示威者许可证，因为他们鼓吹暴力。

这是 WSC 的一个经典例子，对一个门外汉来说答案是超级容易的。凭常识、逻辑推理和理解句子的意思，我们可以理直气壮地断定**他们在第一句中指的是市议员，而在第二句中，指的是示威者。**

**这个结论是基于对第一句中 ***怕*** ***暴力*** 和第二句中 ***主张*** ***暴力*** 的理解。**

**挑战在于创建一个能从二进制选择中正确回答的模型；对于非专家来说，很明显，一个不能得到正确答案的程序在理解和难度上有严重的差距，因为它远远超出了当前的技术水平**

**[![](img/e2cbc822a2bedfe54be48f1b1387f52b.png)](http://www.track.datadriveninvestor.com/ExpertViewI1B)**