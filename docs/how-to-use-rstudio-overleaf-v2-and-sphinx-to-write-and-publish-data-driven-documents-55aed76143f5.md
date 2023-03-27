# 如何使用 Rstudio、Overleaf v2 和 Sphinx 编写和发布数据驱动的文档

> 原文：<https://medium.datadriveninvestor.com/how-to-use-rstudio-overleaf-v2-and-sphinx-to-write-and-publish-data-driven-documents-55aed76143f5?source=collection_archive---------17----------------------->

![](img/a708a2701d0f842c8ca4c61e6c8f1013.png)

Photo by [Arif Riyanto](https://unsplash.com/@arifriyanto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

虽然这在很大程度上是一项正在进行的工作，并且我正在构建概念验证，但是将 Rstudio(您也可以使用常规 R 和文本编辑器，它不一定是 Rstudio)、R、文本编辑器(我尝试在 linux 笔记本电脑上使用 geany，理论上它应该工作得很好，但是 geany 行为不正常)、sphinx 和 over leaf v2(over leaf 的最新版本)结合起来，可以很好地实现一次编写，随处发布。我会写得更详细，但以下是步骤:

1.  在背面版本 2 中启动一个项目(假设您已经在背面有一个帐户；如果没有，获得一个免费帐户)
2.  设置背页项目与 github 的链接(假设你已经有一个 github 账户，如果没有，在 github 上获得一个免费账户)
3.  用`git clone <github repo address>`克隆 github repo
4.  进入这个目录`cd github_repo_folder`
5.  假设你已经安装了 sphinx，在这个文件夹中做`sphinx-quickstart`，并按照说明设置你的 sphinx 文件夹。大多数说明都很直观，一定要对 sphinx.autodoc 说“是”
6.  假设你已经安装了 R(如果没有，从 R 网站安装 R)，从 R app 内部安装`install.packages("knitr")`；或者如果你安装了 Rstudio，我想它会附带`knitr`包
7.  创建一个文件`touch foo.Rrst`。我把它命名为`foo`，但是你可以给它取任何名字。
8.  在这个文件中写 R 代码和编织重组文本材料。为了获得最佳效果，我建议继续在一个单独的文件中运行 R 代码，并且只在`foo.Rrst`文件中使用相关的 R 代码段。
9.  当你完成后，在 R 中执行`knit("foo.Rrst")`，它将生成一个`foo.rst`文件。将此`foo.rst`文件添加到您的`index.rst`文件列表中。
10.  然后，做`make latex`。
11.  然后使用`git add .`、`git commit -m "your message here"`和`git push`来填充您的回购。
12.  把文件放到你的背页，然后开始欣赏

这些步骤中的许多步骤您只需执行一次。目前，您将看到文档文本形式的所有内容。我不喜欢这样，所以我的待办事项列表将包括更改 sphinx 中的`config.py`文件的设置，使其看起来像一篇论文或书籍、报告或文章。