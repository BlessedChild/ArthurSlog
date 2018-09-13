# Slog65_项目上线之ArthurSlog个人网站上线4

* ArthurSlog
* SLog-65
* Year·1

* Guangzhou·China
* September 9th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [ArthurSlog Page](http://www.arthurslog.com)

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [NPM Package Page](https://www.npmjs.com/~arthurslog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

天下难事必作于易 天下大事必作于细

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

### 开始编码

* 服务端环境已经配置好了，现在启动自己编写的服务器

* 先切换至自己编写的文件路径下

> cd /usr/local/src/nodeserver

* 启动服务器

> node index.js

* ok，现在用自己的电脑打开浏览器，输入域名 www.arthurslog.com

* 正常情况下，可以看到正常显示出来的页面

* 现在我来退出服务器窗口

* 然后再打开浏览器，输入域名 www.arthurslog.com

* 会发现，网页无法访问了

* 这是因为，当服务器的窗口关闭的时候，服务器也被一起关闭了

* 为了让服务器一直在服务器上一直运行

* 这里可以使用一个nodejs写的工具 forever

* 根据 [forever手册](https://www.npmjs.com/package/forever)

* 现在重新登陆服务器，输入以下指令

> sudo npm install forever -g

* 然后切换至我们的文件路径下

> cd /usr/local/src/nodeserver

* 使用forever指令启动服务，并让服务一直在后台运行

> sudo forever start ./index.js

* 现在用自己的电脑打开浏览器，输入域名 www.arthurslog.com

* 正常情况下，可以看到正常显示出来的页面

* 现在我来退出服务器窗口

* 然后再打开浏览器，输入域名 www.arthurslog.com

* 会发现，网页依旧可以正常访问

* 至此，我的个人网站 [www.ArthurSlog.com](www.ArthurSlog.com) 正式上线了。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
