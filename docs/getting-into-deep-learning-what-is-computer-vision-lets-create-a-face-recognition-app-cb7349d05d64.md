# 进入深度学习，什么是计算机视觉？让我们创建一个人脸识别应用程序！

> 原文：<https://medium.datadriveninvestor.com/getting-into-deep-learning-what-is-computer-vision-lets-create-a-face-recognition-app-cb7349d05d64?source=collection_archive---------40----------------------->

![](img/0a941b0303f2e7617848803c154849f0.png)

# 星球大战+韩 Solo +人工智能！

最近在一篇文章上看到有人用人工智能把哈里森·福特插入电影:**《Solo:一个星球大战的故事》**。它使用深度学习人工智能，分析给定个人的大量照片，在这种情况下，哈里森·福特，然后创建一个多种位置和姿势的图像数据库。这项技术然后使用该数据库智能地对源剪辑执行自动人脸替换。你好新世界！

开始是对学习数据科学、Python 库及其解决业务问题的算法的兴趣，变成了对理解机器学习、计算机视觉和识别图像中的人脸的渴望！

每次我读一篇关于数据科学的文章，都会看到这些新词。所以我决定开始这个挑战，去更多地了解这个神奇的人工智能世界。

**但是什么是机器学习呢？**

我们可能看不到，但机器学习就在我们的手机里，在我们今天使用的产品里。在图片中标记人物听起来很熟悉？视频推荐系统？像网飞和脸书这样的大公司正在他们所有的产品中使用这项技术。机器学习包括一套算法，这些算法解析数据，从中学习，然后应用这些知识做出智能决策。你给计算机输入一套规则和任务，它就会找到完成这些任务的方法。

另一方面，计算机视觉是一种人工智能，它允许机器捕捉、处理和分析真实世界的图像和视频，以从物理世界中提取有意义的上下文信息。

如今，计算机视觉应用于医疗保健、农业、银行、汽车和工业等不同领域。计算机视觉技术正在帮助医疗保健专业人员准确地对可能通过减少或消除不准确的诊断和不正确的治疗来挽救患者生命的状况或疾病进行分类。农民们开始采用计算机视觉技术来监测农作物的健康状况。银行正在使用图像识别应用程序，这些应用程序应用机器学习来分类、提取数据和验证文档。

昨晚我读了一篇关于人工智能的文章，文章说中国杭州的一所学校正在使用面部识别来监控学生的行为。这项技术根据学生的情绪范围对他们进行分类，从反感到高兴。该系统还根据学校数据库交叉检查所有学生的面部，以标记出勤情况，并有能力预测学生是否感到不适。

因此，经过几个小时的尝试，获得了正确的 python 库，安装了视频编解码器并获得了一些视频，我将向您展示在视频文件上运行人脸识别的结果。

我用的是布拉德·皮特和詹妮弗·安妮斯顿的视频。得到了每个人的照片，以教机器如何在视频中识别他们:

![](img/e4fe9e104018ddcdfbb2de4e1f2881ab.png)![](img/a38e1dd3e4e3973b7f5dec765a03c872.png)

多么令人难以置信的结果！从未想象过机器可以学会这样做，但今天计算机视觉和人工智能的现实是，机器需要人类的帮助才能获得更好的结果。