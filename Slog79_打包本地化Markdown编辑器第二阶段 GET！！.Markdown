# Slog79_打包本地化Markdown编辑器第二阶段 GET！！
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-79
* Year·1

* Guangzhou·China
* September 20th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [MSDN: ArthurSlog](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

柔弱胜刚强 鱼不可脱于渊 国之利器不可以示人

---

### 开发环境MacOS(High Sierra 10.13.6 (17G65))

#### 需要的信息和信息源：

* [Electron](https://electronjs.org/docs)

* [ArthurSlogMarkdownEditor 的 Github地址](https://github.com/BlessedChild/ArthurSlogMarkdownEditor)

### 开始编码

* 上一篇是把ArthurSlog.com网站上的Markdown编辑器本地化了

* 本次来打包本地化的 ArthurSlogMarkdownEditor

* 打包完之后，就可以直接双击启动了，不需要再敲命令行来启动

* 本次使用的打包工具是 [electron-packager](https://github.com/electron-userland/electron-packager)

* 让我们切换至工程目录下

> cd ~/Desktop/ArthurSlogMarkdownEditor/

> sudo npm i electron-packager --save-dev

> sudo npm install electron-packager -g

* 更新一下 package.json

~/Desktop/ArthurSlogMarkdownEditor/package.json
``` json
{
  "name": "ArthurSlogBrowser_Nodejs",
  "productName": "ArthurSlogMarkdownEditor",
  "version": "0.1.0",
  "description": "This is a Browser by Nodejs",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "electron  .",
    "package-mac": "electron-packager . --overwrite --platform=darwin --arch=x64 --icon=assets/icons/mac/ICON.png.icns --prune=true --out=release-builds",
    "package-win": "electron-packager . electron-tutorial-app --overwrite --asar=true --platform=win32 --arch=ia32 --icon=assets/icons/win/ICON.png.ico --prune=true --out=release-builds --version-string.CompanyName=CE --version-string.FileDescription=CE --version-string.ProductName=\"ArthurSlogMarkdownEditor\"",
    "package-linux": "electron-packager . electron-tutorial-app --overwrite --asar=true --platform=linux --arch=x64 --icon=assets/icons/linux/ICON.png --prune=true --out=release-builds"
  },
  "keywords": [],
  "author": "ArthurSlog",
  "license": "ISC",
  "devDependencies": {
    "electron": "^2.0.9",
    "electron-packager": "^12.1.2"
  },
  "dependencies": {
    "markdown-it": "^8.4.2"
  }
}
```

* 新建一个文件夹 assets/，用于存放应用的图标，文件目录如下：

``` txt
assets
   | -- icons
          | -- mac
                | -- ICON.png.icns

            -- win
                | -- ICON.png.icns

            -- linux
                | -- ICON.png
```

* 完整的代码、和编译好（打包好）的可执行文件 已上传至 Github：[https://github.com/BlessedChild/ArthurSlogMarkdownEditor](https://github.com/BlessedChild/ArthurSlogMarkdownEditor)

* 希望感兴趣的朋友可以一起参与进来

* 上一张应用的图吧

* 强势的插入一张图 ![ArthurSlogMarkdownEditor](https://github.com/BlessedChild/ArthurSlogMarkdownEditor/blob/master/icon_.png?raw=true)

* 目前已 编译好macOS环境下的可执行文件，后面继续保持更新

* 至此，ArthurSLogMarkdownEditor编辑器本地化第二阶段 GET！。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
