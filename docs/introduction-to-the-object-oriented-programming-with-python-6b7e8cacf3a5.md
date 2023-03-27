# Python 面向对象编程简介

> 原文：<https://medium.datadriveninvestor.com/introduction-to-the-object-oriented-programming-with-python-6b7e8cacf3a5?source=collection_archive---------10----------------------->

![](img/60914e987b771a5d02783b0abc5e2af9.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

在早期，编程就是直接写机器码，也就是 1 和 0 的二进制形式。随着计算机科学领域的进步，类似于英语的中级语言如 C 语言被引入。随着计算机程序长度的增长，程序员面临模块化的问题。由于 C 语言遵循单一的编码结构，程序员不可能合作编码。因此，面向对象编程的概念应运而生。今天，所有的高级语言都是 C++、Java、Python、PHP、Ruby、Javascript、C#等等。支持面向对象编程。在本文中，我们将使用 **Python 3** 作为编程语言来探索 OOP(众所周知的)。本文假设您熟悉编程的基础，比如 python 或任何其他高级编程语言。

# 什么是面向对象编程？

这个问题的答案只在于它的名字。顾名思义，OOP 就是关于对象的。编程中的对象类似于现实世界中的实体，例如汽车、学生、雇员。就像这个世界上所有的汽车都有一些共同的特征，像发动机、颜色、车门、变速器、燃料类型、制造年份等等。尽管所有这些特性的值可能因车而异。类似地，一个学生将有一些特征，如姓名、学号、家乡、专业、入学年份等。尽管所有这些特征的价值会因学生而异。同样，当我们想在我们的软件/程序中表现这样一个真实世界的实体时，我们将它们定义为一个**对象**。包含真实数据(姓名、卷号、家乡等值)的每个单独的唯一对象。在学生对象的情况下)被称为该对象的**实例**。OOP 中使用的一些常用术语解释如下:

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

## 类别:

类是定义对象的地方。一个类充当一个对象的蓝图。一个类包含一个对象的**属性**和**方法**。属性就是通常所说的编程中的变量。它们包含数据，例如，在学生对象中，属性可以是学生姓名、学号、专业、家乡、分数等。而方法就是编程中通常所说的函数。它们定义了对象的行为。例如，在 student 对象中，我们可以将一个方法定义为“result ”,它将返回特定学生获得的分数的百分比，将一个方法定义为“grade ”,它将基于获得的百分比返回要授予该学生的分数。让我们看看如何在 Python 中定义一个类。我们将坚持以学生为榜样。

```
 class Student:
       pass
```

上面的代码显示了`class`关键字用于声明一个类。按照惯例，类名的第一个字母大写。如前所述，如果没有属性和方法，类本身什么也做不了，所以让我们声明它们。

```
class Student:
      name = "John"
```

在上面的代码中，我们为 class Student 声明了属性“name ”,并赋予了它一个特定的值。现在我们将为这个类创建一个对象实例。

```
#initiate the Student class
student1 = Student()#print the name of the object
print(student1.name)Output:
---------------------------------------------------------------
>> John
```

## 构造函数方法:

在上面的代码中，我们在类本身中声明了学生的名字，但是如果我们想在运行时声明学生的名字，也就是在程序执行期间，该怎么办呢？为此，我们需要定义一个构造函数方法。在 OOP 中，构造函数是一种特殊的方法，用来初始化对象。在 python 中，`__init__`关键字是为构造函数方法保留的。每当实例对象被初始化时，`__init__` 方法被调用。

用构造函数方法声明该类:

```
#Declaring the class
class Student:
      def __init__(self,name):
          self.name = name#Initialize the object
#This time parameter is given at the time of initializing object
student1 = Student("John")#Printing the name of the object
print(student1.name)Output
-----------------------------------------------------------
>> John
```

在上面的代码中，我们遇到了一个新词`self` 需要注意的是`self` 在 python 语言中并不是一个保留关键字，但它是按约定使用的。当我们开始在我们的类中定义方法时，我们会学到它。让我们定义一个方法，用问候语显示学生的名字。

## 实例方法:

```
class Student:
      def __init__(self,name):
          self.name = name

      #defining the dispaly() method     
      def display(self):
          return print("Welcome to our academy ",self.name)#calling the display() method on student1 object
student1.display()Output:
-----------------------------------------------------------------
>> Welcome to our academy John
```

这里我们在类 Student 中定义了一个新的方法 display()。注意，`self`变量将对象 student1 的实例传递给类构造函数 __init__ 和方法 display()。让我们再创建一个相同类的对象。

```
#Initializing an object
student2 = Student("Sam")#Calling the method diplay() on object student2
student2.display() Output:
--------------------------------------------------------------------
>> Welcome to our academy Sam
```

从上面的例子中，我们可以看到，`self`变量将对象 student2 的实例传递给类构造函数和方法 display()，从而创建了一个带有新数据的新对象。

在这篇介绍性文章中，我们看到了什么是面向对象编程(OOP ),以及如何使用 Python 编程语言开始使用它。在接下来的文章中，我们将深入探讨 OOP 的高级概念，如继承、封装和多态。