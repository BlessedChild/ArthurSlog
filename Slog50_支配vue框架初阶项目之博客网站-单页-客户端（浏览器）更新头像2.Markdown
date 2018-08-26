* ArthurSlog
* SLog-50
* Year·1

* Guangzhou·China
* Aug 26th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

要成就一番事业 既要靠本事上位 又得懂拉拢站队

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [统一资源定位符(URL)](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_URL)

* [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

* [vue模版语法 v-bind](https://cn.vuejs.org/v2/api/#v-bind)

* [FormData](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData)

* [FormData 对象的使用](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)

* [通过AJAX提交表单和上传文件可以不使用FormData对象](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest#Submitting_forms_and_uploading_files)

* [URL.createObjectURL()](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/createObjectURL)

### 开始编码

* 首先，先理一下思路：

``` txt
1.用户登陆、客户端（浏览器）登陆 ->
2.向服务端发送一条信息，获取用户数据 ->
3.服务端处理客户端发来的数据，返回相应的数据 ->
4.客户端（浏览器）接收返回的数据 ->
5.客户端（浏览器）解析返回的数据 ->
6.客户端（浏览器）根据解析好的数据，进行业务处理
（将处理好的数据路由到相应的前端的逻辑功能） ->
7.客户端（浏览器）渲染页面
```

* 上一篇文章，实现个头像的更新功能，但是需要重新登陆的时候，才会显示更新的图片

* 这次要做的，就是提交更新后让图片马上更新成最新的图片

* 考虑一下具体的实现逻辑，使用 vue.js框架双向数据流的功能，可以有下面几种方式：

1. 客户端（浏览器）在提交图片给服务器成功之后，同时客户端（浏览器）把提交的图片覆盖本地的图片

2. 客户端（浏览器）提交图片给服务器后，重新向服务器发送请求，获取最新的图片数据，页面上渲染最新的图片数据

3. 客户端（浏览器）在选择了准备传送的图片之后，提交图片给服务器之前，页面渲染最新的图片

* 选择第三种方法，我们要在选择图片的时候，同时渲染新的图片

* 根据 [vue模版语法 v-bind](https://cn.vuejs.org/v2/api/#v-bind)，使用 v-bin 绑定 图片的src，让我们可以在 client/signup.js 里可以动态修改 图片的src 的值，正因为 vue.js框架双向数据流的特性，当在 client/signup.js 修改 图片的src 的值的时候，页面上也会同时渲染新的图片

* 更新后的完整代码
client/signup.js
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
    image: '',
    imageSrc: '/image/ArthurSlog_icon.jpg'
  },
  methods: {
    uploadfiles: function () {
      var xhr = new XMLHttpRequest()
      var fd = new FormData()

      var self = this
      xhr.open('POST', host + 'uploadfiles', true)

      xhr.onload = function () {
        //self.commits = xhr.responseText
        self.commits = xhr.responseText
      }
      fd.append('myFile', this.image)
      xhr.send(fd)
    },
    filesChange: function (event) {
      this.image = event.target.files[0]
      this.imageSrc = window.URL.createObjectURL(event.target.files[0])
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

* 更新的部分：

server/index.js
``` js
//data部分
data: {
    imageSrc: '/image/ArthurSlog_icon.jpg'
}
//methods部分
methods: {
    filesChange: function (event) {
        this.image = event.target.files[0]
        this.imageSrc = URL.createObjectURL(event.target.files[0])
    }
}
```

* [URL.createObjectURL()](https://developer.mozilla.org/zh-CN/docs/Web/API/URL/createObjectURL)，使用这个方法生成一个 URL资源定位符赋值给图片的src，更新图片

* 同时，我们需要更新 html文件，在html文件里使用 vue.js模版语法 v-bin

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
                <img id="ArthurSlog_icon" v-bind:src="imageSrc" alt="ArthurSlog_icon" />
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

* 更新部分：

client/app.html
``` html
<div>
    <img id="ArthurSlog_icon" v-bind:src="imageSrc" alt="ArthurSlog_icon" />
</div>
```

* 使用 v-bin 绑定了src的值之后，通过 imageSrc 这个对象，js文件 可以 html文件里面图片的 src的值

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html，点击 signin 按钮

* 输入账号：ArthurSlog 密码：ArthurSlog，点击登陆

* 成功登陆之后，点击 “选择文件” 按钮，选择一张你电脑里的图片，然后点击“打开”

* 正常执行的情况下，你会发现，你的头像已经变成了你最新选取的图片了

* 再点击 uploadfiles 按钮，观察 服务端终端，正常情况下成功接收到文件，并打印出文件信息

* 刷新页面，点击 signin 按钮

* 输入账号：ArthurSlog 密码：ArthurSlog，点击登陆

* 正常情况下，头像已经更新为你最近更改的图片了

* 至此，我们实现了客户端头像选取后即时更新的功能。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
