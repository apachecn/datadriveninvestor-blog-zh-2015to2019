# 使用 Google Colab 的 GPU 增强 XGBoost 的功能

> 原文：<https://medium.datadriveninvestor.com/increasing-the-power-of-xgboost-with-the-use-of-google-colabs-gpu-230f11fcdea4?source=collection_archive---------1----------------------->

![](img/32f30c2aef278fa35d4c16aa7b002efd.png)

Photo by [Rene Böhmer](https://unsplash.com/@qrenep?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我的上一篇文章中(参见此[链接](https://medium.com/datadriveninvestor/improving-the-classification-with-tuning-of-pipelines-and-ensemble-models-and-xai-eb69eb60dbfb)，我已经探索了集合模型(随机森林和打包/粘贴分类器)的超参数调整，以及使用管道来简化分类过程。

使用的数据是 T2 1994 年美国收入普查数据集。里面有**婚姻状况**、**年龄**、**工种**、**更多**的信息。目标列 **high_income** 记录年薪小于或等于 50k(0)和年薪大于 50k(1)。值得注意的是，本文中也使用了它。

[](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) [## DDI 编辑推荐:5 本让你从新手变成专家的机器学习书籍|数据驱动…

### 机器学习行业的蓬勃发展重新引起了人们对人工智能的兴趣

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/03/editors-pick-5-machine-learning-books/) 

与上一篇文章不同的是，在这一篇文章中，我将使用 [XGBoost 算法](https://xgboost.readthedocs.io/en/latest/index.html)定制之前呈现的管道，并且将它的性能与在数据集分类过程中使用 Google Colab 的 GPU 进行比较。

有关 Google Colab 及其 GPU 使用的更多信息，请参见本文[。](https://medium.com/deep-learning-turkey/google-colab-free-gpu-tutorial-e113627b9f5d)

# 笔记本的改进

基本上，改进后的笔记本和之前的笔记本的区别在于库的加载和算法调整的步骤。

在加载库中，加载了 XGBoost 库和 Python 时间模块。

对于算法调整，随机森林是用以前最好的超参数设置的，并且包括 XGBoost 分类器(参见下面的代码片段)。

```
# The full pipeline as a step in another pipeline
# with an estimator as the final step.
pipe = Pipeline(
          steps = [("full_pipeline", full_pipeline_preprocessing),
                   ("fs", SelectKBest()),
                   ("clf", XGBClassifier())])# Creating a dictionary with the hyperparameters.
search_space = [
     {"clf": [RandomForestClassifier()],
      "clf__n_estimators": [800],
      "clf__criterion": ["gini", "entropy"],
      "clf__max_leaf_nodes": [300],
      "clf__random_state": [seed],
      "clf__oob_score": [True],
      "fs__score_func": [chi2],
      "fs__k": [10]},
     {"clf": [XGBClassifier()],
      "clf__n_estimators": [300],
      "clf__max_depth": [4],
      "clf__learning_rate": [0.1],
      "clf__random_state": [seed],
      "clf__subsample": [1],
      "clf__colsample_bytree": [1],
      "clf__tree_method": ["gpu_hist"],  # For using the GPU.
      "fs__score_func":[chi2],
      "fs__k":[13]}
]# Defining StratifiedKFold object -> 10-StratifiedFolds
kfold = StratifiedKFold(n_splits=num_folds,
                        random_state=seed, shuffle=True)# Creating the GridSearchCV object.
grid = GridSearchCV(estimator=pipe, 
                    param_grid=search_space,
                    cv=kfold,
                    scoring=scoring,  # Accuracy
                    return_train_score=True,
                    n_jobs=-1,
                    refit="AUC")  # AUC == ROC# Getting the time start.
tmp = time.time()# Fitting the GridSearchCV object.
best_model = grid.fit(X_train, y_train)# Printing the time spent.
print("CPU Training Time: %s seconds" % (str(time.time() - tmp)))
print("GPU Training Time: %s seconds" % (str(time.time() - tmp)))
```

> 根据 [XGBoost 文档](https://xgboost.readthedocs.io/en/latest/parameter.html)，参数 **tree_method** 表示 XGBoost 中使用的树构造算法，其默认值为 **auto** 。对于 **GPU 支持**，其值必须设置为 **gpu_hist** 。

运行训练过程后，计算两种方法花费的时间——有和没有 GPU 支持。

```
+-----------------------+------------------------+
|  Processing Location  |  Time Spent (seconds)  |
+-----------------------+------------------------+
|         CPU           |   311.7510848045349    |
|         GPU           |   301.1867105960846    |
+-----------------------+------------------------+
```

此外， **XGBoost 分类器**被认为是**对该数据集进行分类的最佳模型**。这证明了这种模型的力量，也说明了为什么这种模型在 Kaggle 比赛中如此使用。它的**训练精度**比随机森林的[高**(见下表)。**](https://medium.com/datadriveninvestor/improving-the-classification-with-tuning-of-pipelines-and-ensemble-models-and-xai-eb69eb60dbfb)

```
+-----------------------+------------------------+
|    Model/Classifier   |    Training Accuracy   |
+-----------------------+------------------------+
|     Random Forest     |        0.914574        |
| XGBoost (without GPU) |        0.920279        |
|   XGBoost (with GPU)  |        0.920415        |
+-----------------------+------------------------+
```

接下来，确定两种方法的测试精度。同样， **XGBoost 分类器超过了随机森林模型**(见下表)。

```
+-----------------------+--------------------+
|    Model/Classifier   |   Test Accuracy    |
+-----------------------+--------------------+
|     Random Forest     | 0.8665745432212498 |
| XGBoost (without GPU) | 0.8747121142330723 |
|   XGBoost (with GPU)  | 0.8765545831414094 |
+-----------------------+--------------------+
```

最后，XGBoost 模型相对于随机森林模型的高性能是显著的。此外，它的性能甚至比使用 GPU 的性能还要高。

改进后的笔记本可以在 [GitHub](https://bit.ly/2ILJaCj) 上获得。

# 结论

从本文执行的分析中，可以看出使用 XGBoost 算法执行监督学习任务的优势。此外，它的性能随着 GPU 的使用而提高。为此，谷歌 Colab 成为一个有价值的工具，因为它有一个免费的 GPU，可以用于任何目的。

# 参考

**Google Colab 免费 GPU 教程**。可在:[https://bit.ly/2r5SjvK](https://bit.ly/2r5SjvK)买到。访问时间:2019 年 10 月 11 日。

伊万诺维奇·席尔瓦。第九课——合奏模型 II。机器学习类。可在:[https://bit.ly/2ntWV12](https://bit.ly/33t9V6r)买到。访问时间:2019 年 10 月 8 日。

**XGBoost 文档**。可在:[https://xgboost.readthedocs.io/en/latest/index.html](https://xgboost.readthedocs.io/en/latest/index.html)买到。访问时间:2019 年 10 月 8 日。