* ArthurSlog
* SLog-43
* Year·1

* Guangzhou·China
* Aug 21th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)



人生就是这样 苦乐相伴 福祸相依

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

* 我们先梳理一下，首先要在客户端部分（浏览器端）实现文件的选择和文件的上传；在服务端实现文件的接收，重要的是接受之后，把接收到的图片替换掉 client/image 文件夹里的图片文件，这样的话，当下次打开浏览器登陆，重新向服务端拉取数据的时候，就会拉取到更新后的图像了

* 所以，我们确定了需要修改的文件分别是 服务端:server\index.js、客户端:client\signup.js、客户端:client\app.html

* 我们先来更新 html 文件，在页面上增加一个上传图片的功能入口，这里我们分成两个操作：

1. 点击选择按钮，弹出本地文件浏览框之后，选择我们要的图片，然后点击确认，锁定我们要的图片

2. 点击上传图片，将我们锁定好的图片上传至服务器，显示上传的结果，客户端要做的事情了就到这里为止了

* 参考 [vue.js官方手册](https://cn.vuejs.org/v2/guide/events.html#%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E6%96%B9%E6%B3%95)

``` html
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
```

``` js
var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})

// 也可以用 JavaScript 直接调用方法
example2.greet() // => 'Hello Vue.js!'
```

* 上面的代码，说明了在使用 vue.js 框架的时候，当你想要关联到 原生DOM事件 的时候，需要做两件事情，第一就是使用 vue.js模版语法 v-on: + 事件（比如 click、change 等等，即：v-on:click、v-on:change）= "方法名（在 js 文件里实现这个方法）"，来创建一个逻辑使 html文件 和 js文件 互相关联；第二件事就是运用（运用的意思就是需要知道这个东西的原理，然后结合场景去使用）  原生DOM事件，通过这个 原生DOM事件，html文件上发生的事件所包含的信息可以传递给 js文件，js文件得到这些信息后 就可以进行加工修改，然后再次渲染到 html文件上

* 首先先观察到关键词 event，google一下“event html”：

``` txt
HTML事件是HTML元素发生的“事物”。

在HTML页面中使用JavaScript时，JavaScript可以对这些事件 做出“反应”。
```

* 举个栗子，比如我们编写出一个按钮，然后点击之后会显示“ArthurSlog”

``` html
<!DOCTYPE html>
<html>
<body>

<button onclick="display()">My name is: </button>

<script>
function display() {
    document.getElementById("demo").innerHTML = "ArthurSlog";
}
</script>

<p id="demo"></p>

</body>
</html> 
```

* 上面的代码，其中事件（event）指的就是“点击按钮”这个动作，也就是“onclick”事件，当发生“onclick”事件的时候，会调用到display（）函数，从而执行display（）函数里面的逻辑，打印出 “ArthurSlog”，上面是没有使用 vue.js 框架时的语法，事件和函数的关联方式就是 onclick=“display()”，而使用 vue.js 框架时，我们需要配合 vue.js 框架使用 vue 的模版语法 “v-on”，所以上面的代码就会变成：

``` html
<!DOCTYPE html>
<html>
<body>

<button v-on:onclick="display">My name is: </button>

<script>
    var signup_container = new Vue({
        el: '#demo',
        data: {
            txt: ''
        },
        methods:{
            display: function {
                this.txt = "ArthurSlog"
            }
        }
    })
</script>

<p id="demo">{{ txt }}</p>

</body>
</html> 
```

* 原来的 onclick=“display()” 变成了 v-on:onclick="display"

* 所以，我们的 html 文件更新为：

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

* 其中更新的部分如下：

client/app.html
``` html
<div>
    <div>Uploading {{ image }} files...</div>
    <br>
    <input type="file" v-on:change="filesChange">
</div>
```

* 同时，我们需要更新客户端的 js文件

* 再次参考 [vue.js官方手册](https://cn.vuejs.org/v2/guide/events.html#%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E6%96%B9%E6%B3%95)

``` html
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>
```

``` js
var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})

// 也可以用 JavaScript 直接调用方法
example2.greet() // => 'Hello Vue.js!'
```

* 仔细观察，可以发现在 js文件 里，“alert(event.target.tagName)” 通过，这个语句，js文件获取到了 html文件里的一些信息，那么这些又是些什么信息呢？google一下“event.target.tagName”，找到 [Event Object](https://www.w3schools.com/jsref/obj_event.asp) 的官方说明，可以理解为 event 的属性（Properties），其中发现我们在找的 [target属性](https://www.w3schools.com/jsref/event_target.asp)，官方解释如下：

```
The target event property returns the element that triggered the event.
```

* 上面的意思就是 event.target 里面包含的东西是一些 “element”，不同的 event 拥有不同的 element

* 可以想到的是，每次发生事件（event）时，有一些 element 就会发生改变，可以这么认为，这些与 event 相关联的 element 就包含在 event.target 中

* 下面我们来实现文件的选择功能，这里会用到 input 标签 和 onchange 事件，也就是说，当选中了我们要的图片之后，就会触发 onchange 事件，然后在 js文件里，我们要通过 event.target 来获取选择到的文件信息

* 这里，input 元素（element）和 event 息息相关，也就是说，event.target 里面包含的就是 input 的属性了，我们google一下 “input type=file”，找到 [<input type="file">](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file)，可以找到：

- | -
- | -
Supported Common Attributes | accept, multiple, required
IDL attributes	| files and value

``` txt
Additional attributes
In addition to the common attributes shared by all <input> elements, inputs of type file also support:

files
A FileList object that lists every selected file. This list has no more than one member unless the multiple attribute is specified.
```
* 上面的话的意思是什么？首先我们知道 input 元素可以获取的类型有 值类型 和 文件类型，这两种类型拥有一些通用的属性，但是，当 input 获取的元素为 文件类型的时候，会拥有 文件类型特有的属性--[文件集合属性](https://developer.mozilla.org/en-US/docs/Web/API/FileList)（也就是我们要找的东西），其中，每个文件拥有的属性就是[文件属性](https://developer.mozilla.org/en-US/docs/Web/API/File)

* 结合上面对 vue.js 模版语法的分析 和 input元素、原生DOM事件（event）的了解，我们对客户端的 js文件 进行更新

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
    image: ''
  },
  methods: {
    filesChange: function(event) {
      this.image = event.target.files[0].name
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

* 更新的部分如下：

client/signup.js
``` js
filesChange: function(event) {
    this.image = event.target.files[0].name
}
```

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html，点击 signin 按钮

* 输入账号：ArthurSlog 密码：ArthurSlog，点击登陆

* 成功登陆之后，点击 “选择文件” 按钮，选择一张你电脑里的图片，然后点击“打开”

* 此时，如果正常执行，你会看到 “Uploading 你选择的图片的名称 files...”

}

* 至此，我们完成了第一步 “1. 点击选择按钮，弹出本地文件浏览框之后，选择我们要的图片，然后点击确认，锁定我们要的图片”。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
