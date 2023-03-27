# Javascript 中的循环及示例

> 原文：<https://medium.datadriveninvestor.com/loops-are-something-that-is-with-us-always-since-the-beginning-of-our-never-ending-journey-of-fa9e04ee144d?source=collection_archive---------5----------------------->

![](img/4ae877cf8ec0c5415f297ec3ba710857.png)

Photo by [Tine Ivanič](https://unsplash.com/@tine999?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**循环**是我们永无止境的学习 JavaScript(或任何编程语言)之旅开始以来一直伴随着我们的东西，所以让我们关注它们。对我来说，最好的学习方法是用我所学的知识创造一些东西，所以我试着为所有的循环提供例子，你可以看到它们做了什么，以及我们如何使用它们

# 我们将涵盖哪些循环

*   while 循环
    *do…While 循环
    *for
    *for..3 .在
    *中，用于…的

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言——数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

所以首先让我们定义什么是**循环**以及为什么我们需要在 JavaScript 中使用它们？你知道当你非常喜欢一首音乐的时候，你会一遍又一遍的听吗？这是一个循环。对于编程来说，循环是一种迭代数组或对象的方式。使用循环，我们确保我们的代码是干燥的。**循环**将循环直到满足条件，或者如果满足条件则循环，直到条件为假。

无限循环是一个没有结尾的循环，很可能会使你的应用程序/网站崩溃

# While 循环

只要评估的条件为真，循环**就会运行。把它想成一个条件语句，一个 ***if*** 语句，但不是运行一次，只要条件为真就运行一次。如果你不写条件或者写一个永远不会变假的条件，也就是说，永远为真，循环永远不会结束。**

**语法**:

```
while(condition)
{
  //code to be executed as long the condition is true
}
```

让我们打印 0 到 5 之间的所有数字:

```
let i = 0;
  while (i < 6) {
    console.log(i);
    i++;
  }
```

这里发生了什么？首先，在**循环**之外将变量设置为 0。然后你写 while 条件为`i < 6`，所以只要 *i* 小于 6，上面的代码就会运行。
代码是什么？括号内的所有内容，所以在这种情况下，打印变量(数字),然后给变量加 1。

所以从 0 开始。零小于 6？对，所以打印出 *i* 即 0，加 1。*我*之后是多少？是的，它是 1，仍然低于 6，所以再做一次，直到 *i* 是 6。因为 6 不小于 6，所以**循环**结束，打印的内容是:

```
let i = 0;
  while (i < 6  ) {
    console.log(i);
    i++;
  } /*
  0
  1
  2
  3
  4
  5 
  */
```

# 让我们现实一点

对我来说，最好的学习方法是看到情况/问题的实用性，在这种情况下，是循环。我会尽我所能做到最实际，但是如果我说得不够清楚或者我如何改进，请随时告诉我。

这只是一个小例子，我想说的是没有什么是永远不会被需要的，至少像这样:)

现在是除夕，你想创建一个小的 10 秒倒计时，直到 0 或直到新年，说还有多少秒到除夕，当达到 0 时，它会说“新年快乐”。

这里发生了什么？

我不会详细讨论 DOM 操作，但是基本上，我们在我们的 **html** 中设置了一个`id`，然后在我们的 js
T1 中设置了一个`id`，在那里我们将显示我们的消息`message.innerHTML=`${countdown}`。另外，我使用了[模板文字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)。

现在是 **while 循环。**我们将变量 *seconds* 设置为 10，这是我们想要开始它的地方，然后我们将变量 *countdown* 设置为一个空字符串，我们将在 JS 中打印倒计时。

然后我们的 **while 语句**说，只要 seconds 变量大于 0，我们就写消息并将变量 seconds 设置为*减*一秒。
在我们刚刚设定它到达零时。循环外
也是如此`countdown =${countdown} ${seconds} Happy new Year`。

因此*常量*信息将在倒计时期间显示倒计时变量，并显示相应的信息。

# do…while 循环

**做……而**的工作有点不同。最大的区别是 **do… while** 循环至少运行一次。基本上，它说当这个条件为真时，至少运行一次。

**语法**:

```
do //statement or code to executewhile(condition)
```

现在，让我们来看看它只运行一次的情况:

```
let i = 0;do {
  i++;
  console.log(`I run at least ${i} times`);
} while (i < 0);console.log(`I run a total of ${i} times`);
// expected result: "I run at least 1 time"
// "I run a total of 1 times"
```

我们将变量设置为 **0** ，并设置循环在每次迭代时加 1，并且只要 I 小于 0 就这样做(*将条件设置为*)。我将一个 console.log 放在语句内部，另一个放在语句外部，以查看它输出的内容。

所以首先 **i** 是 0，我们加 1，打印“我至少跑了 1 次”。然后我们检查条件:I 小于 0 吗？好了， **i** 现在是 1，大于 0，所以循环停止，它会打印“我总共运行了 1 次。
例如，如果您想查看差异，请将条件更改为 5

```
let i = 0;do {
  i++;
  console.log(`I run at least ${i} times`);
} while (i < 5);console.log(`I run a total of ${i} times`);
/* expected result:
"I run at least 1 time"
"I run at least 2 time"
"I run at least 3 time"
"I run at least 4 time"
"I run at least 5 time"
"I run a total of  5 times"*/
```

这里你可以看到当它循环不止一次时它是如何工作的。I 从 0 开始，然后加上 1，就变成了 1。上面印着“我至少跑一次”。然后，因为 I 仍然小于 5，所以再加 1，这样做，直到 I 为 5，然后打印以上所有内容。

# for 循环

JavaScript 中最常用的循环之一是循环的**。当我开始用 JS 编码的时候，这是我到今天为止用得最多的一个。一开始，我不太明白它是如何工作的，所以当我在 for 循环中开始
时，我试图用一种我能理解的方式来解释，代码会重复，直到条件评估为 false。**for 循环的用途之一是循环遍历一个数组**。**

**语法**:

```
for([initialization];[condition]; [final-expression])
```

所以在使用时，看起来会像这样:

```
for(let i =0; i <5 ; i++){
    //do something
}
```

为了解释，我们先来看一个简单的例子。你想循环从 0 到 4 的所有数字并打印它们，上面的循环就是要用的那个。

所以初始化( **i=0** )是我们定义变量的地方，因为我们想从 0 开始，我们把变量定义为 0。

条件( **i < 5** )是在每个循环结束时计算的表达式，当它为假时，循环停止。所以在这种情况下，在每次循环中，都会检查 I 是否**小于 5** 。

最终表达式( **i++** )通常用作增量。你需要考虑的是，最终表达式出现在条件被求值之前

**//做点什么**部分是只要条件(i < 5)为真它就会运行的代码。
在 for 循环中，可以使用 break 或 continue 语句。

那么我们来看一个更现实的例子。你有一个网站，你想添加你看到的电影，并在屏幕上显示它们。首先，在我们的 html 中，让我们创建我们的 div，在那里我们将表示我们的电影。

```
<h1>Movies I see</h1>
      <div id="movies"></div>
```

在我们的 js 中，我们用可以添加或删除的电影创建数组。

```
let movies = [
  "Constant Gardener",
  "Batman",
  "Pulp Fiction",
  "Heat",
  "Godfather"
];
```

现在让我们用一个 **getElementById** 从 html 中获取 div:

```
let myMovies = document.getElementById("movies");
```

然后，我们创建一个空字符串，在那里我们将渲染所有的电影。

```
let myList = "";
```

现在我们想循环播放现有的电影，我们可以用 for 循环来创建它。

```
for (let i = 0; i < 5; i++) {
    console.log(movies[i]);
  }
```

那么循环中会发生什么呢？首先，我们创建一个变量并设置为 **0** 。为什么是 0？从我们的第一个元素开始。如果我们把它改成 1，你会看到它不会打印电影《常数加德纳》。我们设定的条件是，当**小于 5 时进行打印。为什么是 5？因为我们有很多电影。然后我们加上 **i++** 来给每个循环总是加一。然后，我们只需要在每个循环中添加我们想要的东西，在这种情况下，我们只想 console.log 它——我们编写 **movies[i]** 来分别编写每个电影。如果你只写**

```
console.log(movies);
```

它将打印电影数组 5 次，而不是 5 部电影。

我们能做些什么来改善它呢？嗯，如果你想再加一部电影呢？如果你有另一个条件，你必须把条件改为 6 和 7，依此类推。这不是真正的生产。所以让我们把它变成动态的。

我们希望它一直循环，直到我们用来循环的变量( **i** )小于电影的数量，对吗？在编程中，数组中元素的数量(本例中是电影的数量)是数组的**长度**，所以我们可以这样写代码:

```
for (let i = 0; i < movies.length; i++) {
    console.log(movies[i]); }
```

就像这样，我们不需要担心我们是否添加了另一部电影，因为它会一直循环。
现在让我们也在屏幕中渲染。我们可以通过在每次循环时创建一个项目符号来实现。

```
for (let i = 0; i < movies.length; i++) {
    console.log(movies[i]); myList = myList + `<li>${movies[i]}</li>`;
  }
```

我们在这里做了什么？所以 **myList** 是一个空字符串，对吗？所以在每一次循环中，我们希望在空字符串中有一个数组元素，当我们循环这个字符串时。

为了让代码更好，让我们把所有东西都放在一个函数周围

```
function myMovies() {
  let myMovies = document.getElementById("movies");
  let myList = "";
  for (let i = 0; i < movies.length; i++) {
    console.log(movies[i]); myList = myList + `<li>${movies[i]}</li>`;
  } myMovies.innerHTML = `${myList}`;
}myMovies();
```

现在我们用我们创建的函数创建 HTML 元素，并呈现在 **myList** 上的数据。

# 因为在

因此，根据[MDN](https://developer.mozilla.org/en-US/),中的***for…遍历对象的可枚举属性，例如 **object.keys** 。例如，构造函数或原型属性不被认为是可枚举的，所以当在***中为…运行**时，您看不到它们**

所以即使在 Js 中，一切都是对象，你也不应该在[数组](https://stackoverflow.com/questions/500504/why-is-using-for-in-with-array-iteration-a-bad-idea)中的中使用**for……主要原因是**for……in**以任意顺序迭代，当迭代一个数组时，索引很重要。所以我们关注为什么以及如何在一个对象中使用它们**

**语法**:

```
for (let key in object) {
 //code in the loop
}
```

所以这里的**键**名就是给对象赋值的名字变量。是在 for 循环中的 *i* 。就像 for 循环中的 *i* 一样，你可以给它取任何名字。**对象**是实际的对象，所以你要把你要循环的对象命名为。让我们看看它是如何工作的，在这个例子中它做了什么。你有一个人对象。

```
let person = {
  name : "Steve",
  age : 35,
  city:"London"
}
```

现在在中使用我们的**for……让我们循环，看看我们得到了什么:**

```
for (let key in person) {
  console.log(key);
}
//name
//age
//city
```

我们得到了对象人的属性，对象的密钥。务必获得您可以做到的价值:

```
for (let key in person) {
  console.log(key);
  console.log(person[key]);
}
//name
//Steve
//age
//35
//city
//London
```

让我们做得更清楚些

```
for (let key in person) {
  console.log(`${key} - ${person[key]}`);
}
//name - Steve
//age - 35
//city - London
```

这很好，也很有用，但是当我们有一个对象构造函数时会发生什么呢？

注意:如果你第一次看到循环，对象构造器可能看起来更高级，我将在以后的文章中讨论它。对于这个例子，假设您想要创建许多 person 对象。所以你得一个一个加。但是如果你能创建一个对象构造函数，它具有所有人都有的属性，那就很容易了，对吗？然后我们有了对象构造函数
，让我们创建那个对象构造函数。

```
let Person = function(name, yearofBirth, job) {
  this.name = name;
  this.yearofBirth = yearofBirth;
  this.job = job;
};
```

然后我们给这个对象添加一个函数:

```
Person.prototype.calculateAge = function() {
  console.log(2019 - this.yearofBirth);
};
```

现在让我们创建一些对象:

```
let Ricardo = new Person("Ricardo", 1992, "teacher");
let Marika = new Person("Marika", 1987, "designer");
ricardo.calculateAge();
marika.calculateAge();
```

现在让我们遍历 Marika 对象:

```
for (var key in marika) {
  console.log(marika[key]);
}/*
Marika
1987
designer
ƒ () {
  console.log(2019 - this.yearofBirth);
}
*/
```

除了对象**玛丽卡、**的属性之外，它还循环遍历函数，这是因为中的**for…遍历原型链的所有属性。因此，我们可以用 **hasOwnProperty** 方法遍历包含 key 对象的属性:**

```
for (var key in marika) {
  if (Person.hasOwnProperty(key)) {
    console.log(marika[key]);
  }
}
/*
Marika
1987
designer
*/
```

所以你可以在中使用**for……来遍历属性名，并从一个对象中检查哪些是具有某些属性的，比如 key 属性**

# 对于...来说

我们要讲的最后一个循环是的**for……。它适用于可迭代的对象，比如数组和字符串。它与 ES6 一起作为 **forEach**
的替代产品出现。
语法与**中的**for…相似，只是改变了 in/on。并且您应该仅在计划对象中使用**中的**for……而**中的**for……在对象中不起作用。**

**语法**:

```
for (let key on object) {
 //code in the loop
}let ingredients = ["dough", "tomato", "cheese"];
for (let key of ingredients) {
  console.log(key);
}//dough
//tomato
//cheese
```

你可以马上看到，它可以做与 for 循环相同的事情，但是更简洁，代码更少
也适用于字符串:

```
const name = "Ricardo";for (const key of name) {
  console.log(key);
}/*
R
I
C
A
R
D
O
*/
```

也适用于**贴图**、**物体**和**集合**，但我们不会在这篇文章中关注它们。有一点它在普通对象上不起作用，那就是因为对象不是“可迭代的”。

但是很好的使用 **for…of** 是在一个节点列表上。例如，如果你在一个页面上有一些相同类别的标题，并且你想要**打开，点击**来改变它们的颜色。输入的…的

**所以 html 有一堆相同类别的标题。
在我们的 JS 文件中，我们用:**

```
const elements = document.querySelectorAll(".names");
```

**然后我们只需为的……添加**:****

```
for (const element of elements) {
  element.addEventListener("click", () => {
    element.classList.add("active");
  });
}
```

****活动的**类是我们想要添加的类，当点击时会使文本改变颜色和位置。
就这样。**

**仍然有很多关于循环的讨论，但是有了这些，你可以开始在你的项目中使用它们，并且知道你想要使用哪一个。让我们开始编码吧。**

**很高兴听到你对这篇文章的反馈以及如何改进。你可以在 Instagram 上关注我，我每周都会在那里发布片段、我正在做的项目以及其他与代码相关的东西。你在我的[个人资料](https://dev.to/mugas)上找到的所有其他链接。**