# 如何在 React 中传递状态

> 原文：<https://medium.datadriveninvestor.com/how-to-pass-state-in-react-e2945dcca324?source=collection_archive---------9----------------------->

[![](img/9156edc323d6b9ff4f540cf0bf88f52b.png)](http://www.track.datadriveninvestor.com/1B9E)

俗话说，除非你能教，否则你不会真正理解一件事。所以这里什么都没有…

要在 React you 中传递状态:

1.  设置一个反应组件。

![](img/702bf8dc68ab9993a8dc2d635b30f998.png)

2.在组件顶部声明状态。这可以是任何东西。

```
state = {
  name: “Awesome person”,
  phone number: 6054756968,
  life motto: “I love rabbits.”
}
```

都可以接受。

![](img/c4637724b4a35003e4a84c94f51dfaa7.png)

3.在您的组件下面，但在导出默认值之前，声明一个将消耗(即使用)您的状态的功能组件。

![](img/38bb56ae41543c8076d94701ab5f0a01.png)

4.传入道具。

![](img/c879e07dd70f38d1a364d80d8f5022eb.png)

5.使用花括号通过功能组件中的 props 消费传递的状态。

**翻译**:把传入的道具放到花括号里的函数里。

![](img/06e74756c0d6c0c6eb74ee0abdbec310.png)

6.使用类组件中的功能组件。没事的时候不要慌。

![](img/01832454cb70a07546d6c511b200f14c.png)

7.告诉功能组件您想要使用状态中的哪些属性。

![](img/5a5b87dfc7d2eb5ac1e023f30008fa97.png)

8.庆祝—状态已通过。

![](img/0937e68be1ed41dd9042c800b216cfd9.png)

最后…这是一个可以玩的沙盒:

 [## 通过状态-代码沙盒

### CodeSandbox 是一个为 web 应用程序量身定制的在线编辑器。

codesandbox.io](https://codesandbox.io/embed/ppywlr4yjx?fontsize=14) [](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言——数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/)