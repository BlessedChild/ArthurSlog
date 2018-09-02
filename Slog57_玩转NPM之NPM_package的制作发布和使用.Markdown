# Slog57_玩转NPM之NPM_package的制作发布和使用

* ArthurSlog
* SLog-57
* Year·1

* Guangzhou·China
* Sep 2th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

越无力才会越发火 人无完人 学会控火

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

* [NPM官方手册](https://docs.npmjs.com/)

### 开始编码

* 首先，登陆 npm官网 注册一个账号

* 完成注册后，记得验证邮箱

* 现在你就拥有了自己的 npm主页了，地址是 https://www.npmjs.com/~你的用户名

* 现在打开命令行，登陆 npm账户

* 切换至桌面，新建一个文件夹 arthur-demo-package

> cd ~/Desktop

> mkdir arthur-demo-package

* 切换至 arthur-demo-package文件夹路径下

> cd arthur-demo-package

* 现在我们来创建并发布我们自己的npm包（NPM PACKAGE）

* 首先，先登录npm账号

> npm login

* 根据提示输入账号、密码和邮箱地址

* 接着，使用npm指令初始化配置文件package.json

> sudo npm init

* 根据提示，设置好自己的帐户名，其他的默认就行

* 现在，我们来编写我们的代码文件index.js 和 自述文件readme.md，其中自述文件为Markdown格式

~/Desktop/arthur-demo-package/index.js
``` js
exports.printMsg = function(){
    console.log("This is a message from the demo package");
}
```

~/Desktop/arthur-demo-package/readme.md
``` md
# This is a messgae from the demo package
```

* ok，接下来最后一步，提交自己编写的 npm package到 npm仓库里去

> npm publish

* 打开你的npm主页，这里打开我自己的主页，[地址](https://www.npmjs.com/~arthurslog)是 https://www.npmjs.com/~arthurslog

* 我们来测试一下自己写的npm package

* 切换至桌面，新建文件夹 testnpmpackage

> cd ~/Desktop

> mkdir testnpmpackage

* 切换至 testnpmpackage文件夹路径下

> cd testnpmpackage

* 初始化npm 配置文件，默认配置

> sudo npm init

* 安装 我们自己编写的npm package

> sudo npm i arthur-demo-package

* 导入我们编写的npm package，编写测试文件

~/Desktop/testnpmpcaksge/test.js
``` js
const arthur = require('arthur-demo-package');

arthur.printMsg(); 
```

* 执行文件

> node test.js

* 结果

``` txt
This is a message from the demo package
```

* 至此，我们完成了 npm package 的制作、发布和使用。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
