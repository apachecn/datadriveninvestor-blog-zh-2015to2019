# ML 的第 34 天–100 天—自动化怪异的人工智能

> 原文：<https://medium.datadriveninvestor.com/day-34-100-days-of-ml-automating-weird-al-a1b30953b492?source=collection_archive---------30----------------------->

[![](img/d1c0725fb74e81d88da379d916d0caa6.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/7fbe54c3ecd15c3c3f4d01405cf188a4.png)

Photo by [Luca Bravo](https://unsplash.com/@lucabravo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

首先，我显然不是为这 100 天的挑战而设计的。很抱歉，谢谢你的耐心。我积压了 20 篇想要写的文章，但是由于许多原因(健康、工作、时间)，我不能抽出时间来写它们，但是我仍然喜欢为这个社区做贡献，因为我已经对它投入了很多，社区也对我投入了很多。

第二，如果你是佛罗里达州的追随者，请让我知道。我们这里急需人工智能人才。

第三，好吧，所以你看到了标题，但你可能不知道我在说什么。怪异铝是开创性的歌曲模仿作家。他在加州大学洛杉矶分校(UCLA)崭露头角，在那里他很年轻就毕业了，并将自己的歌曲创作和手风琴技能传授给了迪门托博士(当时是一位电台名人)和一个名为“第一广场”的公共节目。在 80 年代的某个时候，他能够转向主流，并从此成为顶级歌曲模仿作家。

因此，在 2015 年，当我学习 Python 并注意到我的喜剧写作中的模式以及了解 NLTK 这样的框架时，我开始想知道歌曲模仿写作是否有可能自动化。快进到 2017 年，当我开始学习递归神经网络时，我开始认为这是一个巨大的可能性。

让电脑押韵应该不难。只要把音素和单词匹配起来，你应该可以用 NLTK 和 Carngie Mellon 的发音词典([http://www.speech.cs.cmu.edu/cgi-bin/cmudict?)做到 in = C+M+U+字典](http://www.speech.cs.cmu.edu/cgi-bin/cmudict?in=C+M+U+Dictionary)。还是那句话，我没有 Linux 盒子，我买不起，所以我不能尝试我想尝试的东西，但这在我的脑海里听起来是一个很容易的项目。

谈过 RNNs 后，给神经网络输入原始歌词，然后怪异的 al 版本可能会给我们一个基本的歌曲模仿生成器，但这将是有限的和怪异的，因为怪异的 al 会根据时间和文化参考进行调整，这就是诀窍。这就是诀窍所在，根据适当的环境进行调整。最重要的是，根据适当的背景进行调整，创造一首常青的歌曲，而不是短期的热门歌曲。

我相信(我也希望)在以前的一篇文章中，我提到过喜剧是 3-7 个神经网络，每个神经网络都与一个上下文相关联，这些网络的结合创造了最佳(最有趣的)幽默。

如果你正在做这样的项目，请告诉我。这绝对是一个很酷的思想实验，看看什么可以和将会被 AI 打乱。

干杯。