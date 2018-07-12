* ArthurSlog
* SLog-4
* Year·1

* Guangzhou·China
* July 11th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

 梦想是锁不住的

### 开发环境MacOS(High Sierra 10.13.5)

* 老规则，首先准备我们需要的信息[Koa官方手册](https://koajs.cn/)、[Koa中间件](https://github.com/koajs/koa/wiki#middleware) 和 我们要用到的中间件[Koa-static](https://github.com/koajs/static)

* 准备的信息差不多，现在切换至桌面路径

> cd ~/Desktop

* 创建一个文件夹node_koa_learningload

> mkdir node_koa_learningload

* 切换路径到新建的文件夹下

> cd node_koa_learningload

* 使用npm初始化node环境，一路enter键完成初始化

> npm init

* 使用npm安装koa和koa-static

> sudo npm install koa koa-static

* 参考[Koa-static说明手册](https://github.com/koajs/static)，我们在当前路径下编写index.js和index.html两份文件

index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();

// $ GET /package.json
app.use(serve('.'));

// $ GET /hello.txt
app.use(serve('test/fixtures'));

// or use absolute paths
app.use(serve(__dirname + '/test/fixtures'));

app.listen(3000);

console.log('listening on port 3000');
```

index.html

``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>ArthurSlog</title>
</head>
<body>

<h1>The static web server by ArthurSlog</h1>

</body>
</html>
```
* index.js是官方栗子，有三种路由方法，我们来分析一下：
1. 根据node工程的配置文件package.json里指定的入口点“main”决定路由

``` js
// $ GET /package.json
app.use(serve('.'));
```

2. 使用相对路径作为路由，默认的路由文件由package.json里的入口点“main”决定

``` js
// $ GET /hello.txt
app.use(serve('test/fixtures'));
```

3. 使用绝对路径作为路由，默认的路由文件由package.json里的入口点“main”决定

``` js
// or use absolute paths
app.use(serve(__dirname + '/test/fixtures'));
```

* 在这里，我们直接用第一种方式，最终的代码为

index.js
``` js
const serve = require('koa-static');
const Koa = require('koa');
const app = new Koa();

// $ GET /package.json
app.use(serve('.'));

app.listen(3000);

console.log('listening on port 3000');
```

* Ok，现在启动静态web服务器

> node index.js

* 打开浏览器测试一下，地址127.0.0.1:3000


* 至此，我们使用koa和中间件koa-static实现了一个静态web服务器，恭喜。

### 欢迎关注我的微信公众号 ArthurSlog

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢