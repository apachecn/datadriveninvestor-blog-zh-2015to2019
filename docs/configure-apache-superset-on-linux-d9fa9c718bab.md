# 在 Linux 上配置 Apache 超集

> 原文：<https://medium.datadriveninvestor.com/configure-apache-superset-on-linux-d9fa9c718bab?source=collection_archive---------0----------------------->

配置之前最好了解一下超集的基础知识，查看我之前的博客关于超集的基础知识 [**这里**](https://medium.com/@syedjunaid.h47/intoducing-apache-superset-an-open-source-data-visualizaton-tool-4684627014fd) 。

# 简介:

之前我们讨论了超集的特性和优点，以及它与其他可视化工具的不同之处。在博客的这一部分，我将演示如何在您的机器上配置超集，以及配置的必备工具是什么。

[](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) [## 为什么数据将改变投资管理|数据驱动的投资者

### 有人称之为“新石油”虽然它与黑金没有什么相似之处，但它的不断商品化…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/01/25/why-data-will-transform-investment-management/) 

# 配置 Apache 超集:

![](img/6b8ce63b3d8bf4da3a51239dd5af8618.png)

## 开始使用:

超集不赞成支持 Python **2。*** 并且仅支持 **3.6** 以利用较新的 Python 特性并减少支持以前版本的负担。我在 **3.6** 上运行了我的测试套件，但是在 **3.7** 上运行应该也可以。

现在有两种方法来配置超集。

通过 Docker 配置，或者通过单独安装后面的 Python 包来配置。

## 通过 Docker 配置超集:

如果你知道 docker，那么你很幸运，我为你提供了初始化开发环境的捷径:

```
git clone https://github.com/apache/incubator-superset/
cd incubator-superset/contrib/docker
*# prefix with SUPERSET_LOAD_EXAMPLES=yes to load examples:*
docker-compose run --rm superset ./docker-init.sh
*# you can run this command everytime you need to start superset now:*
docker-compose up
```

**请注意:**Docker 相关文件和文档是由社区贡献的，并不是由参与项目的核心提交者积极维护和管理的。截至 2019 年 1 月，已报告了一些问题。

## 通过单独安装 Python 包来配置超集:

**操作系统依赖关系:**

超集将数据库连接信息存储在其元数据数据库中。为此，我使用了`cryptography` Python 库来加密连接密码。不幸的是，这个库有操作系统级的依赖性。

对于 **Debian** 和 **Ubuntu** ，以下命令将确保安装所需的依赖项:

```
sudo apt-get install build-essential libssl-dev libffi-dev python-dev python-pip libsasl2-dev libldap2-dev
```

**Python 虚拟人:**

建议在 virtualenv 中安装 Superset。Python 3 已经发布了 virtualenv。但是如果由于某种原因它没有安装在您的环境中，您可以通过您的操作系统的软件包安装它，或者您可以从 pip 安装:

为了安装 python 包，我使用了 **pip3.6** ，如果你还没有安装，安装 pip3.6..

```
sudo apt install python3-pip#Now install Virtualenv through pip3.6pip3.6 install virtualenv
```

您可以通过以下方式创建和激活 virtualenv:

```
python3 -m venv venv
. venv/bin/activate
```

**Python 的设置工具和 pip:**

按照以下几个简单的步骤安装超集:

```
# Install superset
pip3.6 install superset

# Initialize the database
superset db upgrade

# Create an admin user (you will be prompted to set a username, first and last name before setting a password)
$ export FLASK_APP=superset
flask fab create-admin

# Load some data to play with
superset load_examples

# Create default roles and permissions
superset init

# To start a development web server on port 8088, use -p to bind to another port
superset run -p 8080 --with-threads --reload --debugger
```

如果您对 Flask 和 Pandas 有错误，请遵循以下步骤:

> pip3.6 卸载熊猫
> pip3.6 安装熊猫==0.23.4
> 
> pip3.6 卸载 sqlalchemy
> pip3.6 安装 sqlalchemy==1.2.18
> 
> pip3.6 安装烧瓶==1.0.0

安装后，您应该能够将浏览器指向正确的主机名:端口 [http://localhost:8088](http://localhost:8088/) ，使用您在创建管理帐户时输入的凭据登录，并导航到菜单- >管理- >刷新元数据。这个操作应该引入你的所有数据源，让超集知道，它们应该出现在菜单- >数据源中，从这里你可以开始处理你的数据！

这就是 Apache 超集配置，我希望我的指南对你有所帮助。