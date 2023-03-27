# 使用 Python 中的多重处理加速 web 抓取

> 原文：<https://medium.datadriveninvestor.com/speed-up-web-scraping-using-multiprocessing-in-python-af434ff310c5?source=collection_archive---------0----------------------->

![](img/ea88eee520f54f10c95ca4b7572aa832.png)

# 什么是网络抓取

网络抓取是一种从网站上提取信息的计算机软件技术。这种技术主要关注于将 web 上的非结构化数据(HTML 格式)转换成结构化数据。

> 简而言之，它从网站上提取数据。

如果你不知道网页抓取，下面有一个手表。

# 多重处理的需要

当我们只处理一个 URL 时，多重处理可能不是很有帮助，但是当抓取多个 URL 来获取数据时，可以观察到性能的显著提高。

我们将首先看到一个没有多重处理的例子，然后将其与多重处理进行比较。

现在让我们运行这个脚本，并找出完成这个过程所需的时间

```
time python3 simple.py
```

下面是以下脚本的输出

```
200 [http://quotes.toscrape.com/page/1/](http://quotes.toscrape.com/page/1/)
200 [http://quotes.toscrape.com/page/2/](http://quotes.toscrape.com/page/2/)
200 [http://quotes.toscrape.com/page/3/](http://quotes.toscrape.com/page/3/)
200 [http://quotes.toscrape.com/page/4/](http://quotes.toscrape.com/page/4/)
200 [http://quotes.toscrape.com/page/5/](http://quotes.toscrape.com/page/5/)
200 [http://quotes.toscrape.com/page/6/](http://quotes.toscrape.com/page/6/)
200 [http://quotes.toscrape.com/page/7/](http://quotes.toscrape.com/page/7/)
200 [http://quotes.toscrape.com/page/8/](http://quotes.toscrape.com/page/8/)
200 [http://quotes.toscrape.com/page/9/](http://quotes.toscrape.com/page/9/)
200 [http://quotes.toscrape.com/page/10/](http://quotes.toscrape.com/page/10/)real    0m6.867s
user    0m0.424s
sys     0m0.069s
```

## 从这个输出中需要注意两件事

1.  所有链接按顺序执行(从第 1 页到第 10 页)
2.  实际花费的时间是 6.867 秒

## 现在让我们看看多处理提供了什么优势。

# **什么是多处理模块**

在我们的例子中，这个模块允许我们同时对多个 URL 进行抓取，从而节省了时间。

## 让我们来读一段官方文件的摘录

> `multiprocessing`是一个支持使用类似于`threading`模块的 API 生成进程的包。`multiprocessing`包提供了**本地和远程并发**，通过使用子进程而不是线程有效地避开了全局解释器锁。
> 
> 因此，`multiprocessing`模块允许程序员充分利用给定机器上的多个处理器。它可以在 Unix 和 Windows 上运行。

阅读更多官方[文档](https://docs.python.org/3.4/library/multiprocessing.html?highlight=process)

# 多重处理方法与常规方法的区别

1.  **从多处理导入池**

```
*from* multiprocessing *import* Pool
```

2.**初始化池**

```
p = Pool(10)
```

这个“10”意味着将同时处理 10 个 URL。

3.**调用函数 scrape**

```
p.map(scrape, all_urls)
```

这里，我们将函数 ***与 ***all_urls*** 进行映射，池 p 将负责并发执行它们中的每一个。***

这类似于在 simple.py 中循环遍历 ***all_urls*** ，但这里是并发执行的。

如果我们有比在 **Pool，**中指定的数量更多的 URL，那么它将花费一些迭代次数。

> 如果 URL 的数量是 100，并且我们指定了 Pool(20)，那么将需要 5 次迭代(100/20)，并且一次将处理 20 个 URL。

4.**呼叫终止()和加入()**

terminate()通常在主程序的可并行化部分完成时调用。

调用 join()等待工作进程终止。

# 使用多重处理时的结果

让我们并行运行这个. py

```
time python3 parallel.py
```

以下是以下命令的输出

```
200 [http://quotes.toscrape.com/page/2/](http://quotes.toscrape.com/page/2/)
200 [http://quotes.toscrape.com/page/1/](http://quotes.toscrape.com/page/1/)
200 [http://quotes.toscrape.com/page/3/](http://quotes.toscrape.com/page/3/)
200 [http://quotes.toscrape.com/page/7/](http://quotes.toscrape.com/page/7/)
200 [http://quotes.toscrape.com/page/4/](http://quotes.toscrape.com/page/4/)
200 [http://quotes.toscrape.com/page/5/](http://quotes.toscrape.com/page/5/)
200 [http://quotes.toscrape.com/page/9/](http://quotes.toscrape.com/page/9/)
200 [http://quotes.toscrape.com/page/8/](http://quotes.toscrape.com/page/8/)
200 [http://quotes.toscrape.com/page/10/](http://quotes.toscrape.com/page/10/)
200 [http://quotes.toscrape.com/page/6/](http://quotes.toscrape.com/page/6/)real    0m1.135s
user    0m0.381s
sys     0m0.119s
```

## 从这个输出中还需要注意两件事

1.  这次链接没有按顺序执行。你可以看到顺序是 2，1，3…这是因为多重处理，一个进程通过不等待前一个进程完成而节省了时间。这被称为并行执行。
2.  实际花费的时间是 1.135 秒，比正常执行少。此外，当 URL 数量增加时，这种差异会快速增长，这意味着多处理脚本的性能会随着 URL 数量的增加而提高。

所以现在你知道如何加快你的网页抓取脚本。亲自尝试一下，并在评论区给出你的反馈。

这里是关于 [Github](https://github.com/umangahuja1/Multiprocessing-Example) 的完整代码。

喜欢这篇文章，请随意表达你的欣赏👏👏👏。

如果你想看 python 相关的教程，可以访问我的 youtube 频道 [Get Set Python](https://www.youtube.com/c/GetSetPython) 。

[](https://www.youtube.com/c/GetSetPython) [## 获取设置 Python

### 享受 Python 带来的乐趣。厌倦了跟随教程，只是写一段代码，创建列表和做无聊…

www.youtube.com](https://www.youtube.com/c/GetSetPython)