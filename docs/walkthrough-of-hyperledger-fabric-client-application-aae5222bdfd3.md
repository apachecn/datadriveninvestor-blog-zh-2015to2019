# Hyperledger Fabric Node SDK 和客户端应用程序的演练

> 原文：<https://medium.datadriveninvestor.com/walkthrough-of-hyperledger-fabric-client-application-aae5222bdfd3?source=collection_archive---------0----------------------->

![](img/4a22092894e74a5db2b5af1aef56dd42.png)

Photo by [designecologist](https://www.pexels.com/@designecologist) in [pexels](https://www.pexels.com)

Hyperledger Fabric 是一个基于容器的区块链框架，用于开发使用即插即用组件的分散式应用程序，旨在使其模块化。这并不意味着我们不能本地创建网络组件(对等点和订购点)。但这并不是软件分发的方式。然而，chaincode 目前只支持容器化(沙箱)环境。

在[上一篇文章](https://medium.com/coinmonks/start-developing-hyperledger-fabric-chaincode-in-node-js-e63b655d98db)中，我已经描述了 Nodejs 链码的核心组件和实现。我们已经建立了我们的开发环境，开发了我们的链码，让一切都在本地运行。我们通过 CLI 容器安装和调用了所有的 chaincode 函数。一切看起来都很好。现在怎么办？这就是我们想要的一切吗？当然不是！我们根本不应该满足。我们需要做更多的工作。作为开发者，我们的目标是用户。毕竟，用户会坐在那里为特定的操作运行各自的 docker 命令吗..？不要！。我们需要建立一个简洁的可点击操作的图形用户界面。

[](https://www.datadriveninvestor.com/2019/02/13/5-real-world-blockchain-applications/) [## 5 行业转型区块链应用|数据驱动投资者

### 除非你一直生活在岩石下，否则我相信你现在已经听说过区块链了。而区块链…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/13/5-real-world-blockchain-applications/) 

自从最近最新发布的 Hyperledger Fabric 1.4 以来，人们渴望使用 Fabric 构建应用程序来解决他们的业务问题。但是，由于配置中结构的复杂性，许多人在构建网络时会遇到困难。如果这是某种程度的复杂性，构建中间件和客户端也是一样的。因为网络是许可的，你不能直接访问网络 API。您需要提供正确的身份和证书才能访问网络。这种对外的认证可以由认证机构(CA)使用 Hyperledger Fabric SDK 提供。然而，在官方文档中有一个很好的教程“[编写您的第一个应用程序](https://hyperledger-fabric.readthedocs.io/en/release-1.4/write_first_app.html)”，解释了客户端应用程序的关键组件。在本文中，我将解释 Hyperledger Fabric Node SDK 中可用的各种模块，以及为网络外部的各种参与者颁发证书所涉及的代码，以及 Fabric Node SDK 如何提供与容器化环境之外的 chaincode 进行交互的访问。

**连接轮廓**

为什么我在这里谈论连接配置文件？嗯，连接配置文件允许 SDK 连接网络。连接配置文件描述了对等体、订购者和认证机构的整个网络拓扑，以及哪些对等体是通道的一部分以及它们的位置。因此，每当客户端提交事务时，它将使用特定通道的连接配置文件中定义的配置填充所有对等体。您只能使用正确的连接配置文件连接到网络。连接配置文件通常由了解网络拓扑的管理员创建。连接配置文件在将客户端连接到网络方面起着关键作用。下面是关于[连接轮廓](https://hyperledger-fabric.readthedocs.io/en/release-1.4/developapps/connectionprofile.html#scenario)的结构说明。

# **Hyperledger Fabric 节点 SDK 中的主要模块**

在下一节中，我们将浏览一些代码。因此，作为先决条件，我们需要对 Hyperledger Fabric SDK 中使用的模块、各种类和方法有基本的了解。所以不建议跳过这一节。

SDK 由三个主要模块组成

**1 .织物网**:

该模块提供了一个高级 API，用于与部署的链代码进行交互。交互包括提交交易和查询。

2.fabric-ca-client:

该模块提供各种认证操作，如用户注册和登记、网络上的重新登记。

3 .结构客户端:

该模块提供网络级操作，如创建通道、将对等体加入通道、安装和实例化链码、提交事务和查询链码、查询事务细节、块高度、已安装的链码等等。

尽管 **fabric-client** 能够执行许多操作，但推荐客户端应用程序使用**fabric-network**API 与部署到 Fabric 网络的智能合约进行交互。因为客户端应用程序的大多数关键类只能从 **fabric-network 继承。**

# **fabric-network** 中的关键类和方法

**光纤网络**有三个主要类别

## **1。网关**

**光纤网络**模块中的网关类用于连接运行中的光纤网络并与之交互。这个类包括各种方法。那些是，

**答:连接:**

这种方法使用现有的用户或管理员身份，根据连接配置文件中定义的对等体及其 IP 地址来连接正在运行的光纤网络。

**b .断开:**

此方法会断开与正在运行的结构网络的连接，并清理缓存。

**c .**T2【getClient:

此方法将当前注册的客户端详细信息作为对象返回。

**d. getNetwork:**

该方法与网络中的指定信道通信。

e. getContract 方法将访问部署到连接配置文件中定义的网络顶部的通道的特定链码。

**f. submitTransaction** 方法将提交一个指定的 chaincode 方法和 args 给对等体(背书者)。

**g** 。 **evaluateTransaction** 类似于 HTTP 请求中的 GET 方法，它只能读取总账状态，用于 chaincode 中的查询方法。

## **2。文件系统钱包**

此类定义了持续到结构文件系统的身份钱包的实现。这个类包括一些常见的方法**存在、导入、删除。**

**a .存在**:

此方法检查文件系统中是否存在提供的标识。

**b .进口:**

该方法将生成的 PKI 和 x509 证书和密钥导入到参与者身份下的文件系统 wallet 中。

**c .删除:**

此方法从文件系统 wallet 中删除特定用户的身份。

## **3。X509WalletMixin**

基本上，CA 以 PKI 格式(公钥基础设施)提供注册证书。此类用于使用 PKI 用户证书在 X.509 凭据模型中创建标识。该类包括用于创建身份的 **createIdentity()** 方法。该 X.509 证书用于签署网络中的交易。

# fabric-ca-client 中的关键方法

**fabric-ca-client** 几乎没有用于 ca 操作的通用方法。这些是**注册、注册、重新注册。**

**一个**。**寄存器**:

此方法用于注册新参与者。注册成功后，返回用户**秘密。**此**秘密**需要在报名时提供。

**b .报名:**

该方法用于在网络中登记注册的参与者。为了注册，用户必须首先注册。如果注册成功，此方法将返回基于 PKI 的证书和用户的私钥。

**c .重新报名:**

可能会出现证书过期或被泄露的情况(因此必须将其吊销)。这就是重新注册的情况，您使用这种方法再次向 CA 注册相同的身份以获得新的证书。

# **代码演练**

在代码演练的这一部分，我们将查看 fabcar 客户端应用程序，以了解如何为访问网络的客户端颁发证书(BYFN)。因此，请确保您正在查看 [fabric-samples](https://github.com/hyperledger/fabric-samples) 存储库中的 [fabcar](https://github.com/hyperledger/fabric-samples/tree/release-1.4/fabcar/javascript) 目录，或者克隆整个存储库，并切换到本地克隆中的 **fabcar/javascript** 目录。您应该看到**enrollment admin . js**、 **registerUser.js** 、 **invoke.js** 和 **query.js.** 这些是需要查看的主要文件。在 Hyperledger Fabric 中，证书颁发是一个两步过程-1。注册 2 .注册

此处的**enrollment Admin . js**用于在网络上注册管理员用户。当我们创建网络时，CA 的管理员用户将被注册为 **admin** 和 secret 为 **adminpw。**检查[这里](https://github.com/hyperledger/fabric-samples/blob/bc72f3e3a681eeca12dc4858d07e938244da825f/first-network/docker-compose-ca.yaml#L23)。所以我们只需要通过提供这些凭证来注册Admin。管理员用户注册后，将向管理员用户颁发基于 PKI 的公钥和私钥，然后还将颁发基于 X.509 的加密证书。这三个凭证将被导入到钱包中。

首先让我们打开**enrollment admin . js**，然而，代码被整齐地注释掉了。我们将回忆一下到目前为止我们所学的内容。

这里，第 7 行和第 8 行从 **fabric-network 导入 **fabric-ca-client** 和类 **FileSystemWallet、X509WalletMixin** 。**

```
const FabricCAServices = require(‘fabric-ca-client’);const { FileSystemWallet, X509WalletMixin }=require(’fabric-network’);
```

从第 12 行到第 14 行，定义了连接概要文件的绝对路径，并将连接概要文件的内容解析到 JSON 中。该连接简档包括关于网络的各种参与者的足够信息。该连接模式广泛用于连接网络。

```
const ccpPath = path.resolve(__dirname, '..’, '..’, 'first-network’, 'connection-org1.json’);
const ccpJSON = fs.readFileSync(ccpPath, 'utf8’);
const ccp = JSON.parse(ccpJSON);
```

从 main 函数中的第 20 行到第 24 行，使用 connection profile 配置来定义网络中使用的证书颁发机构。如果您可以在 first-network 中看到连接配置文件，则在文件的最下面一行有一个对象 **certificateAuthorities** ,其中包含与 CA 相关的所有信息。将使用连接配置文件中定义的 **url** 和**名称**创建 **FabricCAServices** 的新实例，并准备好注册管理员。如果管理员注册成功，这个 **ca** 实例也可以用于注册用户。

```
const caInfo = ccp.certificateAuthorities[‘ca.org1.example.com’];
const caTLSCACerts = caInfo.tlsCACerts.pem;
const ca = new FabricCAServices(caInfo.url, { trustedRoots: caTLSCACerts, verify: false }, caInfo.caName);
```

从第 24 行到第 30 行，一个新的目录 **wallet** 将在当前目录中创建。将为 **wallet** 创建一个新的 fabric FileSystemWallet 实例，以检查和导入身份。从第 30 行到第 34 行，它将使用 **FileSystemWallet** 类的 **exists** 方法检查管理员用户是否存在于 wallet 中。如果身份 **admin** 不存在，将继续注册。

```
const walletPath = path.join(process.cwd(), 'wallet');
const wallet = new FileSystemWallet(walletPath);
console.log(`Wallet path: ${walletPath}`);// Check to see if we’ve already enrolled the admin user.
const adminExists = await wallet.exists(‘admin’);
 if (adminExists) {
console.log(‘An identity for the admin user "admin" already exists in the wallet’);
        return;
        }
```

在第 37 行，调用来自 **fabric-ca-client** 模块的 **enroll** 方法，使用 **enrollmentID** 和 **enrollmentSecret** 作为参数对象。如前所述，如果注册方法成功，它将返回注册的**管理员**的基于 PKI 的证书和私钥的对象。

```
const enrollment = await ca.enroll({ enrollmentID: ‘admin’, enrollmentSecret: 'adminpw' });
```

在第 38 行，将通过提供在先前注册中生成的证书和私钥作为 **createIdentity()** 方法的参数，为 admin 创建 X.509 身份标准。

```
const identity = X509WalletMixin.createIdentity(‘Org1MSP’, enrollment.certificate, enrollment.key.toBytes());
```

当此方法成功时，它将返回基于 X.509 的加密签名证书。该证书可广泛用于注册新用户。在第 39 行，先前生成的 PKI 证书和 X.509 签名证书将在 **admin** 的身份下导入到 wallet 中。

```
await wallet.import(‘admin’, identity);
```

**注册用户:**

正如我们已经知道的，新用户的注册只能由 CA 完成，它应该有一个适当的 x509 标准签名证书来为新用户颁发身份。在前面的代码部分中，我们看到了管理员注册是如何完成的，以及 x509 签名证书是如何颁发给管理员的。同样的方法也适用于注册用户。为此，用户需要首先注册。虽然 **registerUser.js** 中的大部分代码类似于**enrollment admin . js，**我们将遍历**register user . js**中的一些新内容，因此，打开 **registerUser.js** 并在此处查看第 36 行**，来自 **fabric-network** 模块的网关**类用于连接网络。众所周知，只有经过授权的参与者才能访问网络。在这种情况下，CA admin 已经被授权，所以我们可以使用 CA admin 身份来连接网络。在下一行中，gateway 通过使用连接配置文件和钱包中的 **admin** 身份来启动到我们网络的连接。它要求网关查看本地主机，因为我们的网络是在本地运行的(asLocalhost : true)。

```
const gateway = new Gateway();

await gateway.connect(ccpPath, { wallet, identity: 'admin’, discovery: { enabled: true, asLocalhost: true } });
```

第 40、41 行返回 CA 的底层管理员。该管理员用于注册用户

```
const ca = gateway.getClient().getCertificateAuthority();const adminIdentity = gateway.getCurrentIdentity();
```

第 44 行使用 **register** 方法注册了一个新用户，将隶属关系、用户 Id、管理员身份作为参数的对象。正如前面模块介绍的， **register** 方法将返回新注册用户的密码，该密码可用于在网络上注册用户。

```
const secret = await ca.register({ affiliation: 'org1.department1’, enrollmentID: 'user1’, role: 'client' }, adminIdentity);
```

在下一行中，注册用户的秘密将被传递给 enroll 方法。用户注册完成后，将颁发 PKI 证书，然后为用户创建身份证书(X.509)。瞧..！！此身份将用于访问网络和与网络交互，X.509 签名证书将用于签名事务。然后，这三个凭证将以用户 **user1 的身份导入到钱包中。**

```
const enrollment = await ca.enroll({ enrollmentID: 'user1’, enrollmentSecret: secret });const userIdentity = X509WalletMixin.createIdentity(’Org1MSP’, enrollment.certificate, enrollment.key.toBytes());await wallet.import(’user1’, userIdentity);
  ```
```

**查询调用链码:**

在前面的章节中，我们已经看到了如何为管理员和用户颁发身份。在这一节中，我们将浏览使用上一节中创建的 **user1** 身份查询和调用 chaincode 的实际代码。因此，打开 **query.js，**传统上作为初始操作，它将导入所需的模块并定义连接配置文件，检查 admin 是否存在，然后检查用户是否注册。

在第 29–30 行，它将启动网关连接，使用 **user1** 身份与网络连接。

```
const gateway = new Gateway();

await gateway.connect(ccpPath, { wallet, identity: 'user1’, discovery: { enabled: true, asLocalhost: true } });
```

在第 33 行，网关将使用 **getNetwork()方法**访问网络中名为‘my channel’的通道

```
const network = await gateway.getNetwork(’mychannel’);
```

在第 36 行，网关将使用**网关**类**的 **getContract()** 方法访问‘my channel’中部署的契约(fabcar)。**

```
contract = network.getContract(’fabcar’);
```

在第 41 行，它将通过获取在**evaluteransaction()**中定义的参数(如果应用的话)来查询一个特定的 chaincode 方法。在这一行中，它查询 **queryAllCars** chaincode 方法。所以不需要论证。

```
const result = await contract.evaluateTransaction(’queryAllCars’);
```

**evaluteransaction()**方法是一个被**得到的**方法。它将简单地选择一个在连接配置文件中定义的对等点，并从该对等点查询特定键的分类帐状态，然后立即返回结果。

在 **invoke.js** 代码中，有一个 **submitTransaction()** 方法，通过取 chaincode 函数名和参数来提交事务。这里， **createCar** 函数将被带参数调用。

```
await contract.submitTransaction(’createCar’, 'CAR12’, 'Honda’, 'Accord’, 'Black’, 'Tom’);
```

因为它将数据写入分类账，所以交易将通过网络进行。一旦签核对等方执行交易，分类帐状态将更新为新车。

# 结论

现在，我们已经探索了 Hyperledger Fabric Node SDK 中的各种模块，并演练了注册和登记用户所涉及的代码。我们研究了 SDK 如何提供与 chaincode 函数交互的访问。您应该对应用程序如何使用 SDK 与区块链网络进行交互有很好的了解。这不是结局。现在一天的访问应用程序是由 REST API 完成的，它还没有在 Hyperledger Fabric 中正式提供。不过用其中一个著名的 JavaScript 库 **express 来构建 API 并不是很难。我做了几个 Hyperledger Fabric 应用程序，使用快速路由和传统的前端工具，目标是初学者。你可以在这里** 看一下其中的一个 [**。**](https://github.com/Salmandabbakuti/blockTrack)

快乐超帐织物🤗

# 参考

1.  https://github . com/hyperledger/fabric-samples/tree/v 1 . 4 . 3/fab car/JavaScript
2.  https://fabric-sdk-node.github.io/release-1.4/index.html
3.  [https://hyperledger-fabric . readthedocs . io/en/release-1.4/write _ first _ app . html](https://hyperledger-fabric.readthedocs.io/en/release-1.4/write_first_app.html)