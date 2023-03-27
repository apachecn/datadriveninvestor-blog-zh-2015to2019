# 如何将 TensorFlow 部署到 Android (feat。TensorFlow Lite)

> 原文：<https://medium.datadriveninvestor.com/how-to-deploy-tensorflow-to-android-feat-tensorflow-lite-957a903be4d?source=collection_archive---------0----------------------->

[![](img/b88e2ceec034ca38502086e14f550c60.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/190406d4b1b138b85c9f2ad3d8e24ca5.png)

在本文中，我将假设您有一个我在上一篇文章中讨论的表单模型，标题为[如何将 TensorFlow 估算器转换为 TensorFlow Lite](https://medium.com/@tylerwalker/how-to-convert-a-tensorflow-estimator-to-tensorflow-lite-a3509a9ba902) 。这一次，我们将研究如何将 TensorFlow Lite 模型融入 Android 项目的细节。

您首先需要的是 TensorFlow Lite 依赖项。我用的是 1.12，因为这是我用来转换模型的同一个版本。我知道事情正在迅速升级，但是那个版本是稳定的并且相当实用:

```
implementation 'org.tensorflow:tensorflow-lite:1.12.0'
```

您将面临的关键问题是如何格式化 TensorFlow Lite 解释器的输入和输出，以便所有内容都通过占位符 op 传递并正常工作。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？-数据驱动型投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

你需要做的第一件事是拖动你的。将 tflite 模型转换成 Android 资产。完成这些后，TensorFlow 代码示例为我们提供了这个方便的函数，可以读入解释器喜欢的格式的文件。

```
fun loadModelFile(path: String): MappedByteBuffer {
    val fileDescriptor = *assets*.openFd(path)    

    val inputStream = FileInputStream(fileDescriptor.*fileDescriptor*)
    val fileChannel = inputStream.*channel* val startOffset = fileDescriptor.*startOffset* val declaredLength = fileDescriptor.*declaredLength* return fileChannel.map(FileChannel.MapMode.*READ_ONLY*, startOffset, declaredLength)
}
```

然后，您可以初始化 TensorFlow Lite 解释器:

```
interpreter = Interpreter(*loadModelFile*("model.tflite"))
```

现在，您需要的只是适当的数据结构来保存解释器的输入和输出。很可能你会有某种代表输入图像的 2D 数组。在我的例子中，预先格式化的数据是一个浮动数组。这需要分配给一个字节缓冲区。我使用这些实用方法来简单地做到这一点:

```
val inputBuffer = ByteBuffer.allocateDirect(4 * 40 * 40)
  .*apply* **{** order(nativeOrder()) **} // 40x40 is my input size, with 4 bytes per float**// clear the buffer and replace w/ input data
fun FloatArray.unwindToByteBuffer() {
  inputBuffer.rewind()
  for (f in this) {
    inputBuffer.putFloat(f)
  }
}
```

有了输入数据结构，我们只需要一个地方来保存输出。如果您遵循我在上一个教程中的建议，您的模型将只输出 SoftMax 张量，以下输出数据结构就足够了:

```
val outputArray = *arrayOf*(FloatArray(2000))
```

请注意，这是一个数组，其大小对应于模型中标签的数量。现在，我们已经准备好运行模型并得出我们的预测:

```
interpreter.run(inputBuffer, outputArray)// Pair<Label, Likelihood>typealias Prediction = Pair<Int, Float>fun getTop10Predictions(output: FloatArray): List<Prediction> {
    val predictions = *mutableListOf*<Prediction>()

    output.*forEachIndexed* **{** index, fl **->** val prediction = (index + 1) *to* fl
        val (currentLabel, currentLikelihood) = prediction

        if (predictions.size < 10) {
            predictions.add(prediction)
        } else {
            val shouldReplace = predictions.*find* **{** val (label, likelihood) = **it** likelihood < currentLikelihood
            **}** if (shouldReplace != null) {
                predictions[predictions.indexOf(shouldReplace)] = prediction
            }
        }
    **}** // log output
      predictions.*forEachIndexed* **{** index, prediction **->** val (label, likelihood) = prediction

          Log.d("TensorFlow Interpreter", "${index + 1}. Prediction: $prediction, Likelihood: $likelihood") **}**

    return predictions
}
```

对输出数组调用此函数，如下所示:

```
getTop10Predictions(output = output[0])
```

所以现在就这样了。我首先跳过了所有涉及如何获取浮点数据的内容。在另一篇文章中，我将介绍如何设置一个相机，并以浮动数组的形式将其输出转换为像素化数据。

希望这是有帮助的。我想提到的最后一件事是，对于那些对机器学习或日语(我知道，不寻常的组合)感兴趣的人，我刚刚向 Play store 发布了一个名为 Kanji Reader 的应用程序。它使用 TensorFlow 解码汉字图像，提供它们的阅读和翻译。

以下是 Play store 条目的链接:

【https://play.google.com/store/apps/details? id = Tyler walker . io . kanji reader

最终，我会一步一步地讲述我是如何做到这一点的，所以请继续关注我，获取更多的机器学习解释和例子。谢谢！

# 参考

1.  tensor flow for poets:[https://github . com/Google code labs/tensor flow-for-poets-2/tree/master/Android/TF lite](https://github.com/googlecodelabs/tensorflow-for-poets-2/tree/master/android/tflite)