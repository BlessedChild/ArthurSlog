# Slog74_UI设计、整理和布局GET！（微信小程序之云开发-全栈时代5）

* ArthurSlog
* SLog-74
* Year·1

* Guangzhou·China
* September 16th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

常道无名 唯德以显之 至德无本 顺道而成之 祸福无门 惟人自召 善恶之报 如影随形

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [小程序官方文档](https://mp.weixin.qq.com/debug/wxadoc/dev/wxcloud/basis/getting-started.html)

* [小程序端API文档（客户端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/)

* [云端API文档（服务端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-server-api/)

### 前言

* 微信开发者工具版本： v 1.02.1809111

* ”云开发“ 封装好了一些常用的业务逻辑，提供了以下方面的相关API供开发者使用：

1. 云函数

2. 数据库

3. 存储管理 

### 开始编码

* 现在先把微信开发工具更新至最新（1.02.1809101），有部分开发人员在微信社区反馈更新之后没有看到“云开发”的按钮

* 解决办法：点击检查更新，等待更新完全完成之后重启开发工具

* 重点：云开发方式需要appid，请准备好

* 当前云开发模版的微信小程序文件结构如下：

``` txt
cloudfunctions
    | - login
          | - index.js
          | - package.json
          | - package-lock.json
          
    | - arthurSlog_getInfo
          | - index.js
          | - package.json
          | - package-lock.json

    | - arthurSlog_methodAdd
          | - index.js
          | - package.json
          | - package-lock.json
          
miniprogram
    | - images
           | - code-db-inc-dec.png
           | - code-db-onAdd.png
           | - code-db-onQuery.png
           | - code-db-onRemove.png
           | - code-func-sum.png
           | - console-entrance.png
           | - create-collection.png
    | - pages
           | - addFunction
                    | - addFunction.js
                    | - addFunction.json
                    | - addFunction.wxml
                    | - addFunction.wxss
           | - chooseLib
                    | - chooseLib.js
                    | - chooseLib.json
                    | - chooseLib.wxml
                    | - chooseLib.wsxx
           | - databaseGuide
                    | - databaseGuide.js
                    | - databaseGuide.json
                    | - databaseGuide.wxml
                    | - databaseGuide.wxss
           | - deployFunctions
                    | - deployFunctions.js
                    | - deployFunctions.json
                    | - deployFunctions.wxml
                    | - deployFunctions.wxss
           | - index
                    | - index.js
                    | - index.wxml
                    | - index.wxss
                    | - user-unlogin.png
           | - storageConsole
                    | - storageConsole.js
                    | - storageConsole.json
                    | - storageConsole.wxml
                    | - storageConsole.wxss
           | - userConsole
                    | - userConsole.js
                    | - userConsole.json
                    | - userConsole.wxml
                    | - userConsole.wxss
    | - style
           | - guide.wxss
    | - app.js
    | - app.json
    | - app.wxss

README.md
project.config.json
```

* 本次来整理一下界面的布局，首先在更新主页面代码如下：

Client：
miniprogram/pages/index/index.wxml
``` html
<!--index.wxml-->
<view class="container">

  <!-- 用户 openid -->
  <view class="userinfo">
    <button open-type="getUserInfo" bindgetuserinfo="onGetUserInfo" class="userinfo-avatar" style="background-image: url({{avatarUrl}})"></button>
  </view>

  <!-- 操作数据库 -->
  <view class="uploader">
    <navigator url="../databaseGuide/databaseGuide" open-type="navigate" class="uploader-text">
      <text>前端操作数据库</text>
    </navigator>
  </view>

  <!-- 获取 openid -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_getInfo">点击获取 openid</button>
  </view>
  <view class="showOpenid">
    <text class="textOpenid">openid：{{openid}}</text>
  </view>

  <!-- 返回两个对象之和 -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_methodAdd">点击返回两个对象之和</button>
  </view>
  <view class="showOpenid">
    <text class="textOpenid">8 + 8 = {{sumResult}}</text>
  </view>

  <!-- 上传图片 -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_uploadImg">上传图片</button>
  </view>
  <!-- 显示图片 -->
  <view>
    <image class="img" src="{{imagePath}}" mode="scaleToFill"></image>
  </view>

</view>
```

* 同时js文件如下，这跟vue是一样的，在data里添加对象供js和html做中介

* 不一样是vue，data里的对象是双向绑定的，对象变，html文件里的对象也会跟着变，页面跟着渲染

* 但在小程序里，你得使用 setdata函数来让页面重新渲染

* 完整代码如下：

Client：
miniprogram/pages/index/index.js
``` js
//index.js
const app = getApp()

Page({
  data: {
    avatarUrl: './user-unlogin.png',
    userInfo: {},
    logged: false,
    takeSession: false,
    requestResult: '',
    fileID: '',
    cloudPath: '',
    imagePath: './user-unlogin.png',
    openid:'',
    sumResult:'',
  },

  onLoad: function() {
    if (!wx.cloud) {
      wx.redirectTo({
        url: '../chooseLib/chooseLib',
      })
      return
    }

    // 获取用户信息
    wx.getSetting({
      success: res => {
        if (res.authSetting['scope.userInfo']) {
          // 已经授权，可以直接调用 getUserInfo 获取头像昵称，不会弹框
          wx.getUserInfo({
            success: res => {
              this.setData({
                avatarUrl: res.userInfo.avatarUrl,
                userInfo: res.userInfo
              })
            }
          })
        }
      }
    })
  },

  onGetUserInfo: function(e) {
    if (!this.logged && e.detail.userInfo) {
      this.setData({
        logged: true,
        avatarUrl: e.detail.userInfo.avatarUrl,
        userInfo: e.detail.userInfo
      })
    }
  },

  onGetOpenid: function() {
    // 调用云函数
    wx.cloud.callFunction({
      name: 'login',
      data: {},
      success: res => {
        console.log('[云函数] [login] user openid: ', res.result.openid)
        app.globalData.openid = res.result.openid
        wx.navigateTo({
          url: '../userConsole/userConsole',
        })
      },
      fail: err => {
        console.error('[云函数] [login] 调用失败', err)
        wx.navigateTo({
          url: '../deployFunctions/deployFunctions',
        })
      }
    })
  },

  // 上传图片
  doUpload: function() {
    // 选择图片
    wx.chooseImage({
      count: 1,
      sizeType: ['compressed'],
      sourceType: ['album', 'camera'],
      success: function(res) {

        wx.showLoading({
          title: '上传中',
        })

        const filePath = res.tempFilePaths[0]

        // 上传图片
        const cloudPath = 'my-image' + filePath.match(/\.[^.]+?$/)[0]
        wx.cloud.uploadFile({
          cloudPath,
          filePath,
          success: res => {
            console.log('[上传文件] 成功：', res)

            app.globalData.fileID = res.fileID
            app.globalData.cloudPath = cloudPath
            app.globalData.imagePath = filePath

            wx.navigateTo({
              url: '../storageConsole/storageConsole'
            })
          },
          fail: e => {
            console.error('[上传文件] 失败：', e)
            wx.showToast({
              icon: 'none',
              title: '上传失败',
            })
          },
          complete: () => {
            wx.hideLoading()
          }
        })

      },
      fail: e => {
        console.error(e)
      }
    })
  },
  // 添加前端代码，向后端服务发起 名为”arthurSlog_getInfo“方法的请求
  // 请求的结果会返回，并保存再 res对象中
  // 这里我们把结果在控制台打印出来
  // 返回appId 和 openId的数据，并保存在res对象中
  arthurSlog_getInfo: function() {
    const this_ = this
    wx.cloud.callFunction({
      name: 'arthurSlog_getInfo',
      complete: res => {
        console.log('callFunction test result: ', res)
        this_.setData({
          openid: res.result.openId
        })
      }
    })
  },
  // 添加前端代码，向后端服务发起 名为”arthurSlog_methodAdd“方法的请求
  // 请求的结果会返回，并保存再 res对象中
  // 这里我们把结果在控制台打印出来
  // 返回appId 和 openId的数据，并保存在res对象中
  arthurSlog_methodAdd: function() {
    const this_ = this
    wx.cloud.callFunction({
        // 云函数名称
        name: 'arthurSlog_methodAdd',
        // 传给云函数的参数
        data: {
          a: 8,
          b: 8,
        },
      })
      .then(res => {
        console.log(res.result)
        this_.setData({
          sumResult: res.result.sum
        })
      })
      .catch(console.error)
  },

  // 添加前端代码,向云端上传图片
  arthurSlog_uploadImg: function () {
    // 选择图片
    const this_ = this
    wx.chooseImage({
      count: 1,
      sizeType: ['original', 'compressed'],
      sourceType: ['album', 'camera'],
      success(res) {
        // tempFilePath可以作为img标签的src属性显示图片
        const tempFilePaths = res.tempFilePaths

        wx.showLoading({
          title: '上传中',
        })

        this_.setData({
          imagePath: tempFilePaths[0],
        })

        console.log(tempFilePaths[0])

        const filePath = tempFilePaths[0]
        const cloudPath = 'ArthurSlog' + filePath.match(/\.[^.]+?$/)[0]
        wx.cloud.uploadFile({
          cloudPath,
          filePath, // 小程序临时文件路径
        }).then(res => {
          // get resource ID
          console.log(res.fileID) //success返回的fileID值    
          console.log(res.statusCode) //success返回的statusCode值
        }).catch(error => {
          // handle error
          console.error('[上传文件] 失败：', error)
          wx.showToast({
            icon: 'none',
            title: '上传失败',
          })
        }).then(() => {
          wx.hideLoading()
        })
      }
    })
  },
})
```

* 代码的解析，请查看注释，应该都不会太难理解的

* 如果有任何问题，欢迎大家留言交流

* 页面的样式，在wxss文件里添加对字体的设置：

Client：
miniprogram/pages/index/index.wxss
``` css
.textOpenid{
  font-size:24rpx;
  word-break: break-all;
}
```

* 现在，请保存好更新过代码的文件

* 接着，在模拟器里对各个按钮进行测试

1. 点击“点击获取openid”，会在下方得到你的 openid

2. 点击“返回两个对象之和”，会在下方得到对象的和

3. 点击“上传图片”，选择图片并“打开后”，图片会上传至云端，同时在页面上显示出来

* 至此，我们对页面进行了一个简单的整理和布局。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
