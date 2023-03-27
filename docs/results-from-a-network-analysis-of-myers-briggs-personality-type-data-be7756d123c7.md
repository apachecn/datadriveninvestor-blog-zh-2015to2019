# Myers-Briggs 人格类型数据的网络分析结果

> 原文：<https://medium.datadriveninvestor.com/results-from-a-network-analysis-of-myers-briggs-personality-type-data-be7756d123c7?source=collection_archive---------17----------------------->

[![](img/02d5de0c365b99bc90a0b93d60188a30.png)](http://www.track.datadriveninvestor.com/J12U)

# 摘要

在先前对 Myers-Briggs 人格类型在社会中的流行进行分析的基础上，我们扩展了对适应情景和进化路径的分析，以探索这些类型之间出现的路径网络。这概述了变革力量的网络。

# 介绍

这是一系列报告中的第三份。

1.  第一份报告介绍了这种方法，并检查了整个美国人口的 Myers-Briggs 型频率数据。
2.  [的第二份报告](https://medium.com/@Anandavala/what-can-data-science-reveal-about-the-gender-based-structure-of-society-44ed4b606b58)扩展了这一分析，以比较男性和女性的类似数据。

而之前我们探索了与迈尔斯-布里格斯人格类型相关的系统压力、适应情景和进化路径。在这里，我们考察了由于系统压力而在不同类型之间形成的网络。

我们构建的网络中，每个节点代表一种特定的人格类型，每条边代表一种适应情景，在这种情景中，存在着从一种类型转变为另一种类型的系统性压力。注意:如果有保持不变的压力，这不会导致优势。

因此，这个网络提供了一个在类型空间内变革力量的概观。

然后，我们将页面排序算法应用于网络，以识别网络中的汇聚点(吸引子)，这些汇聚点使用不同的颜色和节点大小来突出显示。

每个网络都讲述了一个复杂的故事，然而这里不会试图解释结果，它们只是为了以后的解释而呈现。

所有的网络都是使用来自 statistical Brain 的[数据计算出来的，statistical Brain](https://www.statisticbrain.com/myers-briggs-statistics/)拥有美国人口中 Myers-Briggs 人格类型的单独总数、女性和男性患病率统计数据。

用于进行该分析的 R 代码可以在 github 上找到[，特别是用于创建下图的文件](https://github.com/anandavala/SCA)[Myers-Briggs-data-analysis . R](https://github.com/anandavala/SCA/blob/master/src/myers-briggs-data-analysis.r)。

有三种主要方法来创建和可视化这些网络；最大压力、全管网和微调管网。

# 最大压力网络

为了创建最大压力网络，对于每个节点，我们只考虑压力变化最大的边，而忽略所有其他边。

这给出了类型空间内**最可能的**进化路径图。

# 女性最大压力网络

![](img/830409daf105daf8a4bf489f0f16916d.png)

# 男性最大压力网络

![](img/2954c43d9b442fbd7671a50eaca5c4aa.png)

# 总(两者)最大压力管网

![](img/68a4d73474ca120616d3d0b6415753a6.png)

# 完全网络

完整的网络是通过考虑存在系统性变革压力的每一个边缘而创建的。

这给出了类型空间中所有进化路径的地图。

# 女性全网

![](img/86ad0165a450f0c3b03fb481b1d3ece2.png)

# 男性全网

![](img/f5cfd7dbcdffe425b55222884c7bd2fb.png)

# 全网络总计

![](img/6880a90fd7ce54c27ede4a21b64a4a7b.png)

# 修剪网络

为了创建修剪的网络，我们采用完整的网络并移除边，仅保留那些在特定百分位数内的边，例如前 50%的边权重。

这给出了边权重大于特定阈值的所有进化路径的**图。**

# 最小连通网络

我们考虑的第一个微调网络是最小连通的。为此，我们逐渐修剪网络中的弱边，直到进一步修剪导致孤立(未连接)节点。

## 女性最小连通网络

![](img/b22df4c4d068345b43f67eba0a2888e7.png)

## 男性最小连通网络

![](img/b37705e26b793dd176bb92a3800c32c7.png)

## 全最小连通网络

![](img/f472bd13ec2deba84221900567ad2320.png)

# 子群网络

我们考虑的下一个微调网络是子群。为了创建这个，我们继续从网络中修剪弱边，直到有少量的子组和不太多的孤立(未连接)节点。

## 女性小组网络

![](img/a078f9a67609d67ce46b6def16346430.png)

**女 1 子组**

![](img/bd11e7a263f601fd6e008b25b7ee7b1e.png)

**女性子群 2**

![](img/f2f76645d17107cb3329cc852237990c.png)

## 男性子群体网络

![](img/67676e819a23410ed2db1e5997906b05.png)

**男性亚组 1**

![](img/e2489491c7d8ca9f0f8d0aff38fd55a7.png)

**男性亚组 2**

![](img/d700d4fccc558ad48960619fb09dfd53.png)

## 子群总数网络

![](img/a7786eea62f1cf4716635101c6a82135.png)

**总分组 1**

![](img/3e0725f7ce32c248e2a6738375bfa7a7.png)

**总分组 2**

![](img/380d49fa1311c4fa1a7356ea90c2f4c4.png)

**总分组 3**

![](img/c44c1cc81295fdba5733b5617f6f387b.png)

# 核心网络

我们考虑的下一个微调网络揭示了子群的核心。为了创建这个，我们继续从网络中修剪弱边，直到子组变小并且有许多孤立的(未连接的)节点。

## 女性核心网络

![](img/cd5101f8aae5b2db5b64179ab8433a53.png)

**母芯 1**

![](img/e75f5c1e7521301fb7aab2f9b8bc7194.png)

**女核心 2**

![](img/658b1f8fd6c10a7fc172f436219985aa.png)

**母芯 3**

![](img/4aabc0d2cbcf3d275e23bd1f2af6e91b.png)

## 男性核心网络

![](img/4aea68840b287f8c091e4cb2a693bd80.png)

**公芯 1**

![](img/e73d15d473044e4bd5d75db106d1c49f.png)

**公芯 2**

![](img/bd67227d18c3fbbd99941d1313f10fa3.png)

**公芯 3**

![](img/048cf477afc4e8e407b16f5f296e16b7.png)

## 核心网络总数

![](img/e8feb35a93eb3589ad842f4a224a3614.png)

**总核心 1**

![](img/4dc61a8b7d335effbd6c32a487e203c0.png)

**总核心 2**

![](img/868aab0a1a39f11d71863a2b4fb18f0b.png)

**总核心 3**

![](img/5038993ad93d20eb90f16a0ce0c97b9d.png)

**总核心 4**

![](img/ec2198fcd5b678bfea13d77e75d93c03.png)