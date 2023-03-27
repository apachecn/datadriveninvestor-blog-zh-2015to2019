# 张量流初学者指南

> 原文：<https://medium.datadriveninvestor.com/a-beginners-guide-to-tensorflow-c6389854b37e?source=collection_archive---------11----------------------->

[![](img/44c30fc3bf481a8a327b7a3fa80cfbc6.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/659f37d92b674f457ba8719344f54419.png)

Google Brain 开发的 [**TensorFlow、**](https://www.tensorflow.org/) 是一个 [**开源的**](https://github.com/tensorflow/tensorflow) 计算库。它主要用于大规模机器学习计算，如训练神经网络。如果你目前正在学习机器学习，并希望开始使用 TensorFlow，那么这篇文章非常适合你。这是一个关于 TensorFlow 的初学者指南，涵盖了它的基础知识。

每当术语 [**TensorFlow**](https://www.tensorflow.org/) 流入讨论时，突然大多数人的思维模式完全转向机器学习，或者更具体地说，深度学习。但实际上，TensorFlow 是一个用于数值计算的开源软件库。在这篇文章中，你将了解 TensorFlow 的底层计算流程。此外，如何做基本计算。

[](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) [## 成为数据科学家所需的 8 项技能——数据驱动型投资者

### 数字吓不倒你？没有什么比一张漂亮的 excel 表更令人满意的了？你会说几种语言…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) 

# 基本原则

TensorFlow 中的计算是使用数据流图完成的。首先在 Python 中为计算定义一个图。然后 TensorFlow 将使用 C++代码运行图表。*但是等等！！* *什么是图形？最简单的形式，一个张量流图可以是这样的:*

上图可能不是什么令人费解的东西，但 TensorFlow 就是这样计算函数的， ***f(X，Y) = X*Y + Y + Z*** 。

如果你真的想了解一些东西实际上是如何工作的，那么以下内容来自 [**TensorFlow**](https://www.tensorflow.org/guide/graphs) 网站本身。

![](img/dda1b339a1048070f3498e50e30b688c.png)

也许最棒的是 TensorFlow 支持并行计算。您可以将图形分成几个部分，并在多个 CPU 和 GPU 上分别运行它们。这使得在使用单个 CPU 或 GPU 时，训练模型的速度比传统方法快得多。

# 安装 TensorFlow

现在，您将亲身体验 TensorFlow 的使用。我们将介绍张量流的安装以及简单的计算，让你熟悉图形的流动。

在开始之前，我强烈建议您查看我以前的一篇文章， [**数据科学环境设置。这将帮助你安装所有需要的软件包和软件。另外，我建议您直接从 Anaconda 终端工作，这将使您的工作更加容易。**](https://debuggercafe.com/data-science-environment-setup/)

好了，现在假设一切准备就绪，在 anaconda 终端上键入以下命令来激活虚拟环境:

`conda activate your_env_name`

在系统上安装 TensorFlow 的下一步:

`conda install tensorflow`

如果你想安装 GPU 支持的 TensorFlow(如果你真的想看到一些有成效的结果，你应该这样做，但显然不是强制性的)，然后键入以下内容:

`conda install tensorflow-gpu`

对于大多数人来说，安装 TensorFlow 的 GPU 版本是不需要的，特别是如果您刚刚开始使用神经网络。但是当你想要训练一些复杂的网络时，这两个版本之间的差异是显而易见的。

接下来，确保 TensorFlow 安装正确:

`python`

Python 外壳被激活后:

`>>>import tensorflow as tf`

`>>>print(tf.__version__)`

您应该可以看到安装在您计算机上的版本。

# 做一些简单的计算

现在是时候在这里变得实际一些了。在本节中，您将定义变量，创建张量流会话并评估结果。对于这一部分，你应该开始你的 Jupyter 笔记本。如果你还没有安装，那么你可以参考这篇文章， [**数据科学环境设置。**](https://debuggercafe.com/data-science-environment-setup/)

你可以跟着走:

```
import tensorflow as tf a = tf.Variable(9, name=’a’) 
b = tf.Variable(3, name=’b’) 
c = tf.Variable(2, name=’c’) res = a*b + b*c
```

那么，上面的代码是做什么的？事实是，几乎什么都没有。但这里需要注意的一点是，它会创建以下计算图:

现在你可能会问，接下来呢？如何实际计算上面的表达式？为此，我们必须创建一个新的 TensorFlow *会话。*tensor flow 会话将初始化上述程序中声明的所有变量，并计算`res`。下面的代码显示了所有这些:

```
sess = tf.Session() sess.run(a.initializer) 
sess.run(b.initializer) 
sess.run(c.initializer) 
result = sess.run(res) 
print(result) sess.close()
```

当您执行代码时，结果应该是 33。关闭会话也非常重要，您必须手动完成。

实际上，您可以通过使用`with`块来使上面的代码块更清晰一些。除此之外，您还可以使用`global_variables_initializer()`函数同时初始化所有变量。这样你可以避免重复一些台词。另一个好处是，您不需要在计算结束时手动关闭会话。下面的程序块会给你一个如何做的清晰思路:

```
init = tf.global_variables_initializer()with tf.Session() as sess: init.run() result = res.eval() print(result)
```

你一定已经注意到了，我们再次在程序块内部调用了一个`run()`函数。这是因为`global_variables_initializer()`函数实际上并不进行初始化。它会根据您声明的名称(init)创建一个节点。然后`run()`方法初始化所有的变量。你一定要看看 [**文档页面**](https://www.tensorflow.org/api_docs/python) 来了解更多的用法。TensorFlow 网站也提供了非常容易上手的例子。

# 尾注

这个帖子到此为止。您已经学习了张量流计算的基础知识。如果你愿意，你可以从所有可用的资源中搜索并做更多的事情。尽管如此，我认为最好的起点是官方的 [**TensorFlow**](https://www.tensorflow.org/) 网站。如果您在本文的概念或代码中发现任何差异，请随时联系我。请分享这篇文章，并留下一个大拇指。是的，你可以在推特 [**上关注我**](https://twitter.com/SovitRath5) 来获得关于新文章的定期更新。

标签:[数据科学](https://debuggercafe.com/tag/data-science/)，[机器学习](https://debuggercafe.com/tag/machinelearning/)， [Python](https://debuggercafe.com/tag/python/) ， [TensorFlow](https://debuggercafe.com/tag/tensorflow/)

*原载于 2019 年 3 月 25 日*[*debuggercafe.com*](https://debuggercafe.com/a-beginners-guide-to-tensorflow/)*。*