# 实施线性和逻辑回归

> 原文：<https://medium.datadriveninvestor.com/implementation-of-linear-and-logistic-regression-dddf700f0df8?source=collection_archive---------5----------------------->

[![](img/0158a2c5bc584c4cf613da77ae6d6a4b.png)](http://www.track.datadriveninvestor.com/1B9E)

[***www.internity，在***](http://www.intermity,in)

![](img/cc3abe4c911aca4b1b6e41cac3e5cb0c.png)

由于我们已经对可用的回归技术有了一些理论观点，现在是使用 python 实现它们的时候了。

在进入实际的实现过程之前，我们应该先了解一下 python 为我们提供的一些内置库的信息。这些库使我们的工作变得非常容易，并且时间消耗也减少了。

像 ***sklearn*** 库有一个模块叫 LinearRegression 和 LogisticRegression。因此，所有的内部工作都被这些模块所掩盖，包括成本函数的计算、梯度下降和许多其他事情。

![](img/d9b15cc271633451fba7fe01d16ec01a.png)

**source : machinelearningplus.com**

```
#First of all we will import some basic librariesimport pandas as pd
import numpy as np#now as talked earlier, we will import the modules of sklearn
from sklearn.linear_model import LinearRegression
from sklearn.linear_model import LogisticRegression
from sklearn.cross_validation import train_test_split#train_test_split function randomly distribute array into training    #and testing subsets
iris = datasets.load_iris()
x = iris.data
y = iris.target
X_train, X_test, y_train, y_test = train_test_split(x, y, random_state=1)
linreg = LinearRegression() #this is to call the function
logreg = LogisticRegression()
linreg.fit(X_train, y_train) #fitting our training data
logreg.fit(X_train, y_train)
y_pred = linreg.predict(X_test)
y_pred1 = logreg.predict(X_test)
print(y_pred)
print(y_pred1)# compute the RMSE of our predictions
print(np.sqrt(metrics.mean_squared_error(y_test, y_pred)))
```

所以在这篇文章中，我们刚刚学习了一种通过使用一些内置库来实现逻辑和线性回归的基本方法。我们在这个过程中使用了虹膜数据集。

它涵盖了关于逻辑和线性回归实现的一些基本理解。

好了，各位，下次再见。编码快乐！！