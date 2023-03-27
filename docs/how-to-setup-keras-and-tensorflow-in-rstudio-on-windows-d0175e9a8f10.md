# 如何在 windows 上的 RStudio 中设置 Keras 和 TensorFlow

> 原文：<https://medium.datadriveninvestor.com/how-to-setup-keras-and-tensorflow-in-rstudio-on-windows-d0175e9a8f10?source=collection_archive---------0----------------------->

![](img/1c28c61c03fed2e73be503dad44868fa.png)

我不得不在课堂作业中使用 R 中的 Keras 和 TensorFlow 然而，我的 Linux 系统崩溃了，我不得不在 windows 上使用 RStudio。对于我来说，我无法让 Keras 开箱即用，也找不到关于如何设置它的好教程。我做了一些研究，这些是我用来最终让它工作的步骤。希望这能节省一些时间！

# 第 1 部分:安装 Python

Keras 和 TensorFlow 都依赖 python 工作。我在使用 Python 3 时遇到了问题。所以我决定使用 anaconda，python 的数据科学发行版，下载并安装这个版本的 Anaconda。这是 3.7 版本，但这是对我有用的版本。我在当前版本的 Anaconda 上不断遇到设置错误。在安装过程中，记得选中复选框，将 anaconda 添加到您的路径中，并将其设置为默认 python。如果愿意，您可以创建一个 virturalenv，但是为了简单起见，我们将在本指南的剩余部分使用基本的 anaconda 环境。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？数据驱动的投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

# 第 2 部分:安装网状

为了让 R 能够与 Python 对话，我们需要安装 Reticulate。所以在 RStudio 中运行 install.packages("reticulate ")。这将下载并安装 r。

# 第 3 部分:在 python 中安装 TensorFlow 和 Keras

运行***pip install tensor flow***和 ***pip install keras*** 在 python 中安装这两个库。您可以通过从 python 运行***import TensorFlow as TF***来测试 tensor flow 安装。如果没有出现错误，您就可以继续下一步了！

# 第 4 部分:在 R 中安装 TensorFlow 和 Keras

从 RStudio/R 运行命令***install . packages(" tensor flow ")***和***install . packages(" keras ")***。接下来，通过运行 ***库(tensorflow)*** 加载 TensorFlow 库。最后通过运行***install _ tensor flow()***安装依赖项。一旦完成，对 Keras 进行同样的操作:运行***【Keras】***，然后运行***install _ Keras()***

# 第五部分:结论

你可以通过在笔记本上运行 ***库*** 和一些 keras 代码来测试安装。如果你没有收到错误，那么你就可以开始了！如果你确实收到一些错误，请在下面评论，我会尽力帮助你。

*谢谢您的阅读，请👏并分享出来帮助别人找到。*

回头见。😃