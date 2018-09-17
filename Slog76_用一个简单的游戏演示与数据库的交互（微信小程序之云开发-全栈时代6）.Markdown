# Slog76_用一个简单的游戏演示与数据库的交互（微信小程序之云开发-全栈时代6）

* ArthurSlog
* SLog-76
* Year·1

* Guangzhou·China
* September 17th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

甚爱必大费 多藏必厚亡 故知足不辱 知止不殆 可以长久

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

* 本次来玩一下数据库，首先在更新主页面代码如下：

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
    <button class="userinfo-nickname" bindtap="arthurSlog_readingBook">我要读书（每次加1点智力值）</button>
  </view>
  <view class="showOpenid">
    <text class="textOpenid" wx:if="{{user_dbFlag}}">{{user_nickName}} 的IQ值：{{page_iq}}</text>
  </view>

  <!-- 获取 openid -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_getInfo">点击获取 openid</button>
  </view>
  <view class="showOpenid">
    <text class="textOpenid" wx:if="{{openid}}">openid：{{openid}}</text>
  </view>

  <!-- 返回两个对象之和 -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_methodAdd">点击返回两个对象之和</button>
  </view>
  <view class="showOpenid">
    <text class="textOpenid" wx:if="{{sumResult}}">8 + 8 = {{sumResult}}</text>
  </view>

  <!-- 上传图片 -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_uploadImg">上传图片</button>
  </view>
  <!-- 显示图片 -->
  <view>
    <image class="img" wx:if="{{imagePath}}" src="{{imagePath}}" mode="aspectFit"></image>
  </view>

</view>
```

* 可以看到，这次把一些对象的名称进行了更新，以便简洁

* 来看一下 js文件里 与页面交互的所有对象

Client： miniprogram/pages/index/index.js
``` js
data: {
  avatarUrl: './user-unlogin.png',
  userInfo: {},   // 用户信息
  logged: false,  // 用来判断用户是否已经授权过了
  cloudPath: '',  // 云端存放文件的路径
  imagePath: '',  // 本地图片文件的路径
  openid: '',
  sumResult: '',  // 云端求和的结果
  page_iq: '',    // 页面上显示的iq值
  user_nickName: '',  // 微信名
  user_dbFlag: false, // 判断标志：判断用户在云端数据库是否存在数据
}
```

* 之前，我们一共写了三个新函数：

1. arthurSlog_getInfo （获取用户 appId 和 openId的数据）

2. arthurSlog_methodAdd （获取两个数相加的和）

3. arthurSlog_uploadImg （向云端上传图片，并在本地显示出来）

* 此次，要编写一个新的函数 arthurSlog_readingBook

* 同时，拓展 onLoad 和 onGetUserInfo 这两个函数

* 先来看新函数 arthurSlog_readingBook：

Client： miniprogram/pages/index/index.js
``` js
arthurSlog_readingBook: function() {
  const this_ = this
  // 验证是否已经授权
  if (app.globalData.logged) {
    // 验证云端是否存在用户数据
    const db = wx.cloud.database()
    const _ = db.command
    // 读取用户数据，并渲染在页面上
    db.collection('Users').where({
      _openid: _.eq(app.globalData.openid) // 填入当前用户 openid
    }).get().then(res => {
      console.log("查询数据库")
      if (!res.data) {
        console.log("云端数据库没有返回数据")
        console.log("用户在数据库没有数据，现在为用户创建数据库")
        // 创建用户数据
        db.collection('Users').add({
            // data 字段表示需新增的 JSON 数据
            data: {
              userName: app.globalData.user_nickName,
              userDate: db.serverDate(),
              IQ: '10'
            }
          })
          .then(res => {
            console.log("用户数据创建成功")
            console.log(res)
          }).catch(console.error)

        app.globalData.user_dbFlag = true
      } else if (res.data) {
        console.log("云端数据库成功返回数据")
        console.log('更新数据库')
        console.log('当前的全局_id值是： ' + app.globalData._id)
        app.globalData.IQ = res.data[0].IQ
        // 如果该用户有数据
        // 页面上IQ的值加1
        // 数据库IQ的值加1
        db.collection('Users').doc(app.globalData.id).update({
          data: {
            IQ: _.inc(1)
          }
        }).then(res => {
          console.log('成功更新数据库')
          console.log(res)
          this_.setData({
            page_iq: ++app.globalData.IQ
          })
        })
      }
    })
  } else if (!app.globalData.logged) {
    // 弹出提示框，显示“请点击头像授权”
    wx.showToast({
      icon: 'none',
      title: '请先点击左上角允许授权',
    })
  }
}
```

* 上面的代码，实现了每次点击 “我要读书” 按钮之后，iq值自增1（也就是每点一次按钮qi加1）

* 怎么实现的，看一下代码可知：

1. 当用户点击 “我要学习” 按钮的时候，判断用户是否已经授权？

2. 已经授权 => 向云端数据库获取用户数据； 未授权 => 弹出提示框，提示用户点击左上角授权

3. 判断获取的数据库是否返回数据？

4. 成功返回不为空的数据 => 把获取到的数据（iq值）更新至页面，然后更新数据库的值（数据库的iq值自增1）; 成功返回为空的数据 => 为用户创建数据，然后更新前端的iq值

* 基本步骤如上，其中1、2步是 arthurSlog_readingBook函数执行的

* 而步骤3、4中，步骤3 有一个需要点击授权的环节，这由 onGetUserInfo函数来负责：

Client： miniprogram/pages/index/index.js
``` js
// 点击弹出“微信授权” 窗口
// 用户点击“允许”，允许开发者获得用户的公开信息（昵称、头像等）
onGetUserInfo: function(e) {
  const this_ = this
  if (!this.logged && e.detail.userInfo) {
    this.setData({
      logged: true,
      avatarUrl: e.detail.userInfo.avatarUrl,
      userInfo: e.detail.userInfo,
      user_nickName: e.detail.userInfo.nickName
    })
    app.globalData.openid = e.detail.userInfo.openId
    // 需要先获得用户信息才能查询数据库
    // 验证云端是否存在用户数据
    const db = wx.cloud.database()
    // 读取用户数据，并渲染在页面上
    db.collection('Users').where({
      _openid: app.globalData.openid // 填入当前用户 openid
    }).get().then(res => {
      if (res.data[0] != null) {
        // 如果用户存在数据
        // 拉取用户的IQ数据
        this_.setData({
          page_iq: res.data[0].IQ,
          user_dbFlag: true
        })
      } else {
        // 创建用户数据
        db.collection('Users').add({
            // data 字段表示需新增的 JSON 数据
            data: {
              userName: app.globalData.user_nickName,
              userDate: db.serverDate(),
              IQ: 10,
              id: app.globalData.openid
            }
          })
          .then(res => {
            this_.setData({
              page_iq: '10',
              user_dbFlag: true
            })
            // 添加新表成功之后，打印数据库的新用户信息
            console.log(res)
            app.globalData._id = res._id
          })

        this_.setData({
          user_dbFlag: true
        })
      }
    })
    app.globalData.logged = true
  }
}
```

* 因为授权之后重新打开小程序，不需要再授权

* 所以，在这里，需要拓展一下 onload函数

* 这样，在打开小程序的时候，客户端自动向云端数据库获取用户数据（iq的值）

* 然后，将获取到的iq值 更新值页面：

Client： miniprogram/pages/index/index.js
``` js
// 小程序页面打开时，默认执行的函数
onLoad: function() {
  if (!wx.cloud) {
    wx.redirectTo({
      url: '../chooseLib/chooseLib',
    })
    return
  }

  const this_ = this
  // 获取用户信息
  wx.getSetting({
    success: res => {
      if (res.authSetting['scope.userInfo']) {
        // 已经授权，可以直接调用 getUserInfo 获取头像昵称，不会弹框
        wx.getUserInfo({
          success: res => {
            this.setData({
              avatarUrl: res.userInfo.avatarUrl,
              userInfo: res.userInfo,
              user_nickName: res.userInfo.nickName,
              logged: true,
              user_dbFlag: true
            })
            app.globalData.logged = true
            app.globalData.user_dbFlag = true
            app.globalData.openid = res.userInfo.openid

            const db = wx.cloud.database()
            const _ = db.command
            // 读取用户数据，并渲染在页面上
            db.collection('Users').where({
              _openid: _.eq(app.globalData.openid) // 填入当前用户 openid
            }).get().then(res => {
              console.log(res.data)
              if (res.data != null) {
                // 如果用户存在数据
                // 拉取用户的IQ数据
                this_.setData({
                  page_iq: res.data[0].IQ,
                  user_dbFlag: true
                })
              } else {
                console.log("拉取云端数据出错")
              }
            })
          }
        })
      }
    }
  })
}
```

* 现在，请保存好更新过代码的文件

* 接着，在模拟器里对各个按钮进行测试

1. 点击“我要读书”，会弹出窗口提示你“请先点击左上角进行授权”

2. 点击“左上角”，点击”允许“授权，现在会在“我要读书”按钮的下方出现“XXX的IQ值：10”

3. 已经允许授权之后，点击“我要读书”，每点击一次，下方出现的IQ值会加1

4. 点击“点击获取openid”，会在下方得到你的 openid

5. 点击“返回两个对象之和”，会在下方得到对象的和

6. 点击“上传图片”，选择图片并“打开后”，图片会上传至云端，同时在页面上显示出来

* 至此，我们使用小程序云开发实现了小程序端和云端数据库的交互。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
