# 云中的深度学习——便宜但高质量

> 原文：<https://medium.datadriveninvestor.com/deep-learning-in-cloud-df0c654d61b1?source=collection_archive---------1----------------------->

[![](img/afd0113551490dc56f16cc88554a8bc8.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/812d4fae8874484ee57b59fb5ab19364.png)

***编辑:*** 显然，谷歌把 Colab 的 GPU 从 K80 换成了特斯拉 T4。所以现在你可以在 Google Colab 免费做高质量的深度学习。但如果你需要更多的权力，你可以去 V100 可抢占的机器，成本远远低于 AWS。

Google Colab 是一个免费的平台，提供用于训练的 GPU，最适合做实验，但对于训练像 Big GANs 和大型语言模型这样的大型模型来说并不理想。而且总是把你的模型上传到 Google Drive，然后在机器中断的时候重新加载，很麻烦。

我有一台像样的 GTX 1060 笔记本电脑，我用它来试验我的模型并设置训练脚本。但一旦完成，我的笔记本电脑对这样的大模型就没用了。所以我开始寻找替代方案。然后我发现了云:D

![](img/81f5479522c2d488ad67d2054741e8c3.png)

Photo by [Christian Wiediger](https://unsplash.com/photos/rymh7EZPqRs?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

说到云，我们中的许多人更喜欢 AWS，因为它已经存在了一段时间，值得信赖，并且有大量的服务。但其价格远高于竞争对手。(为了训练我的模型，我将比较 GPU 机器的价格。)

[](https://www.datadriveninvestor.com/2019/01/07/the-ultimate-learning-path-for-deep-learning-in-2019-more/) [## 2019 年深度学习的终极学习路径及更多...-数据驱动型投资者

### 又一个美好的一周，一些好的教育内容将会到来。我最喜欢的&最受欢迎的帖子之一…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/07/the-ultimate-learning-path-for-deep-learning-in-2019-more/) 

`p2.xlarge`成本仅为 0.9 美元/小时，再次毫无用处，因为 K80 GPUs 在深度学习方面表现不佳。【V100 每小时 3 美元，这在许多情况下是值得的，但仍然太贵。去`spot instance`每小时只需 1.2 美元。这才是我喜欢的。

我继续搜索，因为我的一些模型需要的计算比 V100 少，1.2 美元/小时对我们大多数人来说仍然很贵。这让我想到了 Paperspace，它是 AWS 的替代品，但仍然提供低端 GPU。

`P4000`paper space 上的 GPU 性能接近桌面级 GTX 1070，每小时成本仅为 0.51 美元。再高点`P5000`接近 GTX 1080，0.78 美元/小时。还有`P6000`就是~GTX 1080 Ti，价位 1.1 美元/小时。`V100`成本 2.3 美元。好消息是这些不是现货实例，所以价格比 AWS 低是合理的。

我使用 paperspace 已经有一段时间了，但他们的前期成本(50GB 硬盘每月 5 美元)对我来说是一种拖累。我一个月只用一台机器进行 5-10 个小时的训练。因此，我对廉价 GPU 的追求仍在继续。

![](img/94fbecaf1949f3b8d1348627e44c62ea.png)

By [PixaBay](https://www.pexels.com/@pixabay) on [Pexels](https://www.pexels.com)

AWS 的竞争对手 Google Cloud 正在成长云平台。他们令人垂涎的价格吸引了我。他们的`Preemptible`(Spot instance)`V100`只需 0.8 美元/小时`Preemptible`特斯拉 T4(与 RTX 2070 或 1080 + Mix precision 相当)只需 0.35 美元/小时。

在 Google Colab 上，你必须不断上传模型到 Google Drive 来保存它，否则它就会丢失。但是在这些机器上，即使它们在关闭时是可抢占，它们的数据仍然是完整的。你所要做的就是不时地保存你的模型，:D