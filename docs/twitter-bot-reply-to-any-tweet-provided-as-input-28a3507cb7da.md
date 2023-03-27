# Twitter 机器人——回复任何作为输入提供的推文！

> 原文：<https://medium.datadriveninvestor.com/twitter-bot-reply-to-any-tweet-provided-as-input-28a3507cb7da?source=collection_archive---------2----------------------->

[![](img/0e0f48e2600a15e213b5165b94726951.png)](http://www.track.datadriveninvestor.com/1B9E)

本文的主旨是创建一个 Twitter bot，它将任何 tweet 的链接作为输入，并向用户提供带有提及的自定义回复。它可能被小公司用于营销目的，或者被学生/业余爱好者用于在 15-20 分钟内学习新东西。

![](img/394fde24ca3a06fb276577a10520379b.png)

如果这个想法激起了你的兴趣，那就跟着我一步一步地完成这个指南。我会链接包含代码的存储库，但强烈建议您自己键入代码。我保证不会单调乏味。

[](https://www.datadriveninvestor.com/2019/01/31/conversational-marketing-is-the-word/) [## 对话式营销是文字数据驱动的投资者

### 在购买之前，先谈一谈。这样做的营销人员将走在游戏的前面。这是保罗·因斯的前提…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/31/conversational-marketing-is-the-word/) 

# **先决条件**

*   一个 Twitter 开发者账户。
*   系统上安装的节点和 npm。
*   对 JavaScript 和 API 有基本的了解。

# **入门**

我们将从创建一个基本的应用程序开始。

> npm 初始化

然后安装 Twit 以使用 Twitter API

> npm 安装 twit

无论何时安装软件包，都要在 install 关键字后用'— save '将它们添加到依赖项中。

在文件 *index.js* 中编写以下代码:

```
// Verify
console.log("Up and running...");// Create a Twitter object to connect to Twitter API
// npm install twit
var Twit = require('twit');// Pull all twitter account info from another file
var config = require('./config.js');// Make a Twit object for connection to the API
var T = new Twit(config);// Set up a user stream tracking mentions to username
var stream = T.stream('statuses/filter', { track: '@<**your-username**>' });// Now looking for tweet events
stream.on('tweet', tweetEvent);
```

在上面的代码中，我们连接到 Twitter，并在建立流连接后查找 tweets。

这为我们的程序设置了样板文件，现在开始创建到您的 Twitter 应用程序的实际连接。转到 Twitter 开发者控制台，在创建应用程序后获取以下详细信息，并将其存储为 *config.js* 。

```
module.exports = {
  consumer_key:         '',
  consumer_secret:      '',
  access_token:         '',
  access_token_secret:  ''
}
```

# 提取细节

我们的应用程序现在可以寻找针对我们用户名的推文，但为了对提供的链接进行回复，我们必须从提供的链接中提取 tweetId，并获得用户名，以便我们可以提到它们。

twitter 上任何推文的链接都是以下形式:

> https://twitter.com/<username>/状态/</username>

直观地说，使用 below regex 从 tweet 提供的链接中提取细节似乎很容易。

```
/https:**\/\/**twitter**\.**com**\/**([a-zA-Z0–9_.]+)**\/**status**\/**([0–9]+)**\?**/g
```

然而，这说起来容易做起来难，因为 Twitter 缩短了其推文中的链接，在收到推文回复后，你不会发现链接是原样的。

不要担心，我们在下一节中已经解决了这个问题。

# **扩展网址**

JavaScript 的承诺和请求这次来帮助我们了，运行下面的命令:

> npm 安装请求
> 
> npm 安装 q

将以下代码添加到您的 *index.js* 文件中:

```
// Use request for expanding given tweet url which gets shortened by twitter by default
var Q = require("q");
var request = require("request");// Code for expanding url shortened by twitter
function expandUrl(shortUrl) {
    var deferred = Q.defer();
    request( { method: "HEAD", url: shortUrl, followAllRedirects: true },
        function (error, response) {
            if (error) {
                deferred.reject(new Error(error));
            } else {
                deferred.resolve(response.request.href);            
            }
    });
    return deferred.promise;
}
```

# **最高潮**

是时候让我们开始编写当一个 tweet 事件被触发时要执行的最终代码了。

将以下代码添加到您的 *index.js* 文件的底部:

```
function tweetEvent(tweet) {
   // Who is this in reply to?
   var reply_to = tweet.in_reply_to_screen_name;

   // What is the text?  
   var txt = tweet.text

   // Get rid of the @ mention
   short_url = txt.replace(/@dev_celestial /g,'');

   var tweet_link = '';
   // Expand the shortened url

   expandUrl(short_url).then(function (longUrl) {
      var my_regex = /https:**\/\/**twitter**\.**com**\/**([a-zA-Z0-9_.]+)**\/**status**\/**([0-9]+)**\?**/g; var extracted_info = my_regex.exec(longUrl); // Username of the given tweet owner

      var name = extracted_info[1]; // Id of the given tweet var id = extracted_info[2];

      // If this was in reply to me
      if (reply_to === 'dev_celestial') {
         var file_text = ''; fs.readFile('Input.txt', (err, data) => {
           if (err) throw err;
           file_text = data.toString(); // Start a reply back to the sender
           var replyText = '@'+ name + ' ' + file_text + ' Right?!';

           T.post('statuses/update', { status: replyText, in_reply_to_status_id: id}, tweeted);
          // Make sure it worked!
          function tweeted(err, reply) {
            if (err) {
              console.log(err.message);
            } else {
              console.log('Tweeted: ' + reply.text);
            }
        }
      })
    }
  });
}
```

我猜你在上面的代码中注意到了，我们使用了一个名为 *input.txt* 的文件中的文本

创建包含定制消息的文件 *input.txt* ，并在 index.js 文件的顶部添加下面一行。

```
// Data from file
var fs = require('fs')
```

现在你已经准备好测试你的代码了，但是在那之前，看看我的代码 [**这里**](https://github.com/TheCelestial25/twitter-bot/) 以免出错。

# **行动！**

为了看到你的机器人在行动:

1.  使用以下命令启动本地服务器

> 节点索引. js

2.用以下格式发送推文:

> @<your-username><link-to-the-tweet></link-to-the-tweet></your-username>

3.等待回复，由于交通繁忙，可能需要几秒钟。

好了，你可以看到你的机器人已经回复了你在 input.txt 中提供的消息文本！

您也可以在 Heroku 上部署这个 bot 作为一个工作进程，使用 procfile 来帮助您。

> ***向你致敬！谢谢你对我的包容！***