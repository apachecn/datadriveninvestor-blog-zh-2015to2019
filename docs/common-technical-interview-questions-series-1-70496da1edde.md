# 常见技术面试问题系列— #1

> 原文：<https://medium.datadriveninvestor.com/common-technical-interview-questions-series-1-70496da1edde?source=collection_archive---------19----------------------->

[![](img/d04177aa625611dc1c7dbeb50d559cae.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/b8b8e32a05409b93823d6882ad305db8.png)

Photo by [Fatos Bytyqi](https://unsplash.com/@fatosi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你可以在这里找到系列主页[的链接](https://medium.com/datadriveninvestor/common-technical-interview-questions-series-announcement-6cd77db4c7fd)

> 数组中出现频率最高的项目

在这一部分中，我们将研究一个非常简单的问题:在给定的数组中寻找最频繁出现的元素

导入' random '模块创建一个随机数组，导入 time 模块记录程序的执行时间

```
import random
import time
```

可以像这样创建一个随机数组:

```
# returns an array of 50 numbers from 1 to 20arr = [random.randint(1,20) for _ in range(50)]
```

这只是一个装饰函数，用来计算任何函数的执行时间

解决这个问题的主要思想是将每个唯一元素的计数存储在字典或哈希映射中。

首先，遍历数组的所有元素，如果该元素作为一个键存在于字典中，那么它的值(count)加 1。否则，创建一个新的键(元素)并将其值(计数)初始化为 1。

在遍历了整个数组之后，现在就有了所有元素的计数。现在您需要做的就是遍历字典的(key，value)对，找到具有最大值(count)的键(element)

由于我们只遍历数组一次，这个函数的时间复杂度是 **O(n)**

取消对 **@time_it** 行的注释，返回执行时间而不是输出

然而，这也可以通过另一种方式来实现，即在遍历数组时获取 max_value，而不是单独遍历最终的字典

## 就这样，你现在知道如何解决这类问题。此外，请记住，数组可以用字符串、元组或任何其他可迭代的元素来替换