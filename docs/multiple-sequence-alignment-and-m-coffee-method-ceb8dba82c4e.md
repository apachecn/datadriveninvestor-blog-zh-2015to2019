# 多重序列比对和 M-Coffee 方法

> 原文：<https://medium.datadriveninvestor.com/multiple-sequence-alignment-and-m-coffee-method-ceb8dba82c4e?source=collection_archive---------26----------------------->

![](img/aa45bc73cbb4b26d33d281ab1deaaae9.png)

“woman in white tank top sitting on bed in front of laptop computer” by [Dylan Gillis](https://unsplash.com/@dylandgillis?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

多序列比对(MSA)是指将一组序列中的同源残基一起在柱中进行比对。通常，一列对齐的残基具有相似的三维结构位置。在这种情况下，我们比对多个序列以获得它们之间的最大匹配。它被广泛应用于许多领域，如预测蛋白质结构和识别蛋白质家族的序列模式。

有几种方法可以用于多序列比对。这些方法基本上可以分为三个部分，即“渐进对齐方法”、“迭代细化方法”和“局部对齐方法”。在渐进式比对方法中，它在引导树的帮助下匹配密切相关的序列。在迭代优化方法中，通过多次重建尝试将找到最佳的排列。迭代优化方法的主要目标是克服渐进对准方法中出现的问题。在局部比对方法中，它更注重通过轮廓、块和模式来比对序列。

M-Coffee 是一个多序列比对包，它是 T-Coffee 的扩展，通过将几个单独方法的输出组合成一个 MSA，使用一致性来估计共有比对。M-Coffee 的特殊性在于，它不是自己计算多序列比对，而是使用其他包来计算比对。然后，它使用 T-Coffee 将所有这些比对组合成一个唯一的最终比对。实际上，这意味着如果用户使用几个包来生成他们的比对，他们可以组合这些比对，而不是选择其中的一个。在实践中，显示出组合的比对平均来说比初始比对更好。此外，它们一致的区域往往是正确对齐的。至于硬件要求，M-Coffee 对 CPU 的要求与最初的 T-Coffee 相似，给出了一组预先计算的 MSA。

由于 M-Coffee 是 MSA 的元方法，研究人员使用了 15 种其他 MSA 算法来进行初始 MSA。ClustalW、T-Coffee、ProbCons、PCMA、Muscle、Dialign2、Dialign-T、MAFFT、FFT-NS1、FFT-NS2、FFT-NSI、F-INSI、G-INSI 和 POA 是初始阶段使用的 MSA。在初始阶段之后，计算方法树以直观地显示各种方法之间的相似程度。通过将 UPGMA 算法应用于距离矩阵来计算该树，并且该树还用于计算方法权重。生成方法树后，通过将每对比对残基分配成对比对权重来生成文库。然后 T-Coffee 试图找到一个权重和最大的排列。使用四种不同的方案来为每种比对方法生成权重，其中两种方案是基于树的，并且是基于前面描述的方法树来计算的。四种不同的加权方案是，

●方差/协方差(VarCov)

●阿尔楚尔·卡里略·李普曼

●汤普森·希金斯·吉布森(THG)

●精确度(ACC)

使用这些加权方案，MSA 更有效地与最终 MSA 对齐。如论文中所述，M-Coffee 在三个主要参考数据集上优于所有单独的方法:HOMSTRAD、Prefab 和 Balibase。它还指出，在逐案的基础上，M-Coffee 提供最佳比对的可能性是任何单独方法的两倍。

## 参考

Wallace IM，O'Sullivan O，Higgins DG，Notredame C，“M-Coffee:将多种序列比对方法与 T-Coffee 结合”，2006 年，核酸研究 34:1692–1699。