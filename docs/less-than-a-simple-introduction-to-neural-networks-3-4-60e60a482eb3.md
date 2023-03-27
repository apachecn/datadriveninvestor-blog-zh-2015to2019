# 不到一个简单的神经网络介绍(3/4)

> 原文：<https://medium.datadriveninvestor.com/less-than-a-simple-introduction-to-neural-networks-3-4-60e60a482eb3?source=collection_archive---------9----------------------->

第一部分:[简介](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-1-2-d48c9843102b)

第二部分:[权重和参数](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-2-4-35326721f6af)

第三部分:[优化和反向传播](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-3-4-60e60a482eb3)

第 4 部分:[隐藏层和非线性](https://medium.com/@ahmedbahaaselim/less-than-a-simple-introduction-to-neural-networks-4-4-c11ecbfc6c11?sk=cc093344c56ad045af667454c78b61ab)

![](img/3261cd0d993540a48da243bc3b8162e5.png)

The image was taken from this [post](https://hackernoon.com/gradient-descent-aynk-7cbe95a778da).

# 优化和损失

在隐藏层和非线性之前，我决定先解释优化和损失。如果你在阅读前两部分之前来到这里，那么不要担心。如果你正在跟帖，想要后者，我会尽量在下周之前写出来。如果你能在评论中给我留下反馈，那就太好了。如果你喜欢我解释的方式，但对不同的话题感兴趣，请给我留下评论，我会尽全力报道。

我将遵循同样的优化和损失的简单性。这是我必须理解的最难的事情之一，因为这是复杂的微积分发生的地方。然而，如果您刚刚开始，所有新的 API 或库，如 Tensorflow、Keras、Pytorch 等..让生活变得简单多了。一行代码就完成了优化设置。

 [## Google Sheets -免费在线创建和编辑电子表格。

### 创建一个新的电子表格，同时在你的电脑、手机或平板电脑上与其他人一起编辑。完成工作…

docs.google.com](https://docs.google.com/spreadsheets/d/1Hoi_BNUFgohDaNMhZ5lwTuk1wYonmHC9ZCuEAYRsJts/edit#gid=1648646185&range=C124) 

在[第 1 部分](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-1-2-d48c9843102b)中，我已经解释过，您可以将优化方法视为尝试值的组合来学习函数的权重/参数([第 2 部分](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-2-4-35326721f6af))。然而，你可能已经猜到事实并非如此。

首先，根据它的表现来优化权重。那么我们如何衡量呢？在前面的例子中，我们正在解方程 y = w *x，我们知道 w=2(我们试图学习的体重)，同样在训练 w = 0.5346* *之前，我对 w 进行了随机初始化。*我们为网络提供了训练样本，包括我们事先已经知道的标签或输出。比如我们知道如果 ***x = 2*** 那么 ***y = 4*** 。第一次迭代/时期，网络执行一个称为**前馈**的操作，它只是意味着用我们已有的值计算函数。让我们看看它在第一次迭代中可能是什么样子:

```
Iteration 1:
x = 2.0  # One example of input
w = 0.5346 # The weight the network is learning
y = 4  # The real output of the function that we already given.Feedforward:
ŷ(predicted/calculated)= wx = 2 * 0.5346 = 1.0692 #FeedForward
```

显然答案是不正确的，注意这个 y 是由网络而不是我们的标签预测的，它通常被称为ŷ (y hat)。这就是前馈。自然，两个问题出现了:网络如何知道这是错误的？我们如何弥补呢？

第一个问题很简单，你将**误差**计算为期望输出之间的差值，如果它们不等于零，那么它就是错误的。当然，在现实生活中，有许多方法可以计算误差，这超出了本教程的范围。对于这个级别，我们可以把**损失函数**想象成计算这个误差的函数: ***误差= y-ŷ.***

到目前为止，我们已经:

1.  **前馈计算 *ŷ.***
2.  损失函数来计算误差。

第二个问题稍微复杂一点。这就是可怕的反向传播的由来。我将不得不简单提一下衍生品的作用。这就是我对微分的看法，它是测量比如说两个变量之间的变化率，回答当我们改变*y*时 *x* 改变了多少的问题，把它放到我们的环境中，当我们改变 *w 时**误差**改变了多少？*这就是计算损失函数相对于 ***w*** (权重)的导数的意义。在一个更大的网络中，与我们目前使用的网络相反，网络将有许多权重和层，所有这些都会导致误差。换句话说，我们有许多权重、许多层和一个要计算的误差。当使用反向传播这个词时，简而言之，它的意思是将误差变化率与网络的其余部分进行积分**，但是**它是从末端到前端开始的(从底部到顶部取决于你想如何可视化它)。如果前馈是一个 c = a +b，然后 e = c + d 的序列，那么反向传播将向相反的方向进行，并计算 e = c+d，然后 c = a + b。当然，它不是在做求和，而是在做偏导数，并从网络的末端开始到起点。

最后，当权重通过**梯度下降进行优化时，神奇的事情发生了。**基本上，它采用计算出比率(梯度/导数)并更新(加/减)权重。重量就是这样变化的。重要的是，它一遍又一遍地这样做，以找到所谓的函数最小值，这反过来意味着，找到具有最低误差的权重值。这里的另一个重要参数叫做**学习率。**这是一个非常重要的数字，乘以计算出的更新权重的速率，告诉网络改变权重的快慢。

总而言之，神经网络的主要操作如下:

1.  **前馈计算 *ŷ.***
2.  损失函数来计算误差。
3.  反向传播，以计算当改变权重值时损失的变化率。
4.  梯度下降来更新和优化权重。

有很多很棒的教程详细地解释了它背后的数学原理。如果你不感兴趣，至少要熟悉它的工作原理，因为这是神经网络的核心。如果你能留下一些反馈，如果它需要更多的简化或你有想法。我会编辑帖子。

下一部分，将做一些编码和实现一个两层网络！