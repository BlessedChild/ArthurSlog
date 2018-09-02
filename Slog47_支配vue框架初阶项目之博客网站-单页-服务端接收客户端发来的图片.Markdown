* ArthurSlog
* SLog-47
* Year·1

* Guangzhou·China
* Aug 24th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

房价太高了大部分人买不起怎么？降房价;工资太低了怎么办？提工资;区分人才和蠢材，回答这两个问题就够了

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [HTTP概述](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_web_server)

* [HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)

* [互联网是如何工作的](https://developer.mozilla.org/zh-CN/docs/learn/How_the_Internet_works)

* [万维网是如何工作的](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/How_the_Web_works)

* [统一资源定位符(URL)](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_URL)

* [什么是超链接](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_are_hyperlinks)

* [创建超链接](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks)

* [AJAX是异步的JavaScript和XML（Asynchronous JavaScript And XML](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)

* [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

* [Using files from web applications](https://developer.mozilla.org/zh-CN/docs/Web/API/File/Using_files_from_web_applications)

### 开始编码

* 本篇实现 服务端对图片的接收

* 上一篇文章，已经完成了客户端部分，html文件 和 js文件都已经完成了；服务端只是做了一个功能来检测客户端是否传来信息

* 这一篇文章，我们来完成服务端对客户端传过来的图片的接收功能

server/index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();
const Router = require('koa-router');
const router = new Router();

// $ GET /package.json
app.use(serve('../client'));

//
router.get('/signin', async (ctx) => {

    var mysql = require('mysql');
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '88888888',
        database: 'my_db'
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

    var addSql = 'SELECT * FROM ArthurSlogAccount WHERE AccountName=?';
    var addSqlParams = [response.name];

    var datas = await new Promise((resolve, reject) => {

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

    if (datas) {
        ctx.body = datas;
    }

    connection.end();
});

//
router.get('/signup', async (ctx) => {

    var mysql = require('mysql');
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '88888888',
        database: 'my_db'
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
        "password": ctx.query.password,
        "firstname": ctx.query.firstname,
        "lastname": ctx.query.lastname,
        "birthday": ctx.query.birthday,
        "sex": ctx.query.sex,
        "age": ctx.query.age,
        "wechart": ctx.query.wechart,
        "qq": ctx.query.qq,
        "email": ctx.query.email,
        "contury": ctx.query.contury,
        "address": ctx.query.address,
        "phone": ctx.query.phone,
        "websize": ctx.query.websize,
        "github": ctx.query.github,
        "bio": ctx.query.bio
    };

    var addSql = 'INSERT INTO ArthurSlogAccount(AccountName, Password, Firstname, Lastname, Birthday, Sex, Age, Wechart, Qq, Email, Contury, Address, Phone, Websize, Github, Bio) VALUES(?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?)';
    var addSqlParams = [response.name, response.password, response.firstname, response.lastname, response.birthday, response.sex, response.age, response.wechart, response.qq, response.email, response.contury, response.address, response.phone, response.websize, response.github, response.bio];



    ctx.body = await new Promise((resolve, reject) => {

        connection.query(addSql, addSqlParams, function (err, result) {
            if (err) {
                reject(err);
                console.log('[INSERT ERROR] - ', err.message);
                return;
            }
            resolve('Singup Successful!');
        });
    });

    connection.end();
});

router.post('/uploadfiles', async (ctx) => {

    console.log('客户端与服务端的 uploadfiles函数 已关联');

});

app.use(router.routes());

app.listen(3000);

console.log('listening on port 3000');

```

server/index.js
``` js
router.post('/uploadfiles', async (ctx) => {

    console.log('客户端与服务端的 uploadfiles函数 已关联');

});
```

* 上面的是上一篇更新的代码，我们把上次更新的部分在更新一次

server/index.js
``` js
router.post('/uploadfiles', koaBody({multipart: true}), async (ctx) => {

    console.log('fields: ', ctx.request.fields);

    console.log('files: ', ctx.request.files);

    const file = ctx.request.files.myFile;
    const reader = fs.createReadStream(file.path);
    const stream = fs.createWriteStream('ArthurSlog_icon' + '.jpg');
    reader.pipe(stream);
});
```

* 同时，因为我们使用了系统IO（input/output）功能、还有对POST数据的解析功能（POST相当于是一些二进制数据，需要根据POST协议进行翻译成字符信息），所以我们需要引用这些功能的代码集：

1. 首先，我们需要接收数据，并写入到服务器本地，所以需要引用关于IO的代码集，在nodejs语言中，这个代码集是 ‘fs’，所以在 js文件 里，需要写上 const fs = require("fs");

2. 再次，我们需要对POST数据进行解析，通过google，在npm里找到koa-body这个代码集，可以用来解析POST数据，所以我们引入koa-body，即：const koaBody = require('koa-body');

3. 因为 koa-body 是第三方代码集，没有包含在nodejs执行文件里，所以，我们需要切换至 server文件夹路径下，然后使用npm安装 koa-body

> cd server

> sudo npm install koa-body

* 更新好的 js文件如下：

server/index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();
const Router = require('koa-router');
const router = new Router();
const fs = require("fs");
const koaBody = require('koa-body');

// $ GET /package.json
app.use(serve('../client'));

//
router.get('/signin', async (ctx) => {

    var mysql = require('mysql');
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '88888888',
        database: 'my_db'
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

    var addSql = 'SELECT * FROM ArthurSlogAccount WHERE AccountName=?';
    var addSqlParams = [response.name];

    var datas = await new Promise((resolve, reject) => {

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

    if (datas) {
        ctx.body = datas;
    }

    connection.end();
});

//
router.get('/signup', async (ctx) => {

    var mysql = require('mysql');
    var connection = mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: '88888888',
        database: 'my_db'
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
        "password": ctx.query.password,
        "firstname": ctx.query.firstname,
        "lastname": ctx.query.lastname,
        "birthday": ctx.query.birthday,
        "sex": ctx.query.sex,
        "age": ctx.query.age,
        "wechart": ctx.query.wechart,
        "qq": ctx.query.qq,
        "email": ctx.query.email,
        "contury": ctx.query.contury,
        "address": ctx.query.address,
        "phone": ctx.query.phone,
        "websize": ctx.query.websize,
        "github": ctx.query.github,
        "bio": ctx.query.bio
    };

    var addSql = 'INSERT INTO ArthurSlogAccount(AccountName, Password, Firstname, Lastname, Birthday, Sex, Age, Wechart, Qq, Email, Contury, Address, Phone, Websize, Github, Bio) VALUES(?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?)';
    var addSqlParams = [response.name, response.password, response.firstname, response.lastname, response.birthday, response.sex, response.age, response.wechart, response.qq, response.email, response.contury, response.address, response.phone, response.websize, response.github, response.bio];

    ctx.body = await new Promise((resolve, reject) => {

        connection.query(addSql, addSqlParams, function (err, result) {
            if (err) {
                reject(err);
                console.log('[INSERT ERROR] - ', err.message);
                return;
            }
            resolve('Singup Successful!');
        });
    });

    connection.end();
});

router.post('/uploadfiles', koaBody({multipart: true}), async (ctx) => {

    console.log('fields: ', ctx.request.fields);

    console.log('files: ', ctx.request.files);

    const file = ctx.request.files.myFile;
    const reader = fs.createReadStream(file.path);
    const stream = fs.createWriteStream('ArthurSlog_icon' + '.jpg');
    reader.pipe(stream);
});

app.use(router.routes());

app.listen(3000);

console.log('listening on port 3000');
```

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html，点击 signin 按钮

* 输入账号：ArthurSlog 密码：ArthurSlog，点击登陆

* 成功登陆之后，点击 “选择文件” 按钮，选择一张你电脑里的图片，然后点击“打开”

* 再点击 uploadfiles 按钮，观察 服务端终端，如果服务端正常接收了客户端传过来的图片，那么早服务端终端上会打印出接收到的文件的详细信息

* 切换至 server文件夹 路径下，会看到接收到的图片文件，并依照代码命名为 “ArthurSlog_icon.jpg”

* 至此，我们完成了服务端对客户端传送来的图片的接收和保存。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢