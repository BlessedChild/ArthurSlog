* ArthurSlog
* SLog-44
* Year·1

* Guangzhou·China
* Aug 22th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

人们会渐渐爱上压迫 崇拜那些使他们丧失思考能力的工业产物

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

* 本篇实现 图片的上传 和 头像的修改

* 上一篇，我们完成了下面的第一步，现在我们来完成第二步

1. 点击选择按钮，弹出本地文件浏览框之后，选择我们要的图片，然后点击确认，锁定我们要的图片

2. 点击上传图片，将我们锁定好的图片上传至服务器，显示上传的结果，客户端要做的事情了就到这里为止了

* 参考 vue.js 框架的模版语法 [v-on](https://cn.vuejs.org/v2/api/#v-on)

* 我们编写出一个按钮，当点击按钮的时候，把我们选择好的图片上传到服务端去：

client/app.html
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
        <template class="container" v-if="pagestate === '0'">
            <div>This is index's page by ArthurSlog</div>
            <br>
            <button v-on:click="signin_index">Signin</button>
            <br>
            <button v-on:click="signup_index">Signup</button>
        </template>


        <template id="Signin" v-else-if="pagestate === '1'">
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
            <button v-on:click="return_index">ReturnIndex</button>
        </template>


        <template id="Signup" v-else-if="pagestate === '2'">
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
            <br>
            <button v-on:click="return_index">ReturnIndex</button>
            <br>
        </template>

        <template id="returnResult" v-else-if="pagestate === '3'">
            <div>
                <img id="ArthurSlog_icon" src="/image/ArthurSlog.png" alt="ArthurSlog_icon" />
            </div>
            <div>
                <div>Uploading {{ image }} files...</div>
                <br>
                <input type="file" v-on:change="filesChange">
                <br>
                <button v-on:click="uploadfiles">uploadfiles</button>
            </div>
            <div id="signinResult">
                <div v-for="(value, key) in commits">
                    {{ key }}: {{ value }}
                </div>
            </div>
        </template>
    </div>
    <script src="./js/signup.js"></script>
</body>

</html>
```

* 更新的部分如下：

``` html
<br>
<button v-on:click="uploadfiles">uploadfiles</button>
```

* 我们让 click事件 关联 uploadfiles函数，也就是说，当点击按钮的时候，会触发 js文件里的 uploadfiles函数

client/js/signup.js
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
    pagestate: '0',
    image: ''
  },
  methods: {
    uploadfiles: function () {
      var xhr = new XMLHttpRequest()
      var fd = new FormData();

      var self = this
      xhr.open('POST', host + 'uploadfiles', true)

      xhr.onload = function () {
        //self.commits = xhr.responseText
        self.commits = xhr.responseText
      }
      fd.append('myFile', this.image);
      xhr.send(fd)
    },
    filesChange: function (event) {
      this.image = event.target.files[0]
    },
    return_index: function () {
      this.pagestate = '0'
    },
    signin_index: function () {
      this.pagestate = '1'
    },
    signup_index: function () {
      this.pagestate = '2'
    },
    signin: function () {
      //当点击登陆的时候，在页面上渲染从服务端返回的数据，把其他的部分隐藏掉
      this.pagestate = '3'

      var xhr = new XMLHttpRequest()

      var self = this
      xhr.open('GET', host + 'signin?' + 'name=' + self.name_signin + '&password=' + self.password_signin, true)

      xhr.onload = function () {
        //self.commits = xhr.responseText
        var myObj = JSON.parse(xhr.responseText);
        self.commits = myObj
      }

      xhr.send()
    },
    addUser: function () {
      //当点击注册的时候，在页面上渲染从服务端返回的数据，把其他的部分隐藏掉
      this.pagestate = '3'

      var xhr = new XMLHttpRequest()

      /*
      xhr.open('GET', host + 'name=' + this.name + '&password=' + this.password + '&firstname=' + 
      this.firstname + '&lastname=' + this.lastname + '&birthday=' + this.birthday
      + '&sex=' + this.currentSex + '&age=' + this.currentAge + '&wechart=' + this.wechart
      + '&qq=' + this.qq + '&email=' + this.email + '&contury=' + this.contury
      + '&address=' + this.address + '&phone=' + this.phone + '&websize=' + this.websize
      + '&github=' + this.github + '&bio=' + this.bio, true)
      xhr.send()
      */

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

* 更新的部分如下：

``` js
uploadfiles: function () {
    var xhr = new XMLHttpRequest()
    var fd = new FormData();

    var self = this
    xhr.open('POST', host + 'uploadfiles', true)

    xhr.onload = function () {
    //self.commits = xhr.responseText
    self.commits = xhr.responseText
    }
    fd.append('myFile', this.image);
    xhr.send(fd)
}
```

* ok，现在把客户端的部分解决了，接下来就是 服务端部分 去接收和处理了，我们更新一下 服务端 的代码，让服务端和我们上面写的函数关联起来： 

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

    console.log('客户端与服务端的 uploadfiles函数 已关联');

});

app.use(router.routes());

app.listen(3000);

console.log('listening on port 3000');

```

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html，点击 signin 按钮

* 输入账号：ArthurSlog 密码：ArthurSlog，点击登陆

* 成功登陆之后，点击 “选择文件” 按钮，选择一张你电脑里的图片，然后点击“打开”

* 再点击 uploadfiles 按钮，观察 服务端终端，如果终端正常打印出字符串 “客户端与服务端的 uploadfiles函数 已关联”，说明客户端与服务端的 uploadfiles功能 已关联了起来

* 至此，我们完成了 客户端与服务端之间 uploadfiles功能 的关联。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
