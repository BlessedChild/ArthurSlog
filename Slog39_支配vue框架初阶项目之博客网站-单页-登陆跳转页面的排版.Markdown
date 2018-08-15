* ArthurSlog
* SLog-39
* Year·1

* Guangzhou·China
* Aug 15th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

当内存通电的一瞬间 就已经开启了时空旅行

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

* 这一次，我们对登陆之后的页面做一个排版

* 参考 vue.js 框架的模版语法[v-for](https://cn.vuejs.org/v2/guide/list.html#%E4%B8%80%E4%B8%AA%E5%AF%B9%E8%B1%A1%E7%9A%84-v-for)

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
            <div v-for="(value, key) in commits">
                {{ key }}: {{ value }}
            </div>
        </template>
    </div>


    <script src="./js/signup.js"></script>
</body>

</html>
```

* 修改的是下面这部分代码

client/app.html
``` html
<template id="returnResult" v-else-if="pagestate === '3'">
    <div v-for="(value, key) in commits">
        {{ key }}: {{ value }}
    </div>
</template>
```

* 我们这次做的是登陆界面的跳转，所以我们看一下 登陆的功能函数 signin

* 下面是对 signin 函数做的更新，把从服务端返回的数据进行 json 解析，在去 html 文件里使用循环语法渲染出来 

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
    pagestate: '0'
  },
  methods: {
    return_index: function() {
      this.pagestate = '0'
    },
    signin_index: function () {
      this.pagestate = '1';
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
        //解析服务端返回的数据
        var myObj = JSON.parse(xhr.responseText);
        self.commits = myObj
      }

      xhr.send()
    },
    addUser: function () {
      //当点击注册的时候，在页面上渲染从服务端返回的数据，把其他的部分隐藏掉
      this.pagestate = '3'

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

* 点击 signin 按钮，输入 账号： ArthurSlog 密码： ArthurSlog，正常执行，页面会一行一行的打印出服务端返回的数据

* 至此，我们实现了登陆页面跳转后的排版。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
