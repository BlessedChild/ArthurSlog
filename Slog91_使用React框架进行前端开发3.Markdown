# Slog91_使用React框架进行前端开发3
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-91
* Year·1

* Guangzhou·China
* October 5th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

宠辱若惊 贵大患若身

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

### 开始编码

* 来不急解释了，先上代码

Client/index.js
``` js
// index.js是入口文件
// ---
// React框架的生命周期（执行过程、执行顺序）： http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

// 
import React from 'react';

// react-dom
// 参考链接： https://reactjs.org/docs/react-dom.html
//
// 如果从<script>标记加载React ，则ReactDOM全局可以使用这些顶级API
// 如果你使用ES6和npm，你可以写import ReactDOM from 'react-dom'
// 如果你使用ES5和npm，你可以写var ReactDOM = require('react-dom')。
import ReactDOM from 'react-dom';

import './index.css';
import App from './App'; // 引入App对象（虚拟DOm）

// 在id等于‘root’的节点上渲染App对象（虚拟DOm）
ReactDOM.render(<App />, document.getElementById('root'));
```

Client/App.js
``` js
///
/// 构造虚拟dom对象
///
import React, { Component } from 'react';

import Header from './Header'
import BodyContainer from './BodyContainer'
import Bottom from './Bottom'

const iphone8Style = { position: "absolute", width: '100%', height: 4096 }

class App extends Component {

  componentWillMount() {
    document.documentElement.style.position = "absolute";
    document.documentElement.style.width = "100%";
    document.documentElement.style.height = "100%";
    document.documentElement.style.margin = "0";
    document.documentElement.style.padding = "0";
    document.documentElement.style.overflowX = "hidden";
    document.documentElement.style.overflowY = "auto";

    document.body.style.position = "absolute";
    document.body.style.width = "100%";
    document.body.style.height = "100%";
    document.body.style.margin = "0";
    document.body.style.padding = "0";
    document.body.style.overflowX = "hidden";
  }

  render() {
    return <div className='page-container' style={iphone8Style}>
      <Header />
      <BodyContainer />
      <Bottom />
    </div>
  }
}
// 导出虚拟dom对象，供主函数进行数据插入和最终webapp渲染
export default App;

```

Client/Header.jsx
``` js
import React, { Component } from 'react'

// Header区域的样式
const searchBarStyle = { position: 'fixed', marginTop: 0, backgroundColor: '#FFFFFF', width: '100%', height: 88}
const searchStyle = { position: 'fixed', marginTop: 0, backgroundColor: '#FFFFFF', width: '100%', height: 88, fontSize: 40, textAlign: 'center', borderStyle: 'none' }
const headerLineStyle = { position: 'fixed', marginTop: 88, backgroundColor: '#F2F2F2', width: '100%', height: 1 }

// Header区域渲染的内容
class Header extends Component {
    render() {
        return <div>
            <div className='searchBar' style={searchBarStyle}>
                <input placeholder='请输入商品名称' style={searchStyle}></input>
            </div>
            <div className='headerLine' style={headerLineStyle}></div>
        </div>
    }
}

export default Header
```

Client/BodyContainer.jsx
``` js
import React, { Component } from 'react'

// BodyContainet区域的样式
const bodyContainerBarStyle = { zIndex: -1, position: "relative", marginTop: 88, marginBottom: 128, height: '100%', width: '100%', fontSize: 40, textAlign: 'center' }
const carouselAreaStyle = { width: '100%', height: 375, fontSize: 40, textAlign: 'center' }
const bulletinBoardStyle = { width: '100%', height: 64, fontSize: 40, textAlign: 'center', borderStyle: 'none' }
const productListStyle = { width: '100%', fontSize: 40, textAlign: 'center' }
const dividingLineStyle = { backgroundColor: '#000000', height: 1, width: '100%' }
const recommendStyle = { backgroundColor: '#FFFFFF', height: 256, width: '100%' }
const navigationBarStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF' }
const navigationBarItemStyle = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const navigationBarItemStyleLeft = { display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '20px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const navigationBarItemStyleLRight = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '20px', textAlign: 'center', fontSize: '30' }
const categoryStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF' }
const categoryItemStyle = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const categoryItemStyleLeft = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '20px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const categoryItemStyleLRight = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '20px', textAlign: 'center', fontSize: '30' }
const productStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF' }
const productItemStyle = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const productItemStyleLeft = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '20px', marginRight: '10px', textAlign: 'center', fontSize: '30' }
const productItemStyleRight = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '10px', marginRight: '20px', textAlign: 'center', fontSize: '30' }

const navigationBarIconItemStyle = {}
// BodyContainer区域渲染的内容
class BodyContainer extends Component {

    render() {
        return <div className='bodyContainer' style={bodyContainerBarStyle}>
            <div>
                <div className='carouselArea' style={carouselAreaStyle}>carouselArea（轮播区域）</div>
                <div style={dividingLineStyle}></div>
                <div className='bulletinBoard' style={bulletinBoardStyle}>bulletinBoard（公告栏）</div>
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
            <div className='recommend' style={recommendStyle}>热销推荐</div>
            <div style={dividingLineStyle}></div>
            <div className='category'>
                <div style={categoryStyle}>
                    <div style={categoryItemStyleLeft}>
                        类目1
                    </div>
                    <div style={categoryItemStyle}>
                        类目2
                    </div>
                    <div style={categoryItemStyleLRight}>
                        类目3
                    </div>
                </div>
                <div style={categoryStyle}>
                    <div style={categoryItemStyleLeft}>
                        类目4
                    </div>
                    <div style={categoryItemStyle}>
                        类目5
                    </div>
                    <div style={categoryItemStyleLRight}>
                        类目6
                    </div>
                </div>
            </div>
            <div style={dividingLineStyle}></div>
            <div className='productList' style={productListStyle}>
                <div style={productStyle}>
                    <div style={productItemStyleLeft}>商品1</div>
                    <div style={productItemStyle}>商品2</div>
                    <div style={productItemStyleRight}>商品3</div>
                </div>
                <div style={productStyle}>
                    <div style={productItemStyleLeft}>商品4</div>
                    <div style={productItemStyle}>商品5</div>
                    <div style={productItemStyleRight}>商品6</div>
                </div>
                <div style={productStyle}>
                    <div style={productItemStyleLeft}>商品7</div>
                    <div style={productItemStyle}>商品8</div>
                    <div style={productItemStyleRight}>商品9</div>
                </div>
            </div>
        </div>
    }
}

export default BodyContainer
```

Client/Bottom.jsx
``` js
import React, { Component } from 'react'


const bottomStyle = { backgroundColor: '#FFFFFF', position: "fixed", bottom: 0, height: 128, width: '100%', fontSize: 28, textAlign: 'center' }
const bottomTabBarStyle = { display: 'flex', alignItems: 'stretch', backgroundColor: '#FFFFFF', height: 128 }
const bottomTabBarItemStyle = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '1px', marginRight: '1px' }
const bottomTabBarItemStyleLeft = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '0.5px', marginRight: '1px' }
const bottomTabBarItemStyleRight = { backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '1px', marginRight: '0.5px' }
const bottomTabBarItemImg = { height: '88px', width: '88px', textAlign: 'center', lineHeight: '88px'}
const bottomTabBarItemText = { height: '40px' }

class Bottom extends Component {
    render() {
        return <div className='bottom' style={bottomStyle}>
            <div className='bottomTabBar' style={bottomTabBarStyle}>
                <div style={bottomTabBarItemStyleLeft}>
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>商城首页</div>
                </div>
                <div style={bottomTabBarItemStyle}>
                    <div>图片</div>
                    <div>购物车</div>
                </div>
                <div style={bottomTabBarItemStyle}>
                    <div>图片</div>
                    <div>推广中心</div>
                </div>
                <div style={bottomTabBarItemStyleRight}>
                    <div>图片</div>
                    <div>个人中心</div>
                </div>
            </div>
        </div>
    }
}

export default Bottom
```

* 至此，实现了一个基础的商城页面组建的构建。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
