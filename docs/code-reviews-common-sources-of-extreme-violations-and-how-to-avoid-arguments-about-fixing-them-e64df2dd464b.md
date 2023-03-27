# 代码评审:极端违规的常见来源以及如何避免关于修复它们的争论

> 原文：<https://medium.datadriveninvestor.com/code-reviews-common-sources-of-extreme-violations-and-how-to-avoid-arguments-about-fixing-them-e64df2dd464b?source=collection_archive---------3----------------------->

![](img/183f4f1b3a2a072a7216e7b681ed747f.png)

刀拔出来了。刀刃磨得锋利是为了冲突。开发商之间发生了激烈的争论。编码人员的激情不是被错误的软件点燃，而是被异常简洁或冗长的代码点燃。这些线是黑客入侵的迹象。任何不同意的程序员都是业余的。只有新手才会产生如此明显违背良好品味的方法和块。然而，不同的偏好，而不是自然法则，是这场冲突和尖酸刻薄的根源。在这种情况下，开发者之间的仇恨是为了不同的目的而交易简洁的不同倾向的结果。这些目标，以及它们的趋势，对于每个开发人员来说都是不同的，这导致了在某些领域的持续冲突。一个这样的地方是冗长或简洁的代码。为了最大限度地减少冲突，团队可以使用代码审查来突出最严重的部分，团队可以就这些部分进行争论，而不是就代码库的每一行和每一个代码块进行争论。

某些代码构造或技术可能会产生极端的违规行为，并引发关于纠正这些违规行为的争论。纠正这些弊端会引发激烈的争论。对于下面列出的特殊语言特征和技巧，这些分歧是可以解决的，或者至少是可以减少的。

# 条件运算符与 If 语句

语言元素，条件操作符和 if 语句，导致了争论，不同的阵营认为每一个都是某些操作的高级技术。这些操作可以通过多种方式实现，每种技术都有优点和缺点。

**If 语句:**当条件密度很高时，If 语句可能会产生大量代码。高密度会使块或方法显得臃肿。然而，用 if 语句编写的代码也是高度可调试的，因为开发人员可以单步执行每一行。

> if(label 1 is required){
> label 1。Color = "红色"；其他的{
> 标签 1。Color = "黑色"；
> }
> 
> if(label 2 is required){
> label 2。Color = "红色"；
> else {
> label 2。Color = "黑色"；
> }
> 
> if(label 3 is required){
> label 3。Color = "红色"；
> } else {
> label3。Color = "黑色"；
> }

**条件操作符:**当条件操作符作为几个 if 语句的替代时，它可以产生一些非常简洁的行。嵌入式条件操作符使得代码非常难以阅读、测试或调试。任何大量使用条件操作符的块或方法也非常紧凑，减少了开发人员必须扫描的代码量。

> health indicator color =(health = = " Good ")？“绿色”:(health = =“Fair”)？“黄”:(健康==“差”)？"红色":(health == "life_support ")？“橙”:“紫”；

**潜在解决方案:**当条件运算符替换基于通过 if 语句实现的条件的高密度值集时，它们是有益的。条件运算符是破坏性的，当它们替换甚至几个相互嵌入的决策时。可以在一行中轻松完成的命令是条件操作符的主要目标，而需要几行的条件是 if 语句的领域。任何对 if 语句或条件操作符的过分使用都应该被纠正，以部署这些结构之一的适当使用。(**注意:**修改可能需要大量的重构。)

> if(health = = " Good "){
> health indicator color = " green "；
> } else if(health = = " Fair "){
> health indicator color = " yellow "；
> } else if(health = = " poor "){
> health indicator color = " red "；
> } else if(health = = " life _ support "){
> health indicator color = " orange "；
> } else {
> health indicator color = " purple "；
> }
> 
> 标签 1。Color = (label1IsRequired)？“红”:“黑”；
> 标签 2。Color = (label2IsRequired)？“红”:“黑”；
> 标签 3。Color = (label3IsRequired)？“红”:“黑”；

# 多个 Return 语句与一个 Return 语句

导致争论的两种特殊风格是多重返回和单一返回。关于方法是否应该有一个 return 语句，或者多个 return 语句是否可以接受，出现了分歧。每种方法都有优点和缺点。

**多重返回语句:**多重返回语句会导致代码难以理解、理解和测试。但是，有多个返回的方法可能比只有一个返回的函数短。

> SomeDataType someMethod(param1，param2，param 3){
> some datatype retVal；
> if(param 1 = = null){
> retVal = null
> }
> if(retVal = = null){
> 返回 retVal；
> }
> 
> if(param2！= null){
> retVal = param 2；
> }
> 如果(retVal。Equals(param2)){
> 返回 retVal
> }
> retVal = param 3；
> 返回 retVal
> }

**一个返回语句:**一个单独的返回语句可能导致长方法。然而，这些过程有一个单点出口，简化了测试和调试。

> some datatype some method(){
> some datatype retVal；
> //数百或数千行代码
> 返回 retVal
> }

**潜在的解决方案:**当代码被不一致地使用时，多次返回会使代码难以理解、遵循和测试。单个 return 语句会导致长方法，当它们被冗长的代码段处理时。通过使用几个而不是一个 return 语句，可以缩短这些冗长的时间跨度，或者至少使其可读。当它们跟随一小段代码时，单次返回是完全可以接受的。任何对单个返回语句或多个返回语句的明显误用都应该被修复，以应用这些风格中的一种被接受的用例。(**注意:**修正可能需要大量的重构。)

> SomeDataType someMethod(param1，param2，param 3){
> if(param 1 = = null | | param 3 = = null){
> 返回 null；
> }
> some datatype retVal = null；
> if(param2！= null {
> retVal = param 2；
> } else if(param1！= null){
> retVal = param 1；
> } ele if(param3！= null){
> retVal = param 3；
> }
> 返回 retVal
> }
> 
> SomeDataType someMethod(param1，param 2){
> some datatype retVal = null；
> for(int I = 0；I<param 1 . length；i++) {
> if(param1[i].equals(param 2)){
> retVal = param 1[I]；
> 破；
> }
> }
> 返回 retVal
> }在循环中中断和继续使用

中断和继续结构是激烈辩论的主题。一方面，开发人员认为中断并继续可以简化控制流。其他程序员认为这些特性使程序的逻辑变得复杂。中断并继续肯定可以用来简化或复杂化代码。这些线可以被发现。

**中断并继续使用:**这些元素可以简化代码，但也可能使代码变得不必要的复杂。

> SomeDataType someMethod(param1，param 2){
> some datatype retVal = null；
> for(int I = 0；I<param 1 . length；i++){
> if(param 1[I]= = null){
> 继续；
> }
> if(param1[i].equals(param 2)){
> retVal = param 1[I]；
> 破；
> }
> }
> 返回 retVal
> }
> 
> SomeDataType someMethod(data，param 1){
> some datatype retVal = null；
> do something:
> for(int I = 0；我< retVal！= nulli++){
> if(I>= data . length){
> break；
> }
> 如果(数据[i].equals(param 1)){
> retVal = data[I]；
> } else {
> 继续；
> }
> }
> 
> if(retVal = = null){
> data—refresh data()；
> 去做某事；
> }
> 
> 返回 retVal
> }

大多数开发人员认为代码应该使用简单的机制来控制流程。哪个具体机制简单是争论的源头。当每种工具都以被广泛接受的方式使用时，这种争论就变得不那么激烈了。对于中断和继续，确实存在可接受的方法。坚持这些惯例以防止分歧并简化控制流程。任何严重违反这些标准的控制手段都应该不加辩论地予以纠正。

> SomeDataType someMethod(data，param 1){
> some datatype retVal = null；
> for(int I = 0；I<param 1 . length；i++) {
> if(data[i] == null){
> 继续；//跳过剩余的循环
> }
> if(data[i])。equals(param 2)){
> retVal = data[I]；
> 破；//不要再循环 b/c 我完成了
> }
> }
> return retVal；
> }

# 防御性例外

异常是指出问题或避免未来问题的一种手段。代码的哪些部分应该指出或避免哪些令人头疼的问题是一个激烈争论的话题。在分歧的一端，编码人员认为普遍的防御性异常可以防止错误，并使错误易于定位。然而，正如一些程序员所争论的那样，这些防御措施会使代码变得臃肿和难以理解。争论双方的开发商都有道理。防御性例外有利也有弊。

**防御型异常的好处和坏处:**使用防御型异常可以防止错误和其他问题，并且具有最小的缺点。当这种技术被不加区别地使用时，这些缺陷就会被放大。

> void someMethod(param1，param 2){
> if(param 1 = = null | | param 2 = = null){
> throw new ArgumentNullException("缺少一个或多个参数")；
> }
> //做方法的东西
> }
> 
> void someMethod(param1，param 2){
> //数十行防御检查…..
> //执行方法
> 的其余部分

**潜在解决方案:**当防御异常被部署在可接受的用法中时，它们的缺陷是最小的。任何背离这些惯例的技术部署都应该被纠正，除非提供了令人信服的理由。

> public void someMethod(param1，param 2){
> //检查公共方法
> 中的每个参数 if(param 1 = = null | | param 2 = = null){
> throw new ArgumentNullException("缺少一个或多个参数")；
> }
> 
> //避开无效数据引起的问题
> if(！isValid(param1) ||！isValid(param2)) {
> 抛出新的 InvalidParameterException("一个或多个参数无效")；
> }
> 
> //用参数
> 做点什么

# 总结

好的和坏的开发人员都会使用这些代码结构和技术。程序员也是人。人类有倾向性。这些倾向在代码中表现出来。偶尔，一个开发人员的冲动会导致他编写出其他编码人员正确批评的代码。被嘲笑的开发者不一定是糟糕的程序员。批评他的程序员不一定是好的开发者。在某一点上，两个人都可能被他们的偏好引入歧途。这些欲望不应该导致发展退化成永无止境的相互辱骂。相反，程序员应该互相审查代码，将他们的战斗限制在最糟糕的部分，并同意通过上述规则解决某些争论。