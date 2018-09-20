# Slog80_打包ArthurSlogMarkdownEditor编辑器至mac平台dmg安装包GET！
![ArthurSlog](https://github.com/BlessedChild/ArthurSlog/blob/master/ArthurSlog_Logo.png?raw=true)

* ArthurSlog
* SLog-80
* Year·1

* Guangzhou·China
* September 21th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog.com](http://www.arthurslog.com)

* [MSDN: ArthurSlog](https://blog.csdn.net/u010997452/article/list/1)

* [GitHub: BlessedChild](https://github.com/BlessedChild/ArthurSlog)

* [NPMJS.com: arthurslog](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

我明白 无论等待我的是什么 选择前行是我唯一确定的答案

---

### 开发环境MacOS(High Sierra 10.13.6 (17G65))

#### 需要的信息和信息源：

* [electron-installer-dmg](https://www.npmjs.com/package/electron-installer-dmg)

### 开始编码

* 本次，把之前打包好的ArthurSlogMarkdownEditor可执行文件打包成一个dmg（MacOS平台）的安装包

* 这里我们需要用到的工具就是 electron-installer-dmg

* So，npm走起（最近看到有人调侃前端开发只需要两步：1. npm i； 2. npm run build）

* 切换至项目路径下

> cd ~/Desktop/ArthurSlogMarkdownEditor/

> sudo npm install electron-installer-dmg --save-dev --unsafe-perm=true

> sudo npm install electron-installer-dmg -g --unsafe-perm=true

* 在按照过程中，可能会出现警告和错误提示(比如node-gyp编译失败))

* 根据[node-gyp的说明：https://github.com/nodejs/node-gyp](https://github.com/nodejs/node-gyp)

* 可知：

``` txt
On macOS
python (v2.7 recommended, v3.x.x is not supported) (already installed on macOS)
Xcode
You also need to install the Command Line Tools via Xcode. You can find this under the menu Xcode -> Preferences -> Locations (or by running xcode-select --install in your Terminal)
This step will install gcc and the related toolchain containing make
```

* 所以，需要打开xcode工具，点击左上角Xcode -> Preferences -> Locations -> Command Line Tools -> Xcode10.0(10A255)

* 之后重新执行

> sudo npm install electron-installer-dmg --save-dev --unsafe-perm=true

> sudo npm install electron-installer-dmg -g --unsafe-perm=true

* 成功安装之后，更新一下 package.json文件：

~/Desktop/ArthurSlogMarkdownEditor/package.json
``` json
{
  "name": "ArthurSlogBrowser_Nodejs",
  "productName": "ArthurSlogMarkdownEditor",
  "version": "0.1.0",
  "description": "This is a Browser by Nodejs",
  "private": "true",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "electron  .",
    "package-mac": "electron-packager . --overwrite --platform=darwin --arch=x64 --icon=assets/icons/mac/ICON.png.icns --prune=true --out=release-builds",
    "package-win": "electron-packager . electron-tutorial-app --overwrite --asar=true --platform=win32 --arch=ia32 --icon=assets/icons/win/ICON.png.ico --prune=true --out=release-builds --version-string.CompanyName=CE --version-string.FileDescription=CE --version-string.ProductName=\"ArthurSlogMarkdownEditor\"",
    "package-linux": "electron-packager . electron-tutorial-app --overwrite --asar=true --platform=linux --arch=x64 --icon=assets/icons/linux/ICON.png --prune=true --out=release-builds",
    "create-installer-mac": "electron-installer-dmg ./release-builds/ArthurSlogMarkdownEditor-darwin-x64/ArthurSlogMarkdownEditor.app ArthurSlogMarkdownEditor --out=release-builds --overwrite --icon=assets/icons/mac/ICON.png.icns"
  },
  "keywords": [],
  "author": "ArthurSlog",
  "license": "ISC",
  "devDependencies": {
    "electron": "^2.0.9",
    "electron-installer-dmg": "^2.0.0",
    "electron-packager": "^12.1.2"
  },
  "dependencies": {
    "markdown-it": "^8.4.2"
  }
}
```

* 上面添加了一条新的构建指令：

~/Desktop/ArthurSlogMarkdownEditor/package.json
``` json
"create-installer-mac": "electron-installer-dmg ./release-builds/ArthurSlogMarkdownEditor-darwin-x64/ArthurSlogMarkdownEditor.app ArthurSlogMarkdownEditor --out=release-builds --overwrite --icon=assets/icons/mac/ICON.png.icns"
```

* Ok，现在执行命令

> sudo npm run package-mac

> sudo npm run create-installer-mac

* 成功构建之后，会在路径 release-builds下生成 ArthurSlogMarkdownEditor.dmg文件

* 双击 ArthurSlogMarkdownEditor.dmg文件，进行安装，把ArthurSlogMarkdownEditor拉拽至文件夹里

* 点击docker上的“启动台”，你会发现 ArthurSlogMarkdownEditor 已经安装成功了

* 点击打开 ArthurSlogMarkdownEditor，测试一下，一切正常

* 至此，完成了打包 ArthurSlogMarkdownEditor编辑器至mac平台dmg安装包。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢