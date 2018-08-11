* ArthurSlog
* SLog-36
* Year·1

* Guangzhou·China
* Aug 12th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

生活需要惊喜和新鲜 人有时候因为很执着一件事 而忘记了自己人生的意义

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

* [AJAX是异步的JavaScript和XML（Asynchronous JavaScript And XML）](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)

* [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

* [Using files from web applications](https://developer.mozilla.org/zh-CN/docs/Web/API/File/Using_files_from_web_applications)

### 开始编码

* 我们开始向单页应用前进，意思就是把多个网页集成到一个网页，把所有的业务都集成到这个页面上来

* 首先，调整一下服务端的 js 文件

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

app.use(router.routes());

app.listen(3000);

console.log('listening on port 3000');
```

* 其中的 

``` js
if(datas){
    ctx.redirect('account.html');
}
```

* 调整为

``` js
if (datas) {
    ctx.body = datas;
}
```

* ok，服务端的代码调整完毕

* 现在启动静态服务器

> node index.js

* 接着继续，我们把 signin.html 和 signup.html 合并在一个页面里 app.html

app.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="./css/style.css">
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <title>signin_ArthurSlog</title>
</head>

<body>

    <div id="signup-container">

        <div>This is signin's page by ArthurSlog</div>
        <p>Singin</p>
        <form id="form1" v-on:submit.prevent="signin">
            <br>
            <div>
                Account: {{ name_signin }}
                <br>
                <input type="text" v-model="name_signin" placeholder="username">
            </div>
            <br>

            <br>
            <div>
                Password: {{ password_signin }}
                <br>
                <input type="text" v-model="password_signin" placeholder="password">
            </div>
            <br>
            <input type="submit" value="登陆">
        </form>
        <br>
        <a href="./index.html">Return index's page</a>

        <div>This is signup's page by ArthurSlog</div>
        <p>Singup</p>

        <form id="form2" v-on:submit.prevent="addUser">

            <br>
            <div>
                Account: {{ name }}
                <br>
                <input type="text" v-model="name" placeholder="username">
            </div>
            <br>

            <br>
            <div>
                Password: {{ password }}
                <br>
                <input type="text" v-model="password" placeholder="password">
            </div>
            <br>

            <br>
            <div>
                Again Password: {{ repassword }}
                <br>
                <input type="text" v-model="repassword" placeholder="repassword">
            </div>
            <br>


            <br>
            <div>
                First Name: {{ firstname }}
                <br>
                <input type="text" v-model="firstname" placeholder="firstname">
            </div>
            <br>

            <br>
            <div>
                Last Name: {{ lastname }}
                <br>
                <input type="text" v-model="lastname" placeholder="lastname">
            </div>
            <br>

            <br>
            <div>
                Birthday: {{ birthday }}
                <br>
                <input type="text" v-model="birthday" placeholder="2000/08/08">
            </div>
            <br>

            <br>
            <div>
                <span>Sex: {{ currentSex }}</span>
                <br>
                <input type="radio" id="sex" value="male" v-model="currentSex">
                <label for="sex">male</label>
                <br>
                <input type="radio" id="sex" value="female" v-model="currentSex">
                <label for="sex">female</label>
            </div>
            <br>

            <br>
            <div>
                <span>Age: {{ currentAge }}</span>
                <br>
                <select v-model="currentAge" id="age">
                    <option disabled value="">Select</option>
                    <option v-for="age in ages">{{ age }}</option>
                </select>
            </div>
            <br>

            <br>
            <div>
                Wechart: {{ wechart }}
                <br>
                <input type="text" v-model="wechart" placeholder="wechart's name">
            </div>
            <br>

            <br>
            <div>
                QQ: {{ qq }}
                <br>
                <input type="text" v-model="qq" placeholder="12345678">
            </div>
            <br>

            <br>
            <div>
                Email: {{ email }}
                <br>
                <input type="text" v-model="email" placeholder="12345678@qq.com">
            </div>
            <br>

            <br>
            <div>
                Contury: {{ contury }}
                <br>
                <input type="text" v-model="contury" placeholder="China">
            </div>
            <br>

            <br>
            <div>
                Address: {{ address }}
                <br>
                <input type="text" v-model="address" placeholder="Guangzhou">
            </div>
            <br>

            <br>
            <div>
                Phone: {{ phone }}
                <br>
                <input type="text" v-model="phone" placeholder="138********">
            </div>
            <br>

            <br>
            <div>
                Websize: {{ websize }}
                <br>
                <input type="text" v-model="websize" placeholder="xxx.com">
            </div>
            <br>

            <br>
            <div>
                Github: {{ github }}
                <br>
                <input type="text" v-model="github" placeholder="Github's URl">
            </div>
            <br>

            <br>
            <div>
                Bio: {{ bio }}
                <br>
                <input type="text" v-model="bio" placeholder="This is the world~">
            </div>
            <br>

            <br>
            <input type="submit" value="完成注册">
        </form>

        <button v-on:click="addUser">addUser</button>

        <a href="./index.html">Return index's page</a>
        <br>
        <br>

        <div>
            {{ commits }}
        </div>
    </div>

    <script src="./js/signup.js"></script>
</body>

</html>
```

* 然后呢，在来调整一下前端的 js 文件

signup.js
``` js
var host = 'http://127.0.0.1:3000/';

var signup_container = new Vue({
    el: '#signup-container',
    data: {
      name_signin: '',
      password_signin: '',
      name: '',
      password: '',
      repassword: '',
      firstname: '',
      lastname: '',
      birthday: '',
      sexs: ['male', 'female'],
      currentSex: 'male',
      ages: ['1', '2', '3', '4', '5', '6', '7', '8',
             '9', '10', '11', '12', '13', '14', '15', '16', '17', '18'],
      currentAge: '18',
      wechart: '',
      qq: '',
      email: '',
      contury: '',
      address: '',
      phone: '',
      websize: '',
      github: '',
      bio: '',
      commits: null,
    },
    methods: {
      signin: function() {
        var xhr = new XMLHttpRequest()

        var self = this
        xhr.open('GET', host + 'signin?' + 'name=' + self.name_signin + '&password=' + self.password_signin, true)
        
        xhr.onload = function () {
          self.commits = xhr.responseText
        }
        
        xhr.send()
      },
      addUser: function () {
        var xhr = new XMLHttpRequest()

        var self = this
        xhr.open('GET', host + 'signup?' + 'name=' + self.name + '&password=' + self.password + '&firstname=' + 
        self.firstname + '&lastname=' + self.lastname + '&birthday=' + self.birthday
        + '&sex=' + self.currentSex + '&age=' + self.currentAge + '&wechart=' + self.wechart
        + '&qq=' + self.qq + '&email=' + self.email + '&contury=' + self.contury
        + '&address=' + self.address + '&phone=' + self.phone + '&websize=' + self.websize
        + '&github=' + self.github + '&bio=' + self.bio, true)
        
        xhr.onload = function () {
          self.commits = xhr.responseText
        }
        
        xhr.send()
      }
    }
  })
```

* 注意看到 html 和 js 文件里发生了变化的部分

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html

* 输入之前注册过的账号密码，然后点击 登陆 按钮

* 正常执行的话，你会在页面的底部发现，登陆后服务端返回的数据

* 至此，我们将 signin.html 和 signup.html 合并在了一起。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
