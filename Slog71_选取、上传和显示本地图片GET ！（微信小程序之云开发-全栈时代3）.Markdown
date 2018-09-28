# Slog71_选取、上传和显示本地图片GET ！（微信小程序之云开发-全栈时代3）
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-71
* Year·1

* Guangzhou·China
* Sep 12th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

道常无为而无不为

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [小程序官方文档](https://mp.weixin.qq.com/debug/wxadoc/dev/wxcloud/basis/getting-started.html)

* [小程序端API文档（客户端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/)

* [云端API文档（服务端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-server-api/)

### 前言

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

* 在使用“云开发”的时候，需要先调用 初始化函数 init

* 小程序端的初始化函数是 wx.cloud.init()

* 云端的初始化函数是 const cloud = require('wx-server-sdk') cloud.init())

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

* 这里提醒一下，就是 cloudfunctions 路径下的文件的名称，就是云端向小程序端提供的方法

* 举个栗子：对于cloudfunctions/arthurSlog_getInfo来说，arthurSlog_getInfo这个文件夹的名字就是云端向小程序端提供的方法

* 现在在小程序端就可以参考[小程序端API文档（客户端）](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/)

* 大部分函数都来源于 对象“wx”，这个 “wx”对象 就类似于服务端的 “wx-server-sdk”对象

* 比如，在小程序端（客户端）有 wx.cloud.callFunction（）、wx.cloud.uploadFile（）等方法

* 再比如，在云端（服务端）有 cloud.init()、cloud.database()、cloud.collection（）等方法

* 现在，我们来接触一下 “小程序·云开发” 的 “存储管理功能”

* 打开小程序端的 miniprogram/pages/index/index.js

Client
miniprogram/pages/index/index.js
``` js
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
  },

  // ...
  // ...
  // ...

  // 添加前端代码,向云端上传图片
  arthurSlog_uploadImg: function() {
    // 选择图片
    const this_ = this
    wx.chooseImage({
      count: 1,
      sizeType: ['original', 'compressed'],
      sourceType: ['album', 'camera'],
      success(res) {
        // tempFilePath可以作为img标签的src属性显示图片
        const tempFilePaths = res.tempFilePaths

        this_.setData({
          imagePath: tempFilePaths[0],
        })

        console.log(tempFilePaths[0])
      }
    })
  },
})
```

* 在这里，我们定义了一个方法arthurSlog_uploadImg，参考 [小程序官方文档](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/storage/uploadFile.html)

* 首先将当前环境对象 映射 给对象 this_

Client
miniprogram/pages/index/index.js
``` js
const this_ = this
```

* 使用 wx.chooseImage 方法，打开本地文件，选择要上传的文件

* 在success函数里，使用setdata函数，更新 imagePath 对象的值，并使得页面上对应的部分重新渲染

* 现在，我们来更新页面文件：

Client
miniprogram/pages/index/index.wxml
``` html
<!--index.wxml-->
<view class="container">

  <!-- ... -->

  <!-- 获取 openid -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_getInfo">点击获取 openid</button>
  </view>

  <!-- 返回两个对象之和 -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_methodAdd">点击返回两个对象之和</button>
  </view>

  <!-- 上传图片 -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSLog_uploadImg">上传图片</button>
  </view>
  <!-- 显示图片 -->
  <view>
    <image class="img" src="{{imagePath}}" mode="scaleToFill"></image>
  </view>

</view>
```

* 这次使用的方法，不需要自己编写云端服务代码，腾讯公司已经提供了

* 保存文件，在模拟器中点击上传图片（我放了一张演示图片在此路径下：miniprogram/images/ArthurSlog.png）

* 选中要上传的文件，点击“打开”

* 正常执行之下，会显示出我们刚刚上传的图片，到这里暂停一下，现在图片还没发送出去

* 在下一篇中，再继续补充

* 至此，我们实现了一个选取本地文件，并显示选中的图片文件。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
