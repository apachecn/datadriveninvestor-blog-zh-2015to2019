# 关于 Python 的更多信息

> 原文：<https://medium.datadriveninvestor.com/more-on-python-1621213b40de?source=collection_archive---------7----------------------->

[![](img/95089f7040f07d2bcd98237896b48a77.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/31faae8061cc1f235a8624f2acc6b131.png)

Python 最好的部分之一是它的内置函数。我仍然发现，许多像我一样的新手开发人员有时并没有获得 Python 的全部好处，而是从头开始编写代码。但是有时候 python 中已经有一个函数可以完成他们的工作。这也是我想到写这篇博客的原因。如果你喜欢，你知道该怎么做，:D

# **列举()**

*   返回一个枚举对象，意思是让你一个一个的迭代。
*   一个*可迭代*一定是一个序列，可以是可迭代的。
*   让我们看看它起作用了。

```
**Syntax**: **enumerate**(iterable, start = 0)>>> websites = ["Coursera", "EdX", "Udacity"]
>>> list(enumerate(websites))
[(0, 'Coursera'), (1, 'EdX'), (2, 'Udacity')]>>> list(enumerate(websites, start = 1))
[(1, 'Coursera'), (2, 'EdX'), (3, 'Udacity')]>>> for index, value in enumerate(websites):
...     print(index, value)
... 
0 Coursera
1 EdX
2 Udacity
```

为什么**枚举**有用？

*   让您选择开始索引。
*   它跟踪索引，所以不会让你在操作数据时出错。

# **Eval()**

*   *表达式*参数作为 Python 表达式进行解析和计算
*   表达式参数是一个字符串

```
**Syntax**: **eval**(*expression*, *globals=None*, *locals=None*)>>> x = 1
>>> y = 2
>>> g = eval('x+y')
>>> g
3
```

我如何看待它作为功能的替代品。

# **Zip()**

*   返回元组的迭代器，其中第 *i* 个元组包含来自每个参数序列或可迭代对象的第 *i* 个元素。
*   当您不关心拖尾时，应该只用于不等长输入，

```
**Syntax**: **zip**(**iterables*)
>>> names = ["Thor", "IronMan", "Cap", "Hawkeye"]
>>> weopens = ["Stormbreaker", "Jarvis", "Shield", "Arrow"]
>>> zipped = zip(names, weopens)
>>> list(zipped)
>>> [('Thor', 'Stormbreaker'), ('IronMan', 'Jarvis'), ('Cap', 'Shield'), ('Hawkeye', 'Arrow')]
```

*   `[zip()](https://docs.python.org/3/library/functions.html#zip)`配合`*`操作符可以用来解压列表:

```
>>> names_unzipped, weapon_unzipped = zip(*zipped)
>>> names_unzipped
>>> ('Thor', 'IronMan', 'Cap', 'Hawkeye')
```

# **过滤器()**

*   从 *iterable* 的那些元素中构造一个迭代器，其中*函数*返回 true。

```
**Syntax: filter**(*function*, *iterable*)>>> def Even(x):
...     if x%2 == 0:            
...             return True
...     else:
...             return False
... 
>>> numbers = [1,2,3,4,5,6,7,8,9,10,44]
>>> output = filter(Even, numbers)
>>> for even in output:
...     print(even)
... 
2
4
6
8
10
44
```

# **地图()**

*   返回一个迭代器，它将*函数*应用于 *iterable* 的每一项，产生结果。

```
**Syntax**: **map**(*function*, *iterable*, *...*)>>> numbers = [1,2,3,4,5,6,7,8,9,10,100]
>>> output = map(Sqaure, numbers)
>>> for sqr in output:
...     print(sqr)
... 
1
4
9
16
25
36
49
64
81
100
10000
```

# **λ()**

*   lambda 函数是一个小型的匿名函数。
*   lambda 函数可以接受任意数量的参数，但只能有一个表达式。

```
**Syntax**: **lambda** arguments: expression
>>> example1 = lambda a,b: a+b
>>> example1(1,2)
3
>>> example2 = lambda name: 'Hello '+ name
>>> example2(Python)
'Hello Python'
```

希望你喜欢。欢迎提出任何改进建议。

Twitter 句柄: [PySg_98](https://twitter.com/PySg_98)

**感谢您阅读**

## 来自 DDI 的相关故事:

[](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4) [## 数据科学和软件工程哪个更有前途？

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

medium.com](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4) [](https://medium.com/datadriveninvestor/deep-learning-explained-in-7-steps-9ae09471721a) [## 用 7 个步骤解释深度学习

### 和猫一起

medium.com](https://medium.com/datadriveninvestor/deep-learning-explained-in-7-steps-9ae09471721a)