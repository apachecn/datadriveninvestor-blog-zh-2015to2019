# 人工智能如何检测儿童绘画中的情绪

> 原文：<https://medium.datadriveninvestor.com/how-artificial-intelligence-can-detect-emotions-in-childrens-drawings-4359cf51ab3d?source=collection_archive---------2----------------------->

[![](img/edd1f54e160a4b5c3832ce0faba409e3.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/6d4f5fee5efd6c3ba7db592353d57ef5.png)

# 孩子们的绘画是他们感受和体验的窗口。

人类找到不同的方式来表达他们的感受。当我们很小的时候，我们不能通过文字和声音进行很好的交流，因为我们还在学习写作和说话，所以绘画是一种特殊的资源，可以表达我们的情感以及我们与家庭甚至世界上其他事物的关系。

绘画让我们对孩子们的恐惧、快乐、噩梦、经历以及个性有了很好的了解。一幅画包含了关于它们的每一个关键信息。

这不是一个了解孩子的明确方法，让我们接受它，有时，它没有任何意义，它只是一个获得乐趣的产品，但有时绘画可以揭示他们在那一刻的感受和想法。

[](https://www.datadriveninvestor.com/2019/02/19/artificial-intelligence-trends-to-watch-this-year/) [## 今年值得关注的人工智能趋势——数据驱动的投资者

### 预计 2019 年人工智能将取得广泛的重大进展。从谷歌搜索到处理复杂的工作，如…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/19/artificial-intelligence-trends-to-watch-this-year/) 

# 通过绘画察觉孩子的情绪

通过儿童的绘画来检测他们的情绪是一项古老的技术，心理学专业人士经常使用。

## 家庭绘画测验

![](img/d3b95272abd5f208e37ad9c01ee72c8c.png)

当你小的时候，你可能是学校里这些普通测试的一部分。治疗师使用包括绘画在内的不同技术来评估儿童的情绪和成熟度。其中最受欢迎的是**家庭绘画测试。**家庭绘画测试让我们了解孩子如何看待他们最亲密的关系。这是一个简单的方法来理解关系和沟通的质量，以及儿童如何基于家庭关系构建他们的现实。

这项技术已经存在了 60 多年。**精神病学家 Miles Porot** 在 1951 年创造了这个方法，现在它是用来评估 5 到 16 岁儿童性格最常用的技术之一。还有其他类似的技术，如**树测试**。

# 绘画技术中的人工智能

在阅读了这个有趣的工具后，我想到了这个伟大的想法，将旧技术和人工智能结合起来，检测不同的儿童情绪，从每个类别中提取有代表性的特征，这样我们就可以解码儿童的绘画，并分配一种特定的情绪。

到目前为止，我认为这是人工智能的一大用途。我可以想象这个 AI 模型如何帮助学校的心理学家和治疗师。我并不认为这可以取代每天所做的艰苦工作，但它确实很有帮助。计算机视觉模型可以加快工作速度，并有助于诊断儿童。

# 创建带标签的数据集

![](img/d37efb1cb8c74f05ea425153fc35a21d.png)

我找不到关于这个想法的论文或数据集来开始这个实验，所以我开始创建一个新的数据集。我从不同的渠道了解到如何根据颜色、形状、位置、风格和其他不同方面来解读儿童绘画。我不是心理学或临床医学家，但我发现了关于这些画及其潜力的非常有趣的信息。

我必须说，我在互联网上寻找绘画的经历真的令人心碎，也是一次大开眼界的经历。从不同的网站上看到真实的儿童绘画，我感到震惊。他们中的大多数都是艺术治疗项目的一部分，这些项目是为了治愈那些患有创伤后应激障碍(T2，PTSD，T3)的儿童。我发现的其他类型的画是关于虐待儿童和家庭暴力的。我还找到了父母离异的孩子的画。

因此，在收集了大量的儿童绘画后，下一个任务是给数据集贴标签。这是我在网上找到的帮助我标记数据集的东西:

## 绘画类型取决于性别(形状和颜色)

![](img/4906e0a12865ddfa20e12067c1044787.png)

我们可以发现女孩和男孩的画之间的差异。的确，女孩更喜欢使用**粉色**和**柔和的颜色**，而男孩更喜欢像蓝色这样的冷色调**。另外**的形状**也各不相同。女孩通常会画圆形的形状，如花朵、心形，而男孩会画角度、方框、直线以及汽车、公共汽车和火箭。他们画一些代表他们性别的东西是很常见的。**

![](img/61cbcbd930eea0911de429fac16abce3.png)

## 让我们多谈谈颜色

他们在绘画中使用的颜色背后有更多的东西:

先说**黑紫**。这些颜色暗示着主导地位，可能会受到对 T21 要求相对较高的孩子的青睐。蓝色很受有爱心并喜欢陪伴的孩子的欢迎。

红色代表兴奋，是不想错过任何事情的孩子们常用的颜色。

**粉色，**女生最喜欢的颜色表示需要**爱和欣赏**。**绿色**是享受**与众不同**的人的颜色。大多数情况下，对于那些有艺术天赋的孩子来说。**黄色**是一种**快乐**的颜色，象征着**智慧和阳光的天性。**

## 风格决定个性

孩子们画画的方式也揭示了他们性格的重要信息。

**详细阐述的图画**揭示了一个感到需要**非常努力的孩子。****生产线的质量**也非常重要。一个用浅色、摇摆不定的虚线画出的人物，展示了一个犹豫不决、缺乏安全感的孩子，他似乎一边走一边思考。相比之下，**大胆、连续、自由绘制的线条**表达了**自信和安全感。**你可能听说过这个，但是**没有手臂**有时被解释为表示**胆怯，这是没有攻击性的孩子**的标志，而如果这个人物是自画像，夸大**手的大小被视为攻击性倾向的象征**。同样地，**小脚被视为不安全的标志，字面意思是不稳定的基础。**

## 绘图的位置

我在网上也发现，在图纸中位置很重要。左侧的通常与**过去和养育**联系在一起，也与**母亲**联系在一起。**右侧**相反，与**未来有关，需要与**沟通，也与**父亲沟通。**

**尺寸**也很重要，一个孩子把一张**大小合适的图画放在纸上被认为是平衡的和安全的，**而**小的数字**画在纸的下边缘或附近，或者画在角落里则表示不安全。

## **形状呢？**

一个**冲动的孩子**可能会画出**大人物，没有脖子，四肢不对称。**一个**焦虑的孩子**会做**云，雨，飞鸟，没有眼睛的数字**。一个**害羞的孩子**通常会画**短小的人物，没有鼻子或嘴巴，微小的人物和手臂靠近身体**像是藏了什么东西在后面。一个**愤怒的孩子**会做**大手大牙，长臂斗鸡眼**。一个**缺乏安全感的孩子**类似于害羞的孩子，会画出**奇形怪状的人物，小脑袋，没有手和倾斜的人物。**

# 创建类

我发现分类有点困难。一个孩子可以表达许多情感。所以，我所做的是关注 3 个类别:

*   **幸福**
*   **焦虑和抑郁**
*   **愤怒与暴力**

我这样做的原因是因为一幅画可以表达许多感情，有些感情是相似的，所以我把它们合并在同一个类别中。当我看到关于战争的图画时，我看到了暴力、愤怒和悲伤。关于家庭暴力和孩子经历父母离婚的绘画表达了焦虑和抑郁。

所以，我很容易将愤怒和暴力结合在一起，画出关于战争的图画，孩子们画出愤怒的脸或表现暴力的人物。

![](img/83aa300c885e2c03e32e83c9014345f0.png)

**焦虑和抑郁**类包含画有哭泣**脸的孩子**和有**雨和云的风景**的图画。

![](img/4c508cddb2c28120a3989415b38e93a3.png)

快乐班是最简单的一门，我找到了许多画有宠物的快乐家庭的图画，有太阳、鲜花和彩虹的彩色风景。

![](img/ea5c328e207af21010ec40d22d17532f.png)

# PyTorch 模型

使用了一个预先训练好的模型和 PyTorch。我将数据集 80:20 分开，分别用于训练和验证。经过一段时间，并调整模型，使其与我制作的数据集配合良好，结果很好，达到了 87%的准确率！

请参见下面的结果:

![](img/b9a74d29af9e366320abc2bfad52f0c2.png)![](img/750433dc24b320f077ed3148f1fa8808.png)

This is a prove that **Anger & Violence** and **Anxiety & Depression** can be found in the same drawing. Sometimes, we experiment all those feelings in one situation.

![](img/51d9d0e3bed48f0733c09f1e376e85f0.png)![](img/51bcbe084f413df5bf29d8f740643a5e.png)![](img/c619bc48b6d529660e452d0b47301ca6.png)![](img/6b941aca4566b5f88d5be241c20c6128.png)

Sad faces, a feature associated with **Anxiety and Depression** class

![](img/d95d026017c77cffa065a5e5b1807322.png)

An eye crying, feature also associated with **Anxiety and Depression** class

![](img/67beb7bb33edc48a0e47965cae1a2b5e.png)

War and dramatic colors: red and orange for fire and black for bombs and explosions. Features associated with **Anger and Violence** class

![](img/59aac7492e10ca3c0fa95b7605d120f4.png)

More war

![](img/4213655109ba37b5d93e7209cc11d680.png)

War. This drawing ma be associating colors with anxiety and Depression class

![](img/3f5284a72d0ead9e79654181daadb266.png)

War

![](img/a2750aebd8209d6aaac3d44f32352e68.png)

war

![](img/3b61f5d1cc3c5e2bd73de3b22490128c.png)

Happy family and sunny day. Colorful drawing associated with **Happiness** class

![](img/06888b67ead09894a2f5d992e5e2b6ae.png)

Colorful drawing. Almost a 100% sure it’s in **Happiness** class

# 结论

*   绘画表达的东西超出了我们的想象
*   如果能把这个技术分享给一些基金会，那就太神奇了。一旦我有了更好的模型和更大的数据集，我可能会在将来考虑这个问题。
*   拥有一种高效的人工智能方法来检测儿童的情绪是帮助心理学专业人士的一种方式。让我们不要忘记有更多的工具一起使用，以提供更好的诊断准确性
*   我可以很容易地看到更多的类别，但这是一个长期的工作要做，并为同一目的收集更多的图纸
*   让专业人士来查看和标记数据肯定会改善这个项目！

# 参考

**学习给儿童画打码**

[](https://novakdjokovicfoundation.org/learn-to-decode-childrens-drawings/) [## 学会解码儿童画|诺瓦克·德约科维奇基金会

### 学习如何解码孩子的图画，更好地了解你的孩子和他的内在性格。儿童的…

novakdjokovicfoundation.org](https://novakdjokovicfoundation.org/learn-to-decode-childrens-drawings/) 

**家庭绘画测验**

[](https://exploringyourmind.com/family-drawing-test/) [## 家庭绘画测试——探索你的思维

### 家庭绘画测试是最著名的儿童情感评估之一。它让我们了解…

exploringyourmind.com](https://exploringyourmind.com/family-drawing-test/) 

书籍通过孩子的眼睛讲述战争故事

[](https://www.bbc.com/news/uk-england-coventry-warwickshire-46461154) [## 书籍通过孩子的眼睛讲述战争故事

### 年轻的难民在绘画中描绘了生活在战区和背井离乡的现实。直到…

www.bbc.com](https://www.bbc.com/news/uk-england-coventry-warwickshire-46461154) 

叙利亚儿童在令人心碎的图画中展示他们的恐惧和创伤

[](https://theirworld.org/news/syrian-children-reveal-their-fears-and-traumas-in-heartbreaking-drawings) [## 叙利亚儿童在令人心碎的绘画中揭示了他们的恐惧和创伤

### 让一个孩子画出他们害怕的东西，你可能会得到愤怒的狗、蜘蛛或黑暗。天空可能充满了…

theirworld.org](https://theirworld.org/news/syrian-children-reveal-their-fears-and-traumas-in-heartbreaking-drawings)