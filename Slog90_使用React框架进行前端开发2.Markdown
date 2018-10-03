# Slog90_使用React框架进行前端开发2
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-90
* Year·1

* Guangzhou·China
* October 4th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

将欲歙之 必故张之 将欲弱之 必故强之 将欲废之 必故兴之 将欲取之 必故与之 是谓微明

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [Cross-origin resource sharing: https://en.wikipedia.org/wiki/Cross-origin_resource_sharing](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)

### 开始编码

* 可能会有点跳，目前已经完成基本的前后端架构、数据库的对接

* 碰到了一点跨域的问题，本篇简单记录一下

* 由于写的速度跟不上开发速度，开发的过程后面每天再补上了

* 跨域问题，说到底就是浏览器的局限问题

* 浏览器的权限过大导致安全机制跟不上，所以暂时对自己做一些限制

* 在总体限制的情况下，来想办法实现具体的业务

* 因此出现了各种解决方案

* 但本质上，都是 “平衡业务与安全，再执行” 的思路

* 这里我采用了CORS （Cross-origin resource sharing），英文理解起来比较准确

* 前后端完整代码：

Client
``` js
import React, { Component } from 'react'

import IssueTable from './IssueTable'
import IssueAdd from './IssueAdd'
import IssueFilter from './IssueFilter'

class IssueList extends Component {
    constructor() {
        super()
        this.state = { issues: [] }
        this.createIssue = this.createIssue.bind(this)
    }

    // 页面加载时执行
    componentDidMount() {
        this.loadData()
    }

    // 向服务器添加数据
    createIssue(newIssue) {
        if (newIssue.owner) {
            fetch('http://localhost:3000/api/issues/POST', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(newIssue),
            })
                .then(response => {
                    const resmsg = response.json()
                    return resmsg
                })
                .then(updateIssue => {
                    updateIssue.created = new Date(updateIssue.created)
                    if (updateIssue.completionDate)
                        updateIssue.completionDate = new Date(updateIssue.completionDate)

                    const newIssue = this.state.issues.concat(updateIssue)
                    this.setState({ issues: newIssue })
                })
                .catch(err => {
                    alert("Error in sending data to server: " + err.message)
                })
        } else {
            console.log('NewIssue.owner is false')
        }
    }

    // 渲染页面
    render() {
        return <div>
            <h1>Issue Traceker</h1>
            <IssueFilter />
            <IssueTable issues={this.state.issues} />
            <IssueAdd createIssue={this.createIssue} />
        </div>
    }
}

export default IssueList
```

Server
``` js
const express = require('express')
// 因为express无法解析POST的body数据，所以需要引入中间件body-parser来解析数据
const bodyParser = require('body-parser')

const Issue = require('./issue.js')

// 引入mongodb驱动
const MongoClient = require('mongodb').MongoClient

const app = express()

app.use(express.static('static'))
app.use(bodyParser.json())

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
// 这里直接用一个all来响应两次请求，不过分成两个请求应该也是可以的
// 接收到一个请求之后，返回一些数据
app.all('/api/issues/POST', (req, res) => {
    console.log(req.body)
    const newIssue = req.body
    if (newIssue.owner) {
        console.log('Accept: ', newIssue)

        newIssue.created = new Date()

        if (!newIssue.status)
            newIssue.status = 'New'

        const err = Issue.validIssueStatus(newIssue)
        if (err) {
            res.status(422).json({ message: `Invalid request: ${err}` })
            return
        }

        if (!newIssue) {
            console.log('newIssue is null')
        }
        else if(newIssue){
            db.collection('issues').insertOne(newIssue)
                .then(result => {
                    return db.collection('issues').find({ _id: result.insertedId }).limit(1).next()
                })
                .then(newIssue => {
                    if (newIssue) {
                        res.header("Access-Control-Allow-Origin", "*")
                        res.header("Access-Control-Allow-Headers", "Content-Type")
                        res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
                        res.header("Content-Type", "application/json")
                        res.json(newIssue)
                    } else {
                        console.log('newIssue is null')
                        return
                    }
                })
                .catch(err => {
                    console.log(err)
                    res.header("Access-Control-Allow-Origin", "*")
                    res.header("Access-Control-Allow-Headers", "Content-Type")
                    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
                    res.header("Content-Type", "application/json")
                    res.status(500).json({ message: `Internal Server Error: ${err}` })
                    console.log('newIssue is error')
                })
        }
    }
    else {
        res.header("Access-Control-Allow-Origin", "*")
        res.header("Access-Control-Allow-Headers", "Content-Type")
        res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
        res.header("X-Powered-By", ' 3.2.1')
        res.header("Content-Type", "application/json")
        res.json(newIssue)
        console.log('Client request is null!')
        return
    }
    console.log('POST: have a req from client')
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

* 这里是[图解示意图: https://upload.wikimedia.org/wikipedia/commons/c/ca/Flowchart_showing_Simple_and_Preflight_XHR.svg](https://upload.wikimedia.org/wikipedia/commons/c/ca/Flowchart_showing_Simple_and_Preflight_XHR.svg)

* 简单来说，当你是GET和HEAD方法 同时没有 自定义的HTTP headers 时，服务器直接返回数据给你

* 除此之外，客户端需要跟服务器进行两次对话

* 第一次是查看 有没有 "Access-Control-*“这样的 headers，如果没有就报错

* 如果有，再返回数据

* 所以第一次并没有真正传出数据，第二次才行

* 至此，使用了 CORS 实现了跨域问题。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
