# Javascript 上的控制流

> 原文：<https://medium.datadriveninvestor.com/control-flow-on-javascript-db6917aa55e4?source=collection_archive---------14----------------------->

> 葡萄牙一位最著名的诗人有一句话是这样的:“Primeiro estranha-se，depois entranha-se”，在英语中是这样的，起初感觉很奇怪，但随后你会感觉到。从一开始，这就是我对 Javascript 的体验。开始的时候，我觉得很奇怪，但随着时间的推移，我越来越喜欢，现在我只想知道越来越多，练习越来越多。

也就是说，我决定写一些关于 Javascript 主题的帖子。通过把它写在这里，我可以更好地学习它，你也会从中发现一些有用的东西。因为我是一个代码新手，而且我主要是为其他代码新手写这些帖子，所以有些事情可能看起来很容易，即使对你我来说也是如此，但这只是为了有一个良好的开端，而不是跳过某个主题中的一些主题。

这个长系列的第一篇是关于 Javascript 中的**控制流。**

在计算机科学中，控制流是指令、语句或功能执行的顺序。在 javascript 中，我们从第一行读到最后一行，除非代码中有一些指令或语句改变了控制流。

我认为最常见的控制流是 if 语句，我们使用了很多代码。例如，如果你的年龄超过 18 岁，你希望网站显示某个页面，否则，网站将呈现不同的页面。这是控制流/条件示例的传统示例

注意:循环是控制流语句的一大部分，但是因为我只想写一篇关于循环的文章，尽管我会在例子中提到和使用它们，但这不是我的重点。

**街区**

block 语句本身并不改变控制流，而是用于对语句进行分组。该块由一对花括号组成。

```
{
first statement;
second statement;
...
} 
```

when use 语句的一个很好的例子是 if 语句。

破裂

破顾名思义，破。打破什么？中断语句或通常情况下中断循环。

参见下一个例子:

```
for (*let* i = 0; i < 5; i++) {
  if (i === 3) {
    break;
  }
  *console*.log(i);
}
//excepted output : 0,1,2
```

在这个循环中，如果我们取出 break，循环将遍历从 0 到 4 的所有值。但是因为我们在 3 上有一个断点，所以它只会从 0 迭代到 2。

基本上，这个条件说如果 *i* 等于 3，那么中断并停止循环。

我们也可以用它给用户提供更多的信息。如果我们想要一个函数，当满足某个条件时，循环遍历一些数字并中断，然后打印出相关信息。在这种情况下，我们希望它会一直循环下去，直到某个数字被 3 除后余数为 0，但也被 5 除，并希望打印该信息。

```
for (*let* i = 5; i < 50; i++) {
  if (i % 3 === 0 && i % 5 === 0) {
    *console*.log(`The division reminder of the number ${i} is 0`);
    break;
  }
  *console*.log(i);
}
expected output :
5 
6
7
8
9
10
11
12
13
14
The division reminder of the number 15 is 0
```

有用吧？

![](img/5a42fd2a2b2f71d0dca91103f139d571.png)

Photo by [Caspar Camille Rubin](https://unsplash.com/@casparrubin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

继续

那么如果*中断*，结束循环，那么*继续*语句会做什么呢？没错，它在那个迭代中跳过循环，继续下一个迭代。

换句话说，当满足 continue 条件时，它将不会运行或打印它，而是直接进入下一个迭代。你说一个例子？好的

```
for ( let i = 0; i<10;i++){
if(i ===5){
continue;
}
console.log(i);
}
excepted output:
0
1
2
3
4
6
7
8
9 
```

如您所见，console.log 将打印除数字 5 之外的所有循环，这是设置 continue 语句的地方。如果您想检查每种情况下发生了什么，我建议您在每个步骤中设置 console.log，并查看它打印的内容:

```
for (*let* i = 0; i < 10; i++) {
 *console*.log(i);
 if (i === 5) {
   continue;
 }
}excepted output:
0
1
2
3
4
5
6
7
8
9
```

因此，如果在 continue 语句之前打印它，它会打印所有内容。如果在 continue 语句之前打印它会怎么样？

```
for (*let* i = 0; i < 10; i++) {

 if (i === 5) {
   *console*.log(i);
   continue;
 }
}excepted output:
5
```

所以在这里，continue 语句出现在 console.log 之后，但是 console.log 已经在条件中，所以它打印该条件。

所以基本上它说， *i 等于 5 吗？*所以打印出来。

正如您在这三个相同代码的例子中所看到的，知道您想在哪里访问您的信息是很重要的。因为我学得更好，会有更多真实的例子，这里有一个。

假设您有一个所有波段的数组，并且您想打印除一个波段之外的信息。为什么？嗯，也许你不想让每个人都知道你喜欢那种俗气的流行音乐，每个人都喜欢说它的坏话。你是怎么做到的？

```
*var* music = [
"placebo",
"smashing Pumpkins",
"pearl jam",
"ornatos violeta",
"feromona"
];for (*var* i = 0; i < music.length; i++) {
  if (music[i] === "ornatos violeta") {
    continue;
  }
*console*.log(music[i]);
}excepted output:
"placebo"
"Smashing Pumpkins"
"Pearl jam"
```

我们来解释一下:

你有一个数组。在你有了遍历整个数组的循环之后。然后，如果数组中有一个元素的名称是您不希望打印的(在本例中是 Ornatos Violeta ),则设置条件。很棒的乐队，顺便说一句，我绝不会让它不印出来)。因此，您会看到迭代元素(I)被设置为您想要的值的数组。

然后设置 continue 语句并将其打印出来。就像这样，它会打印所有你想要的波段，跳过你不想要的。

开关(并由**联想到*if*语句)**

所以一个 ***switch*** 语句是在你不得不在同一个函数中使用多个 ***if*** 语句时使用的。所以 ***if*** 语句是你在代码中最常使用的，你可能知道它是什么，但我会给出一个简短的解释。

如果指定的条件为真，if 语句将执行一条语句。如果为 falsy，则可以执行其他语句，或者检查其他条件。

所以拿起最后一个例子，检查数组中是否有特定的元素，并用 if 语句输出 true。

```
*var* music = [
"placebo",
"smashing Pumpkins",
"pearl jam",
"ornatos violeta",
"feromona"
];if (music[0] === "placebo){
  console.log(true)}
else {
  console.log(false)
 } excepted output:
"placebo"
```

所以这里我们检查 ***如果*** 数组的索引 0 等于“安慰剂”，打印出 true。在这种情况下，它是。我们还把 **else** 声明为当条件不满足时。对于干净的代码，如果只使用 else 语句，您可以像这样编写不带括号的代码:

```
if (music[0] === "placebo){
  console.log(true)
}
  console.log(false)excepted output:
true
```

它将输出相同的结果。但是如果你还有一个条件要检查呢？你可以使用 ***else if*** 语句:

```
var music = [
"placebo",
"smashing Pumpkins",
"pearl jam",
"ornatos violeta",
"feromona"
];if (music.includes("placebo")) {
  console.log(true);
} else if (music[0] === "feromona") {
  console.log(false);
} else {
  console.log(okay);
}excepted output:
true
```

所以这里检查第一个条件，如果**数组**包含“安慰剂”。(我在这里使用的方法 ***包含*** ，顾名思义就是检查**数组**是否包含你要搜索的元素)。在第二个条件中，我们检查 **index[0]** 是否是带有 ***else if*** 语句的“feromona”，该语句的工作方式类似于另一个 ***if*** 。然后我们把 ***else*** 语句放在最后，以防条件都不满足。但是如果我们有太多的如果呢？这就是 switch 语句的由来。

```
function job(name){

  switch (name){
    case "professor":
      console.log("you teach well");
      break;
    case "artist":
      console.log("I like your painting");
      break;
    case "singer":
      console.log("I love your voice");
      break;
    default:
      console.log("what you do?");
  }
}job("professor");
```

让我们开始吧。 ***开关*** 语句允许您为想要检查的元素创建一组选项。

在这种情况下，您有一个函数，对于不同类型的作业，它将打印不同的内容。但是你如何使用 ***开关*** ？要使用 ***开关*** 语句你必须按情况划分，分别为每个 ***情况，*** 选项中的每一个。所以在这个例子中，在**案例** 1 *中，使用的参数*是一个教授，它将打印“你教得很好”，如果是*艺术家*和歌手，它也会相应地这样做。

为什么要休息？我们使用 break 语句，因为如果不这样做，代码将继续执行下一个块。

您可以在 ***开关*** 案例中使用**默认“案例”**，它的工作方式类似于 **else** 语句，即如果不满足任何条件，代码将执行该语句。

这是 Javascript 中控制流的基础。你可以复制代码并在 [Jsbin](https://jsbin.com/) 中播放，例如，看看它是如何工作的。JS 中有更多的控制流语句，还有更多关于循环的内容。但是在不久的将来，我会在一篇关于循环的文章和例子中告诉你。

请通过此处或通过 [Twitter](https://twitter.com/mugas11) 或 [Instagram](https://www.instagram.com/mugas_codes/) 向我发送您的评论和意见。我会发布更多的内容、教程、视频和其他所有与编码相关的内容。快乐的创作:)