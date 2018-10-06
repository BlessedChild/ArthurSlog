# Slog92_使用React框架进行前端开发4
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-92
* Year·1

* Guangzhou·China
* October 6th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [个人网站：http://www.arthurslog.com](http://www.arthurslog.com)

* [CSDN：https://blog.csdn.net/u010997452/article/list/1](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub：https://github.com/BlessedChild/ArthurSlog](https://github.com/BlessedChild/ArthurSlog)

* [NPM：https://www.npmjs.com/~arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金：https://juejin.im/user/59f2a424f265da432f305c66/posts](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书：https://www.jianshu.com/u/b9ebe10f0534](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault：https://segmentfault.com/u/arthurslog/articles](https://segmentfault.com/u/arthurslog/articles)

为无为 事无事 味无味

---

### 开发环境MacOS(Mojave 10.14 (18A391))

### 信息源

### 开始编码

* 目前属于使用react的初阶，先把基础页面弄好

* 再一步一步升级

* 今天完成了商城主页的布局设计

* 剩下的分为八个页面 进行原型设计之后继续开发

* 图片暂时先由普通div代替

* 下面上今天更新的代码：

Client/Header.jsx
``` js
import React, { Component } from 'react'

// Header区域的样式
const HeaderBarStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', position: 'fixed', marginTop: '10px', width: '100%', height: 88, backgroundColor: 'rgba(0,0,0,0)' }
const searchBarStyle = { position: 'relative', marginTop: 0, width: '100%', height: 88, backgroundColor: 'rgba(0,0,0,0)', width: '90%' }
const searchBarIconStyle = { position: 'absolute', left: '0px', width: '88px', height: '88px', backgroundColor: 'rgba(0,0,0,0.1)', textAlign: 'center', lineHeight: '88px', borderStyle: 'none', borderRadius: '50px' }
const searchStyle = { position: 'relative', marginTop: 0, backgroundColor: 'rgba(0,0,0,0.1)', width: '100%', height: '84px', fontSize: 40, textAlign: 'center', borderStyle: 'none', borderRadius: '50px', border: '1px solid #F2F2F2' }

// Header区域渲染的内容
class Header extends Component {
    render() {
        return <div style={HeaderBarStyle}>
                <div className='searchBar' style={searchBarStyle}>
                    <div style={searchBarIconStyle}>图片</div>
                    <input placeholder='请输入商品名称' style={searchStyle}></input>
                </div>
        </div>
    }
}

export default Header
```

Client/BodyContainer.jsx
``` js
import React, { Component } from 'react'

import IssueList from './IssueList'

// BodyContainet区域的样式
const bodyContainerBarStyle = { zIndex: -1, position: "relative", marginTop: 0, marginBottom: 128, height: '100%', width: '100%', fontSize: 40, textAlign: 'center' }
const carouselAreaStyle = { width: '100%', height: 375, fontSize: 40, textAlign: 'center', lineHeight: '375px' }
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
// BodyContainer区域渲染的内容
class BodyContainer extends Component {
    /*
    render() {
        return <div>
                <div>2. navigationBar（导航栏）</div>
                <div>2.1 所有商品|2.2 拼团|2.3 促销</div>
                <div>商品1|商品2|商品3</div>
                <div>商品4|商品5|商品6</div>
                <div>商品7|商品8|商品9</div>
                <IssueList />
            </div>
    }
    */
    render() {
        return <div className='bodyContainer' style={bodyContainerBarStyle}>
            <div>
                <div className='carouselArea' style={carouselAreaStyle}>carouselArea（轮播区域）</div>
                <div style={dividingLineStyle}></div>
                <div style={bulletinBoardStyle}>
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
const bottomTabBarItemStyle = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '1px', marginRight: '1px' }
const bottomTabBarItemStyleLeft = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '0.5px', marginRight: '1px' }
const bottomTabBarItemStyleRight = { alignItems: 'center', display: 'flex', flexDirection: 'column', backgroundColor: '#d8f0f3', color: '#000000', width: '33.3%', marginLeft: '1px', marginRight: '0.5px' }
const bottomTabBarItemImg = { height: '88px', width: '88px', textAlign: 'center', lineHeight: '88px', backgroundColor: '#FFFFFF' }
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
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>购物车</div>
                </div>
                <div style={bottomTabBarItemStyle}>
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>推广中心</div>
                </div>
                <div style={bottomTabBarItemStyleRight}>
                    <div style={bottomTabBarItemImg}>图片</div>
                    <div style={bottomTabBarItemText}>个人中心</div>
                </div>
            </div>
        </div>
    }
}

export default Bottom
```

* 上一张目前商城界面的图：

* ![ArthurSlogStore](https://github.com/BlessedChild/LogofAxu/blob/master/images/Slog92/Store_Index.png?raw=true)

* 至此，暂时完成了‘商城主页’的页面布局。

---

* 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* 如果你喜欢我的文章 欢迎点赞 留言

* 谢谢
