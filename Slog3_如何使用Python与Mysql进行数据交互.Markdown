* ArthurSlog
* SLog-3
* Year·1

* Guangzhou·China
* July 9th 2018

![关注微信公众号“ArthurSlog”](https://user-gold-cdn.xitu.io/2018/7/6/1646bea7831103bb?w=256&h=260&f=jpeg&s=38655 "微信扫描二维码，关注我的公众号")

自己的梦想需要你自己去实现

### 开发环境MacOS(High Sierra 10.13.5)

* 打开base，测试一下python，默认版本应该是Python 2.7.10

> python

在Mysql的官网获取Python与Mysql的交互手册[Mysql官方手册](https://dev.mysql.com/doc/connector-python/en/)

* 我们需要知道的事情 了解一下

This manual describes how to install and configure MySQL Connector/Python, a self-contained Python driver for communicating with MySQL servers, and how to use it to develop database applications.

* 这段话就是实现Python与Mysql数据交互的关键 如果你看不懂 说明你想的太多 做的太少

* 下载安装[Mysql/Python接口文件](https://dev.mysql.com/downloads/connector/python/)

* 安装过程可能会碰到安全权限，打开“系统偏好设置”，打开“安全性与隐私”，点击左下角的“打开”，继续完成安装，忽略警告和提示，一直安装到底，安装结果可能会部分失败，不用理他。

* 现在，对接文件已经到位

* 接下来测试Mysql数据库，如果还没安装或者安装了还没配置，移步[Mysql数据库配置](https://juejin.im/post/5b3e533e6fb9a04f8c5eb9f3)，完成Mysql数据库的安装和配置；或者在[Mysql官方下载](https://dev.mysql.com/downloads/mysql/)，安装官方手册安装。

* 根据[官方手册的说明](https://dev.mysql.com/doc/connector-python/en/connector-python-example-connecting.html)

* 接下来编写完整的Python文件，对Mysql数据库进行[查询操作](https://dev.mysql.com/doc/connector-python/en/connector-python-example-cursor-select.html)

pythontodatabase.py
``` python
import mysql.connector

cnx = mysql.connector.connect(user='root', password='661475chen', host='127.0.0.1', database='my_db')
cursor = cnx.cursor()

query = ("SELECT * FROM Account ")

cursor.execute(query)

for (ID, AccountName, Password) in cursor:
  print("{}, {}, {}".format(
    ID, AccountName, Password))

cursor.close()
cnx.close()
```

* Python语法使用[Python官方手册](https://docs.python.org/2/)

* 分析一下代码，Python与Mysql交互的基本流程如下：

1. 导入Mysql/Python-Connector模块，import mysql.connector
2. 连接数据库，获得返回值对象cnx(这个也就是与Mysql通信的对象)，cnx = mysql.connector.connect()
3. 获得cursor对象，这个是关键点，参考[Python官方手册](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor.html)，cursor = cnx.cursor()
4. 配置sql指令的对象，query = ("")
5. 发送并执行sql指令，cursor.excute(query)，这个也是关键点，参考[Python官方手册](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html)
6. 关闭cursor对象，cursor.close()
7. 关闭通信对象，cnx.close()

* OK,分析完成，切换至代码文件路径下

> python pythontodatabase.py

* 正常执行，输入Account表的数据内容

1 - ArthurSlog - ArthurSlog

* 至此，Python与MySQL成功实现了数据交互。

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://user-gold-cdn.xitu.io/2018/7/6/1646bea7831103bb?w=256&h=260&f=jpeg&s=38655 "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
