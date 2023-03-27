# 用 Python 创建模型(OOP)

> 原文：<https://medium.datadriveninvestor.com/create-a-model-in-python-oop-b117015f08f2?source=collection_archive---------0----------------------->

![](img/562a6d33daacd16821bc11c2b5ea82fa.png)

所有的对象都有一些属性和它们能做的许多不同的事情。按照同样的思路，所有的对象都可以被解构为不同的属性和动作。让我们以电影数据库为例。它们都将具有诸如标题、评级、运行时间等属性。如果有一种方法可以将所有电影的所有属性归为一类，不是更容易吗？这就是 OOP 发挥作用的时候了。

我们可以从创建一个“电影”模型开始。在一个新文件中，我们将定义我们的类:

```
class Film(object): 
```

我们用“类”来给电影分类。我们传递给它一个对象，因为它是一个对象，并且来自一个对象，通过这样做，我们可以把它当作一个对象。

[](https://www.datadriveninvestor.com/2019/03/25/a-programmers-guide-to-creating-an-eclectic-bookshelf/) [## 创建折衷书架的程序员指南|数据驱动的投资者

### 每个开发者都应该有一个书架。他的内阁中可能的文本集合是无数的，但不是每一个集合…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/25/a-programmers-guide-to-creating-an-eclectic-bookshelf/) 

现在我们需要给它分配属性。确保每一部新电影的创作都和其他电影一样。我们将为此创建一个函数或操作:

```
def __init__(self):
```

在继续之前，让我们先看看这个。函数“_ _ init _ _ ”( initializing 的简称)将在每次创建新的电影对象时运行。“自我”是正在被创建的东西，我们将把它传入，然后赋予它属性。让我们先给它分配 3 个基本属性。

```
def __init__(self):
        self.title = "Men in Black"
        self.rating = "PG-13"
        self.runtime = "1h 55m"
```

下一步，我们将为电影指定标题、分级和播放时间。看起来我们都准备好了，让我们看看这将如何工作。

```
film = Film()
```

在这里，我们通过将“film”分配给“Film”来创建一个“Film”实例。制作"电影"和类电影的实例。这将赋予“film”类 Film 的所有属性和功能。如果我们现在要做这样的事情:

```
film.title
 #"Men in Black"
```

这里“电影标题”将返回“黑衣人”。太好了！我们现在好像有工人阶级了。唯一的问题是，电影的任何实例都将具有相同的标题，因为我们静态地分配了标题。如果我们想要一个不同的标题。我们可以简单地这样做:

```
film = Film()print(film.title)
 #// "Men in Black"film.title = "Pretty Woman"print(film.title)
# "Pretty Woman"
```

我们可以这样改变它，但是每次都这么做似乎很乏味。因此，让我们回到我们的电影模型，并设置它更加动态。

```
class Film(object):
    def __init__(self, title, rating, runtime):
```

如果我们把它设置成也需要接受属性，这样我们就可以把它的属性分配给那些特定的属性。就像我们以前做的那样，只是我们将属性分配给那些占位符:

```
class Film(object):
    def __init__(self, title, rating, runtime):
        self.title = title
        self.rating = rating
        self.runtime = runtime
```

看起来不错！让我们看看现在会发生什么:

```
film = Film()print(film.title)//TypeError: __init__() takes exactly 4 arguments (1 given)
```

我们得到一个错误，但这是一个好迹象！如果我们读对了，它会显示它在工作。它说它缺少参数，即我们的“标题、评级、运行时间”。你可能会困惑为什么它说 1 是给定的。那是因为它指的是“自我”，也就是我们正在创造的实例。让我们给它剩下的属性:

```
film = Film("Pretty Woman", "R", "2h 5m")print(film.title)
# "Pretty Woman"
```

成功了！下一步是把它植入我们的数据库，这完全取决于你用的是哪一种。如果您使用 MongoDB，您可能需要在电影模型中创建一个函数，在插入之前将数据转换为 JSON 格式。

这是 python 面向对象模型背后非常基本的创造和思想。它的使用帮助我们在程序中加速和保持结构。我希望你喜欢这个概念，并从中获得乐趣！