# 遗留项目重构:用 Retrofit2 和 RxJava 处理 API 错误

> 原文：<https://medium.datadriveninvestor.com/legacy-project-refactoring-handling-api-errors-with-retrofit2-and-rxjava-c9f8b23c7673?source=collection_archive---------0----------------------->

[![](img/10904c6b16bc31445f64b7cc7b5e4e89.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/295d4d6febc4edec63090b6eb1562dd0.png)

遗留项目有自己的特点，使用它们可能是一个挑战。这样的项目在不断扩大，开发人员在添加新的 API 请求、技术、框架、库等等。曾经伟大的架构变得过时，无法处理如此多的额外结构。这是重构的时候了。

[](http://go.datadriveninvestor.com/5ML1) [## DDI 编辑推荐:5 本机器学习书籍，让你从新手变成数据驱动专家…

### 机器学习行业的蓬勃发展重新引起了人们对人工智能的兴趣

go.datadriveninvestor.com](http://go.datadriveninvestor.com/5ML1) 

我是 Mobindustry 的一名 Android 开发人员，目前正在从事一个历时五年的项目，该项目仍在快速发展。因为它很老了，所以我们用了很多 API 来使不同的特性工作并处理后端。最近，应用程序很难支持所有这些 API 请求，我需要找到一个解决方案。

> 对于包括我在内的许多开发者来说，改造已经成为网络交互的标准工具

我选择了 RxJava 和 retrieval 作为我解决这个问题的主要工具。RxJava 是一个反应式编程框架，它使得对真实世界的情况建模和管理异步操作变得很容易。

翻新是一个灵活方便的框架，有助于建立有效和快速的 API 管理。这是一个适用于 Android 和 Java 的类型安全的 HTTP 客户端。对于包括我在内的许多开发人员来说，它已经成为网络交互的标准工具。它使得发送请求和接收响应变得极其容易。

要将 API 响应作为对象接收，可以使用转换器。在附加适配器的帮助下，您不仅可以接收**调用**类型的对象，还可以接收像这样的反应类型的对象:

*   **可观测、可观测<响应>和**可观测<结果>****
*   **可流动，可流动<响应>** ，和**可流动<结果>**
*   **单次，<单次响应>** ，和**单次<结果>**
*   **也许，也许<响应>** ，也许**T42【结果>**
*   **可完成**，其中无功分量被去除

T 代表我们得到的物体的类型。

在本文中，我将探讨如何让一个现成的**订阅者**或**观察者**来处理您从 RxJava 的改进中获得的数据。这将允许您在一个地方处理所有错误:应用程序的业务逻辑。这意味着您可以:

*   保存您在回复中收到的数据
*   计算下一个请求
*   显示请求的结果。

# 如何使用 reference 2 处理 API

我会给你一个详细的教程来处理 API 的改进。

1.第一步是向项目添加依赖项:

```
implementation 'com.squareup.retrofit2:retrofit:version’
implementation 'com.squareup.retrofit2:converter-gson:version'
implementation 'com.squareup.retrofit2:adapter-rxjava2:version'
```

注意，我的改造和适配器版本是 2.5.0。重要的是它们是相同的。

2.初始化改装:

```
public static Client getInstance() {
	return ourInstance;
}
Retrofit retrofit = new Retrofit.Builder()
	.baseUrl(BASE_URL)
	.client(okHttpClient)
	.addConverterFactory(GsonConverterFactory.create())
.addCallAdapterFactory(RxJavaCallAdapterFactory.create())
	.build();
```

3.描述您将用来获取 API 请求以进行改进的接口:

```
public interface Api {
@GET("users")
Call<List> getUserList();
}
```

4.要在 RxJava 中执行相同的任务，您需要使用以下代码:

```
@GET("users")
Observable<List> getUserList();
}
```

5.请求本身应该是这样的:

```
public void getUsers (ResultCallback callback) {
Call<List> call = Api.getInstance().getUserList();
call.enqueue(callback)
}
```

回调将以对象的形式存储服务器响应，**响应<列表>。如果回应还可以！，在 **response.body()** 请求的帮助下，您将在 **onResponse(Call call，Response response)** 方法中获得预期的**列表**。**

6.现在你需要解决翻新的问题。然后，它将向服务器发送一个请求，并返回一个 RxJava 数据流:

```
public Observable<List> getUsers () {
return  Api.getInstance().getUserList();
```

7.要处理 Rx 响应，您需要使用以下代码:

```
getUserList()	
.observeOn(AndroidSchedulers.mainThread())
	.subscribe(users -> 
{//some action},
throwable->
{//error handling}
);
```

这就是你需要设置的处理 API 的流程。但是，如果您的应用程序收到一个错误作为对请求的响应，会发生什么呢？这是 API 处理的一个非常重要的部分。如果你不给你的应用程序提供处理不同错误的方法，它会导致崩溃。

# 改进中 API 错误的处理:解决方案

使用 API 请求时，您可能会收到两种类型的错误:

*   HTTP 错误
*   请求处理错误

为了确保应用程序始终如一地工作，您需要处理它处理和应对错误的方式。有几种方法可以做到这一点:

1.给你的 **okHttp**
2 添加一个自定义接口拦截器。当使用**调用**对象时，可以在方法实现回调中使用下面几行代码:

*   对于处理错误: *void onResponse(调用 Call，响应 Response)；*
*   对于 HTTP 错误: *void onFailure(Call call，Throwable t)；*

3.使用 RX 时，请使用:

*   对于处理错误:在方法 **onNext(T t)** 中，如果你在 **t** 对象中发现错误
*   对于 HTTP 错误:在方法 void**on error(Throwable t)**中，当您根据异常的类型处理错误时

您还可以为 **Subscribe** 函数创建一个**可观察的**接口(或可选接口，如 **Single** 、 **Maybe** 和 **Completable** )。

# 在改造中处理 API 错误:解决方案缺陷

我提到的每个解决方案都有缺点；有些比较大，有些比较小。当您处理 API 错误时，您需要将它们考虑在内，以便为您的项目选择最佳解决方案，并确保您知道如果您的解决方案不能按预期工作时该做什么。

例如，实现拦截器接口起初似乎是一个完美的解决方案，因为您可以在 OkHttp 的早期阶段处理错误。但是，这就是你会遇到一些问题的地方。

> 我提到的每一个解决方案都有缺点；有些比较大，有些比较小。当您处理 API 错误时，您需要将它们考虑在内

要在应用程序中实现错误处理行为，您需要将应用程序的上下文转移到 OkHttpClient 中。错误处理行为包括通知用户一个错误，或者向后端发出一个额外的或替代的请求。

当您将上下文转移到 OkHttpClient 时，如果您更改上下文，这可能会导致应用程序中出现不可预测的错误。这也可能导致内存泄漏。

使用 RxJava2Adapter 直接在 Subscribe 函数中处理错误是一个好主意，除非有两个以上的方法需要处理错误。

# 处理 API 错误的最佳方式

在尝试不同的 API 错误处理解决方案时，我想到了一个完美的解决方案，它涉及在反应式数据流中处理错误。我使用 RxJava 实现了这一点。

这个想法是以一个对象的形式获得对我们请求的响应，不管有没有错误，或者接收一个 HTTP 错误作为某种类型的异常。这样我们可以像处理 HTTP 错误一样处理内部错误。

这就是我们需要让它工作。

1.首先，创建一个对象，它将包含**上下文**和应用程序在任何错误情况下的行为。为此，您需要实现一个接口来创建不同的错误处理器:

```
public interface BaseView {
   Context getContext();
}
```

我是这样实现处理器的:

```
public class RxErrorHandling implements BaseView {
   private WeakReference context;RxErrorHandling(Context context){
	this.context = new WeakReference<>(context);
} private Context getContext() {
       return context.get();
   }public void exampleInnerErrorWithCode (int code){
	//in case you received an internal error code from your server, use this method to handle the error 
Log.e(“TAG”, “Inner error with code ” + code);
//You can display Toast as well, because we got Context
}public void onTimeoutError (){
	//you process the error here if you got the TimeoutException 
Log.e(“TAG”, “TimeoutException”);
}public void onNetworkError (){
	//if the NetworkErrorException was initialized, process the error here  
Log.e(“TAG”, “ NetworkErrorExeption”);
}
	...
}
```

2.此时，我们需要用两个方法创建一个类。这些方法将处理服务器响应和 HTTP 错误。

```
class ResponseWrapper{
	private RxErrorHandling baseView;

	ReponseWrapper(RxErrorHandling view){
		this.baseView = view;
	}
	//Method for handling internal errors in the response
	public handlingResponse(BaseResponse response){
		if (!resp.isSuccess()) {
		//In case there is an internal error in the response, send the error code to the view to get a reaction
			baseView.exampleInnerErrorWithCode(resp.getErrorCode);
		}
	//Here you initialize the method for generating own error
   	catchError(resp.getCode(), resp.getError()); } //Method for handling HTTP errors
	public handlingException(Throwable e){
	if(e instanceof SocketTimeoutException){
		baseView.onTimeoutError ();
	}elseIf(e instanceof IOException){
		baseView.onNetworkError()
	}//Method for generating your own exception
	private void catchError(String code, String error) {
		try {
			throw new ResponseException(error, code);
		} catch (ResponseException e) {
			throw Exceptions.propagate(e);
		}
	}
}
```

这些都是为 API 错误处理做准备所必须做的事情。最后要做的是提出一个请求，将下面的内容添加到 **subscribe()** :

*   **map()** —用于检查服务器响应中是否有错误。如果有，这个函数会处理它们或者生成一个异常。
*   **dooner error()**—用 **subscribe()** 中的 **onError** 方法初始化的处理器。这个处理器允许我们处理 HTTP 异常或在 **ResponseWrapper** 类的 **catchError(字符串代码，字符串错误)**中创建的异常。

```
ResponseWrapper wrapper = new ResponseWrapper(this)
getUserList()	
.observeOn(AndroidSchedulers.mainThread())
// if there were no exceptions from HTTP, than map() will be initialized
.map(response -> {wrapper.testResponse(response);
   			return response;}
		)
		//if there was an HTTP or a .doOnError exception -> {
			wrapper.testExceptions(e);})
.subscribe(
users -> 
{//some actions},
throwable->
{//individual error processing}
);
```

这就是你以最好的方式有效处理你的 API 错误所需要的。

# 结论

出于几个原因，用 Retrofit2 和 RxJava 处理 API 错误是一个很好的解决方案。

首先，去掉过多的、重复的代码。通常，一个应用程序对错误的反应是相同的，对类似错误的整体行为必须是相同的。例如，如果您收到一个 404 错误，您需要显示一个错误弹出窗口(例如 Toast)。在 403 禁止错误的情况下，应用程序应该显示授权屏幕。

使用这种策略的第二个原因是它的灵活性。如果需要其他行为，可以在 **subscribe()** 函数中添加到 **onError()** 中即可。

第三个原因，也是最好的一个原因是，在反应式编程中，您可以将响应视为数据流。遗产 **AsyncTasks** 在这里不会打扰你。

希望这篇文章对你有用。如果您对处理 API 请求和错误有任何疑问，请务必联系 Mobindustry。

**获得免费咨询！**
sales@mobindustry.net

[https://www . mob industry . net/legacy-project-refactoring-handling-API-errors-with-retro fit 2-and-rx Java/](https://www.mobindustry.net/legacy-project-refactoring-handling-api-errors-with-retrofit2-and-rxjava/)