* ArthurSlog
* SLog-35
* Year·1

* Guangzhou·China
* Aug 11th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

减少做一些“没脑子”的决定 学会用用宏观代替直观 用数据代替感受 用“慢思考”代替“快思考”

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

* 之前我们使用 vue.js 框架，同时参考了 [webAPI](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

* 然后在 js 文件里使用 [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) 对象

* js 文件操作浏览器通过 http协议 向服务器传递用户输入的信息数据，这样实现了一个用户注册的功能

* 服务端把客户端（浏览器）传送过来的数据，存储进数据库，然后给客户端（浏览器）返回一个执行结果

* 本篇就是从服务端获取注册功能的执行结果，然后在页面上显示出来

* 下面给出修改后的代码

signup.html
``` html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="./css/style.css">
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <title>signup_ArthurSlog</title>
</head>

<body>

    <div id="signup-container">
        <div>This is signup's page by ArthurSlog</div>
        <p>Singup</p>

        <form id="form" v-on:submit.prevent="addUser">

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

* 再看一下 js 文件

signup.js
``` js
var host = 'http://127.0.0.1:3000/signup?';

var signup_container = new Vue({
    el: '#signup-container',
    data: {
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
      commits: null
    },
    methods: {
      addUser: function () {
        var xhr = new XMLHttpRequest()

        var self = this
        xhr.open('GET', host + 'name=' + self.name + '&password=' + self.password + '&firstname=' + 
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

* 注意看到 html 文件里新添加的部分

``` html
<div>
    {{ commits }}
</div>
```

* 我们根据 vue.js 框架，在这里双大括号里的 commits 与 js 文件里的 commits 相关联

* 然后我们希望当服务端把执行结果 完整的 返回的客户端（浏览器）之后，把这个返回的值 赋予 commits 这个对象，然后重新渲染页面（vue.js 做的事情），这样我们在页面上就可以看到执行了结果了，也就知道注册是成功或者失败了

* 当然，在这里，我们之前编写服务端代码的时候，在逻辑里写了“如果注册成功，返回‘Signup Successful！’这样的字符串”，所以，当注册成功的时候，我们在页面上看到的，就会出现 “Signup Successful！”

* 现在，我们看下 js 文件里的改动：

``` js
methods: {
    addUser: function () {
    var xhr = new XMLHttpRequest()

    var self = this
    xhr.open('GET', host + 'name=' + self.name + '&password=' + self.password + '&firstname=' + 
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
```

* 其中，把 xhr.open() 这个函数执行完的返回值 赋予 self 这个对象

* 然后，根据 [webAPI](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequestEventTarget/onload)，可知：

``` txt
XMLHttpRequestEventTarget.onload 是 XMLHttpRequest 请求成功完成时调用的函数。

callback 是请求成功完成时要执行的函数。它接收一个 ProgressEvent 对象作为它的第一个参数。this 的值(即上下文)与此回调的 XMLHttpRequest 相同。
```

* 使用示例：

XMLHttpRequestEventTarget.onload
``` js
var xmlhttp = new XMLHttpRequest(),
  method = 'GET',
  url = 'https://developer.mozilla.org/';

xmlhttp.open(method, url, true);
xmlhttp.onload = function () {
  // 处理取回的数据(在 xmlhttp.response 中找到)
};
xmlhttp.send();
```

* ok，现在启动你的服务器（server路径下）

> node index.js

* 然后，打开浏览器，输入 127.0.0.1:3000，进入注册界面，填写完你的注册信息，点击“完成注册”按钮

* 现在，在页面的最下端，应该出现了一行新的字符串，他代表了你刚刚的注册行为已经成功完成！

``` txt
Singup Successful!
```

* 至此，我们在使用 vue.js 框架的情况下，实现了 展示注册结果的功能。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
