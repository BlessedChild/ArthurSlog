# Slog100_使用React框架进行前端开发11
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-100
* Year·1

* Guangzhou·China
* October 21th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

人生天地之间 若白驹过隙 忽然而已

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [Ajax](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started)

* [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

### 开始编码

* 本次以‘商城首页’的公告栏为例

* 让页面在加载的时候 向服务器发起请求

* 客户端请求‘公告栏的数据’

* 服务端接受到客户端的请求之后

* 对请求进行路由 和 处理

* 然后将结果传递给客户端

* 具体的逻辑代码如下：

client/
``` js
import React, { Component } from 'react'

// 引入轮播组件
import Carouselarea from './carouselarea/carouselarea'
// 引入配置文件
import Config from '../../../../config.json'
// 引入样式文件
import './BodyContainer.less'

class BodyContainer extends Component {
    constructor(props) {
        super(props)
        this.state = { bulletinBoard_Text: '' }

        this.recbulletinBoard_Text = this.recbulletinBoard_Text.bind(this)
    }

    render() {
        return <div className='mobile_StoreIndex_BodyContainer'>
            <Carouselarea />
            <div className='bulletinBoard'>
                <div className='bulletinBoardImg'>图片</div>
                <div className='bulletinBoardBar'>{this.state.bulletinBoard_Text}</div>
            </div>
            <div className='navigationBar'>
                <div className='navigationBarItem'>
                    <div className='navigationBarIconItem'>图片</div>
                    <div>所有商品</div>
                </div>
                <div className='navigationBarItem'>
                    <div className='navigationBarIconItem'>图片</div>
                    <div>拼团</div>
                </div>
                <div className='navigationBarItem'>
                    <div className='navigationBarIconItem'>图片</div>
                    <div>限时促销</div>
                </div>
                <div className='navigationBarItem'>
                    <div className='navigationBarIconItem'>图片</div>
                    <div>秒杀</div>
                </div>
            </div>
            <div className='recommendBar'>
                <div className='recommendBarImg'>图片</div>
                <div>热销推荐</div>
            </div>
            <div className='theBestProduct'>
                <div className='theBestProduct_topBar'>
                    <div className='theBestProduct_topBar_title'>镇店之宝</div>
                    <div className='theBestProduct_topBar_more'>更多</div>
                </div>
                <div className='theBestProductList'>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目1</div>
                    </div>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目2</div>
                    </div>
                </div>
            </div>
            <div className='theBestProduct'>
                <div className='theBestProduct_topBar'>
                    <div className='theBestProduct_topBar_title'>专业工具</div>
                    <div className='theBestProduct_topBar_more'>更多</div>
                </div>
                <div className='theBestProductList'>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目1</div>
                    </div>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目2</div>
                    </div>
                </div>
            </div>
            <div className='theBestProduct'>
                <div className='theBestProduct_topBar'>
                    <div className='theBestProduct_topBar_title'>新品上市</div>
                    <div className='theBestProduct_topBar_more'>更多</div>
                </div>
                <div className='theBestProductList'>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目1</div>
                    </div>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目2</div>
                    </div>
                </div>
            </div>
            <div className='theBestProduct'>
                <div className='theBestProduct_topBar'>
                    <div className='theBestProduct_topBar_title'>力荐专区</div>
                    <div className='theBestProduct_topBar_more'>更多</div>
                </div>
                <div className='theBestProductList'>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目1</div>
                    </div>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目2</div>
                    </div>
                </div>
            </div>
            <div className='theBestProduct'>
                <div className='theBestProduct_topBar'>
                    <div className='theBestProduct_topBar_title'>特惠专区</div>
                    <div className='theBestProduct_topBar_more'>更多</div>
                </div>
                <div className='theBestProductList'>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目1</div>
                    </div>
                    <div className='theBestProductListItem'>
                        <div className='theBestProductListItemImg'>图片</div>
                        <div className='theBestProductListItemText'>类目2</div>
                    </div>
                </div>
            </div>
            <div className='aboutWe'>
                <div className='aboutWeImg'>图片（关于我们）</div>
                <div className='shoppingProcess'>图片（购物流程）</div>
                <div className='customerService'>
                    <div className='customerServiceTitle'>客服在线</div>
                    <div className='customerServiceText'>售前售后的任何问题，请及时联系客户，我们一定妥善为您解决。如果没有得到及时的回复，也不要慌张，我们上线后会第一时间回复。</div>
                </div>
                <div className='OrderInfo'>
                    <div className='OrderInfoTitle'>订单信息</div>
                    <div className='OrderInfoText'>我们会按世纪付款顺序完成商品发货、尽快将宝贝呈进您的生活。如遇节假日或特殊天气，可能会延迟，请您耐心等待。关注公众号，进入店铺即可查询所有订单及订单状态</div>
                </div>
                <div className='tips'>
                    <div className='tipsTitle'>温馨提示</div>
                    <div className='tipsText'>每款商品的信息、活动、发货等会有所不用，下单前请务必查看清楚哟～</div>
                </div>
                <div className='others'>
                    <div className='othersList'>
                        <div className='othersListItem'>实物拍摄</div>
                        <div className='othersListItem'>品质保障</div>
                        <div className='othersListItem'>闪电发货</div>
                    </div>
                    <div className='purchaseNotes'>
                        <div>购买须知</div>
                        <div className='purchaseNotesArrow'>></div>
                    </div>
                </div>
            </div>
            <div className='mobile_personalCenter_bodyContainer_footer'>
                <div className='mobile_personalCenter_bodyContainer_footer_nagivation'>
                    <div>店铺主页</div>
                    <div className='mobile_personalCenter_bodyContainer_footer_nagivation_line'></div>
                    <div>推广中心</div>
                    <div className='mobile_personalCenter_bodyContainer_footer_nagivation_line'></div>
                    <div>关注我们</div>
                    <div className='mobile_personalCenter_bodyContainer_footer_nagivation_line'></div>
                    <div>店铺信息</div>
                </div>
                <div className='mobile_personalCenter_bodyContainer_footer_companyLogo'>
                    <img src='' alt='公司Logo'></img>
                </div>
            </div>
            <div style={{ marginBottom: '128px' }}></div>
        </div>
    }

    componentDidMount() {
        this.recbulletinBoard_Text()
    }

    recbulletinBoard_Text() {
        const myObj = { func: 1, object: "test" }
        fetch(Config.baseUrl + 'api/client', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(myObj),
        })
            .then(response => {
                console.log('Add data to message successfuly')
                // 这里获取到了服务端返回的‘公告栏’的数据 resmsg
                const resmsg = response.json()
                console.log('Response1: ', resmsg)
                console.log('Response2: ', response)
                return resmsg
            })
            .then(resmsg => {
                // 然后 传值给‘公告栏’
                // 接着 重新渲染（局部渲染）页面
                // 语法 查一下setState里怎么使用对象
                this.setState({
                    bulletinBoard_Text: resmsg
                })
            })
            .catch(err => {
                alert("Error in sending data to server: " + err.message)
            })
    }
}

export default BodyContainer
```

* 本次把 样式独立出去 代码看起来清爽一些了

* 可以看到其中的关键部分在于

``` js
...
constructor(props) {
    super(props)
    this.state = { bulletinBoard_Text: '' }

    this.recbulletinBoard_Text = this.recbulletinBoard_Text.bind(this)
}
...

...
<div className='bulletinBoard'>
    <div className='bulletinBoardImg'>图片</div>
    <div className='bulletinBoardBar'>{this.state.bulletinBoard_Text}</div>
</div>
...

...
componentDidMount() {
    this.recbulletinBoard_Text()
}

recbulletinBoard_Text() {
    const myObj = { func: 1, object: "test" }
    fetch(Config.baseUrl + 'api/client', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(myObj),
    })
        .then(response => {
            console.log('Add data to message successfuly')
            // 这里获取到了服务端返回的‘公告栏’的数据 resmsg
            const resmsg = response.json()
            console.log('Response1: ', resmsg)
            console.log('Response2: ', response)
            return resmsg
        })
        .then(resmsg => {
            // 然后 传值给‘公告栏’
            // 接着 重新渲染（局部渲染）页面
            // 语法 查一下setState里怎么使用对象
            this.setState({
                bulletinBoard_Text: resmsg
            })
        })
        .catch(err => {
            alert("Error in sending data to server: " + err.message)
        })
}
...
```

* 这里 func的值等于1 代表了我们发起的是请求‘公告栏’数据的 请求

* 服务端接收到之后 发现func等于1

* 就会路由到‘公告栏’处理函数中去

* 接着把处理好的数据反馈给客户端

* 客户端接到反馈的信息之后

* 替换state.bulletinBoard_Text的值 然后重新渲染页面

* 这样 我们就得到了最新反馈到的数据 并显示了出来

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
            //res.header("Access-Control-Allow-Headers", "X-Requested-With, Content-Type")
            //res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS")
            //res.header("X-Powered-By", ' 3.2.1')
            //res.header("Content-Type", "application/json;charset=utf-8")
            // 这里 我们把object传给函数进行处理 同时还需要把res也传给函数 可以对客户端做出反馈
            //const results = Func1.func1(recDatas.object)
            //res.json(results)
            //console.log(results)
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
            //res.header("Content-Type", "application/json;charset=utf-8")
            let result = BulletinBoard.ReturnBBInfo(recDatas.object)
            res.json(result)
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
            //res.header("Content-Type", "application/json;charset=utf-8")
            res.json('error');
    }
})
```

* switch里的写法有一些语法的问题 不影响结果就不理了

* 关键可以看一下注释的内容

* 注释的内容 解释了一个业务上的逻辑设计

* 这次增加了新的判定状况 用于路由‘公告栏’处理函数

``` js
'use strict'

// 来自客户端的object
// 或者这么说 来自父级的 object
// 这里是客户端向服务端请求‘公告栏’的数据
// So object是空的

function func(object) {

    if (object == null) {
        return `客户端传来的值是空的`
    }
    else if (object != null) {
        // 这里 需要定义‘公告栏’的数据
        return '[欢迎来到ArthurSlogStore]' + '当前时间是： ' + '[' + new Date() + ']'
    }
    else {
        console.log('未知错误')
    }
}

module.exports = {
    ReturnBBInfo: func
}
```

* 经过测试 客户端成功地在每次加载页面时 拉取到‘公告栏’的数据

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore](https://github.com/BlessedChild/ArthurSlogStore)

* 至此，实现了页面加载时 动态加载服务端数据的业务逻辑。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
