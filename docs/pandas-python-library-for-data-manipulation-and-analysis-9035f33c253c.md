# Pandas:用于数据操作和分析的 Python 库

> 原文：<https://medium.datadriveninvestor.com/pandas-python-library-for-data-manipulation-and-analysis-9035f33c253c?source=collection_archive---------16----------------------->

![](img/b52bcd23fc299ca449dcf83f5ff7ba29.png)

Photo by [chuttersnap](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*   [Pandas](https://pandas.pydata.org/pandas-docs/stabl) 是一个 python 模块，使数据科学变得简单而有效
*   Python 和熊猫被广泛应用于学术和商业领域，包括金融、神经科学、经济学、统计学、广告、网络分析等等。
*   用于在内存数据结构和不同格式之间读写数据的 It 工具:CSV 和文本文件、Microsoft Excel、SQL 数据库。
*   数据集的高性能合并和连接。
*   [笔记本](https://github.com/namratesh/Machine-Learning/blob/master/17_Dec_Pandas.ipynb)链接。

安装熊猫命令

```
**pip install pandas**
```

**进口熊猫**

![](img/9ce84d3309246ec502667c15232b31ae.png)

**Series** :是一个一维标签数组，能够保存任意数据类型(int、float、number、python 对象)。轴标签统称为索引。

![](img/539032a419aa3b08900ff6b96a58c06f.png)

*   pd.series 用于创建系列。

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

**DataFrame** :是二维或多维数组标记的数据结构，具有不同类型的列。

![](img/1ee9fc22d62c79483208c6f1200aaff2.png)

*   警察。DataFrame 用于创建 dataframe。

**序列和数据帧**有什么区别？

![](img/1300f97f88cd4a19a7c2a214214af854.png)

*   Series 是一维数组，其中数组是系列的集合。可以是两个或者更多。

让我们再创建一个数据帧

![](img/0b53d4c9e4fae878a23677641bab8280.png)

**连接数据帧**

![](img/1eeaaca09339dd29117d3625c90e862f.png)

我们正在使用 iris 数据集来了解更多关于熊猫的信息。

**加载数据集**

![](img/e4903b6d2651e6e0db2a61c5d651976f.png)

*   *pd.read_csv 用于加载数据集。*

**前 5 行**

![](img/9a4a94d5bb197eec8bd68f5b64992201.png)

**最后 5 排**

![](img/3b0eb33d7465e5993a26951ee682a238.png)

**标签:**从头到尾给出范围索引。

![](img/8e3ab9e1ae712f8a50e9726faea8c391.png)

**列:**它给出了列名。

![](img/dcfcec57fd770cdfb15bcf90a8d138e0.png)

**数据集的类型:**它给出了每一列的数据类型。

![](img/3e6fddb77c8af57e7eb27365eaa20fb4.png)

**数据形状:**给出行数和列数，

![](img/92315120ae80bdcef2e0cb6862fe84bc.png)

**信息数据集:**它给出数据类型和非空值计数。

![](img/682fae339934a4b6d532b21d738e7277.png)

**开始 10 行的选择**

![](img/b52e311bea976f96cc024840768699f0.png)

**选择除前 10 行之外的所有行**

![](img/b13e9708eee0e643247a574e52ab4ca0.png)

**最后 10 行的选择**

![](img/67c725f80e978589e3a7313fb52b5ade.png)

**每第 10 行的选择**

![](img/68a02f29e250057cdc02fe0b531d3d9a.png)

**选择列**

![](img/74ef591b829a44931a4b4ff864ca72b0.png)

**列的含义**

![](img/b46d86ad55d52de5e5c26b756e0b26be.png)

**列的标准偏差**

![](img/6db41983712b27f15e44eb01a56fc61c.png)

**列的中间值**

![](img/d4d7dc6e16f5bff623044065c7bd002d.png)

**数据集的统计汇总**

![](img/0ea3ecee370eaef69a5698f30e92042d.png)

**数据转置**

![](img/2d4a947a9798f3757958ca6330dfcf04.png)

**检查重复值**

![](img/09f74984d4c78e703c7cce2f0c814b53.png)

**按轴分类数据**

![](img/da1da833a324706a54d4339fe2ffed25.png)

**按值排序数据**

![](img/fb12dd3863742389142571cd6a10e45d.png)

**检查数据中的空值**

![](img/d415df60b7e3621cd96c449263e907da.png)

**如果缺少任何值，则删除一行**

![](img/c97d54707e2403bd0e19c9b055a267aa.png)

**如果行的所有值都丢失，则删除该行**

![](img/0de9322fa761f48f2ff071830554d055.png)

欢迎建议！！！