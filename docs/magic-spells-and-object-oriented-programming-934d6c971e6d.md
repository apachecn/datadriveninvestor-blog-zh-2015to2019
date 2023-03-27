# 魔咒和面向对象编程

> 原文：<https://medium.datadriveninvestor.com/magic-spells-and-object-oriented-programming-934d6c971e6d?source=collection_archive---------15----------------------->

你是否和我一样，一直为没有收到你的霍格沃茨来信而悲伤？你和我一样，是一个崭露头角的软件开发员吗？如果我在这里告诉你，虽然你没有魔杖，但你的指尖拥有比你可能意识到的更多的魔力——通过你的编程技巧！

![](img/30f15b135ad6e648b273456211b58a07.png)

Source: [https://giphy.com/gifs/harry-potter-ron-ss-HFdZPf52z9x4s](https://giphy.com/gifs/harry-potter-ron-ss-HFdZPf52z9x4s)

出于本文的目的，我将深入探讨面向对象编程的独特魅力。对于具体的例子，我将使用 Ruby 语言。

面向对象编程(OOP)是一种编程范例，其中代码中的所有内容都被视为一个对象。它模拟了现实生活，因为对象之间相互作用，以创建一个有凝聚力的程序——这与魔法如何用于与现实生活中的对象进行交互没有什么不同。

这到底是怎么回事？每个对象都是一个特定类的实例。类将它们的实例定义为具有某些属性或特征，这些属性或特征可以在整个程序中操作或使用。对象也有内置代码，也称为方法，允许您利用它们的属性或对对象采取行动，而不必真正编写任何代码来这样做。

![](img/432acc2f98b7560666306554083273ea.png)

Source: [https://giphy.com/gifs/harry-potter-applause-zeeYz6iGGoaA0](https://giphy.com/gifs/harry-potter-applause-zeeYz6iGGoaA0)

内置方法就像每个人在霍格沃茨第一年学习的基本咒语。它们出现在你的教科书中，从一开始就很容易使用(除非你是纳威·隆巴顿)。当你学习其中一个咒语时，你真正需要做的只是知道它的语法(说“Alohomora！”以特定的动作挥动你的魔杖)，并且知道你可以在什么类型的物体上施法(门/锁)。很简单，对吧？你不必像麻瓜那样做任何插入钥匙和转动钥匙的工作。内置方法也是一样。

假设你想得到一个数组的长度。你可能认为你需要做大量的工作，比如定义一个计数器变量，遍历数组中的每个元素，每次递增计数器。但是你没有！已经有一个咒语——我是说方法——为数组做这件事了！你所要做的就是简单地在数组上调用`.length`，数组的长度就会被返回。

这是因为`#length`是一个内置于 Ruby 中特定对象类的方法。它直接在您的 Charms 教科书中提供，或者在在线 Ruby 文档中提供(无论哪一个都是您选择的资源)。

![](img/e29dc8c237d4b8638e9aebad40d355fc.png)

Source: [https://giphy.com/gifs/hermione-granger-nB7m7qOvSQbXG](https://giphy.com/gifs/hermione-granger-nB7m7qOvSQbXG)

但是如果你想要完成的一些功能在你的教科书中没有出现呢？你可以建立自己的自定义法术，或方法！

西弗勒斯·斯内普，在他生命中的某个时刻，决定要有能力割破敌人的肉，让他们慢慢流血而死。那么他做了什么？他在 Person 类中构建了自己的自定义方法！我从未见过源代码，但我想象它是这样的:

```
class Person ... def sectumsempra(enemy)
    enemy.flesh.split("")
    self.dark_wizard = true
  endend
```

Person 类的每个实例都有一个设置为布尔值的属性`dark_wizard`。Person 对象总是用一个值为`false`的`dark_wizard`来实例化(如果您想知道的话)。因此，当 Person 类的实例调用`#sectumsempra`方法时，它们的`dark_wizard`属性的值被更改为`true`，原因很明显。

传递给该方法的参数应该是 Person 类的另一个实例。Person 对象也有一个名为`flesh`的属性，它指向一个 String 对象。String 对象有一个内置的方法`#split`，当用`(“”)`参数调用时，它允许你把字符串的组成部分分成一个数组。不幸的是，现在 Person 类的任何实例都可以作为`#sectumsempra`方法的参数传递。

![](img/2faba289215b7b0fc1e1aa59ea37b363.png)

Source: [http://harrypotterfanon.wikia.com/wiki/File:Harry_Potter_(Untold_Stories)-1485481831.gif](http://harrypotterfanon.wikia.com/wiki/File:Harry_Potter_(Untold_Stories)-1485481831.gif)

谢天谢地，斯内普好心地写了另一个方法，颠倒了`#sectumsempra`方法:

```
Class Person ... def vulnera_sanentur(enemy)
    enemy.flesh.join
    self.dark_wizard = false
  endend
```

在对`enemy`调用`#sectumsempra`之后，`enemy.flesh`现在是一个数组。数组有一个内置的方法`#join`，它将数组的元素组合成一个字符串。因此，`#vulnera_sanentur`方法可以让你治愈`#sectumsempra`方法造成的皮肉之伤。

`#vulnera_sanentur`还将调用该方法的实例的`dark_wizard`值设置为`false`，因为如果他们有心反转`#sectumsempra`，他们就不会那么糟糕。然而，这确实让人质疑哈利的`dark_wizard`属性值是什么，因为他自己在调用`harry.sectumsempra(malfoy)`之后并没有调用`#vulnera_sanentur`方法。也许他可以证明(不是双关语)是活在他身体里的伏地魔让他这么做的？

所有这些奇迹都是由面向对象编程的范例实现的。它允许我们与代码进行交互，就像我们对现实生活中的物体施魔法一样。所以不要再认为自己是麻瓜或者哑炮了。把自己想象成编程的女巫或巫师。

![](img/ea04e78202003e918ad9c30049cc6393.png)

Source: [https://giphy.com/gifs/harry-potter-magic-hermione-granger-gT8F4peUvNYUo](https://giphy.com/gifs/harry-potter-magic-hermione-granger-gT8F4peUvNYUo)