# JavaScript 中的面向对象编程

> 原文：<https://medium.datadriveninvestor.com/object-oriented-programming-in-javascript-5b719738903e?source=collection_archive---------23----------------------->

[![](img/ab3a51f5ff74568a81a8cfe09bfd3cb4.png)](http://www.track.datadriveninvestor.com/IntelSplit)

昨天我们从 OOP 概念中学习了类和对象。今天我们将学习 JavaScript 中的继承和多态。

![](img/61632a1a641ad60466dd41f79e88692e.png)

credits: [https://de.123rf.com/](https://de.123rf.com/)

**传承！**

继承——我用一个例子来解释。

Gopi 和 Sudhakar 有两只手。两者的区别是他们的行为还是别的。所以，我们不用提两个人都有两只手两次。为此，我们将在类 Human 中创建一个变量，提到两者都有两只手。然后我们将分别创建 Gopi 和 Sudhakar 类。如果我们想提到 gopi 有两只手，我们可以通过从 Human 类中获取 Sudhakar 的数据。

所以基本上它是从基类继承的。利用继承，我们可以减少重复编写相同的代码。

看看代码，“extends”关键字用于从基类继承数据。super 函数用于从基类构造函数中获取变量。

**多态性！**

多态性——用于覆盖 JavaScript 中的方法。

让我们从一个例子中学习，

看看代码，play 方法写了两次，这就是所谓的“方法覆盖”。hockey.play()将执行 hockey 类中的函数，并提醒“dinesh 玩曲棍球”。

让我们尝试另一种方法，只是将 play()从曲棍球课中删除。那就不一样了。hockey.play()将首先检查 hockey 类中的 play 函数 play()不是在 Hockey 类中编写的。因此，它将检查基类中的 play()。警报将是“迪内什打板球”。

> 你快要说哇了！！！

明天我将探索封装和抽象。#加入我

D ay 10。这是我的博客，明天见！

[![](img/ab3a51f5ff74568a81a8cfe09bfd3cb4.png)](http://www.track.datadriveninvestor.com/IntelSplit)