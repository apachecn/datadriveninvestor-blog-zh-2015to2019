# 构建 JavaScript Mad 库

> 原文：<https://medium.datadriveninvestor.com/building-a-javascript-mad-libs-ab8c191f798c?source=collection_archive---------3----------------------->

![](img/fe1537bd428d100a2a81097688351bf5.png)

Photo by [David Menidrey](https://unsplash.com/photos/MYRG0ptGh50?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/halloween?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 大家好。本周我要谈论的是工伤、Hacktober 和一个 JavaScript MadLibs。

本周我在工作场所受了伤。我不能说得太详细，但我的手腕被强行向后弯曲。什么都没坏，但是有炎症和一些疼痛。对于想编码的人来说不太好！

2 我从【2018 年十月抢到了一件 t 恤！如果你不熟悉的话， [Digital Ocean](https://www.digitalocean.com/) 会奖励 10 月期间在 [GitHub](https://github.com/) 上至少提出 5 次拉请求的编码员一件免费衬衫。

起初我觉得我在编码方面太缺乏经验，但我看了看，发现了一些我理解的要求。感谢[Netuitive](https://github.com/Netuitive)/[Netuitive-statsd](https://github.com/Netuitive/netuitive-statsd)、 [VedVid](https://github.com/VedVid) / [RAWIG](https://github.com/VedVid/RAWIG) 和[dipakkr](https://github.com/dipakkr)/[A-to-Z-Resources-for-Students](https://github.com/dipakkr/A-to-Z-Resources-for-Students)接受我的投稿！

我用 JavaScript 完成了我的万圣节涂鸦。这是一种接受用户输入和/或使用预先填充的数据来告诉一个*幽灵的故事*的形式。

My JavaScript Mad Libs

**有什么好的:**

*   它接受用户的输入并把它放入故事中。
*   或者使用自动填充，它为故事使用预先填充的数据。
*   或者两者都有:如果用户感到厌烦&只填写了几个框，然后使用自动填充，他们的输入被使用，空框使用预填充的数据。
*   它可以适当地按比例缩小。
*   故事本身是一个放入 div 的变量。用户输入的每个单词都被放入 story 变量的不同跨度中。
*   我用了一些 BootStrap 让它看起来更漂亮。

**改进空间:**

*   我觉得 JavaScript 和 HTML 太臃肿了。
*   由于输入框是相似的，我觉得可能有一种方法可以使用循环来使代码更加简洁。
*   类似地，JavaScript 重复了许多类似的代码。我觉得应该有一种方法可以遍历它们，用一个变量(x)替换特定的数字(1 到 20)。
*   我可以写一些不同的故事，使用同样的 20 个输入框，但是每次打印不同的故事。

我仍在学习我的免费代码营课程。我刚刚完成了“React 和 Redux”的单元，并开始了单元项目的工作。