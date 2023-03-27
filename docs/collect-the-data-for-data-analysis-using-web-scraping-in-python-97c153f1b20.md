# 使用 Python 中的 Web Scraping 收集用于数据分析的数据

> 原文：<https://medium.datadriveninvestor.com/collect-the-data-for-data-analysis-using-web-scraping-in-python-97c153f1b20?source=collection_archive---------2----------------------->

[![](img/30b1489fafa1bfbd75ae67c5a327c214.png)](http://www.track.datadriveninvestor.com/1B9E)

这篇文章是关于如何在 Linux 环境下开始从网站上自动抓取数据，然后使用它从数据中发展一些洞察力。我们要刮 craigslist.org 网站

## TL；速度三角形定位法(dead reckoning)

按照这个链接，并获得源代码文件夹。→[https://github.com/jayeshmanani/Web-Scraping-Using-Scrapy](https://github.com/jayeshmanani/Web-Scraping-Using-Scrapy)

[](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) [## 为什么数据将改变投资管理——数据驱动的投资者

### 有人称之为“新石油”虽然它与黑金没有什么相似之处，但它的不断商品化…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) 

*我不建议从任何网站上抓取任何东西。此贴仅供学习之用。不要误用它。最好使用 API 从任何网站收集数据，如果他们提供相同的。*

![](img/24864b6c115dcd1312ad192e5d1b81ff.png)

Ref — [https://cdn-images-1.medium.com/max/2400/1*f2-zeAOSNB4RGlqH9emTlQ.jpeg](https://cdn-images-1.medium.com/max/2400/1*f2-zeAOSNB4RGlqH9emTlQ.jpeg)

希望你的机器上已经安装了 Python。

首先，我们为这个项目设置虚拟环境。因此，处理依赖性会更容易。

为了创建虚拟环境，您可以首先创建存储文件的目录

因此，在你想要的位置/目录创建一个文件夹，命名为你想要的名字。

如果您使用的是 Linux，您可以使用终端并按照步骤操作。

我正在桌面上创建一个名为 Scrapy_Project 的文件夹。(我用的是 Linux)

```
mkdir ~/Desktop/Scrapy_Project
```

现在，使用 Linux 命令移动到我们刚刚为项目创建的目录

```
cd ~/Desktop/Scrapy_Project
```

现在，我们将使用下面提到的命令在文件夹中创建虚拟环境

```
python3 -m venv venv_scrapy
```

现在，你可以看到有一个新的文件夹出现在你的项目文件夹 Scrapy_Project 中

您可以使用命令检查当前目录中的文件和文件夹列表

```
ls
```

现在，我们激活使用命令创建的虚拟环境

```
source venv_scrapy/bin/activate
```

现在，你可以看到在你的 Linux 用户名之前你会看到环境名。

所以，我们已经成功地激活了虚拟环境。

您可以在最后使用命令停用虚拟环境

```
deactivate
```

现在从安装和使用 Scrapy 开始学习使用 Scrapy 框架。

```
pip install scrapy
```

成功安装框架后，您可以继续使用命令开始我们的第一个 Scrapy 项目

```
scrapy startproject myFirstScrapy
```

这将创建一个名为 myFirstScrapy 的新文件夹，其中包含一些预定义的文件。

现在进入刚刚创建的 myFirstScrapy 文件夹

现在我们要创建一个蜘蛛，它可以使用命令抓取网页

```
scrapy genspider jobs [www.mumbai.craigslist.org/search/eve](http://www.mumbai.craigslist.org/search/eve)
```

现在，您可以在名为 jobs.py 的 myFirstScrapy/spider 目录中找到这个蜘蛛

现在，在您选择的任何文本编辑器中打开 jobs.py 文件。

你会发现一些预定义的东西。

编辑 start_urls，将此 URL 放在已经提到的= = '[https://mumbai.craigslist.org/search/eve'](https://mumbai.craigslist.org/search/eve')
的位置，并在允许的域名中添加替换此链接= =>'[www . Mumbai . craigslist . org '](http://www.mumbai.craigslist.org')

现在它看起来会像

```
*import scrapy**class JobsSpider(scrapy.Spider):
 name = ‘jobs’
 allowed_domains = [‘*[*www.mumbai.craigslist.org'*](http://www.mumbai.craigslist.org')*]
 start_urls = [‘*[*https://mumbai.craigslist.org/search/eve'*](https://mumbai.craigslist.org/search/eve')*]**def parse(self, response):
 pass*
```

这里 start_urls 是你的刮刀开始刮削工作的 U。

现在，将这一行添加到 jobs.py 中的解析函数中

```
print(‘Extracting…’ + response.url)
```

这将打印它正在解析的 Url 的名称

现在将这段代码添加到解析函数中。这将获取所有带有类结果标题的 CSS 元素。它会将 titles 变量中的元素存储为一个列表。

```
titles = response.css(‘a.result-title::text’).getall()
```

现在做一个循环，并使用枚举器一个接一个地打印名字，以便将计数打印出来。

```
*for serial_number, title in enumerate(titles):
 print(serial_number, title)*
```

整个 jobs.py 文件看起来就像下面的代码片段。

```
*# -*- coding: utf-8 -*-
import scrapy**class JobsSpider(scrapy.Spider):
 name = ‘jobs’
 allowed_domains = [‘*[*www.mumbai.craigslist.org'*](http://www.mumbai.craigslist.org')*]
 start_urls = [‘*[*https://mumbai.craigslist.org/search/eve'*](https://mumbai.craigslist.org/search/eve')*]**def parse(self, response):
 print(‘Extracting…’ + response.url)**titles = response.css(‘a.result-title::text’).getall()**for sr_no, title in enumerate(titles):
 print(sr_no, title)*
```

现在，您可以进入终端，使用命令开始抓取将要发生的事件的标题

```
scrapy crawl jobs
```

这将在终端中打印姓名和计数

如果您想要将 JSON 文件或 CSV 文件作为输出，您可以使用此步骤

在循环开始之前添加这一行

```
result = dict()
```

现在在循环中添加如下代码

```
*for sr_no, title in enumerate(titles):
 print(sr_no, title)
 result[‘sr_no’] = sr_no
 result[‘title’] = title
 yield result*
```

然后使用该命令再次启动 crawler

```
scrapy crawl jobs -o output.csv
```

最后，它将数据作为 output.csv 保存到项目文件夹中的 CSV 文件中。

做得对。恭喜你构建了你的第一个网络抓取工具。

请继续访问此处以获取更多此类帖子，并每天不断学习新的东西。

在此查找包含蜘蛛代码的 jobs.py 文件→

你喜欢这个职位吗？请在评论框中分享你的观点，或者给我留言→[https://jayeshmanani.github.io/#contact](https://jayeshmanani.github.io/#contact)

在 Github 上关注我→[https://github.com/jayeshmanani](https://github.com/jayeshmanani)

在 Medium 上跟随我→[https://medium.com/@jayeshmanani](https://medium.com/@jayeshmanani)