# Slog99_使用React框架进行前端开发10
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-99
* Year·1

* Guangzhou·China
* October 20th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

吾言甚易知 甚易行 天下莫能知 莫能行

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [Ajax](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started)

* [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

### 开始编码

* 本次来实现前端和后端的接口设计

* 这里使用原生的Fetch函数

* 先在前端页面添加一个函数 绑定页面组件的点击事件 用于向后端发起请求并传递数据

* 这里添加在商城首页的‘公告’组件上 绑定该组件的点击事件

client/
``` js
import React, { Component } from 'react'

import Carouselarea from './carouselarea/carouselarea'

// 引入配置文件
import Config from '../../../../config.json'

const bulletinBoardStyle = { alignItems: 'center', display: 'flex', flexDirection: 'raw', width: '100%', height: 64, fontSize: 40, textAlign: 'center', borderStyle: 'none' }
const productListStyle = { width: '100%', fontSize: 40, textAlign: 'center' }
const dividingLineStyle = { backgroundColor: '#000000', height: 1, width: '100%' }
const recommendStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#FFFFFF', width: '100%' }
const navigationBarStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF' }
const navigationBarItemStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '25%', marginLeft: '10px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const navigationBarItemStyleLeft = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '25%', marginLeft: '20px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const navigationBarItemStyleLRight = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '25%', marginLeft: '10px', marginRight: '20px', textAlign: 'center', fontSize: '30' }
const categoryStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF' }
const categoryItemStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const categoryItemStyleLeft = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '20px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const categoryItemStyleLRight = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '20px', textAlign: 'center', fontSize: '30' }
const categoryImgItemStyleLeft = { width: '220px', height: '220px', textAlign: 'center', lineHeight: '220px', backgroundColor: '#FFFFFF' }
const productStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF' }
// const productItemStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const productItemStyleLeft = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '50%', marginLeft: '20px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const productItemStyleRight = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '50%', marginLeft: '10px', marginRight: '20px', textAlign: 'center', fontSize: '30' }
const productImgItemStyle = { width: '400px', height: '400px', textAlign: 'center', lineHeight: '400px', backgroundColor: '#FFFFFF' }

const productItemInfoTextStyle = { width: '400px', marginLeft: '0px', textAlign: 'left' }
const productItemInfoPriceStyle = { width: '400px', marginLeft: '0px', textAlign: 'left' }
const productItemInfoStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', width: '400px' }
const productItemInfoTextareaStyle = { width: '400px', textAlign: 'left', margin: '0px' }

const bulletinBoardIconStyle = { width: '56px', height: '56px', fontSize: '12px', textAlign: 'center', lineHeight: '56px', marginLeft: '20px' }
const recommendIconStyle = { width: '256px', height: '256px', textAlign: 'center', lineHeight: '256px', borderStyle: 'solid' }


const navigationBarIconItemStyle = { width: '200px', height: '200px', textAlign: 'center', lineHeight: '200px', backgroundColor: '#FFFFFF', borderStyle: 'solid' }

// BodyContainet区域的样式
// const bodyContainerBarStyle = { position: "relative", marginTop: 0, marginBottom: 128, height: '100%', width: '100%' }

// BodyContainer区域渲染的内容
class BodyContainer extends Component {

    render() {
        return <div>
            <Carouselarea />
            <div>
                <div style={dividingLineStyle}></div>
                <div style={bulletinBoardStyle} onClick={this.toucha}>
                    <div style={bulletinBoardIconStyle} >图片</div>
                    <div className='bulletinBoard'>bulletinBoard（公告栏）</div>
                </div>
                <div style={dividingLineStyle}></div>
            </div>
            <div className='navigationBar' style={navigationBarStyle}>
                <div style={navigationBarItemStyleLeft}>
                    <div style={navigationBarIconItemStyle}>图片</div>
                    <div>所有商品</div>
                </div>
                <div style={navigationBarItemStyle}>
                    <div style={navigationBarIconItemStyle}>图片</div>
                    <div>拼团</div>
                </div>
                <div style={navigationBarItemStyle}>
                    <div style={navigationBarIconItemStyle}>图片</div>
                    <div>限时促销</div>
                </div>
                <div style={navigationBarItemStyleLRight}>
                    <div style={navigationBarIconItemStyle}>图片</div>
                    <div>秒杀</div>
                </div>
            </div>
            <div style={dividingLineStyle}></div>
            <div className='recommend' style={recommendStyle}>
                <div style={recommendIconStyle}>图片</div>
                <div>热销推荐</div>
            </div>
            <div style={dividingLineStyle}></div>
            <div className='category'>
                <div style={categoryStyle}>
                    <div style={categoryItemStyleLeft}>
                        <div style={categoryImgItemStyleLeft}>图片</div>
                        <div>类目1</div>
                    </div>
                    <div style={categoryItemStyle}>
                        <div style={categoryImgItemStyleLeft}>图片</div>
                        <div>类目2</div>
                    </div>
                    <div style={categoryItemStyleLRight}>
                        <div style={categoryImgItemStyleLeft}>图片</div>
                        <div>类目3</div>
                    </div>
                </div>
                <div style={categoryStyle}>
                    <div style={categoryItemStyleLeft}>
                        <div style={categoryImgItemStyleLeft}>图片</div>
                        <div>类目4</div>
                    </div>
                    <div style={categoryItemStyle}>
                        <div style={categoryImgItemStyleLeft}>图片</div>
                        <div>类目5</div>
                    </div>
                    <div style={categoryItemStyleLRight}>
                        <div style={categoryImgItemStyleLeft}>图片</div>
                        <div>类目6</div>
                    </div>
                </div>
            </div>
            <div style={dividingLineStyle}></div>
            <div className='productList' style={productListStyle}>
                <div style={productStyle}>
                    <div style={productItemStyleLeft}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                    <div style={productItemStyleRight}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                </div>
                <div style={productStyle}>
                    <div style={productItemStyleLeft}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                    <div style={productItemStyleRight}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                </div>
                <div style={productStyle}>
                    <div style={productItemStyleLeft}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                    <div style={productItemStyleRight}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                </div>
                <div style={productStyle}>
                    <div style={productItemStyleLeft}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                    <div style={productItemStyleRight}>
                        <div style={productImgItemStyle}>图片</div>
                        <div style={productItemInfoStyle}>
                            <div style={productItemInfoTextStyle}>
                                商品介绍
                        </div>
                            <div style={productItemInfoPriceStyle}>
                                <span style={productItemInfoTextareaStyle}>¥</span>
                                <span style={productItemInfoTextareaStyle}>8888</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div style={{ marginBottom: '256px' }}></div>
        </div>
    }


    toucha() {
        const myObj = { func: 0, object: "test" }
        fetch(Config.baseUrl + 'api/client', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(myObj),
        })
            .then(response => {
                console.log('Add data to message successfuly')
                const resmsg = response.json()
                console.log('Response1: ', resmsg)
                console.log('Response2: ', response)
                return resmsg
            })
            .catch(err => {
                alert("Error in sending data to server: " + err.message)
            })
    }
}

export default BodyContainer
```

* 额 代码有点长 没经过整理和优化

* 但是 可以看到其中的关键部分在于

``` js
...
// 引入配置文件
import Config from '../../../../config.json'
...

...
<div style={bulletinBoardStyle} onClick={this.toucha}>
    <div style={bulletinBoardIconStyle} >图片</div>
    <div className='bulletinBoard'>bulletinBoard（公告栏）</div>
</div>
...

...
toucha() {
    const myObj = { func: 0, object: "test" }
    fetch(Config.baseUrl + 'api/client', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(myObj),
    })
        .then(response => {
            console.log('Add data to message successfuly')
            const resmsg = response.json()
            console.log('Response1: ', resmsg)
            console.log('Response2: ', response)
            return resmsg
        })
        .catch(err => {
            alert("Error in sending data to server: " + err.message)
        })
}
...
```

* 这里把后端的地址 定义在了外部文件config.json里面 

* 然后在‘商城首页’的‘公告栏’组件上绑定点击事件

* 事件关联了toucha函数 该函数向服务端发起请求

* 发起的请求包含了两个数据 一个是‘func: 0’ 一个是 ‘object: "test"’

* func代表了功能函数的代码 后端通过前端传过来的func的值来判断 前端当前想干什么想执行哪个函数

* 而object就是 前端传给后端的数据内容了 这些数据传给后端之后 由后端进行相应的处理 处理完了之后再怎么弄就看开发的时候怎么来设计了

* 下面是后端的代码

``` js
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
    // 接到来自客户端的数据
    /*
    const newDatas = req.body
    // 对接受到的数据进行检测判断 这里是第一种方式
    if ((newDatas.count != 0) && (newDatas.count < 5)) {
        console.log('Accept: ', newDatas)
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
        // 如果接收到的数据不符合预期
        res.header("Access-Control-Allow-Origin", "*")
        res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
        res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
        res.header("X-Powered-By", ' 3.2.1')
        res.header("Content-Type", "application/json;charset=utf-8")
        res.json(newIssue)
        console.log('Client request is err!')
        return
    }

    console.log('POST: have a req from client')
    */

    // 现在采用第二种方式
    // 首先接收到来自客户端的数据 并保存在 recDatas对象里
    const recDatas = req.body
    // 接着 我们约定好的数据结构 就是 包头+包体
    // 也就是 func + object 这样的数据结构
    // 所以 首先判断func的值 然后根据不同的值 执行不同的函数
    switch (recDatas.func) {
        case 0:
            console.log('接收到了func等于0的数据')
            res.header("Access-Control-Allow-Origin", "*")
            res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
            res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
            res.header("X-Powered-By", ' 3.2.1')
            res.header("Content-Type", "application/json;charset=utf-8")
            // 这里 我们把object传给函数进行处理 同时还需要把res也传给函数 可以对客户端做出反馈
            const results = Func1.func1(recDatas.object)
            res.json(results)
            console.log(results)
            break;
        case 1:
            Func1(recDatas.object, res);
            break;
        case 2:
            Func1(recDatas.object, res);
            break;
        case 3:
            Func1(recDatas.object, res);
            break;
        case 4:
            Func1(recDatas.object, res);
            break;
        case 5:
            Func1(recDatas.object, res);
            break;
        case 6:
            Func1(recDatas.object, res);
        default:
            res.header("Access-Control-Allow-Origin", "*")
            res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
            res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
            res.header("X-Powered-By", ' 3.2.1')
            res.header("Content-Type", "application/json;charset=utf-8")
            res.json('error');
    }
})
```

* switch里的写法有一些语法的问题 不影响结果就不理了

* 关键可以看一下注释的内容

* 注释的内容 解释了一个业务上的逻辑设计

* 最后经过测试 前后端成功实现了数据交互 接下来进行具体的业务设计 比较繁琐

* 这里把最关键的思想已经呈现出来了 一次不讲太多 避轻就重比较合适

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore](https://github.com/BlessedChild/ArthurSlogStore)

* 至此，确定了前后端的数据交互的业务逻辑的设计。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
