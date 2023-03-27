# OWASP ZAP 的自动化安全测试

> 原文：<https://medium.datadriveninvestor.com/automated-security-tests-with-owasp-zap-c5326c9970a6?source=collection_archive---------0----------------------->

![](img/d259f461c79b0cd385ed778eab921d56.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/security?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

首先，如果我们可以将 Selenium Webdriver 测试与 ZAP 集成，那么我们就可以通过 ZAP APIs 准备好自动化的安全测试。尽管围绕这个主题有很好的文档，但我已经看到很多人在将测试与 ZAP 集成时面临问题。在 [Traveltriangle](https://traveltriangle.com/) ，技术团队积极使用 OWASP 作为安全测试的主要工具。这篇博客展示了使用 ZAP APIs 实现这种集成的实际步骤。

*注意—以下内容不包括 OWASP ZAP 功能、ZAP 安全扫描类型、ZAP 内部使用和阅读扫描报告。幸运的是，这里有非常好的关于 ZAP* [*所有特性的文档。请过一遍。*](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project)

让我们从实际的集成开始。

[](https://www.datadriveninvestor.com/2019/02/12/ready-or-not-the-revolution-is-upon-us/) [## 不管准备好了没有，革命就在我们面前|数据驱动的投资者

### “对于技术如何影响我们的生活和重塑经济，我们必须形成全面的全球共识……

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/12/ready-or-not-the-revolution-is-upon-us/) 

最重要的步骤是启动 [ZAP 可执行文件](https://github.com/zaproxy/zaproxy/wiki/Downloads)。selenium 测试将与 ZAP 可执行文件通信，因此必须在已配置的机器上启动。ZAP 可执行文件支持各种[命令行参数](https://github.com/zaproxy/zap-core-help/wiki/HelpCmdline)，但是这里我们将使用最少的参数。

```
zap.sh -daemon -host some-host -port some-port -config api.addrs.addr.regex=true -config api.disablekey=true*zap.sh -- a startup script provided by ZAP**-daemon - Start in a headless configuration**-host, -port - The ZAP host and port where selenium tests will eventually listen**-config api.addrs.addr.regex=true - Allow any source IP to connect**-config api.disablekey=true - by default it is false*
```

一旦 ZAP 可执行文件启动，下一步就是配置 selenium 驱动程序，并将 ZAP APIs 库添加到 selenium 框架项目中，如果框架项目使用像 maven 这样的构建工具，则添加 1 的依赖项。 [OWASP ZAP API 客户端](https://mvnrepository.com/artifact/org.zaproxy/zap-clientapi)和 2。 [OWASP Zed 攻击代理](https://mvnrepository.com/artifact/org.zaproxy/zap)。

想法是使用我们上面启动的 ZAP 代理地址启动 selenium 驱动程序。示例代码片段如下—(供使用 chrome 驱动程序的参考)

```
//setting up chrome options
ChromeOptions chromeOptions = new ChromeOptions();
chromeOptions.addArguments("--ignore-certificate-errors");//set the proxy to use ZAP host and port 
String proxyAddress = ”<ZAP_machine_IP>:<ZAP_machine_PORT>";Proxy zap_proxy = new Proxy();
zap_proxy.setHttpProxy(proxyAddress).setSslProxy(proxyAddress);

//set the desired capabilities to use zap_proxy object.DesiredCapabilities capabilities = DesiredCapabilities.chrome();
capabilities.setCapability(CapabilityType.PROXY, zap_proxy);
capabilities.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true);
capabilities.setCapability(CapabilityType.ACCEPT_INSECURE_CERTS,true);
capabilities.setCapability(ChromeOptions.CAPABILITY, chromeOptions);
ChromeDriverService service = new ChromeDriverService.Builder()
							.usingAnyFreePort()
							.usingDriverExecutable(new File(<chromedriver executable path))
							.build();
service.start(); // initiate the driver with required chrome options and capabilities.Webdriver driver = new ChromeDriver(service, options);
```

如果需要在远程机器上执行测试，请使用具有适当功能的 RemoteWebDriver。只要确保你指的是 ZAP 的正确代理地址。完成这些后，当 selenium 测试执行时，ZAP 将在后台通过 selenium 测试创建导航应用程序页面的扫描树，这被称为[被动扫描](https://github.com/zaproxy/zap-core-help/wiki/HelpStartConceptsPscan)。ZAP 使用这个扫描树来执行其他扫描，如主动扫描、蜘蛛攻击等。ZAP 通常需要一些时间来完成被动扫描，因此在代码中，一旦所有测试执行完成，您必须等待被动扫描完成。示例代码片段如下-

```
{
// create an object of org.zaproxy.clientapi.core.ClientApi using ZAP host and port.private static ClientApi api = new ClientApi(ZAP_HOST, ZAP_PORT); // function to wait for passive scan to complete
private static void waitForPassiveScanToComplete() {

System.out.println("--- Waiting for passive scan to complete --- ");
 try {
	  api.pscan.enableAllScanners(); // enable passive scanner.

          // getting a responseApiResponse response = api.pscan.recordsToScan();      

          //iterating till we get response as "0".while(!response.toString().equals("0")) {
		response = api.pscan.recordsToScan();
	    }
	  } catch (ClientApiException e1) {
			      e1.printStackTrace();
		       }
      System.out.println("--- Passive scan completed! ---");
  }
 }
}
```

所以，被动扫描完成了。通过 ZAP APIs 你可以启动[主动扫描](https://github.com/zaproxy/zap-core-help/wiki/HelpStartConceptsAscan)和[蜘蛛扫描](https://github.com/zaproxy/zap-core-help/wiki/HelpStartConceptsSpider)。示例代码片段如下-

```
{// create an object of org.zaproxy.clientapi.core.ClientApi using ZAP host and port.

private static ClientApi api = new ClientApi(ZAP_ADDRESS, ZAP_PORT);private String application_base_url = "https://<application_url>/";// Example function to start and synchronize with active scan.private static void startActiveScan() {

  System.out.println("Active scan : " + application_base_url);

try {
   // initiate the active scan -  refer doc to underatand the  constructor parameters.  
   ApiResponse resp = api.ascan.scan(application_base_url, "True", "False", null, null, null);
   int progress;

// scan response will return the scan id to support concurrent scanning.String scanid = ((ApiResponseElement) resp).getValue(); // Polling the status of scan until it completeswhile (true) {Thread.sleep(5000);progress =Integer.parseInt(((ApiResponseElement)api.ascan.status(scanid)).getValue());System.out.println("Active Scan progress : " + progress + "%");if (progress >= 100) {
              break;
          }
}
System.out.println("Active Scan complete");
  }
  catch(Exception e) {
     e.printStackTrace();
	  }
 }
}
}
```

类似地，启动蜘蛛扫描的示例代码片段如下-

```
{// create an object of org.zaproxy.clientapi.core.ClientApi using ZAP host and port.  
private static ClientApi api = new ClientApi(ZAP_ADDRESS, ZAP_PORT);private String application_base_url = "https://<application_url>/"; // Example code to start and synchronize the spider scan.private static void startSpiderScan() 
{
  System.out.println("Spider : " + application_base_url);
  try {
       // Start the spider scan - refer the documentation of ZAP  APIs to understand the spider scan 
       ApiResponse resp = api.spider.scan(TARGET, null, null, null, null);
       int progress; // scan response will return the scan id to support concurrent scanning.

       String scanid = ((ApiResponseElement) resp).getValue(); // Polling the status until it completes
       while (true) {
            Thread.sleep(1000);
            progress =Integer.parseInt(((ApiResponseElement) api.spider.status(scanid)).getValue());
            System.out.println("Spider progress : " + progress + "%");
            if (progress >= 100) {
                break;
            }
        }
        System.out.println("Spider complete");
        }
        catch(Exception e) {
      	  e.printStackTrace();
        }
}
}
```

我们已经了解了不同的扫描是如何开始的，下一步是访问和使用所执行扫描的漏洞报告。但是，可以使用 curl 请求来访问扫描报告

```
Alerts: ZAP_HOST:ZAP:PORT/JSON/core/view/alerts
Report: ZAP_HOST:ZAP:PORT/OTHER/core/other/htmlreport
```

正如我们在这里讨论的测试自动化，所以报告也应该被自动获取，一个使用 ZAP APIs 的示例代码片段如下

```
// example fucntion to store an html report.private static void getReports() {private String application_base_url = "https://<application_url>/";   try {
     // calling core apis to get html report in bytes.
     byte[] bytes = api.core.htmlreport();

     // getting the alert messages and just printing those.
     ApiResponse messages =  api.core.messages(application_base_url,"0","99999999");
     System.out.println(messages);

     // storing the bytes in to html report.
     String str = new String(bytes, StandardCharsets.UTF_8);
     File newTextFile = new File("report.html");
     FileWriter fw = new FileWriter(newTextFile);
     fw.write(str);
     fw.close();
  } catch (Exception e) {
  e.printStackTrace();
}
```

我希望这些内容对你有所帮助，并能解决人们在自动化安全测试中面临的问题。