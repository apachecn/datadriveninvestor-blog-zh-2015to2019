# 构建分类器以预测人的活动类别

> 原文：<https://medium.datadriveninvestor.com/building-a-classifier-to-predict-activity-category-of-a-human-84eaf2d9803e?source=collection_archive---------8----------------------->

根据 [UCI 机器学习库](http://archive.ics.uci.edu/ml/index.php)的说法，人类活动识别数据集来自 30 名受试者的日常活动记录，他们随身携带一部嵌入惯性传感器的腰部安装智能手机。每人进行六项活动，分别是:走、上楼、下楼、坐、站、卧。如何从传感器获得数据的程序、数据及其描述以及预处理都可以在这里[获得](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)。

我使用[支持向量机](https://en.wikipedia.org/wiki/Support_vector_machine) (SVM)构建了一个多类分类器。SVM 试图用一个清晰的决策边界来区分数据类别，该决策边界与任何类别的最近数据点都有很大的距离。我现在将介绍我的方法。

使用 [Google Colab](https://colab.research.google.com) ，我们打开一个新的 Python3 笔记本。数据文件可以导入到 Google Drive 中，并从 Google Colab 中访问。我们可以使用下面几行代码将这些文件导入笔记本。

```
from google.colab import drive
drive.mount('/content/gdrive')
```

然后，服务器会要求我们按照一个链接，将我们转到授权谷歌驱动器文件流访问我们的谷歌驱动器。将创建一个令牌，然后我们将它复制到笔记本上提供的文本输入中。当该说的都说了，该做的都做了，我们应该看看`Mounted at /content/gdrive.`

我们现在将把数据分为训练数据和测试数据。首先，我们从 *features.txt* 中获取我们的特性列表，因此:

```
with open('/content/gdrive/My Drive/features.txt') as feature_file:
  names = feature_file.readlines()
  names = map(lambda x: x.strip(), names)
  names = list(names)
```

然后拆分我们的数据:

```
X_train = pd.read_csv('/content/gdrive/My Drive/X_train.txt', header=None, delimiter=r"\s+", names=names)
X_test = pd.read_csv('/content/gdrive/My Drive/X_test.txt', header=None, delimiter=r"\s+", names=names)
y_train = pd.read_csv('/content/gdrive/My Drive/y_train.txt', header=None)
y_test = pd.read_csv('/content/gdrive/My Drive/y_test.txt', header=Noney_train.columns = ['label']
y_test.columns = ['label']# we will need this for fitting the model
y_train_fin = y_train.values.ravel()
y_test_fin = y_test.values.ravel()
```

为了确保我们的数据是标准化的，我们使用来自`preprocessing`模块的`sklearn`的`StandardScaler`并转换我们的数据，本质上是移除平均值并缩放到单位方差。我们可以用如下所示的几行代码做到这一点。

```
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train_fin = scaler.fit_transform(X_train)
X_test_fin = scaler.transform(X_test)
```

我们可以使用不同形式的内核来实现 SVM 模型。我基本上是通过线性、高斯和多项式核来衡量哪个模型能够达到最高的精度。为了获得更准确的研究结果，我们使用了 [KFold 交叉验证](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.KFold.html)技术。我们将训练数据分成 k 个连续的折叠。每个折叠用作一次验证，而剩余的 k -1 个折叠用作训练集。然后，我们汇总各种模型的分数，并按如下方式打印结果:

```
from sklearn.model_selection import KFold
from sklearn import svm
import numpy as npsvc_linear = svm.SVC(kernel='linear')
svc_gaussian = svm.SVC(kernel='rbf')
svc_poly = svm.SVC(kernel='poly')# split into 5 folds
k_fold = KFold(n_splits=5)scores_linear = np.array([svc_linear.fit(X_train_fin[train], y_train_fin[train]).score(X_train_fin[test], y_train_fin[test]) 
for train, test in k_fold.split(X_train_fin)])scores_gaussian = np.array([svc_gaussian.fit(X_train_fin[train], y_train_fin[train]).score(X_train_fin[test], y_train_fin[test]) 
for train, test in k_fold.split(X_train_fin)])scores_poly = np.array([svc_poly.fit(X_train_fin[train], y_train_fin[train]).score(X_train_fin[test], y_train_fin[test]) 
for train, test in k_fold.split(X_train_fin)])print("Scores for linear SVM ", scores_linear)
print("Train accuracy LINEAR: %0.2f (+/- %0.2f)" % (scores_linear.mean(), scores_linear.std()/2))
print("Scores for gaussian SVM ", scores_gaussian)
print("Train accuracy GAUSSIAN: %0.2f (+/- %0.2f)" % (scores_gaussian.mean(), scores_gaussian.std()/2))
print("Scores for polynomial SVM ", scores_poly)
print("Train accuracy POLY: %0.2f (+/- %0.2f)" % (scores_poly.mean(), scores_poly.std()/2))print("Train accuracy: %0.2f (+/- %0.2f)" % (scores.mean(), scores.std()/2))
```

运行上面的代码后，我们得到这样的结果:

```
Scores for linear SVM  [0.92454113 0.90210741 0.93197279 0.94761905 0.96462585]
Train accuracy LINEAR: 0.93 (+/- 0.01)
Scores for gaussian SVM  [0.92726037 0.90754589 0.91632653 0.92789116 0.95782313]
Train accuracy GAUSSIAN: 0.93 (+/- 0.01)
Scores for polynomial SVM  [0.91434398 0.90210741 0.91768707 0.92040816 0.93061224]
Train accuracy POLY: 0.92 (+/- 0.00)
```

正如我们所见，线性和高斯 SVM 核是可比的。然后我们可以看到每个人在测试集上的表现:

```
y_pred_linear = svc_linear.predict(X_test_fin)
y_pred_gaussian = svc_gaussian.predict(X_test_fin)
y_pred_poly = svc_poly.predict(X_test_fin)from sklearn.metrics import accuracy_scoreprint("Linear ", accuracy_score(y_test_fin, y_pred_linear))
print("Gaussian ", accuracy_score(y_test_fin, y_pred_gaussian))
print("Poly ", accuracy_score(y_test_fin, y_pred_poly))
```

运行上述代码后，我们获得了以下结果:

```
Linear  0.9491007804546997
Gaussian  0.9433322022395657
Poly  0.9124533423820834
```

正如我们所见，线性核做得最好，尽管仍然与高斯核相当。

此外，使用线性内核，我们可以创建一个交叉表来更好地可视化 SVM 在测试集上的表现:

```
svc_linear.fit(X_train_fin, y_train_fin)crosstab = pd.crosstab(y_test_fin.flatten(),   svc_linear.predict(X_test_fin),
                   rownames=['True'], colnames=['Predicted'],
                   margins=True)
crosstab
```

我们获得下表。看起来我们的模型做得很好。然而，似乎我们的模型在处理 4 和 5 时遇到了一点麻烦。为什么？因为如果我们看它们代表的活动，4 代表坐着，5 代表站着。很明显，这些活动是静止的，加速度计和陀螺仪关于这些活动的数据非常相似。

```
+------------+------+------+------+------+------+------+------+
| Predicted  |  1   |  2   |  3   |  4   |  5   |  6   | All  |
+------------+------+------+------+------+------+------+------+
| True       |      |      |      |      |      |      |      |
| 1          | 495  |   0  |   1  |   0  |   0  |   0  |  496 |
| 2          |  16  | 453  |   2  |   0  |   0  |   0  |  471 |
| 3          |   6  |  15  | 399  |   0  |   0  |   0  |  420 |
| 4          |   0  |   2  |   0  | 434  |  55  |   0  |  491 |
| 5          |   0  |   0  |   0  |  18  | 514  |   0  |  532 |
| 6          |   0  |   0  |   0  |   0  |   0  | 537  |  537 |
| All        | 517  | 470  | 402  | 452  | 569  | 537  | 2947 |
+------------+------+------+------+------+------+------+------+
```

就是这样！我们可以尝试的一件事是应用[主成分分析(PCA)](https://en.wikipedia.org/wiki/Principal_component_analysis) 来降低数据的维度。这是因为我们有太多可能导致过度拟合的特征。另一件事是把这变成一个二元分类问题，我们试图预测一个活动是静止的还是移动的。

# 结论

我希望这篇文章对你有深刻的见解和帮助。请分享你的想法。