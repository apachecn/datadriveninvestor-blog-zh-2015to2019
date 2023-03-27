# Python 变量和数据类型

> 原文：<https://medium.datadriveninvestor.com/python-variables-and-data-types-bea73c9fbf9d?source=collection_archive---------7----------------------->

## 一段代码不会咬你，它只是抛出一个错误。

![](img/80c48d00b02c6911e2a1cdbe3f855749.png)

“person holding sticky note” by [Hitesh Choudhary](https://unsplash.com/@hiteshchoudhary?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Python 是**动态类型语言**。这意味着你**不需要**到**在使用变量**之前声明它。这使得 python 不同于其他编程语言，如 C、C++、Java 等。

```
>>> x = 5
>>> type(x)
int
```

Python 会自动检测赋值变量的数据类型。幸运的是，它的数据类型与其他数据类型基本相同。以下是 python 数据类型的一些示例:

```
1       ->  int
1.0     ->  float
"1"     ->  str
[1]     ->  list
(1,2,3) ->  tuple
{"x":1} ->  dict
```

乍一看，也许我们对 tuple 和 dict(字典)并不熟悉。我会在其他机会尽量解释。

> 变量就像计算机内存中的一个盒子，你可以在里面存储一个值。—阿尔·斯威加特

我们也可以一次分配多个变量。有一些给多个变量赋值的方法，查看下面的代码:

```
>>> a, b, c, d = 1, 2.0, "3", [4]
>>> type(a)
int
>>> type(b)
float
>>> type(c)
str
>>> type(d)
list>>> x = [1, "2", {"y":3}, [4]]
>>> a, b, c, d = x
>>> print(a, b, c, d)
(1, '2', {'y': 3}, [4])
```

它很灵活，对吧？但是，这种灵活性是有后果的。由于 python 没有声明变量，所以会有变量曲解、无返回信息等漏洞。

> 把它想象成一个储物柜，你可以把东西放进去，以后需要的时候再拿出来。然后你有更多的储物柜来存放更多的物品。但是如果没有标签或注释，就很难找到物品或猜测储物柜里有什么。

有一些方法可以减少这种漏洞，比如使用变量注释( [PEP 526](https://www.python.org/dev/peps/pep-0526/) )和函数注释( [PEP 3107](https://www.python.org/dev/peps/pep-3107/) )。

```
>>> x: int = 5
>>> y: int
>>> y = 1
>>> z: int = "abc" 
#z will be flagged as error by type checker, but OK at runtime.
```

# 结论

Python 是一种动态类型语言**，**，这意味着在使用变量之前不需要声明变量。数据类型通常与其他编程语言相同。除了它的优点之外，还有一些在将来可能导致问题的漏洞。