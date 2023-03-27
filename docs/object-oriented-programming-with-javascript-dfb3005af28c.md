# JavaScript 中的面向对象编程

> 原文：<https://medium.datadriveninvestor.com/object-oriented-programming-with-javascript-dfb3005af28c?source=collection_archive---------10----------------------->

![](img/61632a1a641ad60466dd41f79e88692e.png)

credits: [https://de.123rf.com/](https://de.123rf.com/)

Javascript 是一种面向对象的编程语言。因此，在 JavaScript 中，我们可以编写面向对象的编程。这就像 c++，我们可以不用对象来写程序。

> OOP 是什么？
> 
> 包含对象的程序被称为 OOP。

因此，如果任何语言支持面向对象，也将支持面向对象的概念。在这里，我喜欢陈述 OOP 中的 6 个概念，

1.  班级。
2.  对象。
3.  封装。
4.  遗产。
5.  多态性。
6.  抽象。

在这个博客中，我们将看到前两个概念。那就是类和对象。首先，我们将看到 JavaScript 中的类。

**上课！**

类是包含数据和方法的组。es6 版本中首次引入的 class 关键字。在使用不同的方法创建 es6 类之前。

我们创造了一个类人。在 person 类中，我们创建了一个构造函数和 getName 函数。“this”关键字引用构造函数的当前对象。因此，当为 person 类创建对象时，this.name 和 this.age 从对象中获取值。this.name 和 this.age 将只在 person 类中使用。

一旦创建了对象，就会执行一个构造函数，并通过该对象调用 getName。

**对象！**

基本上，对象是用来调用类内部的函数和数据的。它被称为类的实例。我们必须创建一个对象来使用类中的数据和函数。为一个类创建“n”个对象总是可能的。

这些对象是使用关键字“new”创建的。在上面的代码中，使用“new”关键字为 person 类创建的对象。对象将值传递给类内部的构造函数。

如上所述，我们为 person 类创建了对象，并将其赋给 obj 变量。尽可能多地使用变量“obj”调用类中的函数和数据。

在第二行中，使用 obj 调用 getName 函数，并在 alert 函数中传递它。因此，一旦 getName 被执行(调用),我们就可以得到一个警告。

如果你喜欢这个博客，我准备好听到一些掌声👏。

看看这篇博客的第二部分，是关于[继承和多态的。](https://medium.com/@dineshsmart101.dm/object-oriented-programming-in-javascript-5b719738903e)

9 年 9 月。这是我的博客，明天见！