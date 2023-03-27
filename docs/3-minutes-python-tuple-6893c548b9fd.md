# 3 分钟 Python | Tuple

> 原文：<https://medium.datadriveninvestor.com/3-minutes-python-tuple-6893c548b9fd?source=collection_archive---------11----------------------->

什么是元组，我们为什么需要它？

![](img/c9bd26a951ecc22e14528b94d983cc4e.png)

Photo by [Arif Riyanto](https://unsplash.com/@arifriyanto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

Tuple 是 python 内置的数据结构之一。除了它是不可变的之外，它就像一个列表，这意味着我们不能在 tuple 对象初始化之后修改它。元组对它可以存储的数据类型没有限制。我们通常将元组用于以特定顺序存储数据的简单数据结构。

```
# one good example of using tuple is coordinates
#   point_1 = (x1, y1, z1)
#   point_2 = (x2, y2, z2)**point_1 = (0.1, 5.7, -1)
point_2 = (2.9, 1, 0)**# We know that the data stored in the coordinate tuple is in certain
#   order, and thus we can predict our data position easily when
#   using them.
```

与 list 一样，tuple 元素也从索引 0 开始，这意味着 tuple 中的第一个元素位于位置 0，第二个元素位于位置 1，依此类推。

## 元组初始化

```
# initialize a tuple. *Recall how we initialize list: a = [1, 2, 3]*
**a = ('a', 'b', 'c')**
```

## 公共元组函数

```
# "ele in tupl" is a predicate that checks if the element is in
#   the tuple.
**a = ('a', 'b', 'c')**
# this evaluates to be True
**'b' in a**
# this evaluates to be False
**'d' in a**
```

## 公共元组操作

```
**a = ('a', 'b', 'c')**# tupl[k] returns the Kth element in the tuple
# this evaluates to be 'b'
**a[1]**# tuple1+tuple2 produce a new tuple containing all the elements from
#   both tuple1 and tuple2 in their order.
# c is now ('a', 'z', 'e', 'x', 1, 'hello')
**c = ('a', 'z', 'e') + ('x', 1, 'hello')**# list(tupl) converts tuple into list, and then we can do
#   modifications on the list.
# d is now ['a', 'z', 'e', 'x', 1, 'hello']
**d = list(c)**# d is now ['a', 'z', 'e', 'x', 1, 'hello', 'world']
**d.append('world')**# tuple(lst) converts list into tuple
# e is now ('a', 'z', 'e', 'x', 1, 'hello', 'world')
**e = tuple(d)**# f is now ('h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd')
**f = tuple('hello world')**# tupl[k:t] returns a new tuple sliced from tupl starting at
#   position K (inclusive) and ending at position T (exclusive).
# The starting index is default to be 0, and the ending index is
#   default to be last position in the tuple.# e is now ('b', 'c', 'd')
**e = ('a', 'b', 'c', 'd')[1:]**
```

# 概述

在今天的帖子中，我们讨论了为什么使用 tuple，以及如何使用 Tuple。Tuple 可以用来按照特定的顺序存储数据，稍后我们可以使用 square braket ([])来进行读取和切片。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

需要注意的一点是 tuple 是不可变的，这意味着我们不能在初始化之后修改 tuple 值。在这篇文章中，我们做的一个技巧是将元组转换成列表，然后修改值。

希望这个帖子有帮助！我以后会发更多类似的帖子，敬请关注！

其他 Python 教程帖子:

[](https://medium.com/@jayshi/3-minute-python-list-f0960c4ba2e7) [## 3 分钟 Python |列表

### 并不是每种语言都有 Python list 这样漂亮的数据结构！

medium.com](https://medium.com/@jayshi/3-minute-python-list-f0960c4ba2e7) [](https://medium.com/@jayshi/3-minute-python-range-74a7a3146cb4) [## 3 分钟蟒蛇皮|系列

### 花 3 分钟学习 python 最基本的内置函数之一——range！

medium.com](https://medium.com/@jayshi/3-minute-python-range-74a7a3146cb4)