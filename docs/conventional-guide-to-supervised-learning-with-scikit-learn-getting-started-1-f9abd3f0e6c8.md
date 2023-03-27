# scikit-learn 监督学习的常规指南—入门(1)

> 原文：<https://medium.datadriveninvestor.com/conventional-guide-to-supervised-learning-with-scikit-learn-getting-started-1-f9abd3f0e6c8?source=collection_archive---------14----------------------->

![](img/7214f8cfdab31ae9becf82633be0a542.png)

这是 scikit-learn 指导监督学习的 92 篇系列文章中的第一篇，撰写这篇文章的目的是为了熟练地实现算法，并能够解释算法背后的算法逻辑。

# 监督学习

在监督学习中，每个例子是一个由一个**输入(训练)**和一个**期望输出值(标签)组成的*对*。**

一个**监督学习算法**分析训练数据并产生一个推断函数，该函数可用于映射新的示例。

以下是所有系列文章的链接——scikit-learn 监督学习的常规指南。

注意:从 2018 年 10 月 6 日开始，每周会有一篇新文章发表

1.[入门(本文)](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-getting-started-1-f9abd3f0e6c8)

2.[普通最小二乘法—广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-ordinary-least-squares-generalized-29cbf1648a25)

3.[岭回归-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-ridge-regression-generalized-linear-a97a4202ac43)

4. [Lasso-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-lasso-generalized-linear-models-4-4931217c0251)

5.[多任务套索-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-multi-task-lasso-generalized-linear-37af44f0e38e)

6.[弹性网络-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-elastic-net-generalized-linear-80ecc2574052)

7.[多任务弹性网络广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-multi-task-elastic-net-generalized-63dba8009183)

8.[最小角度回归-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-least-angle-regression-generalized-11b4ce2dec89)

9.[拉斯拉索-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-lars-lasso-generalized-linear-models-fccd556c984a)

10.[正交匹配追踪(OMP)-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-orthogonal-matching-pursuit-omp-d3de1ffef841)

11.[贝叶斯回归——广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-bayesian-regression-generalized-a3f1653c7286)

12.[逻辑回归——广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-logistic-regression-generalized-e9783c414588)

13.[随机梯度下降— SGD-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-stochastic-gradient-descent-sgd-14068f286a7f)

14.[感知器-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-perceptron-generalized-linear-2e3c85a8940a)

15.[被动攻击算法-广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-passive-aggressive-algorithms-ebf800f7fbcb)

16.[稳健回归:异常值和建模误差——广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-robustness-regression-outliers-and-e122c6d77b84)

17.[多项式回归:用基函数扩展线性模型——广义线性模型](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-polynomial-regression-extending-d835c543ba94)

18.[利用线性判别分析进行降维——线性和二次判别分析](https://medium.com/datadriveninvestor/conventional-guide-to-supervised-learning-with-scikit-learn-dimensionality-reduction-using-linear-109a3f071112)

19.[LDA 和 QDA 分类器的数学公式——线性和二次判别分析](https://medium.com/datadriveninvestor/conventional-guide-to-supervised-learning-with-scikit-learn-mathematical-formulation-of-the-lda-8b64cfd93c0e)

20.[LDA 降维的数学公式——线性和二次判别分析](https://medium.com/@venali/conventional-guide-to-supervised-learning-with-scikit-learn-mathematical-formulation-of-lda-9b5ca7c01710)

21.[收缩率——线性和二次判别分析](https://medium.com/@venali/this-is-the-twenty-first-part-of-a-92-part-series-of-conventional-guide-to-supervised-learning-c5f16338c28d)

22.[估计算法——线性和二次判别分析](https://medium.com/@venali/estimation-algorithms-linear-and-quadratic-discriminant-analysis-22-58dfe14e595b)

23.[仁岭回归](https://medium.com/datadriveninvestor/conventional-guide-to-supervised-learning-with-scikit-learn-kernel-ridge-regression-23-d6a9f64e9c6f)

24.分类-支持向量机(即将推出)

25.回归-支持向量机(即将推出)

26.密度估计，新奇检测-支持向量机(即将推出)

27.复杂性-支持向量机(即将推出)

28.实用技巧-支持向量机(即将推出)

29.核函数-支持向量机(即将推出)

30.数学公式-支持向量机(即将推出)

31.实施细节-支持向量机(即将推出)

32.分类—随机梯度下降(即将推出)

33.回归-随机梯度下降(即将推出)

34.稀疏数据的随机梯度下降(即将推出)

35.复杂性-随机梯度下降(即将推出)

36.停止标准-随机梯度下降(即将推出)

37.实际使用技巧-随机梯度下降(即将推出)

38.数学公式-随机梯度下降(即将推出)

39.实施细节-随机梯度下降(即将推出)

40.无人监管的最近邻居(即将推出)

41.最近邻分类(即将推出)

42.最近邻回归(即将推出)

43.最近邻算法(即将推出)

44.最近质心分类器(即将推出)

45.高斯过程回归(GPR)(即将推出)

46.GPR 示例(即将推出)

47.高斯过程分类(GPC)(即将推出)

48.GPC 示例(即将推出)

49.高斯过程的内核(即将推出)

50.交叉分解(即将推出)

51.高斯朴素贝叶斯-朴素贝叶斯(即将推出)

52.多项式朴素贝叶斯-朴素贝叶斯(即将推出)

53.补充朴素贝叶斯-朴素贝叶斯(即将推出)

54.伯努利朴素贝叶斯—朴素贝叶斯(即将推出)

55.核外朴素贝叶斯模型拟合(即将推出)

56.分类-决策树(即将推出)

57.回归-决策树(即将推出)

58.多输出问题-决策树(即将推出)

59.复杂性-决策树(即将推出)

60.实用技巧-决策树(即将推出)

61.树算法:ID3、C4.5、C5.0 和 CART-决策树(即将推出)

62.数学公式—决策树(即将推出)

63.Bagging 元估计器-集成方法(即将推出)

64.随机树木的森林-综合方法(即将推出)

65.AdaBoost-集成方法(即将推出)

66.梯度树推进-集成方法(即将推出)

67.投票分类器—集成方法(即将推出)

68.多标签分类格式-多类和多标签算法(即将推出)

69.一对多类和多标签算法(即将推出)

70.一对一多类和多标签算法(即将推出)

71.纠错输出码-多类和多标签算法(即将推出)

72.多输出回归-多类和多标签算法(即将推出)

73.多输出分类-多类和多标签算法(即将推出)

74.分类器链-多类和多标签算法(即将推出)

75.回归子链—多类和多标签算法(即将推出)

76.移除低方差要素-要素选择(即将推出)

77.单变量特征选择-特征选择(即将推出)

78.递归特征消除-特征选择(即将推出)

79.使用 SelectFromModel 进行功能选择-功能选择(即将推出)

80.作为管道一部分的功能选择-功能选择(即将推出)

81.标签传播—半监督(即将推出)

82.等渗回归(即将推出)

83.概率校准(即将推出)

84.多层感知器—神经网络模型(监督)(即将推出)

85.分类-神经网络模型(监督)(即将推出)

86.回归-神经网络模型(监督)(即将推出)

87.正则化-神经网络模型(监督)(即将推出)

88.算法-神经网络模型(监督)(即将推出)

89.复杂性-神经网络模型(监督)(即将推出)

90.数学公式-神经网络模型(监督)(即将推出)

91.实际使用技巧-神经网络模型(监督)(即将推出)

92.通过热启动-神经网络模型实现更多控制(监督)(即将推出)

# 信用

所有学分归入 Scikit-learn 文档，所有参考资料均符合官方用户指南。

也感谢我的朋友，他相信“对我来说，成功就是我创造了足够的影响力，让世界变得更美好”，这激励我从零开始，以便在某个时刻创造不同。

# 关于作者

我是 venali sonone，职业是数据科学家，也是管理专业的学生，希望在金融行业发展我的职业生涯。