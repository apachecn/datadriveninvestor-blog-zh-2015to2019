# JavaScript 中的事件循环

> 原文：<https://medium.datadriveninvestor.com/event-loop-in-javascript-b7ff47202716?source=collection_archive---------0----------------------->

[![](img/0a8dbc334790a9f1cab369a4f971cc71.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/4e8486a5bb9ce905b3ee69e72484facf.png)

众所周知，JavaScript 是单线程的，这意味着它不能利用 JAVA、C#、Python 等的多线程。我们没有同时运行多个进程的选项，相反，我们只有一个线程来运行所有的进程。

首先让我们了解一下，我们所说的**单线程是什么意思。**顾名思义，*单线程*应用是指在任何给定时间点只能运行一个进程的应用。这些进程被放在一个被称为**调用栈**的数据结构中。顶层进程完成并从堆栈中弹出(移除),实现堆栈中的下一个进程/方法。这种情况会一直发生，直到堆栈变空。

让我们看一个简单的例子来更好地理解调用堆栈:

```
function one(){
    return two();
}
function two(){
    return three();
}
function three(){
    return four();
}
function four(){
    return "completed";
}
console.log(one());
```

在上面的代码片段中，当我们调用方法 ***one* ，**时，它被添加到调用堆栈中。但是 ***一个*** 会一直留在调用栈中，直到完全执行。

让我们试着看看方法调用:

```
one -> two -> three ->four
*calls = ->
```

堆栈将如下所示:

```
+-----------+   +-----------+   +-----------+   +-----------+
|Call Stack | ->|Call Stack | ->|Call Stack | ->|Call Stack |
+-----------+   +-----------+   +-----------+   +-----------+
| four      |   | three     |   | two       |   | one       |
| three     |   | two       |   | one       |   +-----------+
| two       |   | one       |   +-----------+
| one       |   +-----------+
+-----------+
```

当 ***four*** 完成其执行时，它被从堆栈中移除。栈自动进行到栈顶的下一个任务(*三个*)，直到栈上没有更多的任务。

我希望您对调用堆栈的工作原理有了基本的了解，因为从这里开始，事情就变得有点棘手了。

尽管 JS 是单线程的，但它本身并不表现为单线程。如果是这样的话，每次调用服务时，调用堆栈都会阻塞所有其他进程，等待服务完成，然后继续执行其他任务。这将增加执行时间(没有人希望这样)，但是我们都知道 JS 不是这样。

让我们修改上面的例子并添加一个 *setTimeOut* 函数，它将表现为一个服务调用:

```
function service(){
    console.log("service called")
}
function one(){
    return two();
}
function two(){
    return three();
}
function three(){
    return four();
}
function four(){
    return "completed";
}setTimeout(service,1000)console.log(one());
```

现在， ***setTimout*** 是一个 ***async*** 方法，它接受一个回调函数作为参数。第二个参数是时间，在此之后回调被触发。

让我们了解一下*异步*功能是如何执行的过程。众所周知，要执行一个函数，我们必须调用它。我们可以通过使用一个触发器来调用它，这个触发器一般是一个事件(比如 onClick、onBlur、timeout)。

我们需要一个将事件映射到特定方法的数据结构。这个数据结构就是**事件表。**但是这个*事件表*只把方法映射到一个事件，并不调用方法本身。事件表将方法发送到**事件队列**，顾名思义，它是一个按照正确的顺序/序列执行的方法队列。

> **事件循环**

现在，这就是臭名昭著的**事件循环**发挥其魔力的地方。

***事件循环*** 基本上是一个死循环，不停的检查调用栈中是否有要执行的东西。如果调用堆栈为空，它将检查事件队列，看是否有要移动到调用堆栈的内容。如果有一个方法存在，它会将它移动到调用堆栈中，然后执行该方法。

让我们想象一下上面的例子:

*注意:假设方法一、二、三、四中的每一个都需要 500 毫秒来完成执行

```
*setTimeout* gets called ->
*setTimeout* is moved to the **Event Table** 
* one method is called ->
* one gets added to the call stack
* one calls two -> 
* two gets added to the call stack
* two calls three->
* three gets added to the call stack
* three calls four ->
* four gets added to the call stackBy the time method *three* finishes, its more than 1000 ms.
The **event table** sends the ***service***method to the **event queue.**All the methods get executed and the call stack becomes empty.The **event loop** checks the **event queue,** and finds the *service* method present. 
It moves the method to the call stack and *service * gets executed.
```

综上所述，**事件循环**是一个无休止运行的进程，它唯一的工作就是监控并将方法从事件队列转移到调用栈。

了解调用堆栈和事件循环是如何工作的，将有助于您更好地理解 JavaScript 在幕后是如何工作的。

*   面试官喜欢用这样的例子来测试你对 JS 的理解。