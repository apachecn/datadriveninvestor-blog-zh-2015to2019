# 优步价格飙升的旧金山实时地理定位地图。

> 原文：<https://medium.datadriveninvestor.com/real-time-mapping-of-geolocation-s-in-san-francisco-for-uber-price-surge-b0059f3e10a0?source=collection_archive---------0----------------------->

[![](img/f6a70f1638bd30603d22b4a6df136b09.png)](http://www.track.datadriveninvestor.com/1B9E)

我必须为我在数据科学项目中的当前学期构建一个数据工程产品。我对不同的想法进行了大量的头脑风暴，最终决定围绕优步出租车的价格飙升行为打造一款产品。价格飙升是我一直感兴趣的一个特征。

因此，我决定为我的产品构建两个功能，一个是实时绘制旧金山价格飙升的位置，另一个是对价格飙升行为进行批量分析或历史分析。

这对于优步的司机来说很有用，他们可以追踪价格上涨的地点，并在这些地区开车以赚取更多的钱。它还将帮助用户识别模式和安排他们的旅行。

我使用大数据技术堆栈来构建这个基础架构。一些主要组件是用于消息处理的 Kafka。处理实时数据的火花流。Spark Streaming 适合我的用例，因为它以微批处理的方式处理数据，并且定期刷新来自 UBER API 的数据。在 spark streaming 中进行处理和转换，然后将数据保存在 Hbase 中。使用 Apache Flask 构建了一个 web 框架，并使用 Google Maps API 来显示浪涌发生的实时位置。一旦实时处理完成，密钥就会更新，数据仅用于喘振行为的历史分析。

我喜欢从零开始构建系统，看到它运行起来会给我巨大的满足感。这学期是一次很棒的学习经历。

下面是我作品的链接。感谢任何反馈。

[https://github.com/deepnarainsingh/RiseInPrice](https://github.com/deepnarainsingh/RiseInPrice)