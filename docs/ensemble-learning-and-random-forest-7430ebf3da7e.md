# 集成学习和随机森林

> 原文：<https://medium.datadriveninvestor.com/ensemble-learning-and-random-forest-7430ebf3da7e?source=collection_archive---------5----------------------->

[![](img/7d2912091cd26a584b4eb9263ee51923.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/aa3746611455b2889dea927700fd0eac.png)

Photo by [Dennis Kummer](https://unsplash.com/@dekubaum?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*这是一种自适应学习方法，将几种算法结合起来，以获得比单个算法更好的结果。*

## 系综方法的主要格言如下:

1.  *减少方差(套袋)。*
2.  *降低偏置(升压)*
3.  *改善预测(堆叠)*

## 集合方法可以以两种方式应用:

1.  ***:在这种方法中，利用了基础学习者的依赖性。这包括对不重要的例子进行评估和重新加权。例如 Adaboost。***
2.  ****并行:** *在这种方法中，利用了基础学习者的独立性。这包括通过简单地平均基础学习者的输出来进行评估。例如随机森林。***

## **该集合可以有两种类型:**

1.  ****同质集成:** *在这里，我们有单基学习算法，比如随机森林，它只使用决策树算法*。**
2.  ****异构集成:** *在此，我们有不同的基估计器算法。***

## **集成学习中使用的技术:**

1.  ****Bagging :** *Bagging 代表引导聚集。减少估计值方差的一种方法是将多个估计值平均在一起。为了汇总基础学习者的输出，bagging 使用*【分类投票】*和*回归平均*。***
2.  ****Boosting:****Boosting 是指能够将弱学习者转化为强学习者的一族算法。然后，通过加权多数投票(分类)或加权和(回归)将这些预测组合起来，以产生最终预测。****
3.  *****堆叠:** *堆叠是一种集成学习技术，它通过元分类器或元回归来组合多个分类或回归模型。基于完整的训练集来训练基础级模型，然后在基础级模型的输出上训练元模型作为特征。****

# ***随机森林算法:***

***随机森林算法是一种监督学习算法。森林里的树的数量和它能得到的结果有直接的关系。它使用许多决策树，在回归的情况下通过平均来预测更准确的结果，在分类的情况下通过投票来预测。***

## ***随机森林算法的工作原理:***

1.  ***从总共 **m** 个特征中随机选择 **K** 个特征，其中**K<m*****
2.  ***在“ **K** ”特征中，使用最佳分割点计算节点“ **d*****
3.  ***使用**最佳分割**将节点分割成 n 个**节点*****
4.  ***重复 1 **到 3** 步骤，直到达到“l”个节点***
5.  ***重复步骤 1 **到 4**n 次，创建**“n”棵树**，构建森林***

***在下一阶段，随着随机森林分类器的创建，我们将进行预测。***

1.  ***采用**测试特性**并使用每个随机创建的决策树的规则来预测结果并存储预测结果(目标)***
2.  ***计算每个预测目标的**票数*****
3.  ***将**高票**预测目标视为来自随机森林算法的**最终预测*****

## ***随机森林算法的优势:***

***与其他分类技术相比，有三个优点:***

1.  ***对于分类问题的应用，随机森林算法将避免过拟合问题。***
2.  ***对于分类和回归任务，可以使用相同的随机森林算法。***
3.  ***随机森林算法可用于从训练数据集中识别最重要的特征，换句话说，特征工程。***