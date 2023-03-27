# 使用木偶师自动化改变世界

> 原文：<https://medium.datadriveninvestor.com/chirag-goel-changing-the-world-with-automation-31c7ba718555?source=collection_archive---------2----------------------->

[![](img/e0365ebe01f78ffc143273859bd780bd.png)](http://www.track.datadriveninvestor.com/1B9E)

—自动化将继续重新定义你的工作(这是一件好事)

Web 自动化可以用软件代替人来完成重复性和繁琐的任务，例如:

[](https://www.datadriveninvestor.com/2019/02/12/ready-or-not-the-revolution-is-upon-us/) [## 不管准备好了没有，革命就在我们面前——数据驱动的投资者

### “对于技术如何影响我们的生活和重塑经济，我们必须形成全面的全球共识……

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/12/ready-or-not-the-revolution-is-upon-us/) 

*   表格填写
*   数据析取
*   屏幕抓取
*   应用程序之间的数据传输
*   网站测试
*   定期报告生成
*   预定活动

> “自动化不需要成为我们的敌人。我认为机器可以让人类的生活更轻松，如果人类不让机器主宰他们的话。”
> 
> ——约翰·肯尼迪

在这篇文章中，我们将讨论使用**木偶师来自动化我们的任务。**

> **木偶师**是一个节点库，它提供了一个高级 API 来通过 [DevTools 协议](https://chromedevtools.github.io/devtools-protocol/)控制 Chrome 或 Chrome。默认情况下，木偶师运行[无头](https://developers.google.com/web/updates/2017/04/headless-chrome)，但可以配置为运行全(无头)铬或铬。

![](img/f9ec84d66aa1ff7950be1e3de60dfa97.png)

我们将通过下面列出的一些基本任务来学习 web 自动化:

1.  嘿木偶师给我看看我的网站
2.  嘿，木偶师，填好我的登记表。
3.  嘿木偶师从 LinkedIn 生成我的 pdf 格式简历

在我们开始上述解决方案之前，让我们先设置木偶师。

```
**npm i puppeteer --save-dev //**you can use yarn also
**npm i puppeteer-core**/* Note: Puppeteer requires at least Node v6.4.0, but the examples below use async/await which is only supported in Node v7.6.0 or greater. */
```

用下面的内容创建一个 [**package.json**](https://github.com/chirag-goel/puppeteer-linkedin-resume/blob/master/package.json) 文件

```
{
  "name": "Puppeteer",
  "author": "Chirag Goel"
}
```

你都准备好了。让我们请木偶师来执行上述任务

1.  **嘿，木偶师，给我看看我的网站**

创建一个文件 [**demo1.js**](https://github.com/chirag-goel/puppeteer-linkedin-resume/blob/master/src/demo1.js) 并粘贴下面的代码。

```
const puppeteer = require('puppeteer');(async () => {
  const browser = await puppeteer.launch({headless: false});
  const page = await browser.newPage();
  page.setViewport({ width: 1366, height: 700});
  await page.goto('http://www.chirag-goel.in');
  setTimeout(async() => { await browser.close(); }, 5000);
})();*/* Launch puppeteer and open a new window. Set viewport to 1000px*700px, go to my website and wait for 5seconds before closing it. */*
```

考验的时候到了。打开终端，转到文件路径，运行
**节点 demo1.js**

## 2.嘿，木偶师，填好我的登记表。

创建文件 [**demo2.js**](https://github.com/chirag-goel/puppeteer-linkedin-resume/blob/master/src/demo2.js) 并复制粘贴以下代码:

```
const puppeteer = require('puppeteer');
const FORM = {
    URL: '[https://www.w3schools.com/howto/tryit.asp?filename=tryhow_css_register_form'](https://www.w3schools.com/howto/tryit.asp?filename=tryhow_css_register_form'),
    PASSWORD_SELECTOR: 'input[name="psw"]',
    REPEAT_PASSWORD_SELECTOR: 'input[name="psw-repeat"]',
    BUTTON_SELECTOR: '.registerbtn',
    EMAIL_SELECTOR: 'input[name="email"]',
};
const CREDENTIALS = {
    USERNAME: '[dummy@dummy.com](mailto:dummy@dummy.com)',
    PASSWORD: 'dummy'
};(async () => {
  const browser = await puppeteer.launch({headless: false});
  const page = await browser.newPage();
  await page.goto(FORM.URL, {waitUntil: 'networkidle0'});/* This form is inside iframe, so we will using iframe reference. You can use page reference if your form in not inside iframe. Example given in demo3.js */

  const frames = await page.frames();
  let iframe = frames.find(f => f.name() === 'iframeResult'); const email = await iframe.$(FORM.EMAIL_SELECTOR);
  await email.click();
  await page.keyboard.type(CREDENTIALS.USERNAME); const password = await iframe.$(FORM.PASSWORD_SELECTOR);
  await password.click();
  await page.keyboard.type(CREDENTIALS.PASSWORD); const rPassword = await iframe.$(FORM.REPEAT_PASSWORD_SELECTOR);
  await rPassword.click();
  await page.keyboard.type(CREDENTIALS.PASSWORD); const button = await iframe.$(FORM.BUTTON_SELECTOR);
  await button.click();

  await page.waitFor(5*1000);
  await browser.close();

})();
```

## 3.嘿木偶师从 LinkedIn 生成我的 pdf 格式简历

创建文件 [**demo3.js**](https://github.com/chirag-goel/puppeteer-linkedin-resume/blob/master/src/demo3.js) 并复制粘贴以下代码，用您的 LinkedIn 凭据替换<用户名> & <密码>:

```
const puppeteer = require('puppeteer');const FORM = {
    USERNAME_SELECTOR: '#username',
    PASSWORD_SELECTOR: '#password',
    BUTTON_SELECTOR: '.btn__primary--large.from__button--floating',
    PROFILE_SELECTOR: 'a[data-control-name="identity_profile_photo"]'
};const CREDENTIALS = {
    USERNAME: '<USERNAME>',
    PASSWORD: '<PASSWORD>'
};(async () => {
  const browser = await puppeteer.launch(); 
  const page = await browser.newPage(); await page.goto('[https://www.linkedin.com/login?trk=guest_homepage-basic_nav-header-signin'](https://www.linkedin.com/login?trk=guest_homepage-basic_nav-header-signin'), {waitUntil: 'networkidle0'}); await page.click(FORM.USERNAME_SELECTOR);
  await page.keyboard.type(CREDENTIALS.USERNAME); await page.click(FORM.PASSWORD_SELECTOR);
  await page.keyboard.type(CREDENTIALS.PASSWORD); await page.click(FORM.BUTTON_SELECTOR); await page.waitForNavigation(); await page.click(FORM.PROFILE_SELECTOR);
  await page.waitForNavigation();
  await page.waitFor(2*1000); await page.pdf({path: 'resume.pdf', format: 'A4'});
  await page.screenshot({path: 'resume.png', fullPage: true}); await browser.close();
})();/* To learn advanced version of creating resume from linkedIn profile refer to -- [https://github.com/chirag-goel/puppeteer-linkedin-resume/blob/master/src/demo3.js](https://github.com/chirag-goel/puppeteer-linkedin-resume/blob/master/src/demo3.js) */
```

检查上述示例的工作 [github](https://github.com/chirag-goel/puppeteer-linkedin-resume) 链接。请继续关注即将发布的 youtube 视频。

[](https://github.com/GoogleChrome/puppeteer) [## 谷歌色素/木偶师

### 无头 Chrome 节点 API。在 GitHub 上创建一个帐户，为 Google chrome/木偶师的发展做出贡献。

github.com](https://github.com/GoogleChrome/puppeteer) 

# 包扎

呜！这就是关于木偶师的一切，期待听到你们将要自动化的一切。敬请关注我以后的文章。

这篇文章对你有帮助吗？如果你有任何问题或想法，请在下面的评论中告诉我！我很想听听他们:)

感谢阅读。这篇文章对你有什么帮助吗？如果我写了，我希望你能考虑分享它，你可能会帮助那些在读这篇文章之前和你有同样感受的人。谢谢你。

> T2:分享让你变得更强大。你倾诉得越多，生活就越能倾注进来。