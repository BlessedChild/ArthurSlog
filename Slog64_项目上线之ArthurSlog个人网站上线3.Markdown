# Slog64_项目上线之ArthurSlog个人网站上线3

* ArthurSlog
* SLog-64
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

多言数穷 不如守中

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

### 开始编码

* 本篇配置服务端环境

* 网站的源码已经传送至服务器

* 我们使用运营商的web端连接登陆服务器（登陆某云控制台，找到服务器登陆选项登陆服务器）

* 这里的服务器环境是CentOS 7.2 64位，首先需要下载安装nodejs

* 打开nodejs官网，找到下载页，Linux Binaries (x86/x64)，选择64-bit，右键复制链接地址

* 在服务器控制台输入：

> wget https://nodejs.org/dist/v8.11.4/node-v8.11.4-linux-x64.tar.xz

* 然后等待下载完毕后

* 使用tar工具解压 node-v8.11.4-linux-x64.tar.xz

> tar tar xf node-v8.11.4-linux-x64.tar.xz

* 解压成功后，在当前路径下有node-v8.11.4-linux-x64文件

* 现在没办法直接

> node -v

* 上面这样是没有效果的

* 所以这里需要使用ln工具，进行链接

* ln的使用方式是这样的“ln -s /path/to/file /path/to/link”

* 所以，为了可以直接在任何地方使用node指令，需要

> ln -s ./node-v8.11.4-linux-x64.tar.xz/bin/node /usr/bin

> ln -s ./node-v8.11.4-linux-x64.tar.xz/bin/npm /usr/bin

* 现在，就可以在任何路径下，直接使用node或者npm指令了

* 至此，服务端的运行环境就配置完了。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
