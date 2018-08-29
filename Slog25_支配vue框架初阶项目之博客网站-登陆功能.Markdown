* ArthurSlog
* SLog-25
* Year·1

* Guangzhou·China
* July 27th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

人的成长 几乎是决定于资源和平台 天份再怎么好的人 没有资源的支持 也无法成才 没有平台的扶持 也无法发挥作用

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

### 开始编码

* 首先，安装[homebrow](https://brew.sh)这个工具来协助我们 （如果已经安装brow就跳过这一步）

> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

* 使用brew安装mysql （如果已经安装mysql就跳过这一步）

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
VALUES ('ArthurSlog','ArthurSlog');
```

Query OK, 1 row affected (0.08 sec)

* 查看一下Account表

> mysql> SELECT * FROM Account;

ID|AccountName|Password
- | - | -
1 | ArthurSlog | ArthurSlog
1 row in set (0.00 sec)

* 退出mysql交互模式

> exit;

Bye

* 切换至项目路径下

> cd node_vue_directive_learningload

* 接下来，我们来完善一下登陆页面 “signin.html”：

signin.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>signin_ArthurSlog</title>
</head>

<body>

    <div>This is signin's page by ArthurSlog</div>
    <p>Singin</p>
    <form action="http://127.0.0.1:3000/singin" method="GET">
        Name: <br>
        <input type="text" name="name"> 
        <br>
        Password: <br>
        <input type="text" name="password">
        <br><br>
        <input type="submit" value="登陆">
    </form>
    <a href="./account.html">Signin</a>
    <br>
    <a href="./index.html">Return index's page</a>

</body>

</html>
```

* 上面的代码增加了使用账号和密码登陆的模块，关于[表单](https://www.w3schools.com/html/html_forms.asp)

``` html
<form action="http://127.0.0.1:3000/singin" method="GET">
    Name: <br>
    <input type="text" name="name"> 
    <br>
    Password: <br>
    <input type="text" name="password">
    <br><br>
    <input type="submit" value="登陆">
</form>
```

* 接下来我们编写后端对应的部分

index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();
const Router = require('koa-router');
const router = new Router();

// $ GET /package.json
app.use(serve('.'));

//登陆模块 signin()
router.get('/signin', async (ctx) => {

    var mysql = require('mysql');
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '88888888',
        database: 'mysql_db'
    });

    
    connection.connect(function (err) {
        if (err) {
            console.error('error connecting: ' + err.stack);
            return;
        }
        console.log('connected as id ' + connection.threadId);
    });
    

    var response = {
        "name": ctx.query.name,
        "password": ctx.query.password
    };

    var addSql = 'SELECT * FROM Account WHERE AccountName=?';
    var addSqlParams = [response.name];

    ctx.body = await new Promise((resolve, reject) => {

        connection.query(addSql, addSqlParams, function (err, result) {
            if (err) {
                reject(err);
                console.log('[SELECT ERROR] - ', err.message);
                return;
            }
            if (result[0].Password == response.password) {
                resolve(result[0]);
                console.log('Welcome~ SingIn Successul ^_^' + '\\' + 'Level: ' + result[0].Level + ' Houses: ' + result[0].Houses);
            }
            if (result[0].Password != response.password) {
                reject('SingIn Fault ^_^!');
                console.log('SingIn Fault ^_^!');
            }
        });
    });
    connection.end();
});

app.use(router.routes());

app.listen(3000);

console.log('listening on port 3000');

```

* 在使用express框架的时候，express 用来传值的是 req 和 res，req 就是从前端网页传过来的信息，而 res 就是我们后端传给前端的信息，这样的设计是根据 [http协议](https://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.2.2) 决定的，其中

* http_URL = "http:" "//" host [ ":" port ] [ abs_path [ "?" query ]] 这是http协议定义的URL协议标准

在express框架环境中
``` js
app.get('/signup', function (req, res) {
 
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
 });
```

* 关键的地方在于，koa框架 不同于 express框架，我们需要让页面在数据库命令执行完成后再进行渲染，以便我们把从数据库获取到的值完整的传给前端，所以我们需要修改一下语法

* 因为 mysql中间件 使用回调而不是承诺（promise），因此，要使用await来构建承诺（promise），如下面代码一样，它将等待承诺得到解决或拒绝

登陆模块 signin()
``` js
var response = {
    "name": ctx.query.name,
    "password": ctx.query.password
};

var addSql = 'SELECT * FROM Account WHERE AccountName=?';
var addSqlParams = [response.name];

ctx.body = await new Promise((resolve, reject) => {

    connection.query(addSql, addSqlParams, function (err, result) {
        if (err) {
            reject(err);
            console.log('[SELECT ERROR] - ', err.message);
            return;
        }
        if (result[0].Password == response.password) {
            resolve(result[0]);
            console.log('Welcome~ SingIn Successul ^_^' + '\\' + 'Level: ' + result[0].Level + ' Houses: ' + result[0].Houses);
        }
        if (result[0].Password != response.password) {
            reject('SingIn Fault ^_^!');
            console.log('SingIn Fault ^_^!');
        }
    });
});
```

* koa 框架与 express 框架不同的地方还在于，koa 使用 “ctx” 代替了 express 框架的 “req” 和 “res” 

* 把 request 和 response 集合成一个 ctx，ctx对应了 req 和 res 的每个属性，参考 [koa官方手册](https://koajs.cn/#-request-)

Request 别名
``` txt
以下访问器和 Request 别名等效：

ctx.header
ctx.headers
ctx.method
ctx.method=
ctx.url
ctx.url=
ctx.originalUrl
ctx.origin
ctx.href
ctx.path
ctx.path=
ctx.query
ctx.query=
ctx.querystring
ctx.querystring=
ctx.host
ctx.hostname
ctx.fresh
ctx.stale
ctx.socket
ctx.protocol
ctx.secure
ctx.ip
ctx.ips
ctx.subdomains
ctx.is()
ctx.accepts()
ctx.acceptsEncodings()
ctx.acceptsCharsets()
ctx.acceptsLanguages()
ctx.get()
```

Response 别名
```
以下访问器和 Response 别名等效：

ctx.body
ctx.body=
ctx.status
ctx.status=
ctx.message
ctx.message=
ctx.length=
ctx.length
ctx.type=
ctx.type
ctx.headerSent
ctx.redirect()
ctx.attachment()
ctx.set()
ctx.append()
ctx.remove()
ctx.lastModified=
ctx.etag=
```

* 例如，你需要获取前端表单里的 “name” 值：

``` js
var name = ctx.query.name;
```

* 再举个栗子，给前端返回一些数据：

``` js
ctx.body = 'Hello ArthurSlog~';
```

* 现在，使用 npm 指令，安装 [mysql中间件](https://www.npmjs.com/package/mysql) 和 [koa-router中间件](https://www.npmjs.com/package/koa-router)

> sudo npm install mysql koa-router

* 你还可以选择 [mysql2中间件](https://www.npmjs.com/package/mysql2)，使用方法参考链接的官方手册

* ok，现在，启动静态web服务器

> node index.js

* 打开浏览器，在地址栏输入 127.0.0.1:3000

* 点击 Signin 进入登陆界面

* 输入账号: ArthurSlog 密码：ArthurSlog

* 点击登陆，成功返回 Json 数据

``` json
{"ID":1,"AccountName":"ArthurSlog","Password":"ArthurSlog"}
```

* 至此，我们完成了前端的登陆功能和后端的登陆模块。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢