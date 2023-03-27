# 我如何通过“自动粘贴”取代笔记本电脑来提高工作效率

> 原文：<https://medium.datadriveninvestor.com/how-i-improved-my-productivity-by-replacing-notebooks-with-automatic-pasting-9f8265426284?source=collection_archive---------16----------------------->

[![](img/154c23270caa09b52eb2b42b8b33a9cd.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/ab04cd3d29b8ed08732cabc62161d28f.png)

## 项目越来越多…

尽管我作为一名数据科学家已经工作了大约两年，但我发现将我的工作描述为“数据科学家”非常简单，因为我负责端到端的算法和数据解决方案，即从设计、原型制作和数据收集到部署和监控。因此，我通常花相当多的时间做数据工程师和机器学习工程师的工作。

当我从学术界转向数据科学家时，我经常使用 j [upyter](https://jupyter.org/) 和 [zeppelin](https://zeppelin.apache.org/) 笔记本；我发现这些伟大的工具非常有助于组织和分享代码，评论，情节，分析和模型原型。另一方面，笔记本也可能鼓励代码模块化和组织方面的不良做法。当我开始担任数据科学家时，我一直在大量使用笔记本电脑。当估计端到端执行项目的时间时，我通常会增加固定的时间来将代码从笔记本移动/重构到脚本中。

然而，随着我处理的项目变得越来越复杂，我发现与使用笔记本相关的开销也变得越来越大。首先，我开始用 [Spark](https://spark.apache.org/) 构建越来越多的管道，用 Scala 或 Python 编码。在 Scala 中工作时，我开始越来越多地使用带有 [REPL](https://docs.scala-lang.org/overviews/repl/overview.html) 的 Spark shell 来交互式地测试和开发管道。我发现使用 spark(或 pyspark)外壳也更容易:

1.  分发库和依赖项。
2.  交互式地尝试各种方法，以更快的速度和更少的资源扩大计算规模。
3.  动态调整 Spark 配置(与每次在 jupyter 中编写不同的内核配置相比)。
4.  升级群集之前调试新版本的库。

然后我开始研究数据驱动的营销归因算法；在属性模型所需的数据规模和粒度级别，我意识到没有可以直接使用的开源库，并在 Scala 中实现了一个库来与 Spark 一起使用。在这里，我发现使用 REPL 非常有帮助，特别是当我不得不在我所工作的集群中对 Spark 配置进行调整，使之与默认配置相差很远时。

后来，我开始为点击付费竞价框架编写多语言库；该库包含运行在不同环境之上的组件:

1.  spark(Python 中的)。
2.  Python 和 R 中的容器化应用程序。
3.  创建和转换由作业调度程序接收的 Dag 定义。

在测试库的不同组件时，我发现直接处理脚本非常有用，这样我就可以隔离我正在处理的特定组件，并记录单元测试的结果。使用 jupyter，我必须跟踪内核正在加载哪个版本的库，或者可能求助于使用几个不同的虚拟环境。

## 粘贴是可怕的…

起初，我只是在 [tmux](https://github.com/tmux/tmux/wiki) 窗口之间复制和粘贴代码。我会在一个窗口中打开一个交互式解释器外壳(python，R，Scala ),在另一个窗口中打开 Emacs。然而粘贴很快就变得可怕了，有了 Emacs 的按键绑定，你甚至开始担心开发一个 RSI…

这就是为什么我开始想，在交互式解释器会话开始时修改一个文件，并告诉解释器执行一系列行该有多好；此外，在修改文件之后，解释器将从最新版本加载代码行，这样我就可以交互式地开发脚本。一旦完成，我就不必担心在不同的笔记本单元中有代码，可能是顺序错误。

本质上，我的目标是

```
# load the script file
myS = AutoPasteFromScript("script.py")# execute specific line range
myS(5,10)
```

这就是我决定为 Python、R & Scala 编写小工具的原因。你可以查看我的 github 回购:[https://github.com/salayatana66/auto-paste-from-script](https://github.com/salayatana66/auto-paste-from-script)。

## 用法示例

我试图让不同语言之间的用法尽可能的相似。例如在 Python 中:

```
from auto_paste_from_script import AutoPasteFromScript

myS = AutoPasteFromScript("script.py")

myS(1,5)
```

在 R 中:

```
source("AutoPasteFromScript.R")

myS <- AutoPasteFromScript$new(fileName="this.R")

myS$exec(1,5)
```

在 Scala 中:

```
import auto.paste.from.script.AutoPasteFromScript

// $intp is the current interpreter
val myS = AutoPasteFromScript("filename.scala", $intp)

myS(1,5)
```

## 关于实现的一些话

这个工具的实现在不同的语言中非常相似。所需要的只是一个重新加载文件的机制和另一个执行代码的机制。对象类将被跨语言调用`AutoPasteFromScript`。

在 Python 中，构造函数只是将脚本文件名作为一个字符串；定义了一个方法`__reload__`来在每次调用`AutoPasteFromScript`时重新加载文件的内容。为了执行一系列行之间的文件内容，使用了一个`exec`语句。这里的一个小问题是使调用者的父框架的环境变量的字典可见；这是通过使用【https://docs.python.org/3/reference/datamodel.html】模块来实现的，在这个模块中可以获得对父框架字典的引用(参见这里讨论的框架对象:)

r 没有 Python 那么成熟的类体系。我选择使用[引用类](http://adv-r.had.co.nz/R5.html)来实现，因为它们看起来最接近 Python 中的引用类。方法是相同的，使用一个`load`方法在每次调用时重新加载文件，使用一个`toString`方法产生一个包含所需行的字符串。要执行代码，我们必须首先解析字符串，然后在[全局环境](http://adv-r.had.co.nz/Environments.html)中评估结果。

Scala 代码是最容易编写的，因为解释器实例`$intp`已经准备好解释字符串了。一个有用的技巧是使用`apply`方法通过语法`myS(line1, line2)`启用访问。我使用 [sbt](https://www.scala-sbt.org/) 工具构建了 Scala 版本。起初，我发现的一个小问题是必须显式地添加`scala-compiler`依赖项来访问 REPL 类`interpreter.IMain`。我发现在 `scala-compiler`中而不是在像`scala-repl`这样的名字中有这个需求有点违背直觉，我花了一点堆栈溢出来找到正确的依赖关系。

任何类型的评论或批评以及对 Github 代码的改进都将受到欢迎。