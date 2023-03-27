# MAFFT:一种新的多序列比对方法

> 原文：<https://medium.datadriveninvestor.com/mafft-a-novel-method-for-multiple-sequence-alignment-8cbc2710a037?source=collection_archive---------7----------------------->

![](img/33049491987eab61d01890978b3e847b.png)

“white jellyfish lot” by [Tiphaine](https://unsplash.com/@tiphaine?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在生物信息学中，MAFFT 是一个针对氨基酸或核苷酸序列的多序列比对程序。该软件以首字母缩略词“使用快速傅立叶变换的多重比对”命名，这是根据该方法使用的主要计算技术命名的。基本上，MAFFT 的开发目标是与现有方法相比大幅减少 CPU 时间。MAFFT 包括两种新技术。

(I)通过快速傅立叶变换(FFT)快速鉴定同源区域，其中氨基酸序列被转换成由每个氨基酸残基的体积和极性值组成的序列。

(ii)简化的评分系统，其在减少 CPU 时间和增加比对的准确性方面表现良好，甚至对于具有大插入或延伸的序列以及相似长度的远亲序列。

两种不同的试探法，渐进式方法(FFT-NS-2)和迭代细化方法(FFT-NS-i)在 MAFFT 中实现。通过计算机仿真和基准测试，比较了 FFT-NS-2 和 FFTNS-i 的性能；与 CLUSTALW 相比，FFT-NS-2 的 CPU 时间大大减少，但精度相当。当输入序列的数量超过 60 时，FFT-NS-i 比 T-COFFEE 快 100 倍以上，而不牺牲精度。

一旦我们开始实施，主要目标是在多序列比对编程中结合局部和全局算法。为此，使用快速傅立叶变换检测局部同源片段。此外，使用限制性全局动态编程进行成对比对。使用类似于 ClustalW 的渐进算法建立多个比对。在这里，通过将比对分成两部分并如下所示重新比对，多次比对被反复改进。

I .快速傅立叶变换以检测局部保守片段

二。段级动态规划选择“一致”段。

三。将残基固定在每个片段对的中心，并在固定点之间重新对齐。

最后，可以认为这是一种快速多重比对方法，适用于基因组序列的自动化高通量分析。MAFFT 程序中介绍的方法也可用作集成对准工作台等核心组件。

## 参考

Katoh K，库马 K，Toh H，Miyata T:maft 第 5 版:多序列比对准确性的提高。核酸研究 2005，33:511–518。

Katoh K，Misawa K，库马 K，Miyata T:maft:一种基于快速傅立叶变换的快速多序列比对新方法。核酸研究 2002，30:3059–3066。