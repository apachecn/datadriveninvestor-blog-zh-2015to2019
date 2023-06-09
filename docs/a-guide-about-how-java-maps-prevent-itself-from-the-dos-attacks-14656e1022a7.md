# 关于 Java Maps 如何防止 DOS 攻击的指南？

> 原文：<https://medium.datadriveninvestor.com/a-guide-about-how-java-maps-prevent-itself-from-the-dos-attacks-14656e1022a7?source=collection_archive---------7----------------------->

[![](img/5763fc2304cf55a9402350b601139455.png)](http://www.track.datadriveninvestor.com/1B9E)

Java 是世界上最流行的编程语言之一，这也是为什么如此多的企业选择 Java 开发来构建他们的软件应用程序。我们都知道 Java 是一种更加安全和健壮的编程语言，因此 Java 开发者能够创建能够防止 DOS 攻击的应用程序。让我们来理解 Java 是如何发展和提高其防止任何类型的 DOS 攻击的能力的。

**Java 中的地图界面**

在 Java 中，java.util.Map 接口表示键和值之间的映射。映射接口不是集合接口的子类型。因此，它的行为与其他集合类型稍有不同。map 有一个众所周知的漏洞，就是创建许多字符串作为键，它们都有相同的散列码。在本文中，我们将看到这是多么容易做到，以及 Java 8+和最新的 Java 版本 HashMap 如何保护自己。

**Java 1.2 中 Java Maps 哈希代码的实现**

你可以和任何一家 Java 开发公司交谈，他们会告诉你 Java 在过去有多安全。让我们讨论一下在 Java 的早期版本中，Java Maps 是如何保护自己的。在 Java 1.2 时代，有一本名为“Java 2 性能和习语指南”的书，书中说我们不应该直接使用 String 作为 HashMap 中的一个键，而应该用一个类包装它，然后缓存 hash 代码。实际上，缓存一个键的哈希代码并不能实现那么多，因为它被缓存在哈希表中。当我们调用 put()和 get()时，我们通常会创建新的键对象来实现这一点，然后再丢弃它们。如果我们抓住关键，我们也可以抓住价值。虽然在某些特定情况下，缓存哈希代码可以提高性能，但一般来说，这并没有多大用处。

[](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) [## 2019 年最值得学习的编码语言——数据驱动的投资者

### 在我读大学的那几年，我跳过了很多次夜游去学习 Java，希望有一天它能帮助我在…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/21/best-coding-languages-to-learn-in-2019/) 

**从 Java 1.0 过渡到 1.2**

让我们以 Java 1.0 为例。在此期间，String 的 hashCode()函数为 O(1)。它最多需要 16 次计算。如果字符串大于 16 个字符，那么它将选取其中的 8 个字符，并使用这些字符生成一个哈希代码。在 Java 1.2 中，他们改变了算法，使用完整的字符串进行计算，因此它变成了 O(n)。如您所知，字符串越长，hashCode()完成所需的时间就越长。因此，在从 Java 1.1 升级到 1.2 的过程中，更改 String 中的哈希代码会导致很多问题。此外，在版本之间移动时，持久哈希表是一个挑战，因为字符串的哈希值现在指向不同的条目。

**Java 1.3 中 Java Maps 哈希代码的实现**

太阳微系统公司在 1996 年推出了 Java，很快很多人开始倾向于雇佣 Java 开发人员来开发他们的应用程序。在 Java 1.3 中，Java 开发人员(即 Sun Microsystems/Oracle 工程师)决定将散列代码缓存在字符串本身中。由于 Java 的广泛流行，他们不愿意增加一个明显的保护来抵御恶意攻击。如果散列码是 0，它将计算它，否则简单地返回它。如果他们使用不同的数字会好得多，因为默认值 0 实际上是一个糟糕的默认值。其他的都可以。因此，哈希代码方法的结构现在看起来像这样

public int hashCode() {

int h = hash

if (h == 0 && value.length > 0) {

//计算哈希代码并将其赋给 hash 和 h

}

返回 h；

}

哈希代码的实际计算现在是这样的

for(int I = 0；I< value.length; i++) {

h = 31 * h + val[i];

}

**Java 9 中 Java Maps 哈希代码的实现**

在 Java 9 之后，由于紧凑的字符串，它变得稍微复杂了一些，但是实际上最终的结果是一样的。例如，字符串“ABC”的哈希代码为((' A' * 31) + 'B') * 31 + 'C '。让我们在 Java 9 引入的 jshell 控制台的代码中检查一下:-

jshell> (('A'*31)+'B')*31+'C '

$1 ==> 64578

jshell >“ABC”。哈希码()

$2 ==> 64578

jshell >(((((((' A ' * 31)+' B ')* 31+' C ')* 31+' D ')* 31+' E ')* 31+' F ')* 31+' G '

$3 ==> -488308668

jshell >《ABCDEFG》。哈希码()

$4 ==> -488308668

jshell >“aaaaaaaa”。哈希码()

$5 ==> -518878239

jshell >“zzzzzzz”。哈希码()

$6 ==> 215481018

你可以在上面的代码中看到,“AAAAAAA”的 hashcode 是负数，而“zzzzzzz”的 hashcode 是正数。如果我们更详细地了解字母表[A-Za-z]中的 7 个字符串，您会发现所有这些都被抵消了，哈希代码等于 0。hash 码为 0 的字符串的重要性在于，如果我们找到一个 hash 为 0 的字符串，我们可以把它和同一个字符串组合起来，它仍然是 0。我们可以让它尽可能长，它将始终只有一个散列码 0。例如，以字符串“ASDZguv”为例。让我们把它组合成一个很长的字符串:-

jshell >“ASDZguv”。哈希码()

$1 ==> 0

jshell >“ASDZguvASDZguv”。哈希码()

$2 ==> 0

jshell >“ASDZguvASDZguvASDZguvASDZguv”。哈希码()

$3 ==> 0

如果我们走极端，那么我们可以创建一个近 20 亿字符长的字符串:-

公共类 VeryLongString {

公共静态 void main(字符串...args) {

StringBuilder sb = new StringBuilder(1 _ 999 _ 999 _ 995)；

for(int I = 0；i < 285 _ 714 _ 285i++) {

sb . append(" ASDZguv ")；

}

string s = sb . tostring()；

for(int I = 0；i < 10i++) {

long time = system . nano time()；

尝试{

system . out . println(s . hashcode())；

}最后{

time = system . nano time()-time；

System.out.printf("time = %dms%n "，(time/1 _ 000 _ 000))；

}

}

}

}

在普通计算机上，每次调用 hashCode()大约需要两秒钟。创建更多更长的字符串将花费更多的时间，因此这不是对哈希映射发起攻击的最佳方法，因为哈希映射本身会通过在内部缓存条目的哈希代码来保护自己。因此，hashCode()在 put()上被调用一次，然后在 get()上被调用一次。

严重的情况是，有人将许多哈希代码为 0 的字符串组合在一起。因为产生的散列码也是 0，所以我们可以制作大量的散列码。实际上，具有相同哈希码的字符串的数量会导致高危险，而不是一个字符串的长度。

在一篇名为 Unhashing a String 的文章中，作者 Joe Darcy 展示了一个很好的算法，通过逆向运行该算法，可以用任何目标哈希代码创建字符串。如果我们想创建一个带有特定字母表的字符串，比如只包含[A-Za-z]范围内的字符，那就有点棘手了。有一些情况是创建数十亿个 String 对象，然后调用它们的 hashCode()，希望通过蛮力找到一个只有 0 值的。现在我会给你一个递归的方法，它可以很好地搜索长度为 7 的字符串和字母表[A-Za-z]。

公共抽象类 BruteForceBase {

受保护的静态最终字节[] alphabet =新字节[26 * 2]；

静态{

for(int I = 0；i < 26i++) {

字母表[i] =(字节)(' A '+I)；

字母表[i + 26] =(字节)(' a '+I)；

}

system . out . println(" alphabet = "+新字符串(alphabet))；

}

}

导入 Java . util . *；

公共类 bruteforecructure 扩展了 BruteForceBase {

公共静态 void main(字符串...args) {

byte[] is =新字节[7]；

Arrays.fill(是，(字节)'！');

check(0，0，is，0)；

}

静态 void 检查(int depth，int h，byte[] is，int target) {

if(深度== 7) {

if (h == target) {

System.out.println(新字符串(is))；

}

返回；

}

for(字节 I:字母表){

is[深度]= I；

check(深度+ 1，h * 31 + i，是，目标)；

}

}

}

这在普通计算机上执行得相当快，在大约 40 秒内运行大约 100 亿个散列码。当我们使用嵌套循环而不是递归时，运行时间大约需要 26 秒。下面是嵌套循环版本:-

公共类 BruteForceNestedLoops 扩展了 BruteForceBase {

公共静态 void main(字符串...args) {

int target = 0；//我们的目标哈希代码

for(字节 i0:字母表){

int h0 = i0

for(字节 i1:字母表){

int h1 = h0 * 31+i1；

for(字节 i2:字母表){

int H2 = h1 * 31+I2；

for(字节 i3:字母表){

int H3 = H2 * 31+i3；

for(字节 i4:字母表){

int H4 = H3 * 31+i4；

对于(字节 i5:字母表){

int H5 = H4 * 31+i5；

for(字节 i6:字母表){

int h6 = H5 * 31+i6；

if (h6 == target) {

byte[]为= {i0，i1，i2，i3，i4，i5，i6 }；

System.out.println(新字符串(is))；

}

}

}

}

你能理解这段代码中发生了什么吗？我们生成的所有字符串都有相同的散列码 0。因此，它们最终都在同一个桶中。在 Java 6 中，这是一个问题，因为桶冲突链表——get()和 put()在时间和成本上是线性的。让我们看看如果你用 Java 6 运行代码，你会看到什么样的数字。稍后我们还会在更高版本的 Java 中看到它，这样你就可以对它们进行比较了。

java 版本“1.6.0_65”

用 128 码测试

时间= 338 毫秒

用 256 码测试

时间= 1371 毫秒

用 512 码测试

时间= 3013 毫秒

用 1024 码测试

时间= 11896 毫秒

用 2048 码测试

时间= 26362 毫秒

使用 4096 号进行测试

时间= 61376 毫秒

你可以很容易地发现这是线性的，因为当条目的数量加倍时，时间也加倍。垃圾收集器和内存布局等其他因素也有可能发挥作用。如果你用 L3 代替 L2，那么你会看到超过 2 倍的减速。

在 Java 7 中，Java 开发人员意识到世界上大多数 HashMaps 键都是字符串。他们还意识到最大的风险是当我们能够可靠地创建散列码为 0 的字符串时。因此，他们创建了第二个哈希算法，可以在 HashMap 中使用，称为 hash32()，它是随机的，以防止类似于我们上面的类中的漏洞。最好将其阈值配置为 512，例如 djdk . map . altashing . threshold = 512。由于我们不能故意造成桶冲突，字符串将很好地分布在整个表中，并给我们恒定的时间查找，尽管线性成本仍然是可能的。现在让我们检查一下 Java 7 的输出，其中 althashing threshold 设置为 512:

带有-djdk . map . altashing . threshold = 512 的 java 版本“1.7.0_80”

用 64 码测试

时间= 206 毫秒

用 128 码测试

时间= 412 毫秒

用 256 码测试

时间= 3 毫秒

用 512 码测试

时间= 3 毫秒

用 1024 码测试

时间= 3 毫秒

*剪下*

使用尺寸 65536 进行测试

时间= 4 毫秒

使用尺寸 1048576 进行测试

时间= 3 毫秒

使用尺寸 4194304 进行测试

时间= 3 毫秒

Java 8 中的一件好事是，Java 开发人员去掉了 String 中的 hash32()方法，决定用更通用的方法来解决这个问题，也就是说，如果在一个桶中有超过一定数量的冲突，HashMap 会创建一个条目二叉树。这就是为什么在编写 hashCode()和 equals()时，应该始终在 Java 代码中实现 Comparable。

下面是在 Java 8 中的运行。在更高版本的 Java(即 Java 9、10 和 11)中的结果也是相同的。

java 版本“1.8.0_181”

用 64 码测试

时间= 80 毫秒

用 128 码测试

时间= 94 毫秒

用 256 码测试

时间= 109 毫秒

用 512 码测试

时间= 122 毫秒

用 1024 码测试

时间= 222 毫秒

使用尺寸 65536 进行测试

时间= 220 毫秒

使用尺寸 1048576 进行测试

时间= 277 毫秒

**结论**

虽然 Java 是一种健壮和安全的编程语言，但是从它的第一个版本 Java 1.0 到 Java 8，我们已经看到了 hashcode 是如何被实现来最大限度地防止 DOS 攻击的。我们已经看到，当我们遇到大量桶冲突时，Java 8 以后的性能要比以前的版本好得多。我们已经展示了在早期的 Java 版本中它是 O(n ),现在在最新的版本中它是 O(log n)。尽管在 Java 8 以后的版本中调用 get()花费的时间很少，但是如果有人给我们发送了大量具有完全相同的哈希代码的字符串，我们现在可以安全地避免这种情况，并且我们现在更加确信 Java Maps 可以防止任何类型的 DOS 攻击。