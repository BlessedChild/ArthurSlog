# Slog88_使用Express实现一个简单的web服务器
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-88
* Year·1

* Guangzhou·China
* October 1th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [MSDN: ArthurSlog](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

在你前进的时候 有的东西 你该扔的就扔了 要不然他耽误你的前途 他成为你最大的阻力 当你成功了 你可以把扔了的东西再捡回来 但是 如果你都不扔 你永远办不成功这件事

---

### 开发环境MacOS(Mojave 10.14 (18A391))

#### 需要的信息和信息源：

* [Express： https://github.com/expressjs/express](https://github.com/expressjs/express)

* [bady-parser: https://github.com/expressjs/body-parser](https://github.com/expressjs/body-parser)

* [REST: https://en.wikipedia.org/wiki/Representational_state_transfer](https://en.wikipedia.org/wiki/Representational_state_transfer)

### 开始编码

* JSON是 REST API 的请求和响应正文中首选的数据编码格式

* Express 是一个迷你但灵活的web应用框架

* Express 自己做的事情很少，通过依赖其他模块（中间件）来提供大部分应用所需要的功能

* Express 的核心是一个路由器，它接收一个客户端的请求，将其匹配到可用的路由上

* 并执行路由所关联的处理程序函数

* 一个路由是由以下部分组成的：

``` txt
1. 一个HTTP方法（GET、POST等）

2. 一个用于匹配请求的URI的路径规范

3. 路由处理程序 处理程序会接收一个请求对象和一个响应对象
```

* Express 基本组成部分包括了 路由（请求匹配、路由参数、路由查找）、处理程序函数（请求对象、响应对象）、中间件

* 具体的说明，请参考 Express官方手册

* 首先新建一个文件夹，并初始化开发环境

> cd ~/Desktop && mkdir ArthurSlogStore

> cd ArthurSlogStore

> sudo npm init -y

> sudo npm i express

* 创建一个js文件 main.js

* 完整的代码如下：

main.js
``` js
const express = require('express')
// 因为express无法解析POST的body数据，所以需要引入中间件body-parser来解析数据
const bodyParser = require('body-parser')

const app = express()

app.use(express.static('static'))
app.use(bodyParser.json())


// 接收到请求后返回的数据
const issues = [
    {
        id: 1, status: 'Open'
    },
    {
        id: 2, status: 'Close'
    },
]

// 接收到一个GET请求之后，返回一些数据
app.get('/api/issues', (req, res) => {
    const metadata = { total_count: issues.length }
    res.json({ _metadata: metadata, records: issues })
})

// 接收到一个POST请求之后，返回一些数据
app.post('/api/issues', (req, res) => {
    const newIssue = req.body
    newIssue.id = issues.length + 1
    newIssue.created = new Date()

    if(!newIssue.status)
        newIssue.status = 'New'

    issues.push(newIssue)

    res.json(newIssue)
    console.log('have a req from client')
})

app.listen(3000, () => {
    console.log('Server start on port 3000 ')
})
```

* 基本代码：

``` js
const express = require('express')
const app = express()

app.use(express.static('static'))

app.listen(3000, () => {
    console.log('Server start on port 3000 ')
})
```

* 上面的代码，实现了一个基本的web服务器，地址为localhost，端口为3000

* 然后我们来添加一个处理程序：

``` js
const express = require('express')
const app = express()

app.use(express.static('static'))

// 接收到请求后返回的数据
const issues = [
    {
        id: 1, status: 'Open'
    },
    {
        id: 2, status: 'Close'
    },
]

// 接收到一个GET请求之后，返回一些数据
app.get('/api/issues', (req, res) => {
    const metadata = { total_count: issues.length }
    res.json({ _metadata: metadata, records: issues })
})

app.listen(3000, () => {
    console.log('Server start on port 3000 ')
})
```

* 这里添加了一个GET请求的处理程序

* 其中

``` js
const metadata = { total_count: issues.length }
res.json({ _metadata: metadata, records: issues })
```

* 当接收到客户端的请求时，返回一个json对象 issues

``` json
[
    {
        id: 1, status: 'Open'
    },
    {
        id: 2, status: 'Close'
    },
]
```

* 此时启动服务器

> node main.js

* 然后打开浏览器，输入地址localhost:3000/api/issues

* 客户端会得到服务端返回的json对象，并在页面上显示出来

``` txt
{"_metadata":{"total_count":2},"records":[{"id":1,"status":"Open"},{"id":2,"status":"Close"}]}
```

* ok，实现GET方法之后，来实现POST方法

* 由于Express 无法直接解析POST方法里的body数据，所以引入中间件body-parser

> sudo npm i body-parser

* 更新代码：

``` js
const express = require('express')
// 因为express无法解析POST的body数据，所以需要引入中间件body-parser来解析数据
const bodyParser = require('body-parser')

const app = express()

app.use(express.static('static'))
// 在Express 框架中引入中间件body-parser
app.use(bodyParser.json())


// 接收到请求后返回的数据
const issues = [
    {
        id: 1, status: 'Open'
    },
    {
        id: 2, status: 'Close'
    },
]

// 接收到一个GET请求之后，返回一些数据
app.get('/api/issues', (req, res) => {
    const metadata = { total_count: issues.length }
    res.json({ _metadata: metadata, records: issues })
})

// 接收到一个POST请求之后，返回一些数据
app.post('/api/issues', (req, res) => {
    const newIssue = req.body
    newIssue.id = issues.length + 1
    newIssue.created = new Date()

    if(!newIssue.status)
        newIssue.status = 'New'

    issues.push(newIssue)

    // 解析并返回json对象
    res.json(newIssue)
    console.log('have a req from client')
})

app.listen(3000, () => {
    console.log('Server start on port 3000 ')
})
```

* 重启服务器

* 我们使用curl工具向服务端发送一个POST请求，打开命令行，输入：

> curl -s http://localhost:3000/api/issues --data '{"title": "Test Test", "owner": "me"}' --header 'Content-Type: application/json' | json_pp { "title": "Test Test", "owner": "me", "created": "2018-10-01T10:20:36.579Z", "status": "New", "id": 3 }

* 服务端返回json对象：

``` txt
{
   "owner" : "me",
   "status" : "New",
   "created" : "2018-09-30T22:02:21.025Z",
   "title" : "Test Test",
   "id" : 3
}
```

* 至此，使用Express 框架实现了一个简单的web服务器。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢