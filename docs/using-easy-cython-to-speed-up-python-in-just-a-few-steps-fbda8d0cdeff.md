# 使用 Easy Cython 只需几个步骤就可以加快 Python 的速度

> 原文：<https://medium.datadriveninvestor.com/using-easy-cython-to-speed-up-python-in-just-a-few-steps-fbda8d0cdeff?source=collection_archive---------1----------------------->

![](img/0274cd4dd9cb243ef91fca858be721ea.png)

对 python 的一个核心批评是，因为它是一种[解释语言](https://medium.com/@DHGorman/a-crash-course-in-interpreted-vs-compiled-languages-5531978930b6)，所以为了灵活性牺牲了性能。关于是使用 C、Go 或 Rust 等编译语言还是 Python、Ruby 或 Perl 等解释语言的争论由来已久，几乎与编程本身一样久远。

我是 python 的超级粉丝，原因有很多，比如它庞大的社区、易读性、大量的框架和库，以及易用性。使用 tornado、Flask 或 Django 制作一个后端 api 只需要几个小时，而不是几个星期。在学习了 [Flutter](http://flutter.dev) / Dart 并习惯了它的解释器/编译器组合后，我开始寻找一种方法来对我用 Python 写的后端服务器代码做同样的事情。我偶然发现了一个叫做 Cython 的便利工具，它似乎是面向科学界销售的，但是解决了翻译速度慢的问题。

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言|数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

Cython 取 python 代码，编译成 C 代码，再编译成机器码。因此，它以典型的 C 速度运行。起初，我持怀疑态度，但在我为 [Chromatic](http://chromatic.fm) 开发的音频代码转换工具上运行后，我发现速度提高了 8 倍，只需对我现有的代码做一些修改。虽然你可以用完整版的 [Cython](https://cython.org) 获得超级定制，但我最喜欢的快速入门工具叫做 [EasyCython](https://pypi.org/project/easycython/) ，你可以使用 pip 获取它。

![](img/27d785680a6e7aa891d037a18a686137.png)

Cython

Cython 允许您将模块转换成 C，然后像导入常规 python 模块一样导入它们。

首先，用 pip 安装 EasyCython:

**$ pip 安装 easycython**

或者如果您使用 python3:

**$ pip3 安装 easycython**

然后重命名要加速的文件。py 扩展名转换为. pyx 扩展名。然后运行以下命令之一:

**$ easycython myfile.pyx**

或者

**$ easycython *。pyx**

EasyCython 将自动完成所有需要的设置，包括创建新的。c 文件以及。所以还是。pyd 文件。c 文件编译成。就这么简单。如果您已经导入了整个文件，您应该可以开始了:

**导入我的文件**

如果您只导入了文件的一部分，您需要修改它以导入整个文件，例如:

**从我的文件导入我的类**

应改为:

**导入我的文件**

还要记住，python 对文件夹的处理很奇怪，所以我在尝试导入子文件夹中的 Cython 化文件时遇到了一些问题，所以现在我所有的 Cython 文件都在根文件夹中。不是最漂亮的结构，但速度提高了 8 倍，我现在就要它了。

如果你想得到更多的定制，你可以使用普通的 Cython，它增加了设置 setup.py 的步骤(这部分 EasyCython 会自动为你完成)。为此，在您的根项目文件夹中创建一个名为 setup.py 的文件，我们可以使用 distutils 来指向我们的模块。

```
**from** distutils.core **import** setup
**from** Cython.Build **import** cythonize

setup(
    ext_modules = cythonize("helloworld.pyx")
)
```

要对整个文件夹执行此操作，我们需要执行以下操作:

```
**from** distutils.core **import** setup
**from** Cython.Build **import** cythonize

setup(
  name = 'MyProject',
  ext_modules = cythonize(["*.pyx"]),
)
```

或者如果您想要指定特定的文件:

```
**from** distutils.core **import** setup
**from** distutils.extension **import** Extension
**from** Cython.Distutils **import** build_ext

ext_modules=[
    Extension("transcoding", ["transcoding.pyx"]),
    Extension("logic", ["logic.pyx"]),
]

setup(
  name = 'MyProject',
  cmdclass = {'build_ext': build_ext},
  ext_modules = ext_modules,
)
```

为了进一步提高速度，你还可以[在你的。pyx 文件，但这不是必需的。我个人没有测试过你通过添加类型获得的速度提升，所以我不能保证能快多少。](https://cython.readthedocs.io/en/latest/src/quickstart/cythonize.html)

值得注意的是，这种方法只适用于导入，所以不要试图将你的整个项目 cythonize。例如，您不能使用普通的 python 命令运行. pyx 文件，因此可以使用它来加速项目中需要大量重复的部分，比如我的例子中的代码转换。尝试不同的设置，看看什么适合你。我想您会惊喜地发现，只需在 python 代码中添加这一小步，性能提升是多么容易和多么微小。

下面是 Calen Hattingh 在 [PyCon Australia 制作的精彩视频，深入探讨了 Cython 实现速度提升的过程和细节。](https://www.youtube.com/watch?v=NfnMJMkhDoQ)