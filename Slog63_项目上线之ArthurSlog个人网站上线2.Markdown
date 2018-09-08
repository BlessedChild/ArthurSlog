# Slog63_项目上线之ArthurSlog个人网站上线2

* ArthurSlog
* SLog-63
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

大成若缺 其用不弊 大盈若冲 其用不穷 大直若屈 大巧若拙 大辩若讷

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 需要的信息和信息源：

### 开始编码

* 网站的所有代码已经编写完毕

* 稍微修改一下package.json

package.json
``` json
{
  "name": "nodeserver",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "koa": "^2.5.2",
    "koa-static": "^5.0.0"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/BlessedChild/ArthurSlog.com.git"
  },
  "author": "ArthurSlog",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/BlessedChild/ArthurSlog.com/issues"
  },
  "homepage": "https://github.com/BlessedChild/ArthurSlog.com#readme"
}
```

* 现在，需要把整个文件夹传送到服务器去

* 这里使用 scp指令

* 打开命令行，输入

> scp -h

``` txt
scp: illegal option -- h
usage: scp [-346BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
           [-l limit] [-o ssh_option] [-P port] [-S program]
           [[user@]host1:]file1 ... [[user@]host2:]file2
```

* scp的使用方法：

``` txt
-v  显示进度。可以用来查看连接、认证、或是配置错误

-P 选择端口

-r 复制目录

1、从本地将文件传输到服务器
scp[本地文件的路径]   [服务器用户名]@[服务器地址]:[服务器上存放文件的路径]

scp /Users/mac/Desktop/test.txt root@192.168.1.1:/root

2、从本地将文件夹传输到服务器
scp -r[本地文件的路径]   [服务器用户名]@[服务器地址]:[服务器上存放文件的路径]

scp -r /Users/mac/Desktop/test root@192.168.1.1:/root

3、将服务器上的文件传输到本地
scp [服务器用户名]@[服务器地址]:[服务器上存放文件的路径]   [本地文件的路径]

scp root@192.168.1.1:/root/default/test.txt /Users/mac/Desktop

4、将服务器上的文件夹传输到本地
scp -r [服务器用户名]@[服务器地址]:[服务器上存放文件的路径]   [本地文件的路径]

scp -r root@192.168.1.1:/root/default/test /Users/mac/Desktop
```

* 所以，执行一下指令，把本地文件夹 nodeserver传送至 服务器上，存放路径是 /usr/local/src/

> scp -r ~/Desktop/nodeserver root@服务器ip地址:/usr/local/src

* 至此，把本地编写好的源码成功传送至服务器上。

---

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
