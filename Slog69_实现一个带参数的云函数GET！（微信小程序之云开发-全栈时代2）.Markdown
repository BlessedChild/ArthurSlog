# Slog69_实现一个带参数的云函数GET！（微信小程序之云开发-全栈时代2）
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-69
* Year·1

* Guangzhou·China
* Sep 11th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

祸兮福之所倚 福兮祸之所伏

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [小程序官方文档](https://mp.weixin.qq.com/debug/wxadoc/dev/wxcloud/basis/getting-started.html)

* [小程序端API文档（客户端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/)

* [云端API文档（服务端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-server-api/)

### 前言

* 腾讯推出“云开发”概念，简单说，就是为开发者提供搭建好的服务器，服务器使用npm安装好了“wx-server-sdk”模块

* 腾讯就是把业务包装在模块里，然后在自己的平台提供的 API，供开发人员调用

* 开发人员可以借助平台进行核心业务开发，实现快速上线和迭代

* 云开发方式，可以和开发者已经使用的云服务相互并存

* ”云开发“ 提供三大基础能力：

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

* 在使用“云开发”的时候，一定要记得最先调用 初始化函数 init，小程序端和云端都需要 初始化函数

Client：
miniprogram/app.js
``` js
//app.js
App({
  onLaunch: function () {
    
    if (!wx.cloud) {
      console.error('请使用 2.2.3 或以上的基础库以使用云能力')
    } else {
      wx.cloud.init({
        env: 'arthurslog-test-d4537a',
        traceUser: true,
      })
    }

    this.globalData = {}
  }
})
```

Server:
cloudfunctions/arthurSlog_getInfo/index.js
``` js
// 云函数入口文件
const cloud = require('wx-server-sdk')

cloud.init()

// 云函数入口函数
exports.main = async(event, context) => {
  return event.userInfo
}
```

* 上面的Server端代码中

Server:
cloudfunctions/arthurSlog_getInfo/index.js
``` js
// 云函数入口文件
//const cloud = require('wx-server-sdk')

//cloud.init()

// 云函数入口函数
exports.main = async(event, context) => {
  return event.userInfo
}
```

* 没有调用到 “wx-server-sdk” 的方法，所以可以注释掉，不影响结果

* 这里提醒一下，就是 cloudfunctions 路径下的文件名称，就是云端向小程序端提供的方法

* 举个栗子 cloudfunctions/arthurSlog_getInfo，arthurSlog_getInfo这个文件夹的名字就是云端向小程序端提供的方法

* 现在在小程序端就可以参考[小程序端API文档（客户端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/)

* 大部分函数都来源于 对象“wx”，这个 “wx”对象 就类似于服务端的 “wx-server-sdk”对象

* 这两个对象都包含了腾讯公司封装好的属性和方法

* 让我们来回顾一下之前的项目文件

Client
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
    requestResult: ''
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
  // 这里我们把结果再控制台打印出来
  // 返回appId 和 openId的数据，并保存在res对象中
  arthurSlog_getInfo: function() {
    wx.cloud.callFunction({
      name: 'arthurSlog_getInfo',
      complete: res => {
        console.log('callFunction test result: ', res)
      }
    })
  },
})
```

* 定位到我们添加的方法区域：

Client
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
    requestResult: ''
  },
  // 添加前端代码，向后端服务发起 名为”arthurSlog_getInfo“方法的请求
  // 请求的结果会返回，并保存再 res对象中
  // 这里我们把结果再控制台打印出来
  // 返回appId 和 openId的数据，并保存在res对象中
  arthurSlog_getInfo: function() {
    wx.cloud.callFunction({
      name: 'arthurSlog_getInfo',
      complete: res => {
        console.log('callFunction test result: ', res)
      }
    })
  },
})
```

* 其中，我们就调用了用了 “wx”对象 的方法，wx.cloud.callFunction()

* 这个方法会让小程序端向云端发送请求，请求的方法名称是 arthurSlog_getInfo（name参数）

* 同时等待服务端的返回的数据，返回的数据保存在res对象中

* 我们再来看云端的代码文件，云函数的传入参数有两个，一个是 event 对象，一个是 context 对象。

Server:
cloudfunctions/arthurSlog_getInfo/index.js
``` js
// 云函数入口文件
//const cloud = require('wx-server-sdk')

//cloud.init()

// 云函数入口函数
exports.main = async(event, context) => {
  return event.userInfo
}
```

* event 指的是触发云函数的事件，当小程序端调用云函数时，

* event 就是小程序端调用云函数时传入的参数，外加后端自动注入的小程序用户的 openid 和小程序的 appid

* context 对象包含了此处调用的调用信息和运行状态，可以用它来了解服务运行的情况

* 现在，我们在小程序端写一个带数据（带参数）的方法，把数据传给云端（服务端），然后小程序端接收返回的数据

* 首先编写客户端代码

Client
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
    requestResult: ''
  },

  //
  //...省略中间的代码.........
  //

  // 添加前端代码，向后端服务发起 名为”arthurSlog_methodAdd“方法的请求
  // 请求的结果会返回，并保存再 res对象中
  // 这里我们把结果在控制台打印出来
  // 返回appId 和 openId的数据，并保存在res对象中
  arthurSlog_methodAdd: function() {
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
      })
      .catch(console.error)
  },
})
```

* 在小程序端：我们创建了一个新的方法，方法名为 “arthurSlog_methodAdd”，传送的云端的数据是 data对象，data对象里面包含了两个对象，a对象和b对象的值都是8

* 现在，我们来创建一个新的服务端方法，同时编写新方法的代码文件：

* 右键 cloudfunctions文件夹，点击“新建node.js云函数”，函数名为 arthurSlog_methodAdd

* 提示安装本地依赖，确定

Server
cloudfunctions/arthurSlog_methodAdd/index.js
``` js
// 云函数入口文件
const cloud = require('wx-server-sdk')

cloud.init()

// 云函数入口函数
// event中包含了来自小程序端的“data对象”的数据
// data对象中有 a对象和 b对象，两个对象的值都为8
// 返回一个sum对象给小程序端，返回的对象就是来自小程序端的两个对象a和b的和
// 返回的数据将会保存在小程序端的res.result对象内
exports.main = async(event, context) => {
  return {
    sum: event.a + event.b
  }
}
```

* ok，现在，右键 arthurSlog_methodAdd 文件夹，点击“上传并部署“

* 现在小程序端和云端的对接准备已经做好了，我们还需要一个交互页面

Client
miniprogram/pages/index/index.wxml
``` html
!--index.wxml-->
<view class="container">

  <!-- 用户 openid -->
  <view class="userinfo">
    <button open-type="getUserInfo" bindgetuserinfo="onGetUserInfo" class="userinfo-avatar" style="background-image: url({{avatarUrl}})"></button>
    <view>
      <button class="userinfo-nickname" bindtap="onGetOpenid">点击获取 openid</button>
    </view>
  </view>


  <!-- 上传图片 -->
  <view class="uploader">
    <view class="uploader-text" bindtap="doUpload">
      <text>上传图片</text>
    </view>
    <view class="uploader-container" wx:if="{{imgUrl}}">
      <image class="uploader-image" src="{{imgUrl}}" mode="aspectFit" bindtap="previewImg"></image>
    </view>
  </view>


  <!-- 操作数据库 -->
  <view class="uploader">
    <navigator url="../databaseGuide/databaseGuide" open-type="navigate" class="uploader-text">
      <text>前端操作数据库</text>
    </navigator>
  </view>

  <!-- 新建云函数 -->
  <view class="uploader">
    <navigator url="../addFunction/addFunction" open-type="navigate" class="uploader-text">
      <text>快速新建云函数</text>
    </navigator>
  </view>

  <!-- 获取 openid -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_getInfo">点击获取 openid</button>
  </view>

  <!-- 返回两个对象之和 -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_methodAdd">点击返回两个对象之和</button>
  </view>

</view>
```

* ok，差不多要大功告成了

* 在页面上添加了“点击返回两个对象之和”按钮，并绑定“arthurSlog_methodAdd”函数之后，保存好文件

* 在模拟器中点击“点击返回两个对象之和”的按钮，观察Console控制台会打印如下内容：

``` txt
{sum: 16}
```

* ok，一个能携带数据给云端（服务端），的小程序端的方法就完成并正常工作了

* 至此，我们实现了一个带参数的小程序端方法，和一个能接受前端参数的云端（服务端）的方法，让他们成功实现了对接并正常工作。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
