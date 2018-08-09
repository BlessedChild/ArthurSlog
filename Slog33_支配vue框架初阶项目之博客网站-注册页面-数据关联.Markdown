* ArthurSlog
* SLog-33
* Year·1

* Guangzhou·China
* Aug 9th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

用七八十年提交一份人生的答卷 这是一场开卷 没有监考老师 有的 是在乎你的人 我想 答案并不是最重要的 重要的是一起答卷的这群人 特别是真正在乎你的人 当答卷提交的那一刻 也许不再是忐忑不安 而是坦然以对 那些经历的种种会一直温暖着人心

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* (必看，这个已经写的够明白的了)[HTTP](https://developer.mozilla.org/zh-CN/docs/Web/HTTP),超文本传输​​协议（HTTP）是用于传输诸如HTML的超媒体文档的应用层协议。它被设计用于Web浏览器和Web服务器之间的通信，但它也可以用于其他目的。 HTTP遵循经典的客户端-服务端模型，客户端打开一个连接以发出请求，然后等待它收到服务器端响应。 HTTP是无状态协议，意味着服务器不会在两个请求之间保留任何数据（状态）。虽然通常基于TCP / IP层，但可以在任何可靠的传输层上使用; 也就是说，一个不会静默丢失消息的协议，如UDP。

* 引用 [mozilla HTTP概述](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_web_server) 上的说明:

概述：
``` txt
“网络服务器（Web server）”可以代指硬件或软件，然而它们都是协同工作的。

在硬件部分，一个网络服务器是一个用来存储网站的组成文件（比如说 HTML 文档，图片，CSS 样式表，和 JavaScript 文件）以及交付它们到终端用户的设备的计算机。它跟互联网连接并可以通过域名像 mozilla.org 来被访问。
在软件部分，一个网络服务器包括几个控制网络用户如何访问托管文件的部分，至少是一个 HTTP 服务器 [HTTP server]。一个 HTTP 服务器是一个能理解URLs (网络地址) 和 HTTP (你的浏览器查看网页时所用的协议) 的软件。
在最基础的层次，每当一个浏览器需要一个网络服务器上的托管文件时，浏览器会通过 HTTP 请求这个文件。当这个请求到达了正确的网络服务器（硬件），这个 HTTP 服务器（软件）返回所请求的文档，同样通过 HTTP。

Basic representation of a client/server connection through HTTP

要发布一个网站，你需要一个静态或动态的服务器。

静态网络服务器（static web server），或者堆栈，由一个计算机（硬件）和一个 HTTP 服务器（软件）组成。我们称它为 “静态” 因为这个服务器把它的托管文件 “保持原样” 地传送到你的浏览器。

动态网络服务器（dynamic web server） 由一个静态的网络服务器加上额外的软件组成，最普遍的是一个应用服务器 [application server] 和一个数据库 [database]。我们称它为 “动态” 因为这个应用服务器会在通过 HTTP 服务器传送托管文件到你的浏览器之前对这些托管文件进行更新。

举个例子，要生成你在浏览器中看到的最终网页，应用服务器或许会用一个数据库中的内容填充一个 HTML 模板。网站像 MDN 或者维基百科 [Wikipedia] 有成千上万的网页，但是它们不是真正的 HTML 文档，它们只是少数的 HTML 模板以及一个巨大的数据库。这样的设置让它更快更简单地维护以及交付内容。
```

托管文件：
``` txt
一个网络服务器首先需要存储这个网站的文件，也就是说所有的 HTML 文档和它们的相关资源 [related assets]，包括图片，CSS 样式表，JavaScript 文件，字形 [fonts] 以及影像。

严格来说，你可以在你自己的计算机上托管所有的这些文件，但是在一个专用的网络服务器上存储它们会方便得多，因为它

会一直启动和运行
会一直与互联网连接
会一直拥有一样的 IP 地址（不是所有的 ISPs 都会为家庭线提供一个固定的 IP 地址）
由一个第三方提供者维护
因为所有的这些原因，寻找一个优秀的托管提供者是建立你的网站的一个重要部分。比较不同服务公司的提议并选择一个适合你的需求和预算的提议（服务的价格从免费到每月上万美金不等）。
一旦你设置好一个网络托管解决方案，你只需要去上传你的文件到你的网络服务器。
```

HTTP通信：
``` txt
第二点，一个网络服务器提供了 HTTP（超文本传输协议）支持。正如它的名字暗示，HTTP 明确提出了如何在两台计算机间传输超文本（比如说链接的网络文档 [linked web documents]）。

一个协议Protocol是一套为了在两台计算机间交流而制定的规则。 HTTP 是一个文本化的 [textual]，无状态的 [stateless] 协议。

文本化
所有的命令都是纯文本的 [plain-text] 和人类可读的 [human-readable]。
无状态
无论是服务器还是客户都不会记住之前的交流。举个例子，仅依靠 HTTP，一个服务器不能记住你输入的密码或者你正处于业务中的哪一步。你需要一个应用服务器来进行这样的工作。（我们会在日后的文章中涵盖这类的技术。）

HTTP 为客户和服务器间的如何沟通提供清晰的规则。我们会在日后的一篇技术文章 中覆盖 HTTP 本身。就目前而言，只需要知道这几点：

只有用户可以制定 HTTP 请求，然后只会送到服务器。服务器只可以回复一个客户的 HTTP 请求。
当通过 HTTP 请求一个文件时，客户必须提供这个文件的URL。
网络服务器必须应答每一个 HTTP 请求，至少也要回复一个错误信息。

在一个网络服务器上，HTTP 服务器要为处理和应答到来的请求负责任。

当收到一个请求时，一个 HTTP 服务器首先要检查所请求的 URL 是否与一个存在的文件相匹配。
如果是，网络服务器会传送文件内容回到浏览器。如果不是，一个应用服务器会建立必要的文件。
如果两种处理都不可能，网络服务器会返回一个错误信息到浏览器，最常见的是 “404 未找到” ["404 Not Found"]。（这错误太常见以至于很多网页设计者花费许多时间去设计 404 错误页面。
```

静态内容和动态内容：
``` txt
粗略地说，一个服务器可以提供静态或者动态的内容。“静态” 意味着 “保持原样地提供”。静态的网站是最容易建立的，所以我们建议你制作一个静态的网站作为你的第一个网站。

“动态” 意味着服务器会处理内容甚至实时地从一个数据库中产生它。这个解决方案提供了更多的灵活性，但是技术堆栈变得更难去处理，让建立网站更惊人地复杂。

以你正在阅读的页面为例子。在正在托管它的网络服务器里，有一个应用服务器会从数据库提取文章内容，安排它的布局，把它放置在一些 HTML 模板中，然后为你传输结果。在这里，这个应用服务器叫做 Kuma 并且是由 Python （使用 Django 构架) 构建的。Mozilla 团队为了 MDN 的特殊要求开发 Kuma，但是这里有很多相似的建立在很多其他技术之上的应用。

这里有太多的应用服务器，所以提供一个具体的服务器是挺难的。有些应用服务器迎合具体的网站类别，像是博客，百科或者电子商店；其他的应用服务器，叫做 CMSs（内容管理系统 [content management systems]），则更加通用。如果你正在开发一个动态网站，花一些时间去选择适合你需求的工具。除非你想要学习一些网络服务器编程 [web server programming]（而这本身就是一个令人兴奋的领域！），你不需要去创建你自己的应用服务器。这只是在重新创造轮子。
```

* [互联网是如何工作的](https://developer.mozilla.org/zh-CN/docs/learn/How_the_Internet_works)

* [万维网是如何工作的](https://developer.mozilla.org/zh-CN/docs/Learn/Getting_started_with_the_web/How_the_Web_works)

* [统一资源定位符(URL)](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_is_a_URL)

* [什么是超链接](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/What_are_hyperlinks)

* [创建超链接](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks)

* [AJAX是异步的JavaScript和XML（Asynchronous JavaScript And XML）](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)

* [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)

* [Using files from web applications](https://developer.mozilla.org/zh-CN/docs/Web/API/File/Using_files_from_web_applications)



### 开始编码

* 修改 signup.html 页面的代码和 signup.js 的代码，让 html 文件里的数据和 js 里的代码关联起来，以便于我们在 js 文件里去控制 html 文件里的数据，并能把用户在 html 页面上输入的数据，用 http 协议传送给服务端

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

        <form action="http://127.0.0.1:3000/signup" method="GET">

            <br>
            <div>
                Account: {{ account }}
                <br>
                <input type="text" name="name" placeholder="username">
            </div>
            <br>

            <br>
            <div>
                Password: {{ password }}
                <br>
                <input type="text" name="password" placeholder="password">
            </div>
            <br>

            <br>
            <div>
                Again Password: {{ repassword }}
                <br>
                <input type="text" name="repassword" placeholder="repassword">
            </div>
            <br>


            <br>
            <div>
                First Name: {{ firstname }}
                <br>
                <input type="text" name="firstname" placeholder="firstname">
            </div>
            <br>

            <br>
            <div>
                Last Name: {{ lastname }}
                <br>
                <input type="text" name="lastname" placeholder="lastname">
            </div>
            <br>

            <br>
            <div>
                Birthday: {{ birthday }}
                <br>
                <input type="text" name="birthday" placeholder="2000/08/08">
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
                <input type="text" name="wechart" placeholder="wechart's name">
            </div>
            <br>

            <br>
            <div>
                QQ: {{ qq }}
                <br>
                <input type="text" name="qq" placeholder="12345678">
            </div>
            <br>

            <br>
            <div>
                Email: {{ email }}
                <br>
                <input type="text" name="email" placeholder="12345678@qq.com">
            </div>
            <br>

            <br>
            <div>
                Contury: {{ contury }}
                <br>
                <input type="text" name="contury" placeholder="China">
            </div>
            <br>

            <br>
            <div>
                Address: {{ address }}
                <br>
                <input type="text" name="address" placeholder="Guangzhou">
            </div>
            <br>

            <br>
            <div>
                Phone: {{ phone }}
                <br>
                <input type="text" name="phone" placeholder="138********">
            </div>
            <br>

            <br>
            <div>
                Websize: {{ websize }}
                <br>
                <input type="text" name="websize" placeholder="xxx.com">
            </div>
            <br>

            <br>
            <div>
                Github: {{ github }}
                <br>
                <input type="text" name="github" placeholder="Github's URl">
            </div>
            <br>

            <br>
            <div>
                Bio: {{ bio }}
                <br>
                <input type="text" name="bio" placeholder="This is the world~">
            </div>
            <br>

            <br>
            <input type="submit" value="完成注册">
        </form>

        <a href="./index.html">Return index's page</a>
        <br>
        <br>
    </div>

    <script src="./js/signup.js"></script>
</body>

</html>
```

* 于此同时，我们把 html 里的数据与 js 关联起来，以便后续在 js 里处理这些数据，把数据传给服务端

signup.js
``` js
var signup_container = new Vue({
    el: '#signup-container',
    data: {
      account: '',
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
      bio: ''
    }
  })
```

* 打开 signup.html 页面，看一下页面是否正常，下一节继续

* 至此，我们完成了 signup.html 与 signup.js 之间的数据绑定。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢