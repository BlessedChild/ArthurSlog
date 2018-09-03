# Slog58_玩转NPM之NPM_package的制作发布和使用

* ArthurSlog
* SLog-58
* Year·1

* Guangzhou·China
* Sep 3th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

有个爱你的人不容易 你怎么舍得伤她的心 一定要趁现在好好努力

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [NPM官方手册](https://docs.npmjs.com/)

### 开始编码

* 本篇我们来更新并发布我们自己的npm包（NPM PACKAGE）

* 切换至文件路径下

> cd ~/Desktop/arthur-demo-package/

* 本次更新自述文件 readme.md

~/Desktop/arthur-demo-package/readme.md
``` md
\# This is a messgae from the demo package

\``` txt
Example.js
\```

\---

\``` js
const arthur = require('arthur-demo-package');

arthur.printMsg(); 
\```
```

* 上述使用的是 [Markdown语法](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

* 打开命令行，登陆npm账号（已登陆的忽略），查看登陆状态

> npm whoami

结果是： 
``` txt
arthurslog
```

* 如果还没登陆，需要输入一下指令，并根据提示输入账号、密码和邮箱地址

> npm login

* 接着，输入以下指令更新版本号，参考 [官方文档](https://docs.npmjs.com/getting-started/publishing-npm-packages)

``` txt
Patch releases (补丁版本)：1.0或1.0.x或~1.0.4
Minor releases (次要版本)：1或1.x或^1.0.4
Major releases (主要版本)：*或x

指令的写法时 sudo npm version <patch>

其中 <patch>，指明了本次发布的为补丁版本，可以替换成上述的另外两个或者时其他的，含义参照官方文档
```

> sudo npm version patch

* 接着，发布我们的最新的 package

> sudo npm publish

* ok，现在已经完成了package的更新和发布了

* 打开你的npm主页，这里打开我自己的主页，[地址](https://www.npmjs.com/~arthurslog)是 https://www.npmjs.com/~arthurslog

* 可以看到，我们的自述页面已经更新了

* 至此，我们完成了Npm package的更新和发布。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
