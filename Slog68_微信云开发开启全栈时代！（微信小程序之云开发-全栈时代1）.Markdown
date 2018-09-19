# Slog68_微信云开发开启全栈时代！（微信小程序之云开发-全栈时代1）

* ArthurSlog
* SLog-68
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

常道无名 唯德以显之 至德无本 顺道而成之 祸福无门 惟人自召 善恶之报 如影随形

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [小程序官方文档](https://mp.weixin.qq.com/debug/wxadoc/dev/wxcloud/basis/getting-started.html)

### 开始编码

* 腾讯推出“云开发”概念，简单说，就是为开发者提供搭建好的服务器，服务器使用npm安装好了“wx-server-sdk”模块

* 腾讯就是把业务包装在模块里，然后在自己的平台提供的 API，供开发人员调用

* 开发人员可以借助平台进行核心业务开发，实现快速上线和迭代

* 云开发方式，可以和开发者已经使用的云服务相互并存

* 现在先把微信开发工具更新至最新（1.02.1809101）

* 云开发方式，需要appid，请准备好

* 新建一个小程序项目，选择“建立云开发快速启动模版”

* 项目建立之后，文件结构如下：

``` txt
cloudfunctions
    | - login

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

* 现在，在开发者工具工具栏左侧，点击 “云开发” 按钮可开通云开发

* 开发环境命名目前不可更改！

* 一个账户可以创建两个环境，创建一个作为测试环境，命名为test，然后平台会给你生成一个环境ID，类似这个样子test-3gh3g12

* 然后在再创建一个生产环境produce

* 点击右上角可以切换开发环境，现在切换回test

* 回到开发界面，右击cloudfunctions路径下的login文件夹，选择上传并部署

* 等待上传成功之后，打开miniprogram路径下的app.js文件，对这个文件进行更新

* 更新之前，先点击微信开发工具的左上角的“云开发”，然后，在云开发界面的左上角找到“环境ID”，复制“环境ID”

* 接下来更新代码：

miniprogram/app.js
``` js
//app.js
App({
  onLaunch: function () {
    
    if (!wx.cloud) {
      console.error('请使用 2.2.3 或以上的基础库以使用云能力')
    } else {
      wx.cloud.init({
        env: 'test-dxx7x',
        traceUser: true,
      })
    }

    this.globalData = {}
  }
})
```

* 添加环境变量 env: 'test-dxx7x'

* 保存修改

* 在模拟器中点击“点击获取openid”

* 在Console控制台里可以看到

``` txt
[云函数] [login] user openid:  o8xxf0Sxxxfdsfdfsdf342
```

* ok,已经实现了简单的一个前后交互逻辑

* 打开微信开发工具的左上角的“云开发”，点击“云函数”

* 可以看到我们的login函数已经出现了，在“函数名称”栏中点击login，可以看到login函数的三大参数：

1. 函数配置

2. 日志

3. 监控

* 其中日志记录就可以当作是后端服务器的控制台了，相关的调用时间和记录都可以差的到

* 还有比较实用的日志筛选功能

* 现在点击左上角的“测试”按钮，可以对函数进行测试

* 点击“运行测试”

* 测试结果：失败

* 查看日志，如下：

``` txt
TypeError: Cannot read property 'openId' of undefined
    at EventHandler.exports.main [as realHandler] (/var/user/index.js:21:28)
    at EventHandler.handle (/var/runtime/node8/bootstrap.js:238:34)
    at invoke (/var/runtime/node8/bootstrap.js:111:22)
    at Timeout.setTimeout [as _onTimeout] (/var/runtime/node8/bootstrap.js:61:9)
    at ontimeout (timers.js:475:11)
    at tryOnTimeout (timers.js:310:5)
    at Timer.listOnTimeout (timers.js:270:5)
```

* 我们点击左上角的“用户管理”，点击右上角的“复制openid“

* 然后我们返回云函数，点击左边的“login”函数，再重新点击右边的“测试”按钮来测试函数

* 双击“openId”右边的值，右键粘贴我们刚刚复制的openID

* 现在点击“运行测试”，结果是

* 测试结果：成功

* 报错消失

* 接下来

* 我们来自己编写一个云服务（后端服务）

* 回到微信开发工具，右键点击cloudfunctions文件夹，点击“新建node.js云函数”，并命名为 "arthurSlog_getInfo"

* 开发工具会在cloudfunctions路径下创建一个 arthurSlog_getInfo 文件夹，文件结构如下：

cloudfunctions/arthurSlog_getInfo
``` txt
cloudfunctions
      | - arthurSlog_getInfo
                 | - index.js
                 | - package.json
                 | - package-lock.json
```

* 这个文件是要放在服务器上，为我们的前端提供服务的

* 这个文件会提供一个“接口”供前后端交互

* 其中package.json文件里，包含了index.js代码的依赖关系

* 简单点说，index.js 里面会引用到 wx-server-sdk这个模块的方法

* 而这些引用的关系，就记录再package.json文件里面

* 我们可以看一下package.json文件里的代码：

cloudfunctions/arthurSlog_getInfo/package.json
``` json
{
  "name": "arthurSlog_getInfo",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "wx-server-sdk": "latest"
  }
}
```

* package.json 是一份配置文件，只用来指导 npm工具做事的方案

* npm工具，是nodejs语言的一个包管理工具，更多的使用方式 参考 [npm官方手册](https://www.npmjs.com/)

* 在我的 Slog57 和 Slog58两篇文章中，介绍了npm的使用和npm package（npm包）的制作、发布和更新

* 感兴趣的可以去翻阅一下

* 好了，回过头来，我们看回来微信“云开发”

* 让我们来打开刚刚创建的 arthurSlog_getInfo路径下的 index.js文件

* 同时添加代码：

cloudfunctions/arthurSlog_getInfo/index.js
``` js
// 云函数入口文件
const cloud = require('wx-server-sdk') //引入腾讯封装好的业务 API

cloud.init() //初始化

// 云函数入口函数
// 导出函数（服务），供前端访问，函数名为 arthurSlog_getInfo
exports.main = async(event, context) => {
  return event.userInfo
}
```

* 编写完成之后，右键arthurSlog_getInfo文件夹，点击“上传并部署”

* 因为云函数中使用 wx-server-sdk 需在对应云函数目录下安装 wx-server-sdk 依赖

* 参考 [微信官方说明](https://mp.weixin.qq.com/debug/wxadoc/dev/wxcloud/guide/functions/wx-server-sdk.html)

* 在创建云函数时会在云函数目录下默认新建一个 package.json 并提示用户是否立即本地安装依赖

* 请注意云函数的运行环境是 Node.js，因此在本地安装依赖时务必保证已安装 Node.js，同时 node 和 npm 都在环境变量中

* 如不本地安装依赖，可以用命令行在该目录下运行：

> npm install --save wx-server-sdk@latest

* ok，现在我们打开 miniprogram/pages/index/index.js 文件：

* 并添加前端代码：（用于向后端发起请求服务）

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

* 然后，再打开 miniprogram/pages/index/index.wxml 文件

* 并添加页面代码，在页面上新建一个 button 组件与js里的方法 “arthurSlog_getInfo”绑定在一起

* 当点击按钮的时候，调用函数“arthurSlog_getInfo”，像云服务（后端）发起请求

miniprogram/pages/index/index.wxml
``` html
<!--index.wxml-->
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

  <!-- 新建云函数 -->
  <!-- fun:  -->
  <view class="uploader">
    <button class="userinfo-nickname" bindtap="arthurSlog_getInfo">点击向云端发起请求</button>
  </view>

</view>
```

* 保存，在模拟器中，点击“点击向云端发起请求”按钮

* 观察控制台打印的信息：

``` txt
callFunction test result:  {errMsg: "cloud.callFunction:ok", result: {…}}
```

* 点击展开 {errMsg 左边的小箭头展开：

``` txt
errMsg
:
"cloud.callFunction:ok"
result
:
{appId: "*****wd1**14*****", openId: "o5***4******N****"}
__proto__
:
Object
```

* 可以看到云端服务返回的 appId 和 openId数据

* 至此，我们对微信“云开发”有了基础的了解和使用。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
