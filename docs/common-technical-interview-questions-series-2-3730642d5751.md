# 常见技术面试问题系列— #2

> 原文：<https://medium.datadriveninvestor.com/common-technical-interview-questions-series-2-3730642d5751?source=collection_archive---------18----------------------->

[![](img/af4a44963d913f749ed5b41aa15e4237.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/4fc47184d73d3aada86ceec81c049516.png)

Photo by [rawpixel](https://unsplash.com/@rawpixel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你可以在这里找到系列主页[的链接](https://medium.com/datadriveninvestor/common-technical-interview-questions-series-announcement-6cd77db4c7fd)

> 字符串中不重复的字符

在这一部分中，我们将研究一个非常简单的问题:在给定的字符串中寻找不重复的字符

导入' random '模块创建一个随机数组，导入' time '模块记录程序的执行时间，导入 string 模块轻松访问 ASCII 字符。

```
import random
import string
import time
```

可以像这样创建一个随机数组:

```
# create a random string of 60000 lowercase charactersst_len = 60000
st = ‘’.join([random.choice(string.ascii_lowercase) for _ in range(st_len)])
```

这只是一个装饰函数，用来计算任何函数的执行时间

有两种方法可以解决这个问题。一个是用字典(hash map)，另一个是用集合。

在第一种方法(字典)中，我们将遍历字符串中的字符，并将每个字符的计数存储在字典中，然后遍历字典以找到计数等于 1 的字符。

这种方法最容易理解和实现。让我们看看代码

在第二个方法(set)中，我们首先初始化两个集合，然后遍历字符串中的字符。对于每个角色，我们必须检查我们是否在之前见过**。为此，我们将使用一个名为“s”的集合来存储我们到目前为止看到的所有独特的字符，我们将使用另一个名为“repeat”的集合来存储已经存在于集合“s”中的字符，也就是说，如果它们重复的话。**

要得到没有重复的字母，我们要做的就是从' s '集合中减去' repeat '集合。简而言之，集合“s”存储给定字符串中的所有字母，集合“repeat”存储字符串中重复出现的所有字符。

让我们看一下代码，以便更好地理解它

由于我们在两种方法中只遍历字符串一次，时间复杂度是 **O(n)**

取消注释 **@time_it** 行以返回执行时间而不是输出

## 就这样，你现在知道如何解决这类问题了。此外，请记住，字符串可以由列表或元组或任何其他可迭代的对象替换