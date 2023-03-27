# 治愈将 CSV 摄入 BigQuery 的痛苦

> 原文：<https://medium.datadriveninvestor.com/the-cure-for-the-pain-of-ingesting-csv-into-bigquery-12ed5c2a5e2a?source=collection_archive---------4----------------------->

[![](img/140ef82f13dfa695d5f70b940addc251.png)](http://www.track.datadriveninvestor.com/1B9E)

将 CSV 文件加载到 BigQuery？您必须至少遇到以下问题之一:

*   右双引号(")和字段分隔符之间的数据。
*   CSV 表遇到太多错误，放弃
*   无法将字段 Field1 的“Field1”解析为 double
*   不是 UTF 8 编码的
*   模式不匹配
*   在您的 CSV 文件中使用双引号“”

**您可能尝试过的解决方案:**

*   从 web 用户界面加载
*   使用命令行“bq load”加载
*   加载 python 代码
*   用 DML 语句加载
*   将 CSV 转换成 JSON，然后从 JSON 文件加载

*痛苦吗？抑郁？下来？感觉忧郁？*

*是的，我也是。*

**治愈将 CSV 摄入 BigQuery 的痛苦**

1.  将 CSV 文件从本地或云存储加载到 **DataPrep**

![](img/431e55da56082aba3337f3ea5c56c604.png)

2.运行一个作业将数据接收到 BigQuery 中

![](img/2ca3238186ebfac956947a100e60f0f4.png)

Choose a project of BigQuery

创建新表或加载到现有表中

![](img/78b0696bd1541213d35d527e54d7fe0a.png)

提交作业

![](img/c5548984761baa6b564f2b3bb71a77af.png)

数据流将选择作业并立即运行它

![](img/1b080d42f166d700be73265b550e6cb1.png)

3 作业完成后，从 BigQuery 检查表

![](img/1fb08d5959dc2722b1643fc42ad4c0d6.png)

搞定了。这张桌子多漂亮啊！无痛苦的伟大开发者体验！

总而言之，诀窍在于 Dataprep 在源数据要求方面比 BigQuery 更宽容，允许数据肮脏、混乱、丑陋、<whatever come="" to="" your="" mind="">等。</whatever>

按照下面的过程，你会看到没有雨的彩虹。

![](img/7bdcde7d89777268f3b4ac0479be4a5e.png)

## 来自 DDI 的相关故事:

[](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4) [## 数据科学和软件工程哪个更有前途？

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

medium.com](https://medium.com/datadriveninvestor/which-is-more-promising-data-science-or-software-engineering-7e425e9ec4f4) [](https://medium.com/datadriveninvestor/deep-learning-explained-in-7-steps-9ae09471721a) [## 用 7 个步骤解释深度学习

### 和猫一起

medium.com](https://medium.com/datadriveninvestor/deep-learning-explained-in-7-steps-9ae09471721a)