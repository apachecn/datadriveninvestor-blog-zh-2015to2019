# 少于神经网络的简单介绍(1/4)

> 原文：<https://medium.datadriveninvestor.com/less-than-a-simple-introduction-to-neural-networks-1-2-d48c9843102b?source=collection_archive---------14----------------------->

![](img/f534e6d71d5cbde0b2f896c887f63f8a.png)

第一部分:[简介](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-1-2-d48c9843102b)

第二部分:[权重和参数](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-2-4-35326721f6af)

第三部分:[优化和反向传播](https://medium.com/datadriveninvestor/less-than-a-simple-introduction-to-neural-networks-3-4-60e60a482eb3)

第 4 部分:[隐藏层和非线性](https://medium.com/@ahmedbahaaselim/less-than-a-simple-introduction-to-neural-networks-4-4-c11ecbfc6c11?sk=cc093344c56ad045af667454c78b61ab)

> 在我的一些学生要求我帮助理解神经网络之后，我已经决定开始这个系列。然而，他们中的大多数人没有很强或足够的数学技能。就像我开始的时候一样，我现在正在攻读机器学习的博士学位，这就是我如何分解它供自己学习的。所以这是为那些低于平均水平的人和完全的初学者准备的，他们正试图弄清楚这一切到底是为了什么。我也将包括关键字，你可以谷歌找到更详细的解释等。我将使用 Python 和 Pytorch，因为它很可爱，很容易在网络内部看到。格式将是一些在第一部分的思想介绍和第二部分的例子编码。你对基础知识了解得越多，打下的基础越扎实，将来使用任何神经网络就越容易。简单地说，轮子不是被重新发明，而是被改进。
> 
> 如果您对我的解释有任何问题，页面顶部有一个神奇的 x，可以让您的所有问题消失。

让我们先说神经网络的想法实际上很简单，它背后的公式并不简单。然而，在我看来，公式是分享想法的许多语言之一，如果你用不同的语言理解这个想法，你最终可以翻译它。

[](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) [## DDI 编辑推荐:5 本让你从新手变成专家的机器学习书籍|数据驱动…

### 机器学习行业的蓬勃发展重新引起了人们对人工智能的兴趣

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) 

关于神经网络，首先要理解的是，它只是另一个接受输入或一组输入并给出输出的函数。幽默我一下，一个函数可以为我们所有人*f*(*x*)=*2+x*。我们可以把函数推得更远一点，说*f*(*x*)=*a*+*x*，其中*‘a’*是一个常数，就像它可以是任何数字一样。现在用最小代数，a 的值是多少

*a* + *x* = 10 给定 *x = 2？*

如果我会数数，我会马上说出 *a* = 8，如果我有点慢，我会从 1 开始一个接一个地把数字加到 *x* 上，看看哪个数字会给出我想要的结果。如果我懂一点代数，我会通过 *a = 10-x 得到它。*我必须在这里指出:第一，有许多方法可以计算我们称之为**的参数**。第二是给出什么是参数的概念，在这种情况下，我们需要计算一个参数*‘a’*。碰巧最常见的方法，也是迄今为止被证明效果最好的方法叫做**梯度下降**，我不会在本文中介绍它(如果有人发现这个有用的话，也许以后会介绍)。

简单来说，训练神经网络的目的是学习一组参数**和**，称为**权重**。因此，我们可以有更多的 a、b、c、d、e、f…z，而不是只有一个。所以你能看出问题所在，对吗？很难跟踪所有这些变量和参数，所以为什么不使用数组，因为我们知道一些编程。这就对了，我们可以有一个列表或者一维数组或者任何你想叫它的东西，包含我们所有的权重[ *a，b，c，d，e，f，…z* )或者说一些机器学习的行话[ *w1，w2，w3，w4，w5，w6，…wn*](*‘权重你看 w’)。数学家们也称之为矢量。请记住，我们仍然在使用类似简单函数的东西:*

*f(x)= ax+bx+CX*≡*f(x)= w1x+w2x+w3x。*

先不要担心网络是如何学习这些值的，现在只要想想我们有一个算法来尝试这些参数的所有可能组合，直到我们得到我们想要的数字。我们将这个虚构的算法称为**优化**。另一个想法是，当我们有两个列表在彼此之上时会发生什么？我们得到一个 2d 数组，数学术语是一个**矩阵。如果你还不想学习线性代数，就把矩阵想象成一个表格。如果矩阵形状是二维的，它通常表现为 2×2 或 2×3。左边的数字是行，右边的数字是列。矩阵是堆叠在一起的向量(向量的向量，列表的列表)。这就是我们第二部分需要的所有信息。**

**总而言之:**

1.  神经网络是在训练阶段学习/发现一些(参数、权重、变量)值的大功能。
2.  学习这些参数的方法将把它称为优化，而不知道它做什么或它是什么。
3.  我们将保持我们的权重在一个向量或矩阵中。

**下一个:**

在下一节中，我将真正探讨权重以及它们如何与输入相乘，以及它们代表什么。下一节将包含带有代码和图形的示例。我不会马上建立你的第一个神经网络，因为外面有很多很棒的教程，所以重点是看看在引擎盖下发生了什么。