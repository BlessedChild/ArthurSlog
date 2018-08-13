* ArthurSlog
* SLog-37
* Year·1

* Guangzhou·China
* Aug 13th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

不管发生什么事情 明天的太阳还是照常升起

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

* 这一次，把首页跟注册登陆页面也合并在一起

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

    <div class="container">
        <div>This is index's page by ArthurSlog</div>
        <br>
        <a href="./signin.html">Signin</a>
        <br>
        <a href="./signup.html">Signup</a>
    </div>

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

* 然后我们来布置页面的路由，把之前三个页面的功能集成在一个页面上，然后相互之间正常衔接

* 这里用到 vue.js 框架的模版语法 v-if

* 不过，首先先把首页的两个超级链接更换成两个按钮

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

            <br>
            <button v-on:click="return_index">ReturnIndex</button>
            <br>
        </template>

        <template id="Signin_result" v-else-if="pagestate === '3'">
            {{ commits }}
        </template>

        <template id="Signin_result" v-else-if="pagestate === '4'">
            {{ commits }}
        </template>
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
      pagestate: '0'
    },
    methods: {
      signin_index: function () {
        this.pagestate = '1';
        },
      signup_index: function () {
        this.pagestate = '2'
        },
      return_index: function() {
        this.pagestate = '0'
        },
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

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html

* 点击 signin 按钮、 ReturnIndex 按钮和 signup 按钮试试

* 至此，我们将 index.html 、 signin.html 、 signup.html 合并在了一个页面。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
