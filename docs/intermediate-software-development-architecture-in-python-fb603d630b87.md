# 中级软件开发:Python 中的架构

> 原文：<https://medium.datadriveninvestor.com/intermediate-software-development-architecture-in-python-fb603d630b87?source=collection_archive---------4----------------------->

## 我如何设置我的服务器端项目

![](img/c3dbf0d60ee7896681edd24c4e3958a5.png)

随着我在过去几年中构建了更多的项目，我开始意识到我在构建东西时的主导模式:模型-视图-控制器(MVC)。我主要构建 API 和前端移动应用程序，到目前为止，这种方法对这些类型的构建工作得很好。我还在我做的每个后端项目中使用 Docker，因为它使开发和部署毫不费力。这绝不是唯一的架构标准，但我认为了解其他开发人员如何改进自己的方法是有帮助的。虽然从严格的标准来看并不完全是 MVC，但我的后端项目的组件如下:

**模型:**将数据存储为易于访问的对象。我有一些类，每个类都有一个构造函数，让我可以将来自其他 API 或前端的任何入站数据存储到方便的对象中，我可以通过调用模型来访问这些对象。AwesomeClass(data_to_store)。item_1。这对于写入数据库非常有用，因为使用 Postgres，您可以将整个模型对象作为字典参数传递给 psycopg2 中的 curs.execute 方法，而不是像这样手动调用字典项:

```
sql_statement = """INSERT INTO %(table)s
                   VALUES (%(item_1)s, 
                           %(item_2)s, 
                           %(item_3)s)"""
curs = self.db.cursor()# -----------------------args = {'table':table,
        'item_1':item_1, 
        'item_2': item_2,
        'item_3': item_3}curs.execute(sql_statement, args)***# vs --------------***class AwesomeClass(object): def __init__(self, data_to_store):
     self.item_1 = data_to_store['item_1']
     self.item_2 = data_to_store['item_2']
     self.item_3 = data_to_store['item_3']import modelsargs = models.AwesomeClass(data_to_store).__dict__
curs.execute(sql_statement, args)
```

__dict__ 是一个特殊的变量，它将所有对象属性作为一个字典返回，因此，如果每个参数都是手动获取的，那么案例 2 中存储在上述 AwesomeClass 模型中的参数是相同的，只是模型对象在需要时是可重用的。另一个需要注意的重要事情是，在 execute 方法中传递参数比使用字符串格式来防止 [SQL 注入](https://www.w3schools.com/sql/sql_injection.asp)要安全得多，所以这种方法使得防止变得非常容易。

**端点**:任意前端的 API 接口。我经常使用 [tornado](https://www.tornadoweb.org/en/stable/) 作为我的网络服务器，因为它快速且易于安装，并支持我需要的所有网络服务。设置 tornado 的一个很好的综合概述可以在这里找到。我通常将它分成包含实际 web 服务器/路由的 server.py 和包含从控制器文件链接到控制器逻辑的实际 web 端点的 endpoints.py。Tornado 通过在端点类中继承 tornado.web.RequestHandler，使端点处理程序的创建变得非常简单:

```
import tornado.webclass BaseHandler(tornado.web.RequestHandler): def write_error(self, code):
       response = 'some error'return self.write(json.dumps(response))class EndPoint1(BaseHandler): def get(self):
      try:
         data = self.fetch_some_data()
         return data
      except Exception as e:
         print("Error: " + str(e)) 
         return self.write_error(500)
```

**控制器**:我把我所有的核心函数放在一个控制器文件里，这样很容易找到。如果逻辑对于一个文件来说太大，我会将它拆分到一个包含多个控制器组件的文件夹中。同样，容易找到是关键，所以我这样设置我的文件夹:

```
--server.py
--endpoints.py
--controllers
    --some_logic_module.py
    --second_logic_module.py
    --some_services.py
--tools
    --docker_staging_deploy.sh
    --run_some_report.sh
--model.py
```

我将一次性工具和脚本分离出来，以免混淆服务器的核心和我作为开发人员使用的东西。请记住，如果您正在处理文件夹，python 中的导入可能有点不可靠。有时，为了导入文件夹，您必须使用 sys 库并指向根文件夹，然后照常导入:

```
import sys

sys.path.insert(1, '/Path/to/root_project/')
from folder1.my_file import MyClass
```

**常用:**我抽象了常用的重复调用函数。像对外部的 API 调用和反复使用的数据库读/写。这样你可以使用[继承](https://www.w3schools.com/python/python_inheritance.asp)来调用你需要的函数:

```
class BaseFunctions: def my_data_pull(self):
        # *Pull some SQL or external API data* return data# -------------------from common import BaseFunctions

class MyClass(BaseFunctions): my_data_pull = self.my_data_pull()
```

**数据库:**我使用 Postgres 作为我需要长期存储的数据的关系数据库。Psycopg2 是 [postgres 的主要 Python 接口，其深度相当于](https://hackersandslackers.com/psycopg2-postgres-python-the-old-fashioned-way/)。对于更多的临时数据，我喜欢使用 Redis 作为密钥对存储，因为它使用起来非常简单，速度非常快，并且支持 Pub/Sub 之类的东西。YouTube 上的工程师对如何使用 Redis[有一个非常简单的解释。](https://www.youtube.com/watch?v=YWIzp3fRvvY)

Docker 是那些改变生活的东西之一，它自动化了过去需要整个团队去做的事情。与 Docker 部署相关的项目包括一个 Docker 文件，它指定了部署步骤和。dockerignore 文件，指示哪些内容不应该发送到映像进行部署(类似于. gitignore 文件，但用于 Docker)。Stackify 的人有一个关于如何使用 Docker 的很棒的教程。

**需求:**所有 python 需求都在 requirements.txt 文件中，使用＄*pip install-r Requirements . txt*可以安装所有依赖项。这可以在本地和 docker 文件中使用以下命令:

```
COPY requirements.txt ./
RUN pip install -r requirements.txt
```

**Cython:** 运行需要加速到 C 语言级别速度的函数。我喜欢对包含重复函数的文件使用这种方法，因为使用 python 解释器会陷入困境。通常你会发现你的方法速度提高了 5-10 倍。我快速浏览了一下如何让 Cython 在这里运行。

**测试:**最后但同样重要的是，我有一个 tests.py 文件，我把所有的测试都放在那里。这使得以后进行代码更改变得不那么麻烦，就好像您的更改破坏了您马上就能知道的测试一样。这些年来，我最大的烦恼之一就是在没有测试的情况下进行构建。写测试并不性感，但是测试是短期的痛苦，可以缓解长期的痛苦。接受现实吧，[学会使用 Python 单元测试模块](https://www.youtube.com/watch?v=6tNS--WetLI)。你不会后悔的。

这绝不是详尽的，也不是建立项目的唯一方式。我还有很多东西需要学习，可能还有许多技巧，如利用微服务进行扩展，但希望这有助于您为需要部署速度而不是大规模部署的简单项目打下基础。编码快乐！