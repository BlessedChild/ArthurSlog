# Slog72_微信小程序之云开发-全栈时代4

* ArthurSlog
* SLog-72
* Year·1

* Guangzhou·China
* Sep 13th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

临河而羡鱼 不如归家织网

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

* 参考 

1. [微信小程序官方文档 -- chooseImage](https://developers.weixin.qq.com/miniprogram/dev/api/media/image/wx.chooseImage.html)

2. [小程序·云开发官方文档 -- wx.cloud.uploadFile](https://developers.weixin.qq.com/miniprogram/dev/wxcloud/reference-client-api/storage/uploadFile.html)

* 本次添加图片上传功能，完整代码如下：

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
        }).then( () => {
            wx.hideLoading()
        })
      }
    })
  },
})
```

* 这里分析一下

* 其实整个操作流程主要分两步，也就是这里使用了两个功能函数的原因

* 首先，用户点击上传按钮，这会出发DOM事件，打开一个窗口供用户进行文件的选择 => 这一步“锁定”文件

* 其次，当学好文件，点击“打开的时候”，客户端首先对文件进行读取，并发送至云端 => 这一步“上传”文件

* 整个过程简单说的话，上面两步可以概括

* 但实际上，在线上使用的时候，往往会有很多意想不到的问题，举个栗子：

1. 上传的文件过大，比如一个1G的图片？

2. 文件在上传之前要加载进内存中，这个过程如果出错怎么解决？

3. 如何判断服务端已经完整接收了小程序端的文件...

4. 以上是比较常见的，事实上还有更多的东西需要考虑....

* 好在，腾讯公司已经把很多细节上的东西帮我们做好了

* 我们只管用，然后提BUG给他们的开发人员 ^ ^

* 在这份代码里，使用了 wx.showLoading() 和 wx.hideLoading() 这两个函数

* 可能你会经常听到“生命周期”这种字眼

* 显然，我们希望在上传文件的时候出现“上传中”的提示，而在确认上传完毕之后关闭“上传中”的提示

* wx.showLoading() 在这里就是一个弹出框，而 wx.hideLoading()就是关闭这个弹出框

* 当上传过程出错的时候，这里使用了 wx.showToast() 来显示消息提示框，提示用户上传失败

* 这里还需要注意一点，就是：

Client：
miniprogram/pages/index/index.js
``` js
const this_ = this
```

* 需要在方法外部，先把当前的环境对象赋给一个新对象

* 然后，再在函数体里执行

Client：
miniprogram/pages/index/index.js
``` js
this_.setData({
  imagePath: tempFilePaths[0],
})
```

* 现在，请保存好更新过代码的文件

* 接着，点击模拟器里的“上传图片”按钮

* 选择样例图片（图片路径在miniprogram/images/ArthurSlog.png），完整代码已经上传至Github: [https://github.com/BlessedChild/ArthurSlog_WeiXinCloudDevelopment]((BlessedChild/ArthurSlog_WeiXinCloudDevelopment))

* 然后点击“打开”

* 这时应该就会弹出一个 “上传中” 的提示框，上传完成之后，提示框才会消失

* 此时，控制台会打印类似下面的信息

``` txt
http://tmp/sadsdasdasdas.dfsdfsdf.fsdfasdfas.png
index.js? [sm]:183 cloud://fdsf-tefsdfsst-d4gfdgd537a.6fsdc7e-fsasd-test-fsd/ArthurSlog.png
index.js? [sm]:184 200
```

* 第一行是小程序临时文件路径

* 第二行是fileID的值

* 第三行是statusCode（状态码）

* 至此，我们实现了一个选取本地文件，并上传至小程序云端，最后在客户端显示上传的图片文件的功能。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
