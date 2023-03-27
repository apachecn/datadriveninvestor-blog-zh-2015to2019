# Python 项目:每年 80 本书的阅读挑战

> 原文：<https://medium.datadriveninvestor.com/python-project-80-books-per-year-reading-challenge-88bfc281add?source=collection_archive---------18----------------------->

[![](img/140ef82f13dfa695d5f70b940addc251.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/7a00bda5b7d02235d350108202ba2cd2.png)

我喜欢阅读，从八岁起，我就开始从我读过的书中写出我最喜欢的诗句。

![](img/ed21a044fb10b647c4b551b364484d86.png)

我过去常常把它们写在我的 Moleskine 上，但后来觉得写在网上更有意义。从 2017 年开始，我一直用 Tumblr 代替。

2017 年，我定下新年决心，一年读 80 本书。我成功了，因为收获太大，我在 2018 年继续读了 80 本书。两年时间，我读了 160 本书。

![](img/ab52d08f2124fc4085602801c760e34b.png)

my most recent read in 01/26/2019\. I plan to continue the new year’s resolution in 2019.

读书本身是有益的，但我想分析我所读的内容。我想了解我的阅读习惯，我读什么类型的书，我最后写了多少引文。

我在 2018 年 6 月开始学习 Python，并制定了个人目标，在我的阅读书籍挑战上开始一个项目。

免责声明:我的编码并不完美。我写这篇文章的原因首先是为了得到反馈，希望能得到一些帮助！如果您能在评论区留下任何建议或提示，我将不胜感激:)

步骤 1:从 Tumblr 下载 blog posts(XML)

![](img/b959a90ce166878bb28ebd9a1a534715.png)![](img/dead4cbd3d243b9c38a88d460a790125.png)

步骤 2:从 XML 文件中提取文本

![](img/cba0a45e73c0dc6dc65359bb711e55c9.png)

步骤 3:遍历文本，使用 regex 查找书号、标题、作者、阅读日期和书籍引用的匹配项。

*注意:XML 文件比我想象的要混乱得多，所以有一些异常值(例外)。*

![](img/d945c8551b666fd431d1350c2d0808c9.png)

complete code [here](https://github.com/jiwon5315/Python/blob/master/Tumblr%20XML%20Data%20Cleaning.ipynb)

步骤 4:检查循环是否有效

![](img/8bfb3150c57f1df61b65128edeb27665.png)

14 articles from The New Yorker magazine were part of the list, which I excluded later.

步骤 5:创建一个熊猫数据框架

![](img/35cbe89aa2a7c9e37627a468e94b47c0.png)

第 6 步:通过找到所有的错误开始清理数据！

![](img/5178a2d3c38708abba3ab5468b11d8c2.png)![](img/fcca80897ff01d78e6aef6f75a410861.png)![](img/9395e407e30302461f7190e3099ba6fe.png)![](img/8306cbccaf818af86566bbbaf34d0d14.png)![](img/1f3085c0d22dfc17718f3bb030fef950.png)

第 7 步:从“图书报价”列，我循环使用一个正则表达式来计算有多少报价，并创建了一个新列。

![](img/a5f46d54000086253cdccbb4caf976a1.png)

第八步:一旦数据更加有组织，我对我的数据集做了三个假设。

![](img/bd483fa59c8deed92d3a6caeda4a28f0.png)![](img/15bfc341a4aed2bf35e65d7abfd4d95d.png)![](img/0ae47a86bc66c2455a91100964f6cce2.png)

第九步:测试假设。

*假设 1:我在 12 月读得最多。*

![](img/76df79caa02b736ea63d9989a35d139d.png)![](img/797916ab422b0a1726751139e172f651.png)![](img/1272a710ff2f2b5cc0cd16227df2388f.png)

结论——我*在十二月*读了更多的书。

假设 2:引用次数超过 10 次的书，情绪是正面的。(引用越多，正面越多)

![](img/7ba255ec3db0f583efbd4ddd5bb123cf.png)![](img/5ea2af502392462208367196dbab9dee.png)![](img/1fdaee540d11f2f09746b9a5a899433a.png)![](img/203f230b2de52da6dce9ff8ceba4bcae.png)![](img/ad4e7868d09b3bb4c1f6c5c87119aa7e.png)

结论——更多的引用并不意味着更多的积极情绪。

假设三:情感分最高的会是一本韩文书。

![](img/56da65acd849a0bbe0c8e3b5d07d77c0.png)![](img/a8cdb16e413131b3b2fb13c63c1ac4bb.png)

结论——关于一本韩国书的最高情感分数，我是对的，但我也错了。textblob 不能处理朝鲜语文本，只能提取英语单词。

**第十步:了解我的极限，放弃！**

意识到我需要将韩语文本翻译成英语，以便进行更公正、更少主观的分析，我尝试了(在我看来)所有的方法。我尝试了 textblob 翻译(这是最好的，但一直崩溃)，googletranslate，pytranslate 等。，但意识到我的技能与我的抱负不相称。

这与我最初想要的相差甚远。我想从最喜欢的作家中抽取前十个单词，也许是一个 ML 函数，我可以在其中键入书名，并根据我的阅读列表等来看看我是否会喜欢它。然而，我认为学习的一部分是有耐心。我的技能还没有达到那个水平，这没关系。一旦我的编码技能更好了，我希望回到这个项目，但在那之前，这是我正在进行的工作，是我学到了多少和我可以实现的可能性的指标。

我写这篇文章是希望作为你的下一个 python 项目，你会对任何书呆子感兴趣。我强烈推荐 80 本书阅读挑战作为旁注。

你可以在这里找到完整的代码。