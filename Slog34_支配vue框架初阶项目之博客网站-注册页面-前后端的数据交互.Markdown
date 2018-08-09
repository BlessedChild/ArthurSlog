* ArthurSlog
* SLog-34
* Year·1

* Guangzhou·China
* Aug 10th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

沉睡的狮子 即将醒来 而世界将为之震撼

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

* 在Slog33里，使用了 vue.js 框架让 html 文件里的元素和 js 文件里的代码互相关联，以便于在 js 文件里使用 js 代码对 html 文件里的元素进行控制；

* 在 js 文件里，使用 vue.js 的规则编写 js 代码，在这里就有个问题了，api是参考 webAPI 还是 vue.js 框架的 API？这个问题，留着在开发过程中解决

* 在 js 里编写的 js 代码，其实做的事情就是 “获取 html 文件里元素的数据”、“获取 html 文件里元素的数据，并对数据进行处理”、“获取 html 文件里元素的数据，并传送给服务端”、“获取 html 文件里元素的数据，并传送给服务端，等待接收服务端传来的数据” 等这些操作
* 上面说的这些东西不需要背（因为你也背不住），只要在开发过程中参照 vue.js官方文档 并结合 web规范就可以编写需要的功能，一般情况下，这些文档都是类似于说明说或者字典的存在，然而....，并不是每个人都会按照这样的思路去做，如果你觉得有更适合你自己的方法，何妨一试，不过请记得控制你的时间成本

* 如果你根据我Slog33中的 html 文件修改，最终的结果是数据关联会有一点问题，所以先让我们把问题先解决（目前为止，我们说的只是前端的 html 和 js）

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

        <form id="form" v-on:submit="addUser">

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
            <ul>
                <li v-for="record in commits">
                    <span class="username">
                        {{ record }}
                    </span>
                </li>
            </ul>
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
      commits: ['null', 'null']
    },
    methods: {
      addUser: function () {
        var xhr = new XMLHttpRequest()
        xhr.open('GET', host + 'name=' + this.name + '&password=' + this.password + '&firstname=' + 
        this.firstname + '&lastname=' + this.lastname + '&birthday=' + this.birthday
        + '&sex=' + this.currentSex + '&age=' + this.currentAge + '&wechart=' + this.wechart
        + '&qq=' + this.qq + '&email=' + this.email + '&contury=' + this.contury
        + '&address=' + this.address + '&phone=' + this.phone + '&websize=' + this.websize
        + '&github=' + this.github + '&bio=' + this.bio, true)
        xhr.send()
      }
    }
  })
```

* 注意看到 html 文件里的 form 部分

``` html
<form id="form" v-on:submit="addUser">
     ...
    <input type="submit" value="完成注册">
</form>
```

* 在这里 v-on:submit 属于 vue.js 的模版语法，作用是 “可以用 v-on 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码”

* 像上面这样，在 js 文件里的 “method” 里创建一个 addUser 的方法，当你在 html 上点击完成注册的按钮的时候，就会调用 addUser 这个方法，方法就会执行你自己编写的逻辑

* 我们现在需要让这个 addUser 方法把我们填写的注册信息，传送给服务端，并等待服务端的执行结果（成功或者失败），然后在页面上显示出来执行的结果

* 去哪里找到这样的方法呢？首先想到的是 webAPI，试着去[官网](https://xhr.spec.whatwg.org/#introduction)找一下

* 再来看看，根据 vue.js 框架的[介绍](https://cn.vuejs.org/v2/guide/index.html)中，vue 的 js 文件结构，因此在方法中：

``` js
methods: {
    addUser: function () {
    var xhr = new XMLHttpRequest()
    xhr.open('GET', host + 'name=' + this.name + '&password=' + this.password + '&firstname=' + 
    this.firstname + '&lastname=' + this.lastname + '&birthday=' + this.birthday
    + '&sex=' + this.currentSex + '&age=' + this.currentAge + '&wechart=' + this.wechart
    + '&qq=' + this.qq + '&email=' + this.email + '&contury=' + this.contury
    + '&address=' + this.address + '&phone=' + this.phone + '&websize=' + this.websize
    + '&github=' + this.github + '&bio=' + this.bio, true)
    xhr.send()
    }
}
```

* [XMLHttpRequest标准](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)定义了一个API，它提供脚本客户端功能，用于在客户端和服务器之间传输数据；其中的 xhr.open() 方法，其实就是给服务端发送 http 请求，所以使用这个方法的时候，会生如下这样的请求，并发送给服务端：

``` url
http://127.0.0.1:3000/signup?name=???&password=???... 这后面的依此类推，我就不写了，因为很长
```

* 上面的请求中，需要包含用户输入的数据，比如name、password等等，其中的 ？？？三个问号，就是代表用户输入的具体的值，在方法中，我们使用 this.name 这样的语法来获取用户输入的值，为什么不能直接使用 name 呢？因为我试过了，不行，哈哈，以后会解释的

* 

``` js
    xhr.open('GET', host + 'name=' + name + '&password=' + password + '&firstname=' + 
    firstname + '&lastname=' + lastname + '&birthday=' + birthday
    + '&sex=' + currentSex + '&age=' + currentAge + '&wechart=' + wechart
    + '&qq=' + qq + '&email=' + email + '&contury=' + contury
    + '&address=' + address + '&phone=' + phone + '&websize=' + websize
    + '&github=' + github + '&bio=' + bio, true)
```

* 再来看一下 xhr.send() 方法，参考 [官方说明](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/send)

``` txt
XMLHttpRequest.send() 方法用于发送 HTTP 请求。如果是异步请求（默认为异步请求），则此方法会在请求发送后立即返回；如果是同步请求，则此方法直到响应到达后才会返回。XMLHttpRequest.send() 方法接受一个可选的参数，其作为请求主体；如果请求方法是 GET 或者 HEAD，则应将请求主体设置为 null。

如果没有使用setRequestHeader（）方法设置 Accept 头部信息，则会发送带有* / *的Accept 头部。
```

* ok，现在启动你的服务器（server路径下）

> node index.js

* 然后，打开浏览器，输入 127.0.0.1:3000，进入注册界面，填写完你的注册信息，点击“完成注册”按钮

* 现在，返回主页，进入登陆界面，填写你刚刚注册的账号和密码，点击登陆，正常情况下，登陆成功后会返回一串 json 字符串

* 至此，我们在使用 vue.js 框架的情况下，实现了前后端的数据交互。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
