# 如何将 TensorFlow Lite 模型部署到 iOS

> 原文：<https://medium.datadriveninvestor.com/how-to-deploy-a-tensorflow-lite-model-to-ios-4b230bb91ac0?source=collection_archive---------1----------------------->

![](img/ba54ed6999f8ae349a07673f894ef6b7.png)![](img/cb452523242b7e7257ff9cc45326f9c1.png)

Photo by [Patrick Tomasso](https://unsplash.com/@impatrickt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这篇文章是我前两篇文章的延续:

1.  [如何将 TensorFlow 模型转换为 TensorFlow Lite](https://medium.com/@tylerwalker/how-to-convert-a-tensorflow-estimator-to-tensorflow-lite-a3509a9ba902)
2.  [如何将 TensorFlow Lite 模型部署到 Android 上](https://medium.com/@tylerwalker/how-to-deploy-tensorflow-to-android-feat-tensorflow-lite-957a903be4d)

本文的起始假设与(2)相同。也就是说，您有一个特定大小的输入数据数组，您有一个 TensorFlow Lite 模型，它有一个相同大小的占位符 op。我们过去部署在 Android 上的完全相同的模型也将适用于 iOS。

为此，您需要两个库，它们可以通过 CocoaPods 安装。如果你没有 CocoaPods，按照这里的说明安装:[https://developers.google.com/ios/guides/cocoapods](https://developers.google.com/ios/guides/cocoapods)。我想如果你在 Mac 上，你应该已经有了`pod`命令。

接下来，只需在项目的根目录下运行`pod install`。向 Podfile 中添加两行，以准备必要的 Firebase 依赖项:

```
pod 'Firebase/Core'
pod 'Firebase/MLModelInterpreter'
```

然后你可以运行`pod install`，可能会刷新 Xcode，这样一切都会变得干净。

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？-数据驱动型投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) 

此时，您实际上可以尝试构建并运行项目，Xcode 会输出各种错误，告诉您向项目注册 Firebase 等等。如果你连续处理每个错误，你最终会被设置好，但我还是会在这里列出步骤，只是因为我爱你。

所以在你的 AppDelegate 文件中，你会想把这一行添加到 didFinishLaunchingWithOptions:

```
FirebaseApp.configure()
```

您也可以在 Firebase 控制台中注册您的应用程序，但由于我们将使用本地模型文件，我不确定这一步是否有必要。更多信息请点击这里:[https://firebase.google.com/docs/ios/setup](https://firebase.google.com/docs/ios/setup)。

# 准备口译员

现在，您应该拥有了在 iPhone 上运行 TensorFlow Lite 模型所需的一切。

首先，添加。tflite 文件添加到项目中。右键单击项目结构，单击将文件添加到“我的项目”，然后添加文件。

首先导入我们之前添加的库:

```
**import** Firebase
**import** FirebaseMLCommon
```

并准备一些当地成员来担任翻译:

```
**var** model: LocalModel!
**var** interpreter: ModelInterpreter!
**var** ioOptions: ModelInputOutputOptions!
```

在 viewDidLoad()中，我们将进行一些初始化。我创建了这个函数，它返回一个表示模型是否成功加载的布尔值:

```
**private** **func** loadModel() -> Bool {
  **guard** **let** modelPath = Bundle.main.path(forResource: "model", ofType: "tflite")
  **else** {
    *// Invalid model path* print("invalid model path")
    **return** **false** } model = LocalModel(
    name: "model",
    path: modelPath
  ) **let** registrationSuccessful = ModelManager.modelManager().register(model) **if** (!registrationSuccessful) {
    print("registration failed")
    **return** **false** } **return** **true** }
```

如果模型初始化进展顺利，我们将继续实例化一个解释器:

```
**private** **func** buildInterpreter() {
  **let** options = ModelOptions(remoteModelName: **nil**, localModelName: "model")
  **let** _interpreter = ModelInterpreter.modelInterpreter(options: options)
  **let** _ioOptions = ModelInputOutputOptions() **do** {
    **try** _ioOptions.setInputFormat(index: 0, type: .float32, dimensions: [1, 28, 28, 1])
    **try** _ioOptions.setOutputFormat(index: 0, type: .float32, dimensions: [1, 1000])
  } **catch** **let** error **as** NSError {
    print("error setting up model io: \(error)")
  } // initialize members
  interpreter = _interpreter
  ioOptions = _ioOptions
}
```

我们可以在`ModelOptions()`中将`nil`传递给`remoteModelName`，因为我们使用的是本地模型文件，而不是托管文件。

# 准备输入数据

假设您有一个输入数据大小为 Int 或 Float 的数组`inputArray`，我们可以如下准备输入数组:

```
**let** inputs = ModelInputs()**var** inputData = Data()**for** pixel **in** inputArray {
  **var** f = Float32(pixel)
  **let** elementSize = MemoryLayout.size(ofValue: f)
  **var** bytes = [UInt8](repeating: 0, count: elementSize)
  memcpy(&bytes, &f, elementSize)
  inputData.append(&bytes, count: elementSize)
}**do** {
  **try** inputs.addInput(inputData)
} **catch** **let** error {
  print("add input failure: \(error)")
}
```

# 运行模型

```
interpreter.run(inputs: inputs, options: ioOptions) {
  outputs, error **in
    guard** error == **nil**, **let** outputs = outputs **else** {
      print("interpreter error")
      **if** (error != **nil**) {
        print(error!)
      }
      **return** } do {
      **let** result = **try** outputs.output(index: 0) **as**! [[NSNumber]]
      **let** floatArray = result[0].map {
        a **in** a.floatValue // get out the float value
      } **let** top = intArray.max()
      **let** label = intArray.firstIndex(of: top!)! + 1
    } catch { // error }
 }
```

就是这样！您需要将输出的标签与某种文本文件进行比较，并获取与之相关的数据。我会把有趣的事情留给你。

此外，我刚刚在 App store 上发布了一个应用程序，利用了这项技术。它被称为汉字阅读器，用于拍摄汉字(日本字符)并立即获得其读数和翻译。对学习语言和努力学习汉字的人有用。

这里是任何感兴趣的应用商店链接:【https://itunes.apple.com/us/app/kanji-reader/id1457506025? mt=8

下一次，我将从人工神经网络(ANN)技术和数据生成的角度，更详细地介绍我是如何完成这个应用程序的。谢谢！