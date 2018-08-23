* ArthurSlog
* SLog-9
* Year·1

* Guangzhou·China
* July 15th 2018

![关注微信公众号“ArthurSlog”](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

* [GitHub](https://github.com/BlessedChild/ArthurSlog)

* [掘金主页](https://juejin.im/user/59f2a424f265da432f305c66/posts)

* [简书主页](https://www.jianshu.com/u/b9ebe10f0534)

* [segmentfault](https://segmentfault.com/u/arthurslog/articles)

现在的时代 可能青山还在 但你已经没柴烧了 因为漫山遍野都是人

---

### 开发环境MacOS(High Sierra 10.13.5)

#### 课前预习：

* Less 是一种动态层叠样式表语言，在语法方面，LESS与CSS较为接近，一个合法的CSS代码段本身也是一段合法的LESS代码段。LESS提供变量、嵌套、混合、操作符、函数等一般编程所需的抽象机制

* 运行环境：LESS可以在客户端上运行（IE6+、Webkit、Firefox），也可以在服务端运行（Node.js、Rhino）

* Less 运行时是一份js文件 less.js

* 使用方式：本篇使用[浏览器直接引入的方式](http://lesscss.org/usage/#using-less-in-the-browser)

* [Less的语法功能](http://lesscss.org/functions/)



### 开始编码

* 现在切换至桌面路径

> cd ~/Desktop

* 创建一个文件夹node_koa_learningload

> mkdir node_less_learningload

* 切换路径到新建的文件夹下

> cd node_less_learningload

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

* 根据less官方网站的 [使用提示](http://lesscss.org/usage/#using-less-in-the-browser-tips)，需要再引用脚本之前包含样式表，所以在当前路径下，根据 [less官方手册](http://lesscss.org/functions/) 编写样式表 stytles.less

styles.less
``` less
@color: red;

h1 {
    color: @color;
}
```

* 现在，引入样式表的路径如下：

``` html
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

* 在当前路径下，git clone 一份 less 的源码：(没有安装git工具的，请先安装)

> git clone https://github.com/less/less.js.git

* 现在，index.html 完整代码如下：

index.html
``` html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>ArthurSlog</title>
<link rel="stylesheet/less" type="text/css" href="styles.less" />
<script src="less.js/dist/less.js" type="text/javascript"></script>
</head>
<body>

<h1>The static web server by ArthurSlog</h1>

</body>
</html>
```

* 如果你现在安装有 Firefox浏览器，可以直接用 Firefox浏览器 打开，应该可以看到效果了，然后你可以结束本篇或者继续接着往下看

* 跳过上面那一步，我们现在启动静态web服务器：

> node index.js

* 打开浏览器器（不一定要Firefox浏览器），在地址了输入 127.0.0.1:3000, 正常执行你会看到以下结果(字体是红色的)

``` html
The static web server by ArthurSlog
```

* 至此，我们介绍了 less.js 的内容和用法，更多信息请参考 [less官方网站](http://lesscss.org/#)。

---

### 欢迎关注我的微信公众号 ArthurSlog

![ArthurSlog](https://github.com/BlessedChild/LogofAxu/blob/master/images/icon_128.jpg?raw=true "微信扫描二维码，关注我的公众号")

### 如果你喜欢我的文章 欢迎点赞 留言
### 谢谢
