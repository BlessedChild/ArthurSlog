# Slog95_使用React框架进行前端开发7
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-95
* Year·1

* Guangzhou·China
* October 11th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

勇于敢则杀 勇于不敢则活 此两者 或利或害 天之所恶 孰知其故？

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [userAgent: http://www.w3school.com.cn/jsref/prop_nav_useragent.asp](http://www.w3school.com.cn/jsref/prop_nav_useragent.asp)

* [Less: http://lesscss.org/](http://lesscss.org/)

* [Webpack: https://webpack.js.org](https://webpack.js.org)

* [jakoblind: https://webpack.jakoblind.no/](https://webpack.jakoblind.no/)

### 开始编码

* 参考 W3C 标准

``` txt
userAgent 属性是一个只读的字符串，声明了浏览器用于 HTTP 请求的用户代理头的值。

一般来讲，它是在 navigator.appCodeName 的值之后加上斜线和 navigator.appVersion 的值构成的。

例如：Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.2; SV1; .NET CLR 1.1.4322)。

注：用户代理头：user-agent header。
```

* 凭借 userAgent，我在页面加载前对页面进行填充

* 在这里 我分成了 mobile 和 pc 两套页面

* 当判断客户端是移动端的话，就装载 mobile端 的页面

* 当判断客户端是pc的话，就装载 pc端 的页面


``` js
///
/// 构造 虚拟dom对象（数据结构）
///
import React, { Component } from 'react'

// 引入mobile的四个主界面
import StoreIndex from './pages/pages_mobile/storeIndex/index'
import ShoppingCart from './pages/pages_mobile/shoppingCart/index'
import StoreActivity from './pages/pages_mobile/storeActivity/index'
import PersonalCenter from './pages/pages_mobile/personalCenter/index'

// 引入pc的主界面
import StoreIndex_Pc from './pages/pages_pc/storeIndex/index'

// 引入配置文件
import Config from './config.json'

class App extends Component {

  constructor() {
    super()
    this.state = {
      data: [],
      padeId: []
    }
  }

  render() {
    let index

    function browserRedirect() {
      let sUserAgent = navigator.userAgent.toLowerCase()
      let bIsIpad = sUserAgent.match(/ipad/i) == "ipad"
      let bIsIphoneOs = sUserAgent.match(/iphone os/i) == "iphone os"
      let bIsMidp = sUserAgent.match(/midp/i) == "midp"
      let bIsUc7 = sUserAgent.match(/rv:1.2.3.4/i) == "rv:1.2.3.4"
      let bIsUc = sUserAgent.match(/ucweb/i) == "ucweb"
      let bIsAndroid = sUserAgent.match(/android/i) == "android"
      let bIsCE = sUserAgent.match(/windows ce/i) == "windows ce"
      let bIsWM = sUserAgent.match(/windows mobile/i) == "windows mobile"
      if (bIsIpad || bIsIphoneOs || bIsMidp || bIsUc7 || bIsUc || bIsAndroid || bIsCE || bIsWM) {
        index = 'mobile'
      }
      else {
        index = 'pc'
      }
    }

    browserRedirect()
    
    // 把四个主界面放在 mobile端 对象里，根据 pageId 的值，选择渲染的界面
    // 例如：
    // padeId = 0，意思就是渲染 StoreIndex 界面
    // padeId = 1，意思就是渲染 ShoppingCart 界面
    // padeId = 2，意思就是渲染 PromotionCenter 界面
    // padeId = 3，意思就是渲染 PersonalCenter 界面

    // mobile端
    let mobile = [<StoreIndex changePage={pageId => this.changePage(pageId)} />, <ShoppingCart changePage={pageId => this.changePage(pageId)} />, <StoreActivity changePage={pageId => this.changePage(pageId)} />, <PersonalCenter changePage={pageId => this.changePage(pageId)} />]
    // pc端 
    let pc = [<StoreIndex_Pc />]

    // 判断客户端是mobile还是pc
    // 根据结果 对页面采用合适的布局
    if (1) {
      index = mobile
      //alert('当前客户端是PC')
    }
    else if (0) {
      index = pc
      //alert('当前客户端是Mobile')
    }
    else {
      alert('请使用Pc浏览器或手机浏览器打开')
    }

    return <div className='page-container'>
      {index[this.state.pageId]}
    </div>
  }

  // componentDidMount
  // 参考链接： https://reactjs.org/docs/react-component.html#componentdidmount
  //
  // componentDidMount()在页面加载之前执行
  componentDidMount() {
    this.loadData()
    console.log('componentDidMount OK')
    // 载入StoreIndex页面
    this.setState({
      pageId: 0
    })
  }

  changePage(pageIds) {
    this.setState({
      pageId: pageIds
    })
  }

  // 向服务器请求数据
  loadData() {
    fetch(Config.baseUrl + 'api/issues/GET')
      .then(response => {
        if (response.ok) {
          console.log('Connect Server')
          response.json()
            .then(data => {
              console.log('Total count of records:', data._metadata.total_count)
              data.records.forEach(issue => {
                issue.created = new Date(issue.created)
                if (issue.completionDate)
                  issue.completionDate = new Date(issue.completionDate)
              })
              // 把服务端传过来的所有数据 存储在 本组件的全局对象 state里面的 data对象里
              this.setState({ data: data })
              // 把服务端传过来的records数据 存储在 本组件的全局对象 state里面的 issues对象里
              this.setState({ issues: data.records })
            })
        } else {
          console.log('Disconnect Server')
          response.json()
            .then(err => {
              alert("Failed to fetch issues: " + err.message)
            })
            .catch(err => {
              alert("Error in sending data to server: " + err.message)
            })
        }
      })

  }
}

// 导出虚拟dom对象，供主函数进行数据插入和最终webapp渲染
export default App;
```

* 工程的结构也 更新为 更加明显的结构

* 同时，设置 html节点的font-size为一个定值

* 页面上的字体采用 css3 的 rem单位特性（随着根节点font-size的大小变化而变化）

* 这次也重写了部分 pc端 页面的样式

* 更新了README，描述了 产品的设计框架

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore_1](https://github.com/BlessedChild/ArthurSlogStore_1)

* 至此，实现了mobile端 和 pc端 的页面适配。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
