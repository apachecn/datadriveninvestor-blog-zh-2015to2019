# 理解 JavaScript 中的回调函数。

> 原文：<https://medium.datadriveninvestor.com/understand-callback-function-in-javascript-b2961cdc9bc7?source=collection_archive---------1----------------------->

[![](img/26f4cbdd7af11bf2fd8afa11d1c8eace.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/40cb3928dda86ca002855ae8b7fff6b8.png)

你首先要明白的是，在 JavaScript 中，函数是第一类对象，这意味着像其他对象一样，我们可以将函数作为参数传递给其他函数，我们可以将函数赋给变量，也可以从其他函数返回函数。

## 什么是回调函数—

作为参数传递给其他函数并可以在一段时间后调用的函数称为回调函数。接受其他函数作为参数的函数被称为高阶函数，它基本上包含了何时调用回调函数的逻辑。

我们用例子来理解一下——

```
function sum(num1,num2){
   return num1+num2}function calculate(num1,num2,sum){ //sum is the call back function return sum(num1,num2); }
var result = calculate(5,6,sum);
console.log(result); // 11
```

检查回调函数的类型总是比检查它是否是函数更好。在上面的例子中，我们没有检查 sum 函数的类型。

```
function sum(num1,num2){
   return num1+num2}function calculate(num1,num2,sum){ //sum is the call back function
    if(typeof sum === 'function'){
          return sum(num1,num2); }}
var result = calculate(5,6,sum);
console.log(result); // 11
```

## 回调函数的使用—

在上面的例子中，你可以看到 calculate 函数什么也不做，它只是简单地立即调用回调函数(即 sum ),这种类型的操作是同步操作。但这并不总是发生，例如当我们从服务器或外部 API 请求数据时，我们不知道我们的数据何时会被返回。在这种情况下，我们必须等待响应，但我们不希望我们的应用程序被冻结。我们希望每一个功能都应该正常工作，当我们从服务器上获得数据时，它会反映在应用程序上。所以回调在这种情况下非常有用。

让我们用例子来理解—

```
function getDataFromServer(callback){ setTimeout(function(){ callback();
       },10000)
}function personDetails(){console.log("PersonDetails are available to use ");
}getDataFromServer(personDetails);  //PersonDetails are available to use
```

在这里，我演示了使用 setTimeout 函数的服务器请求，它只是在指定时间后执行一个函数。

在上面的例子中 getDataFromServer 在 1 s 后执行回调函数，所以当数据可用时我们可以回调函数来执行依赖于该数据的任务。

## 这在回调函数中—

`this`在每个函数中是一个特殊的关键字，它的值取决于函数是如何被调用的，而不是如何或在哪里被定义的。

当回调函数使用`this`对象时，我们必须修改如何调用回调函数，否则如果在全局函数中传递，它将指向`window`对象。

```
var student = {age:22,
   fullName:'Not Set',
   setFullName : function(firstName,lastName){
      this.fullName = firstName+' '+lastName;
   }
}function userInput(firstName,lastName,callback){callback(firstName,lastName);
}userInput('satyendra','kannaujiya',student.setFullName);console.log(student.fullName); //Not Set
console.log(window.fullName); //satyendra kannaujiya
```

在上面的例子中，回调函数不会设置对象 student 的全名，因为`userInput`是一个全局函数，在全局范围内的值是`window`。

我们可以使用`call`或`apply`来保存它。调用和应用的第一个参数是`this`或调用对象的值。

```
var student = {age:22,
   fullName:'Not Set',
   setFullName : function(firstName,lastName){
      this.fullName = firstName+' '+lastName;
   }
}function userInput(firstName,lastName,callback, object){callback.call(object,firstName,lastName)
}userInput('satyendra','kannaujiya',student.setFullName, student);console.log(student.fullName); //satyendra kannaujiyaconsole.log(window.fullName); //undefined
```

## 感谢阅读。☺️

## 来自 DDI 的相关故事:

[](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [## 数据科学和软件工程哪个更有前途？-数据驱动型投资者

### 大约一个月前，当我坐在咖啡馆里为一个客户开发网站时，我发现了这个女人…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/23/which-is-more-promising-data-science-or-software-engineering/) [](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/) [## 成为数据科学家所需的 8 项技能——数据驱动型投资者

### 数字吓不倒你？没有什么比一张漂亮的 excel 表更令人满意的了？你会说几种语言…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/07/8-skills-you-need-to-become-a-data-scientist/)