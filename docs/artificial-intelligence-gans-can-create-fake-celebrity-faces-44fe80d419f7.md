# 人工智能+ GANs 可以制造假的名人脸

> 原文：<https://medium.datadriveninvestor.com/artificial-intelligence-gans-can-create-fake-celebrity-faces-44fe80d419f7?source=collection_archive---------2----------------------->

[![](img/e3260bdb22a8e55371110b507bbe8f46.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/35ad667ac4dd85d186f0c2b2a4ac13af.png)

生成对抗网络是深度学习领域的一个研究热点。gan 通过训练两个相互竞争的独立网络来解决问题。一个网络产生答案(生成式)，而另一个网络区分真实答案和生成的答案(鉴别器)。

gan 是由蒙特利尔大学的 Ian Goodfellow 和其他研究人员创建的。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？-数据驱动型投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

GANs 的目标是竞争性地训练两个网络，以便在一段时间后，两个网络都不能相对于另一个网络取得进一步的进展，或者生成器成为鉴别器网络不能区分真假的专家。

当我看到一个假巴拉克·奥巴马说话像真的一样的视频时，我感到很惊讶。嘴唇和声音的同步让人印象深刻。

你可以在这里看到同样的视频:

在这次 TED 演讲中，计算机科学家 Supasorn Suwajanakorn 展示了一个人工智能和 3D 模型来创建照片级的假视频。这是 GANs 做的。

[](https://www.ted.com/talks/supasorn_suwajanakorn_fake_videos_of_real_people_and_how_to_spot_them/transcript?language=en) [## “真人假视频——如何识别”的文字记录

### TED Talk Subtitles and Transcript:你认为你擅长识别虚假视频吗？在这些视频中，名人说了一些事情…

www.ted.com](https://www.ted.com/talks/supasorn_suwajanakorn_fake_videos_of_real_people_and_how_to_spot_them/transcript?language=en) 

这让我读到了更多关于 GANs 能做什么的内容，这些用例真的很有趣。应用领域越来越大，您可以将 GANs 用于以下目的:

*   图像翻译
*   面部属性操作
*   医学中的异常检测
*   面部完成
*   视频预测和生成
*   创造艺术

# GANs 是如何工作的？

就像我之前说的，GAN 的架构由两个网络组成:鉴别器和生成器。生成器创建新的图像，而鉴别器评估它们是真的还是假的。鉴别器决定将图像分类为真的还是假的。

作为一个例子，让我们想象我们正试图使用猫的数据集来复制猫的图片。鉴别器的目标是识别哪些图片属于 Cats 数据集。

生成器的职责是创建新的合成图像，传递给鉴别器，期望它会被归类为真实的，即使它是假的。因此，生成器的最终目标是为鉴别者创建几乎完美的猫的图片，而不被发现。鉴别器的目标是将来自生成器的图像识别为伪像。

如果我们可以用几个步骤来描述这个过程，它将是这样的:

1.  向生成器输入数据集(**示例:**名人面孔)，这样它就可以返回新的图像
2.  新生成的图像与取自实际数据集的一些图像一起被传递给鉴别器
3.  在接收到所有伪造和真实的图像后，鉴别器返回概率，一个在 0 和 1 之间的数字， **1** 代表对真实性的预测， **0** 代表伪造

![](img/e3628d27806ccd1dbb48999adfe6d4af.png)

GAN Architecture

# 用 PyTorch 和 CelebA 数据集生成新面孔

受到一些关于与甘斯合作创造新面孔的教程和论文的启发，我得到了 **CelebA 数据集**来做这个实验。主要步骤如下:

*   从官方网站获取数据集
*   使用所需的库(Torch 和 Torchvision)创建 GPU Colab 环境
*   训练两个网络:生成网络和鉴别网络
*   将结果可视化并进行比较

![](img/21fab5f1b3364f77fb941e4dd6ed2b4a.png)

# 大规模名人面孔属性(CelebA)数据集

这个数据集包含超过 **20 万张**名人图片，每张图片都有 40 个属性注释。图像覆盖了大的姿态变化和背景混乱。西里巴有很大的多样性，数量大，注释丰富，包括

*   10177 个身份，
*   202，599 个面部图像，以及
*   5 个标志位置，每幅图像 40 个二元属性注释。

![](img/12463173a14ccf1fb7dbeaa37312a859.png)

# 【PyTorch 的结果

下面，您可以看到一个比较真实图像和生成的假图像的可视化效果:

![](img/8258cfef2526ec839f766bf70310fa50.png)

# 使用 Tero Karras (NVIDIA)、Samuli Laine (NVIDIA)、Timo Aila (NVIDIA)的基于**风格的生成器架构生成对抗网络**

你会对 GANs 领域的进步感到惊讶。来自 NVIDIA 的 Tero Karras、Samuli Laine、Timo Aila 的一篇新论文名为:“GANs 的基于风格的生成器架构”，提出了一种使用风格转移的生成式对抗网络的替代生成器架构。新的架构导致自动学习、无监督地分离高级属性(例如，当在人脸上训练时的姿势和身份)和生成的图像中的随机变化(例如，雀斑、头发)，并且它使得能够对合成进行直观的、特定比例的控制。新的生成器在传统的分布质量度量方面改进了最先进的技术，导致明显更好的插值属性，并且也更好地解开了变化的潜在因素。为了量化插值质量和解缠，我们提出两种新的自动化方法，适用于任何发电机架构。

使用这种新颖的模型，结果好得多，创建高质量的人脸。

玩了他们在 Kaggle 上的演示，创造了一些随机的面孔。这些是结果:

![](img/3dd478610ac62f69e2d16ad038d5bff8.png)![](img/b7692bbe8813e1612cf3fe6b4cd06792.png)![](img/c77a88fcebcb45a1d3643ef2c3a62275.png)![](img/74f854b4160069b42572d7805ab00e65.png)![](img/397d089b9dfee544fd14240091f7ed28.png)![](img/25c161e379faf98d9a3f0b931078007f.png)![](img/2e495cd68fa308428fe2d3a62573e041.png)![](img/1441443132d72e0645018e0c6822d837.png)![](img/dcff17189428f035af8b39cc686cbc70.png)![](img/8c9d24a71c2d09f22cf06fa73cdcfa01.png)![](img/ffd2d538a6736d8284b777eb9f65ac1f.png)![](img/314f7988fe7fdf34be3791f3679ec7b0.png)![](img/b32980bbba432bd0027988ff1c8d439f.png)![](img/563558d7356649bf46c6c29e65f8359c.png)![](img/889cc344480a69efb859b6318be46cc3.png)![](img/88171c5a92c09be77ca4ab0355fe4df8.png)![](img/171dbf1540ee32afdf955038b6fb94f8.png)![](img/98ce2efea7e5b1606ff8fef0c8161113.png)![](img/1cfdec87bbabfd6e6595b0d51509c05c.png)![](img/e348b74967697e48ca7a97d627162286.png)![](img/df9086426bc1d7607257e4a5fd803a13.png)![](img/d6fac78f5722c2d53207c650fbc7d684.png)![](img/cc3735d9e7371e8a3aa2e16b72afe5a8.png)![](img/2adbc10279b44f02db6e3cd535cd0072.png)![](img/b15b1e9d2819c6c2b549ebab1b9c4eac.png)![](img/d8c08bd3c0fef32a6e2e02a9eec6cd93.png)![](img/02446907dd389d967987eae23cb2d88b.png)![](img/1ff5e1893e29da15b2b0889ccb291c48.png)![](img/16c094da39bc07fed941c355b8ca4508.png)![](img/a6ac9d19e2afcb3295f4b91cb0e33933.png)![](img/367eb4de2cde462846b544004f64dd7e.png)![](img/dbf83891cc8948ea60cef16330fe1e15.png)![](img/3ada7af76f53ed81bb584c20ca528b98.png)![](img/d9290ceeb005a2322f71af625f946b25.png)

Fake people?

# 失败

当机器无法复制人脸时:

![](img/2f6df16fde03753a144f8c4cad1d4e61.png)![](img/7e49d22244b81ce4404c226f361d1010.png)![](img/2b298c1e9531998b5b9e826086d79021.png)

您可以在这里使用他们的演示:

[https://www.kaggle.com/virita/tl-gan-demo/](https://www.kaggle.com/virita/tl-gan-demo/edit)

# 结论

在这个领域有很多工作要做，但是研究人员已经做了很多工作来获得一个新的架构。用例将会增加，因为有大量的可能性。

希望你喜欢这篇文章。很快就要分享笔记本了！

# 参考

**官方知识库:**

[](https://github.com/NVlabs/stylegan) [## NVlabs/stylegan

### 官方 TensorFlow 实现。为 NVlabs/stylegan 开发做贡献，创建一个帐户…

github.com](https://github.com/NVlabs/stylegan) 

**研究论文:**

 [## 一种基于风格的生成对抗网络生成器体系结构

### 我们借鉴风格转移理论，提出了一种新的生成对抗网络生成器结构

arxiv.org](https://arxiv.org/abs/1812.04948) 

PyTorch 实现教程:

 [## DCGAN 教程- PyTorch 教程 1.0.0.dev20190125 文档

### 本教程将通过一个例子对 DCGANs 进行介绍。我们将训练一个生成性的对抗网络…

pytorch.org](https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html) 

**CelebA 数据集:**

 [## 大规模名人面孔属性(CelebA)数据集

### 名人人脸属性数据集(CelebA)是一个大规模的人脸属性数据集，拥有超过 20 万张名人图片…

mmlab.ie.cuhk.edu.hk](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html) 

```
@inproceedings{liu2015faceattributes,
 author = {Ziwei Liu and Ping Luo and Xiaogang Wang and Xiaoou Tang},
 title = {Deep Learning Face Attributes in the Wild},
 booktitle = {Proceedings of International Conference on Computer Vision (ICCV)},
 month = December,
 year = {2015} 
}
```