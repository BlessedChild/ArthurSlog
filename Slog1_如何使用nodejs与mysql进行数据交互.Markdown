* ArthurSlog
* SLog-1
* Year·1

* Guangzhou·China
* July 6th 2018
![关注微信公众号“环游的球”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

没有人能阻挡我前进的道路

### 安装nodejs作为开发服务器的工具（macOS）
* 打开终端,切换至Desktop路径
> cd Desktop
* 新建一个文件夹“nodejs_learningload”
> mkdir nodejs_learningload
* 切换至nodejs_learningload路径
> cd nodejs_learningload
* 现在开始安装nodejs了：
* 使用[homebrow](https://brew.sh)这个工具来协助我们
> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
* 根据命令行提示继续操作，完成homebrew的下载和安装（下载、安装可能需要一些时间），然后使用brew安装nodejs
> brew install node
* 检查node是否完整安装
> node -v

v10.6.0
> npm -v

6.1.0
* 至此nodejs完整安装完成

### 安装Mysql，配置Mysql
* 使用brew安装mysql
> brew install mysql
* 启动mysql,检查mysql是否完整安装
> mysql.server start
* Starting MySQL
* .SUCCESS!
* 配置Mysql,设置root账户的密码为8个8
> mysqladmin -u root password 88888888
* 登陆数据库
> mysql -u root -p
* 输入密码，再按enter键,命令行会变成以下状态
> mysql>
* 输入SQL命令，按enter键执行，列出已有的数据库
> mysql> show databases;

Database|
------ |
information_schema |
mysql|
performance_schema|
sys|
4 rows in set(0.01 sec)

* 我们创建一个数据库"my_db"
> mysql> create database my_db;

Query OK, 1 row affected (0.02 sec)
* 进入my_db数据库
> mysql> use my_db;

Database changed
* 我们创建一个表“Account"
```
mysql> CREATE TABLE Account
(
ID int NOT NULL AUTO_INCREMENT,
AccountName varchar(255) NOT NULL,
Password varchar(255) NOT NULL,
PRIMARY KEY (ID)
);
```
Query OK, 0 rows affected (0.09 sec)

* 向Account表里插入一行数据
```
mysql> INSERT INTO Account (AccountName, Password)
VALUES ('ArthurSlog','ArthurSlog);
```
Query OK, 1 row affected (0.08 sec)

* 查看一下Account表
> mysql> SELECT * FROM Account;

ID|AccountName|Password
- | - | -
1 | KingArthur | KingArthur
1 row in set (0.00 sec)

* 退出mysql交互模式
> exit;

Bye

### 实现nodejs和Mysql的数据交互

* 切换当前路径至～/Desktop/nodejs_learningload
> cd ～/Desktop/nodejs_learningload
* 使用npm，执行npm命令初始化环境
> npm init
* 一路默认enter就行，再当前路径下生成一个package.json文件
* 使用npm，执行npm命令安装express模块
> sudo npm install express
* 接下来，开始编写逻辑代码
* 一共要写两个个文件，index.html、index.js
* index.html: 主页
* index.js: web服务器，提供web服务和路由功能，其中还有最为关键的函数（路由），可以连接数据库，执行SQL命令的函数

index.html
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>SingUp</title>
</head>
<body>
    <p>Sing up</p>
    <form action="http://127.0.0.1:8081/singupAccount" method="GET">
        Name: <input type="text" name="name"> 
        <br>
        Password: <input type="text" name="password">
        <br>
        <input type="submit" value="注册">
    </form>
    <br>
</body>
</html>
```
* 其中，关键的地方在这个位置
``` html
    <form action="http://127.0.0.1:8081/singupAccount" method="GET">
        Name: <input type="text" name="name"> 
        <br>
        Password: <input type="text" name="password">
        <br>
        <input type="submit" value="注册">
    </form>
```
* 这里使用\<from>\</from>标签
``` html
action="http://127.0.0.1:8081/singupAccount" method="GET"
```
* 仔细看这里
``` html
action="http://127.0.0.1:8081/singupAccount"
```
* express的路由功能在这里体现
``` html
/singupAccount
```
* 这个路由（方法）/singupAccount，我们将会在另一个文件（index.js）里编写好，以供前端调用

index.js
``` js
var express = require('express');
var fs = require("fs");
var app = express();
 
app.use(express.static(__dirname));

app.get('/singupAccount', function (req, res) {
 
    var mysql      = require('mysql');
    var connection = mysql.createConnection({
      host     : 'localhost',
      user     : 'root',
      password : '88888888',
      database : 'my_db'
    });
     
    connection.connect();

    var response = {
        "name":req.query.name,
        "password":req.query.password
    };

    var  addSql = 'INSERT INTO Account(AccountName, Password) VALUES(?,?)';
    var  addSqlParams = [response.name, response.password];

    connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
            console.log('[INSERT ERROR] - ',err.message);
            res.send('执行sql出错!');
            return;
        }
        res.send('Welcome~ SingUp Success ^_^');
    });

    connection.end();
 })

var server = app.listen(8081, function () {
 
  var host = server.address().address
  var port = server.address().port
 
  console.log("应用实例，访问地址为 http://%s:%s", host, port)
})
```

* 在index.js里面，使用express模块的静态路由功能，路由的是我们的主页

* 静态路由，程序一启动就会执行静态路由的方法，这个方法就是打开我门的主页

``` js
var express = require('express');

var app = express();
 
app.use(express.static(__dirname));
```

* 使用express的web服务器功能，实现了一个web服务器，ip：127.0.0.1:8081

``` js
var server = app.listen(8081, function () {
 
  var host = server.address().address
  var port = server.address().port
 
  console.log("应用实例，访问地址为 http://%s:%s", host, port)
}
```

* 最关键的地方在下面这里，实现了一个路由（方法），当前端路由到这个方法的时候，让程序连接mysql数据库，并向mysql数据库里添加数据

``` js
app.get('/singupAccount', function (req, res) {
 
    var mysql      = require('mysql');
    var connection = mysql.createConnection({
      host     : 'localhost',
      user     : 'root',
      password : '88888888',
      database : 'my_db'
    });
     
    connection.connect();

    var response = {
        "name":req.query.name,
        "password":req.query.password
    };

    var  addSql = 'INSERT INTO Account(AccountName, Password) VALUES(?,?)';
    var  addSqlParams = [response.name, response.password];

    connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
            console.log('[INSERT ERROR] - ',err.message);
            res.send('执行sql出错!');
            return;
        }
        res.send('Welcome~ SingUp Success ^_^');
    });

    connection.end();
 })
```

* /singupAccount这个路由（方法）是关键，首先，在方法里面需要先配置mysql连接参数

``` js
    var mysql      = require('mysql');
    var connection = mysql.createConnection({
      host     : 'localhost',
      user     : 'root',
      password : '88888888',
      database : 'my_db'
    });
```

* 连接参数配置好后，连接mysql数据库

``` js
connection.connect();
```

* 成功连接上mysql数据库了，前端的数据会先传递给路由（方法）/singupAccount
* 这个时候前端的数据是保存在全局变量req.query里面的，一共有两个值“name”和“password”

``` js
req.query.name
req.query.password
```

* 此时，声明一个变量response用来保存这两个前端传过来的值

``` js
    var response = {
        "name":req.query.name,
        "password":req.query.password
    };
```

* OK,现在需要做最后一步了，让Mysql执行SQL命令，把前端的传过来的数据正确的插入数据库里

``` js
    var  addSql = 'INSERT INTO Account(AccountName, Password) VALUES(?,?)';
    var  addSqlParams = [response.name, response.password];

    connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
            console.log('[INSERT ERROR] - ',err.message);
            res.send('执行sql出错!');
            return;
        }
        res.send('Welcome~ SingUp Success ^_^');
    });
```

* 执行完SQL命令后，断开与数据库的连接

``` js
connection.end();
```

### 最终测试

* 首先打开终端，并打开mysql数据库，查看Account表里的内容

```
mysql -u root -p
Enter password:

mysql>
mysql> use my_db;
Database changed
mysql> select * from Account;

ID	AccountName	Password
1	KingArthur	KingArthur
1 row in set (0.00 sec)
mysql> 
```

* 再打开一个新的终端，切换当前路径至～/Desktop/nodejs_learningload,执行index.js文件，启动web服务器
> node index.js
* 打开浏览器，键入地址127.0.0.1:8081，打开主页
* 键入“Name”值“KingArthur2”，键入“Password”值“KingArthur2”，然后点击提交
* 页面跳转，并显示“Welcome~ SingUp Success ^_^”
* 此时，调出另一终端，查看数据库里的Account表
* > mysql> select * from Account;

```
ID	AccountName	Password
1	KingArthur	KingArthur
2   KingArthur2 KingArthur2
2 row in set (0.00 sec)
```

* 至此，nodejs与mysql成功进行了数据交互。

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢

