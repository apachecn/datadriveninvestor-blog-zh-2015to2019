# 利用 Prodmodel 简化数据科学开发

> 原文：<https://medium.datadriveninvestor.com/easier-data-science-development-with-prodmodel-8e63b42f9c23?source=collection_archive---------15----------------------->

![](img/0a91143517074669cb3e5c2de490e976.png)

数据科学的发展是一个实验和迭代的过程。这涉及到大量的试验和错误，很容易忘记哪些已经过测试，哪些没有。下面的例子展示了我开发的开源数据工程工具 [Prodmodel](https://github.com/prodmodel/prodmodel) 如何帮助解决这些问题。它适用于 Python 3.5 或更高版本。

[](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) [## 成为数据科学家所需的 8 项技能|数据驱动型投资者

### 数字吓不倒你？没有什么比一张漂亮的 excel 表更令人满意的了？你会说几种语言…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) 

Prodmodel 背后的思想是将建模管道构建为 Python 函数调用。然后，该工具对这些函数返回的对象进行版本化、缓存和重用。这样，您就不必记住您正在试验的各种数据或模型文件或代码片段。

安装简单:`pip install prodmodel`

让我们假设您的项目在`project`文件夹中，一个`project/input.csv`文件，一个将它转换为训练数据特征的 Python 函数，以及另一个从中训练模型的函数。

`project/features.py`

```
def create_features(data):
    # Turn the raw data into model features
    return features
```

`project/model.py`

```
def train_model(features):
    # Train a model
    return model
```

Prodmodel 需要有一个`project/build.py`文件。该文件包含您的“构建目标”——对您想要版本化和保存的对象的引用。

```
from prodmodel.rules import rulesdata = rules.data_file('input.csv')features = rules.transform(
    objects={'data': data},
    file='features.py',
    fn='create_features'
)model = rules.transform(
    objects={'features': features},
    file='model.py',
    fn='train_model'
)
```

现在你可以运行`prodmodel build project:model`来训练你的模型。

这一切有什么意义？

1.  如果您只更改管道的部分——如模型训练部分，即`model.py`中的任何内容——并重新训练您的模型，Prodmodel 不会重新运行特征转换。相反，它重用以前缓存的版本。
2.  如果您更改了管道中的任何内容(比如添加一个新功能)，但没有成功，您可以恢复代码更改，Prodmodel 会自动切换回以前构建的版本。您不需要手动创建备份并恢复它们。只要切换回代码的完全相同的版本，您之前构建的所有内容都可以立即使用。

还有其他好处(比如 S3 集成)，我将在一系列文章中介绍。同时，查看这个[示例项目](https://github.com/prodmodel/prodmodel/tree/master/example)以获得该工具功能的更完整列表。

*原载于*[*https://dzone.com*](https://dzone.com/articles/faster-data-science-development-with-prodmodel)*。*