# 3 分钟蟒蛇皮|系列

> 原文：<https://medium.datadriveninvestor.com/3-minute-python-range-74a7a3146cb4?source=collection_archive---------15----------------------->

由于其简洁明了的语法，Python 是最流行的编程语言之一。这个帖子系列将花大约 3 分钟的时间介绍一些 python 基础知识。今天的话题是**范围**。

![](img/51fac4e80bb956c31d85bbd41167ff04.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

range 用于快速生成整数列表。

```
range(start_index, end_index, stepsize)
```

在这个内置函数中，start_index 是整数列表的起点，end_index 是列表的终点。步长是我们在列表中的元素之间增加/减少的数量。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

*像 python 中的其他内置函数一样，end_index 是排他的，这意味着它不会被包含在内。*

## 范围示例:

```
*# this function returns [1, 2, 3, 4, 5, 6, 7, 8, 9]*
**range(1, 10, 1)** *# this function returns [1, 3, 5, 7, 9]*
**range(1, 10, 2)***# this function returns [1, 2, 3, 4, 5, 6, 7, 8, 9]*
**range(1, 10)***# this function returns [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]*
**range(10)**
```

# 范围的使用

可以使用范围的几个例子:

## 在 python 中遍历列表:

```
**example_list = [1, 2, 3, 4, 5]***# this prints out 1, 2, 3, 4, 5 sequentially
# len(lst) returns the total number of elements within that list* **for i in range(len(example_list)):
  print(example_list[i])***# this prints out 5, 4, 3, 2, 1 sequentially. Using range(k)[::-1]  # can reverse the generated integer list, and this could potentially # be used to iterate through the list in reverse order*
**for i in range(len(example_list))[::-1]:
  print(example_list[i])***# this also prins out 5, 4, 3, 2, 1 sequentially. This is another
# way to iterate through the list in reverse order*
**for i in range((len(example_list))-1, -1, -1):
  print(example_list[i])**
```

## 将事情执行 k 次:

```
*# this prints 'hello world' five times*
**for _ in range(5):
  print('hello world')**
```

# 概述

**Range(start_index，end_index，stepsize)** 可用于以正常或相反顺序遍历列表。

```
**for i in range(len(lst)):
  print(lst[i])**
```

也可以用来执行东西 k 次。

```
**for _ in range(5):
  print("hello world")**
```

请让我知道我如何才能改善这个职位。以后我会发更多类似的帖子！

其他 Python 教程系列:

[](https://medium.com/@jayshi/3-minute-python-list-f0960c4ba2e7) [## 3 分钟 Python |列表

### 并不是每种语言都有 Python list 这样漂亮的数据结构！

medium.com](https://medium.com/@jayshi/3-minute-python-list-f0960c4ba2e7)