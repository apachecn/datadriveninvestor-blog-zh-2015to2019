# 变分算法和论文得出的结论

> 原文：<https://medium.datadriveninvestor.com/variational-algorithms-and-conclusions-obtained-from-the-thesis-29b5a744d687?source=collection_archive---------3----------------------->

![](img/db3628077360a14f1bf493e71e00423f.png)

Photo by [Lanju Fotografie](https://unsplash.com/@lanju_fotografie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这是我关于量子机器学习的期末论文系列文章的最后一篇。我们已经讨论了量子计算和机器学习的广泛主题。你可以查看之前进入我的个人资料的文章，它们是按顺序排列的。

在这最后一篇文章中，我们将看到什么是**变分算法**，并且我们将给出一些在整个工作中得到的最终想法和结论。

# 变分算法

量子计算是一门学科，在今天的技术下，很难研究。这主要是因为我们缺乏开发完美量子计算机的技术。换句话说，我们现在的量子计算机并不完美。从这个意义上说，我们不能按照自己希望的方式执行量子算法。出于这个原因，自 2012 年以来，研究人员一直在开发被称为**变分算法**的混合量子经典算法。

这种算法寻求使用近期量子计算机以及经典计算机来解决复杂问题。已经开发了许多算法，并且目前正在开发中。

现在有许多变分算法:

*   变分量子本征解算器(VQE)
*   量子绝热优化算法
*   量子神经网络(QNN)
*   量子支持向量机
*   变分量子分类器(VQC)
*   量子氮化镓(QGAN)

这仅举几个例子。所有这些都可以在诸如 Qiskit (IBM) [1]、草莓地(Xanadu) [2]或 Penny Lane (Xanadu) [3]等图书馆中找到。

这些库使用量子优化技术来执行机器学习，或者换句话说，使用机器学习技术来学习量子状态或模式。

在以后的文章中，我们将使用上面提到的库探索这些算法的一些应用。

# 论文的最后结论

在最后一节中，我们将解释在整个工作中得到的结论。接下来，将讨论未来的观点和对该主题的简要个人意见。

这项工作的主要目标是看看人工智能和量子计算是否可以一起工作。这个目标的答案是肯定的。更重要的是，它是物理学、计算机科学和数学中最有前途的研究分支之一。量子机器学习与物理学有直接联系，因为它基于量子计算，这使得它非常适合模拟量子系统。

如今，该领域的研究由私营部门主导，其中谷歌、IBM 和 D-Wave Systems 等公司最为突出。我们还发现未来的合作，如大众汽车和谷歌的合作，以便在交通优化中实现量子计算[4]。

考虑到整个工作中所说的一切，我们可以得出结论，目前量子机器学习中有两个主要的工作分支。第一种是用量子理论的概率描述来描述随机过程。这种方法用于玻尔兹曼机器情况下的概率采样(见[文章](https://medium.com/@agus.bignu97/application-of-quantum-annealing-to-training-deep-neural-networks-6e91ccf201ec))，用于必须区分量子态情况下的贝叶斯定律(见[文章](https://medium.com/@agus.bignu97/bayesian-network-structure-learning-using-quantum-annealing-1de6c849e7fd))，以及用于量子强化学习的马尔可夫过程(见[文章](https://medium.com/datadriveninvestor/reinforcement-learning-using-quantum-boltzmann-machines-7949855d3dd))。第二，许多研究人员试图找到量子算法来取代经典的机器学习算法，以解决特定的问题。它们表明，就要解决的问题的复杂性而言，它是可以改进的。对于量子 SVM 与经典算法(参见[文章](https://medium.com/datadriveninvestor/implementation-of-quantum-svm-using-the-qiskit-library-9eabb6a6270a))这样的算法来说，量子计算机的计算能力有助于我们解决复杂的优化计算。

目前，这种方法与上面提到的两种方法没有什么不同。研究人员试图利用量子计算机，因为它们比经典计算机具有更强的计算能力。这是因为叠加和量子理论的概率性质，使得更容易面对概率采样，或者如前所述，描述和模拟随机过程。

尽管到目前为止提到的优点，我们可以找到阻碍这一学科进程的缺点。

虽然量子算法在数据处理方面提供了巨大的优势，但在阅读它们的时候却很难做到。这意味着，在某些情况下，读取数据的成本可能会主导量子算法的成本。想想大数据时代，如果我们想用量子机器学习来完成这方面的任务，这是短期内必须解决的事情。

在监督学习领域，模型从输出数据中学习。以量子计算为例，学习一些量子算法的完全解作为一个比特串，需要学习指数数量的比特，这使得量子机器学习的一些应用不可行。通过对输出数据进行统计并从中学习，可以在短期内解决这个问题。然而，这是必须努力的事情。

另一方面，这一学科所需要的硬件是相当创新的，并且是不断变化和研究的。如今，这个话题是量子机器学习研究面临的主要障碍之一。

展望未来，预计其增长不会停止。此外，将发展新的研究分支，以便应用于工业。一种可能的前进方式是研究量子数据的应用，而不是经典数据。这将让我们更好地理解量子计算机。这也将产生一个良性循环，就像经典计算中发生的那样，使他们在技术方面的进步更快。与此同时，开发高效的硬件也是一条必须努力的道路，这将需要大量的研究

最后，我将提一下我个人对这个问题的想法。为了理解这个学科在未来的重要性，可以做一个类比。量子机器学习和量子计算可以比作计算机科学和经典计算在 40 年代和 50 年代的情况。从那时起，它开始蓬勃发展，今天使用的计算机所依赖的许多技术和理论基础都得以实现。所以还有很多工作要做。

# 结论

总之，我要感谢所有关注这一系列文章的人。如果你有任何要求或问题，你可以给我发邮件到 agus.bignu97@gmail.com。

我会继续张贴关于 QML:教程，不同技术和算法的解释。敬请期待！

你可以在 LinkedIn 上找到我:[https://www.linkedin.com/in/agustin-bignu-946694132/](https://www.linkedin.com/in/agustin-bignu-946694132/)

还有推特:【https://twitter.com/agusbignu 

保持下去！

# 参考

[1]Qiskit.org

[2][https://strawberryfields . readthedocs . io/en/stable/index . html](https://strawberryfields.readthedocs.io/en/stable/index.html)

[3][https://pennylane.readthedocs.io/en/latest/](https://pennylane.readthedocs.io/en/latest/)

[4]大众，谷歌 Kooperation。2017 年 11 月。