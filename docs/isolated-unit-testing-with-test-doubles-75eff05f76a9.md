# 使用测试替身的隔离单元测试

> 原文：<https://medium.datadriveninvestor.com/isolated-unit-testing-with-test-doubles-75eff05f76a9?source=collection_archive---------9----------------------->

[![](img/3a63c8456d24a8633c13a2a1060c2bfc.png)](http://www.track.datadriveninvestor.com/1B9E)![](img/e97361ec5e4f2a0d68c76ead7cd81d1b.png)

## Ruby 中一个非常简单的例子，带有 rspec 和 rspec-mocks

当实践测试驱动开发时，确保单元测试实际上只测试代码库的一个单元(通常是一个类)是很重要的。如果您的单元测试过于依赖外部类，那么确定测试失败的原因就变得很困难。实现隔离的一个常见方法是实现 test double，而不是依赖外部类的内部工作方式。

像特技替身一样，替身测试者会立即行动，替换测试中的真实物体。测试替身有助于隔离您的单元测试，确保您编写的测试实际上测试了单个单元。它们还可以通过避免昂贵或缓慢的过程来帮助加速您的测试，例如向实际的 API(您可能拥有也可能不拥有)发出请求，或者查询数据库(可能包含生产数据或者需要被植入)。

被测试的方法或类通常被称为被测系统，或 SUT。在强类型语言中，test double 必须符合 SUT 所依赖的对象的接口。通过符合对象的接口，SUT 不知道它是在一个对象中传递的，而不是在生产中通常接收的对象。在像 Ruby 这样的动态语言中，doubles 充当了 [duck types](https://en.wikipedia.org/wiki/Duck_typing) 的角色，响应它所代表的系统的实现中存在的方法调用。在这个例子中，我们将使用 Ruby 和 RSpec 关注后一种类型。

本文假设您已经熟悉单元测试(特别是 RSpec)。如果你对这些话题还不太适应，在回到模拟之前，这里有一些推荐读物。

*   关于测试的三个层次的介绍:“[实用测试金字塔](https://martinfowler.com/articles/practical-test-pyramid.html)”
*   关于用 RSpec 进行单元测试的介绍:[“RSpec 介绍”](https://www.theodinproject.com/courses/ruby-programming/lessons/introduction-to-rspec)

# 关于命名法的一个注记

如果你看看测试替身和模拟之间的区别，你可能会惊讶地发现，对他们的区别并没有达成共识。 [Martin Fowler](https://martinfowler.com/articles/mocksArentStubs.html#TheDifferenceBetweenMocksAndStubs) 认为前者利用状态验证，而后者利用行为验证来测试给定的对象。虽然这种区别可能在理论层面上起作用，但您选择的嘲讽框架通常会决定您的区别。例如，rspec-mocks 模糊了两者之间的区别。根据 RSpec 模拟[文件](http://rspec.info/documentation/3.4/rspec-mocks/):

> rspec-mocks 是一个 rspec 的双重测试框架，支持生成的双重测试和真实对象上的方法存根、假货和消息预期。

不同模拟库和框架之间的模拟和双精度测试的不同实现，使得必须始终阅读文档，而不是依赖于关于模拟或双精度测试实际上是什么的先入为主的概念。

与软件开发的大多数方面一样，持有强烈观点的热情开发人员通常会支持或告诫某些关于测试的哲学。我的目标并不是要说服你应该选择一种测试方法而不是另一种。相反，我希望证明，一旦您熟悉了可用的工具，隔离单元测试并不困难。

# 一个简单有益的例子

![](img/f2d6552b99a61d1de624a35bc36e809c.png)

在一个更完美的世界里，每个人都会有一只宠物。人类将能够通过预定的动作与它的宠物互动:喂食、抚摸等。这些行为会影响宠物的情绪和身体素质。

为了将该行为抽象成面向对象的代码，我们可以考虑几个捕获所需行为的类。首先，我们需要一个用宠物初始化的`Human`类。因为不同种类的宠物彼此差异很大，所以我们想要创建一个类的层次结构来表示不同的可能的宠物种类。超类`Pet`将包含所有宠物共有的功能。在这个例子中，我们假设所有的宠物都在吃东西，它们都会发出某种声音。一个特定的物种将能够进一步完善所有宠物共有的行为，它甚至可能添加自己独特的行为。

在这个例子中，`Human`类将依赖于`Pet`类(可能还有它的继承类),因为`human`实例将调用`pet`实例上的方法。换句话说，`Human`类是我们的 SUT。为了演示 doubles 的使用测试如何允许我们在类的依赖项被创建之前开发和测试一个类，我们将在测试它的同时开发我们的`Human`类。

# 实例化一个人

我们可以遵循 Freemand 和 Pryce 在*Growing Object-Oriented Software By Tests*和中的建议，编写我们的测试，就好像被测系统的实现已经存在一样(84)。这种方法帮助我们开始考虑好的变量名和方法名。该策略还帮助我们开始了解实例化和对象需要多少设置。复杂、冗长的设置可能意味着我们可以将一些设置步骤抽象成一个不同的类。

使用 [RSpec expectations](https://www.rubydoc.info/gems/rspec-expectations/frames) ，我们的第一个测试应该简单地断言一个实例化的`human`包含并公开一个`pet`。我们真的不想偏离构建`Pet`类的轨道，但是为了确保我们的 doubles 匹配我们最终的实现，我们将创建`instance_double`而不是一个普通的旧`doubles`。当使用`instance_double`时，如果您想要替换的对象不包含您想要使用的方法，RSpec 将抛出一个错误。

```
describe Human do
  context "init" do 
    it "should initialize a Human with a Pet" do
      pet = instance_double("Pet") 
      human = Human.new(pet)
      expect(human.pet).to eq(pet)
    end
  end
end
```

我们的测试失败并出现错误是不足为奇的:

```
An error occurred while loading ./spec/human_spec.rb.
Failure/Error:
  describe Human do
    context "init" do
      it "should initialize a Human with a Pet" do
        pet = instance_double("Pet")
        human = Human.new(pet)
        expect(human.pet).to eq(pet)
      end
    end
  endNameError:
  uninitialized constant Human
# ./spec/human_spec.rb:6:in `<top (required)>'
```

通常我会通过做最少的事情来解决一个错误，重新运行测试，并重复这个循环，直到我最终失败。实际上，为了避免本文中的大量冗余，我会多写一点代码。因为每个人都需要一只宠物，我们将确保每个新的`human`都必须创建一个`pet`，并且我们将通过一个`attr_reader`来访问那个`pet`。

```
class Human 
  attr_reader :pet

  def initialize(pet)
    [@pet](http://twitter.com/pet) = pet 
  end 
end
```

在像 Java 这样的强类型语言中，您需要确保 test double 符合预期的接口。否则，您的代码将无法编译，并且您将无法运行您的测试。对于 Ruby，我们需要在我们的`#initialize`中更加详细一点。

```
class Human 
  attr_reader :pet 

  def initialize(pet)
  raise ArgumentError.new("A Human must be initialized with a Pet") unless pet.is_a?(Pet)  

  [@pet](http://twitter.com/pet) = pet
  end
end
```

不幸的是，我们的 test double 不是`Pet`的实例。如果您在测试中使用`puts(pet.class.name)`，您会看到`pet`实际上是`RSpec::Mocks::InstanceVerifyingDouble`的一个实例。为了防止初始化时出错，我们需要*存根*我们希望 double 返回的响应。我们将在下面进一步探讨存根，但是存根只是对方法调用的硬编码响应。下面，您可以看到我们是如何指定方法的

```
context "init" do 
  it "should initialize a Human with a Pet" do
    pet = instance_double("Pet")
    allow(pet).to receive(:is_a?).with(Pet).and_return(true) # STUB CONFIGURATION
    human = Human.new(pet)
    expect(human.pet).to eq(pet)
  end
end
```

我们的单一测试现在应该是绿色的！当然，这个错误是意料之中的行为，所以我们应该为这个场景创建一个测试。为了避免给人留下 test double 是一种`Pet`的印象，我们将移除 test double 并传入一个 String 类型的参数。

```
it "should throw an error if a Human is not initialized with a Pet" do
  pet = "Not a pet"
  expect { Human.new(pet) }.to raise_error(ArgumentError)
end
```

# 喂养我们的宠物

![](img/bcbe3778fd2ff3208236495c4e546597.png)

如果你养了一只猫，你可能会被大声的喵喵叫声吵醒，要求食物。考虑到这一点，我们应该让人类做的第一件事就是给它毛茸茸的朋友喂食。像人类一样，宠物也会经历饥饿，所以喂养它会改变它的饥饿程度。

即使是这样一个简单的例子，我们也很快触及了单元测试的边界:外部依赖性。在现实世界中，您调用的方法可能不会像我们即将实现的方法那样简单。他们也可能改变。它们甚至可能不会像预期的那样工作。为了避免您为找出可能错误的来源而头疼，您希望确保您的单元测试中没有单元与另一个单元的实现相耦合。

在这种特定情况下，我们可以使用间谍实现独立测试。

## **间谍**

![](img/dd3d8b5394b57a163efa0530215261d0.png)

顾名思义，间谍监视一个对象，跟踪对一个对象的方法的调用次数，甚至是传递到这些调用中的参数。根据您正在使用的模仿库，spy 可能会在不改变其底层行为的情况下包装自己。然而，rspec-mocks 创建了间谍`as_null_object` s，所以你正在监视的代码永远不会运行。尽管这种行为可能看起来很烦人，但它最终有助于专注于开发当前测试下的系统。

如上所述，我们使用一个`instance_spy`而不是一个普通的旧的`spy`来构建一个非常简单的依赖框架。

```
context "feeding a pet" do 
    it "should cause the pet to eat" do 
      pet = instance_spy("Pet")
      human = Human.new(pet)

      human.feedPet()
      expect(pet).to have_received(:eat) # SPY ASSERTION
    end
  end
```

因为我们还没有创建`#feedPet`方法，所以我们得到以下错误:

```
Failures:1) Human feeding a pet should cause the pet to eat
     Failure/Error: human.feedPet()NoMethodError:
       undefined method `feedPet' for #<Human:0x00007f9780057db8>
     # ./spec/human_spec.rb:19:in `block (3 levels) in <top (required)>'
```

根据我们的错误，稍微超出了它的要求，我们向`Human`添加了下面的实例方法。

```
def feedPet() 
    self.pet.eat()
end
```

然而，这仍然会给我们带来预期的误差:

```
Failures:1) Human feeding a pet should cause the pet to eat
     Failure/Error: self.pet.eat()
       the Pet class does not implement the instance method: eat
     # ./lib/human.rb:9:in `feedPet'
     # ./spec/human_spec.rb:19:in `block (3 levels) in <top (required)>'
```

现在要消除我们的错误所需要的就是下面这个对`Pet`类的空实例方法:

```
def eat()
end
```

如果你对这个空方法感到不舒服，你总是可以在它里面提出一个错误。这样，如果您不小心调用了实际的方法，您会马上知道。如上所述，`pet` test double 不会调用实际的方法，即使它要求该方法存在。

```
def eat() 
  raise "Pet#eat has not been implemented"
end
```

当我们稍后到达`Pet's`单元测试时，我们可以确定我们实际上想要`#eat`方法做什么。也许我们希望跟踪宠物的饥饿水平，当它被喂食时，饥饿水平会增加一。也许我们想跟踪宠物的体重，如果宠物已经吃饱了还吃东西，体重就会增加。也许这只宠物就像我的老猫一样，不管你怎么喂它，它的饥饿程度都会很高。因为我们的独立测试，我们可以专注于`human`的行为，而不用同时关心`pet`的行为或状态的变化。

# **模仿宠物**

可以肯定地说，每个宠物主人都模仿过它的宠物发出的声音，所以我们接下来将测试这一点。这个测试的幼稚方法可能是断言我们期望从宠物那里收到的字符串。然而，宠物的声音改变有很多原因。也许猫饿的时候会发出嘶嘶声，但是吃饱了就会发出咕噜声。或者我们的`human`在它的旧宠物逃跑后收养了一个新物种。

## 存根

我们将利用一个存根，而不是依赖一个很可能会改变的值。断言一个存根响应有助于我们遵守 [Liskov 替换原则](https://en.wikipedia.org/wiki/Liskov_substitution_principle)，该原则声明“程序中的对象应该可以用它们的子类型的实例替换，而不会改变程序的正确性。”换句话说，只要`pet`表现得像`pet`并公开预期的方法，我们的`human`与哪种`pet`交互就不重要。

如上所述，我们依靠一个`instance_double`来确保我们已经为我们的依赖类奠定了基础。

```
context "imitating a pet" do 
  it "should speak the sound that its pet makes" do 
    pet = instance_double("Pet")
    stubbedPetSound = "Oink" 
    allow(pet).to receive(:speak).and_return(stubbedPetSound)
    human = Human.new(pet) imitation = human.imitatePet()
    expectedImitation = "It's so funny when my pet says #{stubbedPetSound}"
    expect(imitation).to eq(expectedImitation)
  end
end
```

到目前为止，我们应该非常熟悉我们预期会收到的错误。

```
Failures:1) Human imitating a pet should speak the sound that its pet makes
     Failure/Error: allow(pet).to receive(:speak).and_return(stubbedPetSound)
       the Pet class does not implement the instance method: speak
     # ./spec/human_spec.rb:29:in `block (3 levels) in <top (required)>'
```

在创建了一个空的`Pet#speak`方法之后，我们将跳过我们知道会因为没有实现`Human#imitatePet`而收到的错误，现在创建那个方法。

```
def imitatePet() 
    return "It's so funny when my pet says #{self.pet.speak()}"
end
```

当单元测试依赖于另一个类的方法的返回值的实例方法时，存根非常有用。在我们上面的例子中，我们不知道我们的宠物会发出什么样的声音。我们甚至不知道主人会养什么样的宠物。当这些东西最终在`Pet`类中改变时，只要公开的方法签名保持不变，我们的`Human`测试就不必改变。

因为我们的`Pet`类还没有外部依赖，所以它不需要 rspec-mocks 框架来保持隔离。只要它没有外部依赖，测试这个类就应该相对简单，所以我不会演示它的测试。

希望这个简单的例子能帮助你理解如何利用模拟来隔离你的单元测试，以及为什么考虑隔离是重要的。

## 如需进一步阅读:

[模仿不是树桩，](https://martinfowler.com/articles/mocksArentStubs.html#TheDifferenceBetweenMocksAndStubs)马丁·福勒

[状态验证](http://xunitpatterns.com/State%20Verification.html) v. [行为验证](http://xunitpatterns.com/Behavior%20Verification.html)