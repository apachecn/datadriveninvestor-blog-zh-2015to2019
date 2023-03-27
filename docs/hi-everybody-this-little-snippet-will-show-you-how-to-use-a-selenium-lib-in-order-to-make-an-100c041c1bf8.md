# 使用 Python 和 Selenium 实现 Web 抓取自动化的一小段代码

> 原文：<https://medium.datadriveninvestor.com/hi-everybody-this-little-snippet-will-show-you-how-to-use-a-selenium-lib-in-order-to-make-an-100c041c1bf8?source=collection_archive---------13----------------------->

![](img/ae77d8b4696c98916b99b912f0e3f66e.png)

“grayscale photo of dew on spider web” by [Rúben Marques](https://unsplash.com/@klaus_blaze?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**大家好**，这个小片段将向你展示如何使用 selenium 库来制作一个自动化的网络抓取工具，你可以用它来分析数据、寻找模式等等。

这个片段是许多其他片段中的第一个，每一个都将向您展示下一步，这个显示了网页中的自动连接，在这种情况下，是 facebook，下一个将向您展示如何使用漂亮的 soap 抓取网页，之后我们将下载数据并将其保存在数据库中，等等。

根据文档，selenium 包用于自动化来自 Python 的 web 浏览器交互，并用于进行自动化测试。

你可以在 https://pypi.org/project/selenium/的[找到更多信息](https://pypi.org/project/selenium/)

支持多种浏览器/驱动程序(Firefox、Chrome、Internet Explorer)以及远程协议。

**支持 Python 版本:Python 2.7，3.4+**

对于安装，您可以使用以下三个选项之一:

使用画中画:

**pip install -U selenium**

您可以从 PyPI 下载源代码发行版(例如 selenium-3.14.0.tar.gz)，将其解压缩，然后运行:

**python setup.py 安装**

最后，如果您正在使用 Anaconda:

**康达安装-康达锻造硒**

我们需要做的第一件事是导入我们将在这个代码片段中使用的库。

在这种情况下，对于第一步，最重要的一步是 selenium，我们将在这里进行自动连接。

在[38]中:

```
**from** **urllib.request** **import** urlopen **as** uReq
**from** **bs4** **import** BeautifulSoup **as** soup
**from** **datetime** **import** datetime, timedelta
**from** **selenium** **import** webdriver
**import** **time**
```

导入库之后，为了运行代码，我们需要选择正确的驱动程序来使用。

**Selenium 需要一个驱动程序来连接所选的浏览器。**

在这里，我们将使用铬，但许多其他可以使用。

你可以在这里找到司机:

```
[https://sites.google.com/a/chromium.org/chromedriver/downloads](https://sites.google.com/a/chromium.org/chromedriver/downloads)
```

您可以在 Selenium 项目的页面中找到更多信息。

安装 Chrome 驱动程序后，我们需要设置一些选项来运行它。

在[39]中:

```
options = webdriver.ChromeOptions()
options.add_argument('--ignore-certificate-errors')
options.add_argument("--test-type")
options.binary_location = "Your drive:\Your directory\chromedriver.exe"
driver = webdriver.Chrome("Your drive:\Your directory\chromedriver.exe")
```

下一步是设置我们将使用的 url，并通过驱动程序获取它。

在[40]:

```
my_url = 'https://www.facebook.com/'
```

在[41]中:

```
driver.get(my_url)
```

在我们的例子中，为了访问网页，我们需要填写一个表单，所以我们需要从相应的字段中获取 html ids。使用像 find-element_by_id 或 find_elements_by_xpath 这样的驱动方法很容易找到它们。

在[42]中:

```
login = driver.find_element_by_id('email');      
senha = driver.find_element_by_id('pass');
```

在[43]中:

```
login.send_keys('your user')
senha.send_keys('your password')
```

在[46]中:

```
submit_button = driver.find_elements_by_xpath('//*[@id="loginbutton"]')[0];
```

在[ ]:

```
Now **is** just submit the information using the click method **and** <i>voilà</i>, we're in.
```

在[47]中:

```
submit_button.click()
```

在接下来的主题中，我们将学习如何使用 beautiful soap 获取数据，[将其存储在数据库中](https://medium.com/@alexandredallalba/persisting-sentiment-analysis-tweets-ce31acfeae8f)并使用一些工具(如 pandas、matplotlib、sklearn 等)对其进行分析。

享受代码，如果你想改进它！

# 再见！！！！