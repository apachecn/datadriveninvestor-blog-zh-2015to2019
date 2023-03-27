# 如何通过命名变量和函数赢得有经验程序员的尊重|数据驱动投资者

> 原文：<https://medium.datadriveninvestor.com/how-to-earn-the-respect-of-experienced-programmers-by-naming-variables-and-functions-67706d37bfb6?source=collection_archive---------9----------------------->

如果你是一个有经验的开发人员，把这篇文章展示给初学者。

![](img/74890eab1d3ebf298464fb29b96f2b3d.png)

# 为什么变量和函数需要特殊的名字？

作为一名程序员，你必须以某种方式命名变量和函数。我们将在 Yandex 的[实习指南中探索命名变量和函数的艺术。](http://practicum.yandex.com)

在编程语言中，变量几乎可以是任何东西，比如“a”或“b”，甚至是“SuperImportantVariable3000”。函数也是如此:它们可以像 yo()一样非常短，也可以像 getnewpagenumberandnavigatetotatpage()一样非常复杂。如何命名变量和函数完全取决于你自己。事实上，现在大多数文本编辑器可以自动建议名字，所以你甚至不用记住它们。

[](https://www.datadriveninvestor.com/2019/03/25/a-programmers-guide-to-creating-an-eclectic-bookshelf/) [## 创建折衷书架的程序员指南|数据驱动的投资者

### 每个开发者都应该有一个书架。他的内阁中可能的文本集合是无数的，但不是每一个集合…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/03/25/a-programmers-guide-to-creating-an-eclectic-bookshelf/) 

然而，在命名变量和函数时，有三件事你必须考虑:

**两周内你会忘记你的代码结构。**如果你今天写一个程序，两到三周后再回头看，你需要花些时间记住不同代码片段的作用。因此，给变量和函数起一个能清楚解释它们做什么的名字会让你的工作容易很多。

**别人会用你的代码工作。**假设你写了一个很棒的程序，它运行得很流畅，你邀请其他人来开发它。现在他们必须明白这一点。如果你的变量和函数被很好地命名，你的同事会更容易看到一切是如何工作的，他们会帮助你。

这影响了你的就业。如果你决定成为一名程序员，你命名变量和函数的方式充分说明了你的专业技能。一个程序可能没有好名字的变量也能工作得很好，但是你可能得不到那份工作。

是时候了解如何以专业的方式命名变量和函数了。

# 如何命名变量

当你开始写代码时，你有简单的程序和简单的变量，比如“屏幕”、“分数”和“文本”。随着项目变得越来越复杂，变量也越来越多——“total score”、“totalScoreBefore”、“totalScoreAfter”和“totalScoreMaxProgressiveLimit”。让我们停下来沉思片刻。

变量名越长，就越难正确输入。自动建议可能会有所帮助，但是如果它不受支持，您的代码可能会因为输入错误而无法工作。

如果用 JavaScript 编写，风险会更大，因为 JavaScript 会动态生成新的变量。想象一下，你不小心输入了“totalScoreMaxProgresLimit”而不是“totalScoreMaxProgressiveLimit”——这个输入错误看起来并不奇怪。JavaScript 将用这个名称创建一个新元素，您将得到两个变量:正确的变量和输入错误的变量。你的程序会启动，但你无法预测它会如何运行。

这就是为什么你要尽量选择简短易懂而不深究的变量名。比如“totalScore”代表一场比赛的最终比分，“maxWidth”是最大宽度。如果您必须在不同的架子上、在组中或在其他包中存储大量变量，那么看看 JavaScript 中的对象和类，您将从中学习。

![](img/b422b563ef265d5a6d01448c19895514.png)

# 如何命名函数

函数是程序中使用的子程序。比如你可以写一个名为 getNumber()的函数，在一定范围内生成一个随机数。或者您可以使用 setTimer()在程序中的某个地方设置一个计时器，并使用该函数在给定的时间后触发一个动作。

函数可以简单地执行一个动作，也可以返回某个值、变量、数组或对象。例如，您可以在子程序中输入一行文本，然后编写一个算法将该文本翻译成外语；在这种情况下，该函数将返回翻译。

函数也可以随意命名，但通常情况下，它们看起来像这样:

shuffle():打乱数组元素。

saveScore():保存游戏的分数。

kill():停止某些东西。

spawn():创建一些东西。

loadDatabase():将数据库加载到内存中。

makeBackup():备份数据并可能将其保存在某个地方。

getSpeed():找出物体移动的速度并返回速度值。

getUserName():在发生某种情况后返回用户名。

getSessionId():返回会话号。

setTimeout():设置一个延迟时间，在此时间之后某件事情发生。

setSpeed():设置某物的速度。

您可能已经注意到，仅仅通过查看函数名，就可以很容易地判断出它做了什么以及它是否返回结果。例如，getScore()返回一个游戏的分数，setScore()设置分数但不返回任何内容，clearScore()重置分数但也不返回任何内容。

# 大写字母呢？

在编程中，函数和变量的命名有两种策略:camelCase 和 snake_case。

在 camelCase 中，具有多个单词的变量是通过将每个新单词的第一个字母用大写字母来命名的，如 getMoney、renderToFrame 和 removeFromBase。这是 JavaScript 的推荐方法。你应该注意 JavaScript 中的变量名和函数名是区分大小写的:getmoney 和 getMoney 是两个不同的函数。

Snake_case 用下划线将几个单词组合在一起。你会经常在 CSS 类中看到这种情况。例子包括 header_marginal 和 form_success。

选择你所使用语言的典型方式。请记住，其他人会阅读您的代码，他们将很难破译具有不寻常名称的函数和变量。

![](img/c617c95cb1f3dfc7dbe2e0bec04cb7f9.png)

# 要避免的变量和函数名

程序员不建议在变量名和函数名上发挥创造性，比如“crazyUnicorn”或 wonderfulWorld()。这些名字并没有告诉我们这些函数是做什么的，它们是否返回了什么，或者为什么首先需要它们。

然而，类似于“unicornCount”的东西是存储独角兽数量的变量的普通名称。initWorld()是一个在电脑游戏中创建世界的函数。

不要在函数和变量名中使用“函数”或“变量”这样的词。“MyVar”和 superFunction()是不好的名字，因为即使是你也会在两周内忘记它们的作用。

不要让名字有歧义，比如变量的“p”、“m”、“t”或“z”，或者函数的 hm()。这些名字太短了，无法清楚地描述任何东西。例外是当你写循环的时候:他们使用像“I”、“n”和“p”这样的变量来计算一个循环已经执行了多少次。这些变量被创建，完成它们的角色，然后在循环结束后立即被销毁。其他任何地方都没有引用它们。

一般来说:给变量和函数命名，就像你希望某个陌生人能读懂它们一样。