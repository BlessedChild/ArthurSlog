# Slog101_使用React框架进行前端开发12
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-101
* Year·1

* Guangzhou·China
* October 24th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

一时一局 我们需要见风使舵

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [require: https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_require](https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_require)

* [module: https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_module](https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_module)

* [export: https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_exports](https://nodejs.org/docs/latest-v8.x/api/modules.html#modules_exports)

* [path: https://www.npmjs.com/package/path](https://www.npmjs.com/package/path)

### 开始编码

* 本次确定了后端的开发规范 和 工程结构

``` txt
// 开发规范
// 所有数据的交互 都通过根目录下的 main.js 
// 其他任何文件 禁止上下路径的引用
// 例如：
// ./js/func1.js文件要引用 ./public/img/01.png文件的时候
// 禁止使用 require(../../public/img/o1.png) 或者 url(../../public/img/o1.png)
// 必须统一采用以下方式：
// const config = require('./main.js') 
```

* 把 在main.js文件里 创建一个对象 config作为整个工程的配置文件 

* 为了尽可能的整洁 不使用单独的全局配置文件

* 而其他文件都只需要引入 main.js文件里的 config对象

* 具体的代码如下：

server/main.js
``` js
// 这里面的后端接口 分为四类
// 第一类是提供给 消费者客户端的接口
// 第二类是提供给 商城管理者的接口
// 第三类是提供给 商城运营者的接口
// 第四类是提供给 商城开发者的接口

// 开发规范
// 所有数据的交互 都通过根目录下的 main.js 
// 其他任何文件 禁止上下路径的引用
// 例如：
// ./js/func1.js文件要引用 ./public/img/01.png文件的时候
// 禁止使用 require(../../public/img/o1.png) 或者 url(../../public/img/o1.png)
// 必须统一采用以下方式：
// const config = require('./main.js') 

// [] is array
// {} is object
// Arrays are Objects
// Arrays are a special type of objects
// The typeof operator in JavaScript returns "object" for arrays
// But, JavaScript arrays are best described as arrays
// Arrays use numbers to access its "elements". In this example, person[0] returns John:
// const person = ["John", "Doe", 46]
// Objects use names to access its "members". In this example, person.firstName returns John:
// const person = {firstName:"John", lastName:"Doe", age:46}
// 总结：
// {}里面放的是object
// 而[]是特殊的object
// 所以 可以写成{[], [], []}或{{}, {}, {}}这样的形式
// 也可以写成[{}, {}, {}]或[[], [], []]这样的形式

// 引入路径方案解决第三方包
// path.join()方法path使用特定于平台的分隔符作为分隔符将所有给定的段连接在一起 然后规范化生成的路径
// 零长度path段会被忽略 如果连接的路径字符串是零长度字符串 则返回'.' 表示当前工作目录
const path = require('path')

// 这里config作为一个object 所以使用{}
const config = {
    jsUrl: path.join(__dirname, "/src/js"),
    imgUrl: path.join(__dirname, "/src/public/img"),
    // 公告栏显示的信息
    BulletinBoardMsg: '[欢迎来到ArthurSlogStore]_当前时间是： '
}
// 导出工程的配置文件
module.exports = config

// 引入demo
const Issue = require(path.join(config.jsUrl, "/issue.js"))
// 引入测试函数
const Func1 = require(path.join(config.jsUrl, "/func1.js"))
// 引入‘公告栏’函数
const BulletinBoard = require(path.join(config.jsUrl, "/func00.js"))

// 引入express框架
const express = require('express')
// 因为express无法解析POST的body数据，所以需要引入中间件body-parser来解析数据
const bodyParser = require('body-parser')

const app = express()

app.use(express.static('static'))
app.use(bodyParser.json())

// 引入mongodb驱动
const MongoClient = require('mongodb').MongoClient

// 接收到一个请求之后，返回一些数据
app.all('/api/issues/GET', (req, res) => {

    db.collection('issues').find().toArray()
        .then(issues => {
            const metadata = { total_count: issues.length }

            res.header("Access-Control-Allow-Origin", "*")
            res.header("Access-Control-Allow-Headers", "X-Requested-With")
            res.header("Access-Control-Allow-Headers", "Content-Type")
            res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
            res.header("X-Powered-By", ' 3.2.1')
            res.header("Content-Type", "application/json;charset=utf-8")

            res.json({ _metadata: metadata, records: issues })
        })
        .catch(err => {
            console.log('Error', err)

            res.header("Access-Control-Allow-Origin", "*")
            res.header("Access-Control-Allow-Headers", "X-Requested-With")
            res.header("Access-Control-Allow-Headers", "Content-Type")
            res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
            res.header("X-Powered-By", ' 3.2.1')
            res.header("Content-Type", "application/json;charset=utf-8")

            res.status(500).json({ message: `Internal Server Error: ${error}` })
        })

    console.log('GET: have a req from client')
})

// 因为跨域请求，客户端每一次完整的通信都会发送两次请求
// 第一次请求是查看 "Access-Control-Allow-Origin" 等header的状态
// 状态允许才进行正式的通讯
// 所以，第一次的请求的里面是不包含我们定义的数据的，第二次才是
//
// 虽然在客户端定义的是POST方法，但由于跨域请求
// 客户端实际上发起了两个请求，第二个请求需要第一个请求的确认
// 如果第一次确认失败，那么第二个请求就不会发出
// 在这个过程中，第一次请求并不是POST方法，而是OPTIONS方法，所以这里使用all方法
// 当第一次请求成功后，第二次请求才是POST方法
// 这里直接用一个all来响应两次请求，不过分成两个请求应该也是可以
// 接收到一个请求之后，返回一些数据
app.all('/api/issues/POST', (req, res) => {
    console.log(req.body)
    const newIssue = req.body
    if (newIssue.owner) {
        console.log('Accept: ', newIssue)
        // newIssue.id = issues.length + 1
        newIssue.created = new Date()


        if (!newIssue.status)
            newIssue.status = 'New'

        // issues.push(newIssue)

        const err = Issue.validIssueStatus(newIssue)
        if (err) {
            res.status(422).json({ message: `Invalid request: ${err}` })
            return
        }

        if (!newIssue) {
            console.log('newIssue is null')
        }
        else if (newIssue) {
            db.collection('issues').insertOne(newIssue)
                .then(result => {
                    return db.collection('issues').find({ _id: result.insertedId }).limit(1).next()
                })
                .then(newIssue => {
                    if (newIssue) {
                        res.header("Access-Control-Allow-Origin", "*")
                        res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
                        res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
                        res.header("X-Powered-By", ' 3.2.1')
                        res.header("Content-Type", "application/json;charset=utf-8")
                        res.json(newIssue)
                    } else {
                        console.log('newIssue is null')
                        return
                    }
                })
                .catch(err => {
                    console.log(err)
                    res.header("Access-Control-Allow-Origin", "*")
                    res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
                    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
                    res.header("X-Powered-By", ' 3.2.1')
                    res.header("Content-Type", "application/json;charset=utf-8")
                    res.status(500).json({ message: `Internal Server Error: ${err}` })
                    console.log('newIssue is error')
                })
        }
    }
    else {
        res.header("Access-Control-Allow-Origin", "*")
        res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
        res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
        res.header("X-Powered-By", ' 3.2.1')
        res.header("Content-Type", "application/json;charset=utf-8")
        res.json(newIssue)
        console.log('Client request is null!')
        return
    }

    console.log('POST: have a req from client')
})

// 这个函数 接收客户端传过来的数据 
// 判断数据里面是否含有 bootomTabBar的值
// 根据四个bootomTabBar的值 来返回每个基础界面的数据
// 上面表述的不好理解 下面举个栗子
// 比如 这个函数 接收到一个数据data data里面包含有数据‘count’ 和 ‘tabBar’
// 并且‘count’等于1 ‘tabBar’也等于1
// 这代表了 客户端想要得到的 bootomTabBar数量是一个 想要得到的bootomTabBar是第一个（商城首页）
// 所以 通过这个函数
// 可以客户端可以请求到 第一个界面的数据、第二个界面的数据、第三个界面的数据、第四个界面的数据
// {
//     count: int, // 这个就是代表了本次要修改的bootomTabBar的数量
//     tabBar: []  // 这个就是代表了本次要修改的bootomTabBar
// }
//
// 这里其实还有另一种方式 就是全部的方法统一一个函数
// 具体是这么做的 例如 app.all('/api/POST', ...
// 那么 怎么判断客户端请求的是哪个功能呢？
// 是这样子的 是通过判断客户端传过来的数据data里面的特定的字段来判断的
// 可以这么看 就是根据客户端传过来的data里的‘func’的值 进行路由的
// 路由什么呢？ 路由到指定的功能函数
// 例如 客户端传过来的数据data里的‘func’==01
// 那么就路由到函数 func1 这个func1函数返回第一个界面的数据
// 如果 ‘func’==02
// 那么就路由到函数 func2 这个func2函数返回第二个界面的数据
// 以此类推
// 那么 想要这么做呢 就需要在后端进行严格的检查判断 需要一套工业级的机制
// 这么看来 有点像在写底层协议了 哈哈
// 包头+包体 的模式
//
// 客户端传过来的数据结构
// {
//     func: int, // 这个就相当于包头
//     object: [] // 这个就相当于包体
// }

app.all('/api/client', (req, res) => {
    console.log(req.body)
    // 现在采用第二种方式
    // 首先接收到来自客户端的数据 并保存在 recDatas对象里
    const recDatas = req.body
    // 接着 我们约定好的数据结构 就是 包头+包体
    // 也就是 func + object 这样的数据结构
    // 所以 首先判断func的值 然后根据不同的值 执行不同的函数
    switch (recDatas.func) {
        // 这个是前后端接口的测试功能
        case 0:
            console.log('接收到了func等于0的数据')
            res.header("Access-Control-Allow-Origin", "*")
            break;
        // 这个来写第一个正式功能
        // 这个写个什么功能好？给前端推点界面的数据好了
        // 这个就推给‘商城首页’里面‘公告栏’组件的数据好了
        // 首先 把功能写出来 单独一个js文件
        case 1:
            console.log('客户端请求公告栏的数据')
            res.header("Access-Control-Allow-Origin", "*")
            res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
            res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
            let result = BulletinBoard.ReturnBBInfo(recDatas.object)
            res.json(result)
            break;
        default:
            res.header("Access-Control-Allow-Origin", "*")
            res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
            res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
            res.json('error');
    }
})

let db

MongoClient.connect('mongodb://localhost:27017', { useNewUrlParser: true })
    .then(connection => {
        db = connection.db('issuetracker')
        app.listen(3000, () => {
            console.log('Server start on port 3000 ')
        })
    })
    .catch(err => {
        console.log('Error: ', err)
    })
```

* 重新调整了一下 引用的路径

* 经过测试 后端正常服务

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore](https://github.com/BlessedChild/ArthurSlogStore)

* 项目持续开发中 记录跟不上开发速度

* 有部分注解在源码的注释里

* 从源码注释可以看到 开发过程是一个实现与时间的权衡工作

* 前期花更多的时间去做好开发规范 后期维护和拓展会大大降低成本

* 但是在前期开发中 却需要耗费大量的成本

* 所以需要根据业务需求 和 收益期望来进行权衡

* 至此，制定了暂行的后端开发规范 并对工程结构进行了相应的调整。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
