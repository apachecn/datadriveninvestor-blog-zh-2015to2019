# 如何将 Tensorflow 估算器转换为 Tensorflow Lite

> 原文：<https://medium.datadriveninvestor.com/how-to-convert-a-tensorflow-estimator-to-tensorflow-lite-a3509a9ba902?source=collection_archive---------3----------------------->

[![](img/19351b98f8b6c189202bbc12b067a63b.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/190406d4b1b138b85c9f2ad3d8e24ca5.png)

这将会是一篇更加直白的，指导手册式的文章。通常，我会尝试深入解释和类比。在这种情况下，我觉得做这种转换的简单指南可以帮助人们避免我遇到的陷阱。有相当不错的 Tensorflow 文档，但它并没有涵盖所有内容。

* * *注:Tenorflow 正在升级。这些说明适用于 Tensorflow 1.12***

这里假设您构建了一个 Tensorflow 估算器，您需要以某种方式将其导出到 Tensorflow Lite，以便您可以在移动设备上轻松运行它。

你要知道，步骤其实很简单。但是通过查看文档，您可能不知道。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？-数据驱动型投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

您首先需要的是一个服务输入接收器功能。基本上，这将暴露模型图的一些节点，以便我们可以提供数据并对其进行预测。同样，文档对此进行了详细描述，但您真正需要的是:

```
*def* serving_input_receiver_fn():
  features = { 'x': tf.placeholder(
    *shape*=[1, 28, 28, 1], // input shape with batch size 1
    *dtype*=dtype) 
  } return tf.estimator.export.ServingInputReceiver(
    features, 
    features
  )
```

定义了服务输入接收器后，您现在可以使用 Estimator 提供的这种方便的方法:

```
model = tf.estimator.Estimator(
  *model_fn*=cnn_model_fun, 
  *model_dir*=model_dir
)model_dir = "/somedir/" // location of modelmodel.export_saved_model(model_dir, serving_input_receiver_fun)
```

这将在与您的模型相同的目录中的一个生成目录中自动创建一个保存的模型。该目录将是一个生成的时间戳。

这个占位符操作所做的是向您的模型图添加一个带有标签“placeholder”的节点在下一步中，我们需要该名称将模型转换为 Tensorflow Lite。

```
tflite_convert --saved_model_dir=/somedir/123456 --input_shapes=1,28,28,1 --input_arrays=Placeholder --output_arrays=softmax_tensor --output_file=/somedir/model.tflite
```

注意，我们将占位符 op 传递给了 input_arrays。对于 output_arrays，您应该已经定义了某种预测操作，并且最好给它一个标签。可以输出多个预测操作。我在做这件事时遇到了问题。我建议只输出你的模型的 softmax 版本。由此，您可以生成任何其他所需的分析形式。

就是这样。遵循这些步骤应该会在您的计算机文件结构中生成一个漂亮的小 model.tflite 文件。您可以从那里将其直接移动到移动项目的资源中。

我想说这一切都是在走下坡路，而且大部分情况下都是如此，特别是因为现在您不会再看到服务输入接收器函数、占位符 op 和 export_saved_model 函数，同时会挠头想知道您是否搞砸了什么，为什么没有更简单的方法。但是，你必须等待。稍后我将写一篇文章，介绍我的 Tensorflow 应用程序，首先是 Android，然后是 iOS。因此，我预计在每个平台的部署过程中会有一些陷阱。

谢谢，如果你遇到任何麻烦，请在下面随意评论，我会尽我所能帮助你！