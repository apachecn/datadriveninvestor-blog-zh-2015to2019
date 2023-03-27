# iTerm & vim 爱好者如何采用 IntelliJ 理念

> 原文：<https://medium.datadriveninvestor.com/how-an-iterm-vim-lover-adopted-intellij-idea-245de54b0945?source=collection_archive---------35----------------------->

![](img/3493e6edde703768c67ad38e22635cf6.png)

Photo by [Kate Remmer](https://unsplash.com/photos/05_sUnshoaE?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/migration?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在使用 vim 研究 C/C++多年之后，当我开始用 Scala 编码时，我的手指还没有准备好接受使用任何 IDE 编写代码。在几年前用不同的 ide 进行了多次失败的尝试后，我又回到 iTerm 和 vim 上，甚至为 java 和 scala 代码编写代码。

Vim 绝对是我唯一选择的编辑器，但是有一些 iTerm 快捷键，没有它们我无法编码。就像 cmd+/cmd-增加和减少字体，cmd+进入全屏模式，我喜欢用它来编码不受干扰，cmd->切换标签。

任何 java/scala 开发人员都知道使用 IDE 进行开发是多么有帮助，所以 IDE 爱好者鼓励我再试一次，幸运的是，我可以在 IntelliJ Idea 中进行一些配置更改，以与 iTerm 和 vim 的工作方式相同的方式使用 IDE 的所有其他好处。这些是

1.  在安装 IntelliJ Idea 时，我使用了黑暗主题(称为 Darcula ),让我在编码时有相同的外观和感觉。
2.  在 intellijIdea 中安装 vimPlugin(它会在安装时要求您启用它)
3.  Intellij Idea ->首选项->编辑增加和减少字体的键映射并添加 cmd+和 cmd -
4.  Intellij Idea ->首选项->编辑键映射添加 cmd + enter 用于“切换无干扰模式”
5.  编辑器制表符->选择下一个制表符将键盘快捷键修改为 cmd + ->
6.  对于选择上一个选项卡，请将键盘快捷键修改为 cmd +

通过这些小的调整，我拥有了我习惯于 vim 的所有 iTerm 特性和额外的 IDE 特性:-)