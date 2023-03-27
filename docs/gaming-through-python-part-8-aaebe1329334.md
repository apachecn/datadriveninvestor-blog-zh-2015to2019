# 通过 Python 玩游戏(第 8 部分)

> 原文：<https://medium.datadriveninvestor.com/gaming-through-python-part-8-aaebe1329334?source=collection_archive---------3----------------------->

[![](img/ad41842e12efd7cc7164191be5351280.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/ee696ab85dc944e4547890355c91b380.png)

Photo by [Sean Do](https://unsplash.com/@everywheresean?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在前面的部分中，我们让我们的城堡变得可以爆炸，并且增加了生命值和计时器。
(如果你错过了上一部分，请在这里 查看 [*。)*](https://medium.com/@asishraz/gaming-through-python-part-7-77a3a7f3226)

把之前的东西都加进去之后，我发现即使计时器归零或者你的健康归零了，游戏还在继续。有点无聊的东西。没有输赢的游戏不是游戏。现在我们将增加一些输赢的场景，使它更具互动性和趣味性。
我们将添加输赢条件，以及我们将添加输赢屏幕。
我们不会在主循环中编写代码，我们将创建一个 win/lose 循环，其中我们必须计算出用户是赢还是输，并相应地显示屏幕。

首先，我们将处理时间参数。也就是说，如果时间到了，那么我们必须停止游戏，并将游戏的结果设置为 1 或赢。
我们将游戏时间设定为 90 秒或 90000 毫秒。

第二，如果城堡被敌人摧毁，那么我们也必须停止游戏，并将游戏结果设置为 0 或失败。
而精度要重要得多，我们无论用哪种方法都要计算精度。
精度应该在 float，否则会将结果四舍五入。为此，我们将编写 **acc[0]*1.0** ，以便将 *acc[0]* 转换为浮点型。

现在我们必须在 game.py 文件的末尾编写这些代码:

# *section -10 —输赢检查*
>>>**if pygame . time . get _ ticks()>= 90000:
>>>running = 0
>>>exit code = 1
>>>if health value<= 0:
>>>running=0:
> > >精度= ACC[0]* 1.0/ACC[1]* 100
>>>其他:
> > >精度=0**
# *section -11 —输赢显示***>>>如果 exitcode==0:
>centex
>>>textrect . centey = screen . get _ rect()。centery+24
>>>screen . blit(game over，(0，0))
>>>screen . blit(text，textRect)
>>>else:
>>>py game . font . init()
>>>font = py game . font . font(Nonecentex
>>>textrect . centey = screen . get _ rect()。centery+24
>>>screen . blit(youwin，(0，0))
>>>screen . blit(text，textRect)
>>>while 1:
>>>for event in py game . event . get():
>>>if event . type = =退出:
>>>py game . QUIT()
>>>退出(0)
>>>py game . display . flip()**

有太多的线要看，但是当你一条一条地走的时候就很容易了。

我们可以在这里看到，第一个' *if* '语句检查时间是到了还是还在。
第二个“*if”*语句是检查你的健康状况还是城堡的健康状况。
第三个’*if’*语句是在寻找你的正确率。

然后在 *section-11* 中，会根据你的输赢状态显示屏幕。
赢图像为赢，输图像为输。

为了显示获胜的图像和失败的图像，我们必须在代码中加载图像。
在 **section-3** 的最后，我们要写加载图片的代码:
**>>>game over = py game . image . load(" resources/images/game over . png ")
>>>you win = py game . image . load(" resources/images/you win . png ")。**

这里有一件重要的事情，我们需要把第 4 节的 while 循环从

**while 1:
bad timer-= 1**

到

**>>>running = 1
>>>exit code = 0
>>>运行时:
>>>bad timer-= 1**

这个'*运行*变量会保持游戏的轨迹，不管游戏是否结束。
' *exitcode* '变量将跟踪玩家，无论他/她是赢了还是输了游戏。

最后，运行游戏，现在玩会更有感觉。

在下一部分，我们将添加音乐和其他音效，以获得更多的酷。
下一部将会超级棒。
感谢您阅读这篇文章

编码快乐！！！

# DDI 特色数据科学课程:

*   [**用于数据科学的 Python**](http://go.datadriveninvestor.com/intro-python/mb)
*   [**Scikit-Learn**](http://go.datadriveninvestor.com/scikitlearn/mb)
*   [**数据可视化**](http://go.datadriveninvestor.com/datavisualization/mb)

**DDI 可能会从这些链接中收取会员佣金。我们感谢你一直以来的支持。*