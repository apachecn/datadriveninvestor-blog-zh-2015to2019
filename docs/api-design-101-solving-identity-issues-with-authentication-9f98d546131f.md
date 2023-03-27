# API 设计 101:通过认证解决身份问题

> 原文：<https://medium.datadriveninvestor.com/api-design-101-solving-identity-issues-with-authentication-9f98d546131f?source=collection_archive---------0----------------------->

![](img/36843229ffd888dac44c7ffa8a3a746e.png)

你必须一直生活在岩石下，才能在你的互联网之旅中没有遇到某种认证。每次要求您输入用户名和密码时，您都会被验证。许多 REST APIs 需要认证，所以在这篇博文中，我们将分为三种类型:基本认证、JWT 令牌和 OAuth。

让我们先了解一些基本知识:

[](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) [## 雅虎财经 API |数据驱动投资者的 6 种替代方案

### 长期以来，雅虎金融 API 一直是许多数据驱动型投资者的可靠工具。许多人依赖于他们的…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) 

**什么是认证？**

一般来说，认证处理确定你是谁，而它的兄弟，授权，处理确定你被允许做什么。因此，当您使用您的用户名和密码组合时，您告诉服务您是谁。或者像在 Medium 上一样，当你点击电子邮件收件箱中的登录链接时，Medium 知道你就是你所说的那个人。

只有被明确授权访问您的 API 的用户才应该被允许访问它。这来自于保护信息的原则[1]。

> *用户对系统中任何资源的默认访问级别应该是“拒绝”,除非他们被明确授予“许可”。*

**你应该如何实现认证？**

简单点，笨蛋。亲吻原则再次出现。使您的身份验证尽可能复杂。不必要的复杂性可能会导致漏洞，使您的 API 不安全。

对于密码，*总是将密码的散列版本*存储在您的数据存储中。因此，如果您的数据存储遭到破坏，黑客就无法轻易猜出密码。

永远不要在 URL 中存储敏感信息。这使得共享凭证成为可能。

```
https://todo.com/users/{id}/delete?apiKey=abcd123456789  //Bad idea
```

**您应该使用哪种身份验证？**

由于存储 DNA 样本并在每次登录时检查您的 DNA 是否匹配非常低效且不可扩展，我们不得不满足于安全性稍差的东西。

这意味着假设一个正确的用户名/密码组合或一个“令牌”就足以识别您的身份。这当然不是绝对安全的，但就目前而言已经足够安全了。

主要来说，三种常见的身份验证是基本身份验证、JWT 和 OAuth。

# 基本认证

![](img/a611d549da16513170884deb402de705.png)

顾名思义，基本身份验证是进行身份验证的一种基本方式。您在每个请求中都指定了您的用户名和密码，就像这样:

Base64 编码用户名和密码(username:password)并放在认证头中。

```
base64('superuser:sosecure') = c3VwZXJ1c2VyOnNvc2VjdXJlHTTP header:
Authentication Basic c3VwZXJ1c2VyOnNvc2VjdXJl
```

然而，base64 编码一点也不安全，因为它非常容易解码。所以这有点像一直带着你的护照，把它作为你主要的身份识别方式。如果有人偷了它，他们可以很容易地冒充你。

然而，对于内部网络上的 API，基本认证可能是合适的。

# JSON Web 令牌

![](img/bec120695607804d752c92ac11973758.png)

JSON web 令牌是一个加密的字符串，包含关于您是谁的信息。这有点像工作或学校的 ID 徽章。它将识别您的身份，并授予您访问您有权访问的区域(资源)的权限。

JWT 在您登录时生成，并存储在每个 HTTP 请求的身份验证头中。

```
Authentication Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJBdXRoZW50aWNhdGlvbiIsImlzcyI6Imt0b3IuaW8iLCJpZCI6MSwiZXhwIjoxNTY5MjQ4MTcxfQ.FLBqzgSDN5w9lrnvGXrSYr0-x6jUtGQxSqL_29YaTVrtcaqt67P7YICpPhixhblBL6GL3-veO_jKha_Cs9fh8w
```

令牌本身分为三个部分。报头、有效载荷和签名[2]。

标头包含有关加密和令牌类型的元数据。有效负载包含关于您是谁以及您拥有什么权限的信息。最后，签名是加密在散列中的报头和有效载荷，因此您可以确保信息没有被篡改。

jwt 还有更多的内容，所以我建议在自己实现它之前深入研究一下。

然而，就像基本身份验证一样，这本身并不是超级安全的。如果有人发现了你的令牌，他们可以很容易地冒充你。不过，他们不会有你的凭证，一旦令牌超时，他们就不能再使用它。

jwt 被广泛使用，因为它们不需要凭证，它们是无状态的，并且它们还允许细粒度的访问控制(在下一篇博客文章中会详细介绍)。

在生成令牌时，要求在 POST 主体中发送凭证，这样它就不会保存在客户端。

# OAuth

![](img/dc8e5186e190ba41f284886c845d2110.png)

OAuth 是一种身份验证标准，它使用类似于 JWT 的令牌，但是它将凭证处理委托给第三方。

因此，您可以使用 OAuth 协议来生成令牌，而不是存储密码。

这意味着你可以向 Google 发送一个认证请求，要求用户通过 Google 使用他们的 Google 凭证进行认证。然后，Google 会向您发送一个令牌来验证用户，并指定您可以访问来自 Google 的哪种用户信息。

这种做法越来越普遍，因为你不必担心存储敏感信息。此外，如果您需要与第三方整合并获得信息许可，这可能是一个不错的选择。

**最重要的是**

为了安全起见，所有这些类型的身份验证都应该在 HTTPS 上实现。所以整个请求都是加密的。那么黑客就更难截获您的凭证或令牌并冒充您。

![](img/33d4b75fe31db69580d9d477a0cda559.png)

**还有其他要求吗？**

你需要授权吗？那么令牌可能是一种可行的方法，因为您可以将用户的角色放在 JWT 负载中。

# 待办事项 API

现在是我们运行 Todo API 的例子。我们的用户可以访问 API 中的所有信息，所以我们可以使用一些身份验证。现在，任何人都可以假装成用户，查看其他人的待办事项。现在是解决这个问题的时候了。

由于我们需要在某些时候为用户定义权限，使用 JWT 似乎是最好的主意。使用 OAuth 是不必要的复杂。

Ktor 甚至提供了 JWTs 的实现。因此，向我们的 API 添加身份验证非常简单。

我们需要一个 JWT 发行者，在用户登录时生成令牌。

```
object JwtConfig { private const val secret = "zAP5MBA4B4Ijz0MZaS48" // This should be hidden in configuration or environment variables
    private const val issuer = "ktor.io"
    private const val validityInMs = 36_000_00 * 10 // 10 hours
    private val algorithm = Algorithm.HMAC512(secret) val verifier: JWTVerifier = JWT
        .require(algorithm)
        .withIssuer(issuer)
        .build() /**
     * Produce a token for this combination of User and Account
     */
    fun makeToken(user: User): String = JWT.create()
        .withSubject("Authentication")
        .withIssuer(issuer)
        .withClaim("id", user.id)
        .withExpiresAt(getExpiration())
        .sign(algorithm) /**
     * Calculate the expiration Date based on current time + the given validity
     */
    private fun getExpiration() = Date(System.currentTimeMillis() + validityInMs)
}
```

然后我们可以告诉 ktor 为每个请求验证 JWT 令牌。

```
val userSource = UserRepository()
    install(Authentication) {
/**
* Setup the JWT authentication to be used in [Routing].
* If the token is valid, the corresponding [User] is                 fetched from the database.
* The [User] can then be accessed in each [ApplicationCall].
*/
       jwt {
            verifier(JwtConfig.verifier)
            realm = "ktor.io"
            validate {
            it.payload.getClaim("id").asInt()?.let(userSource::find)
            }
        }
    }
```

最后，我们通过将它们包装在`authenticate {}`中来指定我们想要认证的路由

因此，现在我们可以看到，如果您试图在未经身份验证的情况下访问端点，API 会返回`401 Unauthorized`。

![](img/9ddd4d467b403048b746b1d66129f1bb.png)

你可以在这里找到所有的代码。

但是，如果您登录，您将被允许访问。它仍然不是完美的，因为一旦你被认证，你仍然可以看到其他人的待办事项，但它比以前更好。

这是我们想在下一篇博文中解决的问题，我们将深入探讨授权。

← **上一篇:** [构建 RESTful API 的基础知识](https://medium.com/@JohanneA/api-101-the-basics-of-building-a-restful-api-6f4a2f6afbaf)

下一篇:即将到来的 10 月 13 日→

# 资源

[1] [RESTful API:安全基础](https://restfulapi.net/security-essentials/)

[2] [JWT.io 简介](https://jwt.io/introduction/)