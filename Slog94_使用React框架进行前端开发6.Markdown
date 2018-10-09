# Slog93_使用React框架进行前端开发6
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-94
* Year·1

* Guangzhou·China
* October 10th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

夫轻诺必寡信 多易必多难 是以圣人犹难之 故终无难矣

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

* [Less](http://lesscss.org/)

* [Webpack](https://webpack.js.org)

* [jakoblind](https://webpack.jakoblind.no/)

### 开始编码

* 本次更新的内容：

``` txt
1. 在文件结构上，将四个主界面独立分开
2. 四个主界面关联底部的TabBar
3. 在工程的根目录下，提供一个config.json配置文件，提供后端地址 baseUrl
4. 暂时为每一个界面配置一个less文件
5. 四个主界面的每个界面的文件结构暂时分为三部分‘header’、‘bodyContainer’和‘bottom’
```

* 其中，再React框架中，父组件通过向子组件传递回调函数，使得子组件可以修改父组件中的值

* 在父组件件中，为四个主界面设定了paageId，分别是0、1、2、3，一起放入一个index对象中

* 同时把父组件的state中的pageId作为index对象的索引

* 然后在四个bottomTabBar上绑定点击事件

* 点击的同时，调用父组件里的函数，并把绑定在TabBar上的pageId传递过去

* 父组件调用setState（）方法，把pageId赋值给父组件state中的pageId

* 因此，父组件中 index对象的索引发生改变

* 页面重新渲染

* 这样就实现了四个主界面跳转的逻辑

* 以下是相关的代码：

./App.js
``` js
///
/// 构造虚拟dom对象
///
import React, { Component } from 'react'

// 引入四个主界面
import StoreIndex from './pages/storeIndex/index'
import ShoppingCart from './pages/shoppingCart/index'
import PromotionCenter from './pages/promotionCenter/index'
import PersonalCenter from './pages/personalCenter/index'

// 引入配置文件
import Config from './config.json'

class App extends Component {

  constructor() {
    super()
    this.state = { padeId: [] }
  }
  render() {
    // 把四个主界面放在 index 对象里，根据 pageId 的值，选择渲染的界面
    // 例如：
    // padeId = 0，意思就是渲染 StoreIndex 界面
    // padeId = 1，意思就是渲染 ShoppingCart 界面
    // padeId = 2，意思就是渲染 PromotionCenter 界面
    // padeId = 3，意思就是渲染 PersonalCenter 界面
    const index = [<StoreIndex changePage = {pageId => this.changePage(pageId)} />, <ShoppingCart changePage = {pageId => this.changePage(pageId)}/>, <PromotionCenter changePage = {pageId => this.changePage(pageId)}/>, <PersonalCenter changePage = {pageId => this.changePage(pageId)}/>]

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

  changePage(pageIds){
    this.setState({
      pageId: pageIds
    })
  }
}

// 导出虚拟dom对象，供主函数进行数据插入和最终webapp渲染
export default App;
```

./pages/storeIndex/bottom/Bottom.jsx
``` js
import React, { Component } from 'react'

const bottomStyle = { backgroundColor: '#FFFFFF', position: "fixed", bottom: 0, height: 128, width: '100%', fontSize: 28, textAlign: 'center' }
const bottomTabBarStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF', height: 128 }
const bottomTabBarItemStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '1px', marginRight: '1px' }
const bottomTabBarItemStyleLeft = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '0.5px', marginRight: '1px' }
const bottomTabBarItemStyleRight = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '1px', marginRight: '0.5px' }
const bottomTabBarItemImg = { height: '88px', width: '88px', textAlign: 'center', lineHeight: '88px', backgroundColor: '#FFFFFF' }
const bottomTabBarItemText = { height: '40px' }

class Bottom extends Component {
    render() {
        return <div className='bottom' style={bottomStyle}>
            <div className='bottomTabBar' style={bottomTabBarStyle}>
                <div className='storeIndex' style={bottomTabBarItemStyleLeft} onClick={this.touchBottomTabBar.bind(this, 0)}>
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>商城首页</div>
                </div>
                <div className='shoppingCart' style={bottomTabBarItemStyle} onClick={this.touchBottomTabBar.bind(this, 1)}>
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>购物车</div>
                </div>
                <div className='promotionCenter' style={bottomTabBarItemStyle} onClick={this.touchBottomTabBar.bind(this, 2)}>
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>推广中心</div>
                </div>
                <div className='personalCenter' style={bottomTabBarItemStyleRight} onClick={this.touchBottomTabBar.bind(this, 3)}>
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>个人中心</div>
                </div>
            </div>
        </div>
    }

    touchBottomTabBar(e) {
        this.props.changePage(e)
    }
}

export default Bottom
```

* 在开发的过程中 常会碰到一些不太理想的情况

* 所以需要以结果为导向 先把基础功能实现出来

* 工程文件已经上传至[Github：https://github.com/BlessedChild/ArthurSlogStore_1](https://github.com/BlessedChild/ArthurSlogStore_1)

* 距离一个基础的商城还缺点东西 下次接着补充

* 至此，完成了四个主界面的文件结构的调整 以及底部TabBar的关联和跳转逻辑。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
