* ArthurSlog
* SLog-41
* Year·1

* Guangzhou·China
* Aug 18th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)



履霜坚冰至

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [样式文件预编译器Sass的安装和使用](https://sass-lang.com/install)

* [样式文件预编译器Sass指导手册](https://sass-lang.com/guide)

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

* 本篇使用 Sass样式预编译器，编写 sass 文件生成 css文件，布置登陆成功后页面的样式

* 参考[Sass官网使用文档](https://sass-lang.com/install)，安装完 Sass编译程序之后，转换过程使用一下命令

> sass xxx.scss xxx.css

* 根据 [Sass官网的使用手册](https://sass-lang.com/guide)

client/css/style.scss
``` scss
$font-stack:    Helvetica, sans-serif;
$primary-color: #ff0000;

body {
  font: 100% $font-stack;
  color: $primary-color;
}

#signup-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

#signinResult {
  display: flex;
  flex-direction: column;
}

#signinResult > div {
  background-color: #f1f1f1;
  width: 300px;
  margin: 5px;
  text-align: left;
  line-height: 50px;
}
```

* 上面的代码参考 w3schools 的 [css文档手册](https://www.w3schools.com/css/css3_flexbox.asp)，我们使用 Flexbox 属性来定位和布局

* 其中新增的代码如下

``` scss
#signinResult {
  display: flex;
  flex-direction: column;
}

#signinResult > div {
  background-color: #f1f1f1;
  width: 300px;
  margin: 5px;
  text-align: left;
  line-height: 50px;
}
```

* 现在，切换到 css 文件夹路径下

> cd client/css/

* 现在，我们要使用 Sass预编译器（其实就是一段代码，一个程序），来把 sass 文件转换为 css 文件

* 根据 [Sass官网的使用说明](https://sass-lang.com/install),"sass sass文件名 css文件名"

> sass style.scss style.

* 现在，scss 文件就转换为 css 文件了，转换的结果如下：

client/css/style.css
``` css
body {
  font: 100% Helvetica, sans-serif;
  color: #ff0000;
}

#signup-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

#signinResult {
  display: flex;
  flex-direction: column;
}

#signinResult > div {
  background-color: #f1f1f1;
  width: 300px;
  margin: 5px;
  text-align: left;
  line-height: 50px;
}

/*# sourceMappingURL=style.css.map */
```

* 同时，需要调整一下 html 文件，把需要调整样式的部分，用 id 属性进行关联

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

* 现在，打开浏览器，输入 127.0.0.1:3000/app.html，点击 signin 按钮

* 输入账号：ArthurSlog 密码：ArthurSlog，点击登陆，正常执行下，数据都居中并带有背景色块

* 至此，我们对 登陆成功的页面 进行了布局和定位。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
