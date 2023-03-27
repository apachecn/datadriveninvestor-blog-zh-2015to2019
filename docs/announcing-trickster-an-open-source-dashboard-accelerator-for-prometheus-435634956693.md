# 宣布 Trickster，普罗米修斯的开源仪表板加速器

> 原文：<https://medium.datadriveninvestor.com/announcing-trickster-an-open-source-dashboard-accelerator-for-prometheus-435634956693?source=collection_archive---------13----------------------->

[![](img/d4ad9d914d8f2a4aa60f806d8f4865fb.png)](http://www.track.datadriveninvestor.com/1B9E)

随着我们继续为我们的客户构建强大的微服务驱动的体验，我们越来越喜欢 [Prometheus](https://prometheus.io/) ，这是一款开源监控和警报工具包，最初由 [SoundCloud](https://soundcloud.com/) 开发，旨在提供对微服务架构的更大可见性。这就是为什么我们如此兴奋地宣布 [Trickster](https://github.com/Comcast/trickster) ，这是我们开发的一个新的开源工具，可以让普罗米修斯仪表盘运行得更流畅更快。

微服务对于我们如何向客户提供服务至关重要。我们的一流视频平台 X1 是在微服务平台上设计和构建的，我们开创性的家庭 Wi-Fi 体验 Xfinity xFi 也是如此。我们从微服务的经验中了解到，监控和警报是一项基本功能，Prometheus 提供了一个优雅的解决方案。

我们也很快意识到，对于普罗米修斯驱动的仪表盘，速度至关重要。

仪表板上多几秒钟的响应时间就可能成为一笔交易的破坏者。每当仪表板加载或重新加载时，许多仪表板都会从时序数据库请求整个时间范围的数据。这可能会导致渲染时间变慢，并且根据发出请求的时间而产生不同的结果。

Trickster 是内部开发的，最近开源了。Trickster 是用 Go 编写的，是 Prometheus HTTP APIv1 的反向代理缓存，它大大加快了从 Prometheus 查询的任何系列的仪表板渲染时间。这是可能的，因为增量代理、步长边界标准化和快进功能。

Trickster 的 delta 代理检查客户机查询的时间范围，以确定哪些数据点已经被缓存，并且只请求仍然需要的数据点来服务来自 Prometheus 的客户机请求。Prometheus 会在每次仪表板加载时查询小的增量更改，而不是数百个数据点的复制数据。通过步长边界标准化功能，Trickster 稍微调整了请求的时间范围，以确保由 Prometheus 返回的所有数据点都对齐。最后，通过 Trickster 的快进功能，无论下一步边界有多远，实时图表始终显示最新数据。

这些功能显著加快了图表加载时间。高度可缓存的数据以用户习惯的方式直观地传达给用户，并且所有仪表板用户在其显示器上看到一致的数据。本月早些时候，在费城举行的第一次 Prometheus meetup 活动中，Comcast 的软件架构师 James Ranson 讨论了 Trickster 是如何开发的，并向我们展示了该软件的现场演示。该活动在候选人办公室举行，其他几个现有的技术聚会也在这里举行。我们高度鼓励每个人使用、改进和回馈 Trickster。你可以在 https://github.com/Comcast/trickster 的[下载源代码。](https://github.com/Comcast/trickster)

普罗米修斯作为继 2016 年 [Kubernetes](http://kubernetes.io/) 之后的第二个托管项目，成为了 [CNCF](https://www.cncf.io/) (云原生计算基金会)的一部分。