# Slog61_NodejsGUI之Electron模块的安装和测试

* ArthurSlog
* SLog-61
* Year·1

* Guangzhou·China
* Sep 6th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [ArthurSlog Page](http://www.arthurslog.com)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

不言之教 无为之益 天下希及之

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* Electron是nodejs的一个第三方模块，[Electron官网](https://electronjs.org/)

* [Electron Github](https://github.com/electron/electron)

* [npm Permissions](https://docs.npmjs.com/misc/config#unsafe-perm)

### 开始编码

* 新建一个文件夹 electron_learningload，然后切换至electron_learningload路径下

> cd ~/Desktop/

> markdir electron_learningload && cd electron_learningload

* 使用npm初始化环境（其实就是创建并配置一个package.json文件）

> sudo npm init

* 然后使用npm安装 electron 开发工具包，根据electron[官方说明](https://github.com/electron/electron/blob/master/docs/tutorial/installation.md)

``` txt
To install prebuilt Electron binaries, use npm. The preferred method is to install Electron as a development dependency in your app:

npm install electron --save-dev
```

* 根据以上，我们使用npm执行一下指令，安装 electron modules

> npm install electron --save-dev

* 结果是报错，错误信息如下

``` txt
Error: EACCES: permission denied

......
```

* ok,这里出现了 EACCES 错误事件，提示权限问题

* 结合 [electron官方说明](https://github.com/electron/electron/blob/master/docs/tutorial/installation.md) 和 [npm官方手册](https://docs.npmjs.com/misc/config#unsafe-perm)，解决方式如下：

> sudo npm install electron --save-dev --unsafe-perm=true

* ok，现在 electron 模块应该安装成功了

* 写个脚本来验证一下

~/Desktop/electron_learningload/index.js
``` js
const electron = require('electron')
const proc = require('child_process')

console.log(electron)

const child = proc.spawn(electron)
```

* 现在切换至文件路径下

> cd ~/Desktop/electron_learningload/

* 执行脚本

> node index.js

* 正常运行下，会打开一个Electron GUI界面

* 至此，我们完成了Nodejs第三方模块Electron的安装和测试。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
